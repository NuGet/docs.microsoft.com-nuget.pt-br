---
title: NuGet cruzada plugins de plataforma
description: NuGet cross plugins de plataforma para NuGet.exe, dotnet.exe, msbuild.exe e Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: fdefc5b6189051fd83b2de644080284c09dd85f4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548200"
---
# <a name="nuget-cross-platform-plugins"></a>NuGet cruzada plugins de plataforma

No NuGet 4.8 + foi adicionado suporte para várias plugins de plataforma.
Isso foi obtido com, criando um novo modelo de extensibilidade de plug-in, que deve estar de acordo com um conjunto restrito de regras de operação.
Os plug-ins são executáveis independentes (executáveis no mundo do .NET Core), que os clientes do NuGet Iniciar em um processo separado.
Trata-se de uma gravação true uma vez, execute em qualquer lugar de plug-in. Ele funcionará com todas as ferramentas de cliente do NuGet.
Os plug-ins podem ser (NuGet.exe, MSBuild.exe e Visual Studio) do .NET Framework ou .NET Core (dotnet.exe).
Um protocolo de comunicação com controle de versão entre o cliente do NuGet e o plug-in é definido. Durante o handshake de inicialização, os 2 processos negociam a versão do protocolo.

Para cobrir todos os cenários de ferramentas de cliente NuGet, é necessário um .NET Framework e um plug-in do .NET Core.
A seguir descreve as combinações de estrutura do cliente dos plug-ins.

| Ferramenta de cliente  | Framework |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| dotnet.exe | .NET Core |
| NuGet.exe | .NET Framework |
| MSBuild.exe | .NET Framework |
| NuGet.exe no Mono | .NET Framework |

## <a name="how-does-it-work"></a>Como ele funciona

O fluxo de trabalho de alto nível pode ser descrito da seguinte maneira:

1. NuGet descobre plug-ins disponíveis.
1. Quando aplicável, o NuGet irá iterar sobre os plug-ins na ordem de prioridade e inicia um um.
1. O NuGet usará o primeiro plug-in que pode atender à solicitação.
1. Os plug-ins serão desligados quando eles não são mais necessários.

## <a name="general-plugin-requirements"></a>Requisitos de plug-in de geral

É a versão atual do protocolo *2.0.0*.
Nesta versão, os requisitos são:

- Ter um assemblies de assinatura Authenticode válida e confiável que serão executado no Windows e Mono. Não há nenhum requisito de confiança especiais para assemblies executados no Linux e Mac ainda. [Problema relevante](https://github.com/NuGet/Home/issues/6702)
- Suporte a iniciar sem monitoração de estado no contexto de segurança atual das ferramentas de cliente do NuGet. Por exemplo, as ferramentas de cliente do NuGet não executará elevação ou inicialização adicional fora o protocolo de plug-in descrito posteriormente.
- Ser não interativo, a menos que explicitamente especificado.
- Seguir a versão do protocolo negociado plug-in.
- Responda a todas as solicitações em um período de tempo razoável.
- Cumpram as solicitações de cancelamento para qualquer operação em andamento.

A especificação técnica é descrita mais detalhadamente nas seguintes especificações:

- [Plug-in de Download de pacote do NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet cruzada plug-in de autenticação de várias plataformas](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>Cliente - interação de plug-in

Os plug-ins e ferramentas de cliente do NuGet se comunicar com JSON em fluxos padrão (stdin, stdout, stderr). Todos os dados devem ser codificados em UTF-8.
Os plug-ins são iniciados com o argumento "-plug-in". No caso de um usuário inicia diretamente um plug-in do arquivo executável sem esse argumento, o plug-in pode fornecer uma mensagem informativa em vez de esperar um handshake de protocolo.
Tempo limite de handshake do protocolo é 5 segundos. O plug-in deve concluir a configuração no como sem que seja necessário um valor possível.
Ferramentas de cliente do NuGet consultará operações com suporte do plug-in, passando o índice de serviço para uma fonte do NuGet. Um plug-in pode usar o índice de serviço para verificar a presença de tipos de serviço com suporte.

A comunicação entre as ferramentas de cliente do NuGet e o plug-in é bidirecional. Cada solicitação tem um tempo limite de 5 segundos. Se as operações devem para levar mais tempo o processo respectivo deve enviar uma mensagem de progresso para impedir que a solicitação atingir o tempo limite. Após um minuto de inatividade um plug-in é considerado ocioso e é desligado.

## <a name="plugin-installation-and-discovery"></a>Descoberta e instalação do plug-in

Os plug-ins serão descobertos por meio de uma estrutura de diretório baseado na convenção.
Cenários de CI/CD e usuários avançados podem usar uma variável de ambiente para substituir o comportamento.

- `NUGET_PLUGIN_PATHS` -Define os plug-ins que serão usados para esse processo do NuGet, prioridade reservado. Se essa variável de ambiente for definida, ela substitui a descoberta baseado na convenção.
-  Local do usuário, o local da página inicial do NuGet em `%UserProfile%/.nuget/plugins`. Esse local não pode ser substituído. Um diretório raiz diferente será usado para o plug-ins do .NET Core e .NET Framework.

| Framework | Local de detecção de raiz  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Cada plug-in deve ser instalado em sua própria pasta.
O ponto de entrada do plug-in será o nome da pasta instalado, com as extensões. dll para o .NET Core e a extensão .exe para o .NET Framework.

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> Atualmente, não há nenhuma história de usuário para a instalação dos plug-ins. Ele é tão simple quanto mover os arquivos necessários para o local predeterminado.

## <a name="supported-operations"></a>Operações com suporte

Duas operações têm suporte com o novo protocolo de plug-in.

| Nome da operação | Versão mínima do protocolo | Versão mínima do cliente do NuGet |
| -------------- | ----------------------- | --------------------- |
| Baixe o pacote | 1.0.0 | 4.3.0 |
| [Autenticação](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>Executando plug-ins no tempo de execução correto

Para o NuGet em cenários de dotnet.exe, plug-ins precisam poder ser executado sob esse tempo de execução específico do dotnet.exe.
É o provedor de plug-in e o consumidor para certificar-se de que uma combinação de dotnet.exe/plugin compatível é usada.
Um problema em potencial que poderia surgir com o local do usuário plug-ins quando, por exemplo, um dotnet.exe no tempo de execução 2.0 tenta usar um plug-in escrito para o tempo de execução 2.1.

## <a name="capabilities-caching"></a>Recursos de armazenamento em cache

A verificação de segurança e a instanciação dos plug-ins é caro. A operação de download acontece com muito mais frequência do que a operação de autenticação, no entanto, o usuário médio do NuGet só é provavelmente terá um plug-in de autenticação.
Para melhorar a experiência, o NuGet armazenará em cache as declarações de operação para a solicitação em questão. Esse cache é por plug-in com a chave de plug-in que está sendo o caminho de plug-in e a expiração para esse cache de recursos é de 30 dias. 

O cache está localizado em `%LocalAppData%/NuGet/plugins-cache` e ser substituída com a variável de ambiente `NUGET_PLUGINS_CACHE_PATH`. Para limpar esse [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), os locais pode ser executada com o `plugins-cache` opção.
O `all` opção locais agora também excluirá o cache de plug-ins. 

## <a name="protocol-messages-index"></a>Índice de mensagens de protocolo

Versão do protocolo *1.0.0* mensagens:

1.  Fechar
    * Direção de solicitação: NuGet -> Plug-in
    * A solicitação não irá conter nenhuma carga útil
    * Nenhuma resposta é esperada.  A resposta correta é para o processo de plug-in seja encerrado imediatamente.

2.  Copiar arquivos de pacote
    * Direção de solicitação: NuGet -> Plug-in
    * A solicitação conterá:
        * a ID do pacote e versão
        * o local de repositório de origem do pacote
        * caminho do diretório de destino
        * um enumerável de arquivos no pacote a ser copiado para o caminho do diretório de destino
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * um enumerável de caminhos completos para arquivos copiados no diretório de destino, se a operação foi bem-sucedida

3.  Copie o arquivo de pacote (. nupkg)
    * Direção de solicitação: NuGet -> Plug-in
    * A solicitação conterá:
        * a ID do pacote e versão
        * o local de repositório de origem do pacote
        * o caminho do arquivo de destino
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação

4.  Obter credenciais
    * Direção de solicitação: plug-in -> NuGet
    * A solicitação conterá:
        * o local de repositório de origem do pacote
        * o código de status HTTP obtido no repositório de origem do pacote usando as credenciais atuais
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * um nome de usuário, se disponível
        * uma senha, se disponível

5.  Obter os arquivos no pacote
    * Direção de solicitação: NuGet -> Plug-in
    * A solicitação conterá:
        * a ID do pacote e versão
        * o local de repositório de origem do pacote
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * um enumerável de caminhos de arquivo no pacote se a operação foi bem-sucedida

6.  Obter declarações de operação 
    * Direção de solicitação: NuGet -> Plug-in
    * A solicitação conterá:
        * o serviço index.json para uma origem de pacote
        * o local de repositório de origem do pacote
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * um enumerável de operações com suporte (por exemplo: download do pacote) se a operação foi bem-sucedida.  Se um plug-in não oferece suporte a origem do pacote, o plug-in deve retornar um conjunto vazio de operações com suporte.

> [!Note]
> Esta mensagem foi atualizada na versão *2.0.0*. É no cliente para preservar a compatibilidade com versões anteriores.

7.  Obter o hash do pacote
    * Direção de solicitação: NuGet -> Plug-in
    * A solicitação conterá:
        * a ID do pacote e versão
        * o local de repositório de origem do pacote
        * o algoritmo de hash
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * um hash do arquivo de pacote usando o algoritmo de hash solicitado, se a operação foi bem-sucedida

8.  Obter versões de pacote
    * Direção de solicitação: NuGet -> Plug-in
    * A solicitação conterá:
        * a ID do pacote
        * o local de repositório de origem do pacote
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * um enumerável de versões do pacote se a operação foi bem-sucedida

9.  Obter índice de serviço
    * Direção de solicitação: plug-in -> NuGet
    * A solicitação conterá:
        * o local de repositório de origem do pacote
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * o índice de serviço se a operação foi bem-sucedida

10.  Handshake
     * Direção de solicitação: plug-in do NuGet <> –
     * A solicitação conterá:
         * a versão atual do protocolo de plug-in
         * a versão do protocolo de plug-in com suporte mínimo
     * Uma resposta conterá:
         * um código de resposta que indica o resultado da operação
         * a versão do protocolo negociado se a operação foi bem-sucedida.  Uma falha resultará no encerramento do plug-in.

11.  inicializar
     * Direção de solicitação: NuGet -> Plug-in
     * A solicitação conterá:
         * a versão da ferramenta cliente NuGet
         * o NuGet ferramenta efetivação idioma do cliente.  Isso leva em consideração a configuração de ForceEnglishOutput, se usado.
         * o padrão tempo limite da solicitação, que substitui o padrão de protocolo.
     * Uma resposta conterá:
         * um código de resposta que indica o resultado da operação.  Uma falha resultará no encerramento do plug-in.

12.  Log
     * Direção de solicitação: plug-in -> NuGet
     * A solicitação conterá:
         * o nível de log para a solicitação
         * uma mensagem de log
     * Uma resposta conterá:
         * um código de resposta que indica o resultado da operação.

13.  Monitorar a saída do processo de NuGet
     * Direção de solicitação: NuGet -> Plug-in
     * A solicitação conterá:
         * a ID de processo do NuGet
     * Uma resposta conterá:
         * um código de resposta que indica o resultado da operação.

14.  Pacote de pré-busca
     * Direção de solicitação: NuGet -> Plug-in
     * A solicitação conterá:
         * a ID do pacote e versão
         * o local de repositório de origem do pacote
     * Uma resposta conterá:
         * um código de resposta que indica o resultado da operação

15.  Definir credenciais
     * Direção de solicitação: NuGet -> Plug-in
     * A solicitação conterá:
         * o local de repositório de origem do pacote
         * último pacote conhecidos origem nome de usuário, se disponível
         * a última senha de origem de pacotes conhecidas, se disponível
         * o último proxy conhecidos nome de usuário, se disponível
         * a última senha proxy conhecidos, se disponível
     * Uma resposta conterá:
         * um código de resposta que indica o resultado da operação

16.  Definir o nível de log
     * Direção de solicitação: NuGet -> Plug-in
     * A solicitação conterá:
         * o nível de log padrão
     * Uma resposta conterá:
         * um código de resposta que indica o resultado da operação

Versão do protocolo *2.0.0* mensagens

17. Obter declarações de operação

* Direção de solicitação: NuGet -> Plug-in
    * A solicitação conterá:
        * o serviço index.json para uma origem de pacote
        * o local de repositório de origem do pacote
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * um enumerável de operações com suporte se a operação foi bem-sucedida.  Se um plug-in não oferece suporte a origem do pacote, o plug-in deve retornar um conjunto vazio de operações com suporte.

    Se a origem de índice e o pacote de serviço forem nula, o plug-in pode responder com a autenticação.

18. Obter credenciais de autenticação

* Direção de solicitação: NuGet -> Plug-in
* A solicitação conterá:
    * URI
    * isRetry
    * NonInteractive
    * CanShowDialog
* Uma resposta irá conter
    * Nome de usuário
    * Senha
    * Mensagem
    * Lista de tipos de autenticação
    * MessageResponseCode