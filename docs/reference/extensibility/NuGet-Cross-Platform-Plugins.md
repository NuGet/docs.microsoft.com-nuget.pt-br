---
title: Plug-ins de plataforma cruzada do NuGet
description: Plug-ins de plataforma cruzada do NuGet para NuGet. exe, dotnet. exe, MSBuild. exe e Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 74b80b1791dcb403c90bb3032c009717c11ffe57
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815309"
---
# <a name="nuget-cross-platform-plugins"></a>Plug-ins de plataforma cruzada do NuGet

No NuGet 4.8 + suporte para plug-ins de plataforma cruzada foi adicionado.
Isso foi conseguido com a criação de um novo modelo de extensibilidade de plug-in, que precisa estar em conformidade com um conjunto estrito de regras de operação.
Os plug-ins são executáveis independentes (executáveis no mundo do .NET Core), que os clientes NuGet iniciam em um processo separado.
Essa é uma verdadeira gravação única, execute o plug-in de todos os lugares. Ele funcionará com todas as ferramentas de cliente do NuGet.
Os plug-ins podem ser .NET Framework (NuGet. exe, MSBuild. exe e Visual Studio) ou .NET Core (dotNet. exe).
Um protocolo de comunicação com versão entre o cliente NuGet e o plug-in é definido. Durante o handshake de inicialização, os 2 processos negociam a versão do protocolo.

Para abranger todos os cenários de ferramentas de cliente do NuGet, é necessário um plug-in de .NET Framework e do .NET Core.
A seguir, a descrição das combinações de cliente/estrutura dos plug-ins.

| Ferramenta de cliente  | Framework |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| dotnet.exe | .NET Core |
| NuGet. exe | .NET Framework |
| MSBuild. exe | .NET Framework |
| NuGet. exe no mono | .NET Framework |

## <a name="how-does-it-work"></a>Como funciona

O fluxo de trabalho de alto nível pode ser descrito da seguinte maneira:

1. O NuGet descobre plugins disponíveis.
1. Quando aplicável, o NuGet irá iterar sobre os plug-ins em ordem de prioridade e os iniciará um a um.
1. O NuGet usará o primeiro plug-in que pode atender à solicitação.
1. Os plug-ins serão desligados quando não forem mais necessários.

## <a name="general-plugin-requirements"></a>Requisitos gerais de plug-in

A versão atual do protocolo é *2.0.0*.
Nesta versão, os requisitos são os seguintes:

- Ter um assembly de assinatura de Authenticode confiável válido que será executado no Windows e no mono. Ainda não há nenhum requisito de confiança especial para assemblies executados no Linux e Mac. [Problema relevante](https://github.com/NuGet/Home/issues/6702)
- Suporte à inicialização sem monitoração de estado no contexto de segurança atual das ferramentas de cliente do NuGet. Por exemplo, as ferramentas de cliente do NuGet não executarão a elevação ou inicialização adicional fora do protocolo de plug-in descrito posteriormente.
- Ser não interativo, a menos que especificado explicitamente.
- Siga a versão do protocolo de plug-in negociado.
- Responder a todas as solicitações em um período de tempo razoável.
- Honra as solicitações de cancelamento para qualquer operação em andamento.

A especificação técnica é descrita mais detalhadamente nas especificações a seguir:

- [Plug-in de download do pacote NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [Plug-in de autenticação entre Plat do NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>Interação do plug-in do cliente

As ferramentas de cliente do NuGet e os plug-ins se comunicam com JSON sobre fluxos padrão (stdin, stdout, stderr). Todos os dados devem ser codificados em UTF-8.
Os plug-ins são iniciados com o argumento "-plugin". No caso de um usuário iniciar diretamente um executável de plug-in sem esse argumento, o plug-in pode fornecer uma mensagem informativa em vez de aguardar um handshake de protocolo.
O tempo limite de handshake de protocolo é de 5 segundos. O plug-in deve concluir a configuração no menor valor possível.
As ferramentas de cliente do NuGet consultarão as operações com suporte de um plug-in passando o índice de serviço para uma origem do NuGet. Um plug-in pode usar o índice de serviço para verificar a presença de tipos de serviço com suporte.

A comunicação entre as ferramentas de cliente do NuGet e o plug-in é bidirecional. Cada solicitação tem um tempo limite de 5 segundos. Se as operações devem levar mais tempo, o respectivo processo deve enviar uma mensagem de progresso para impedir que a solicitação atinja o tempo limite. Após 1 minuto de inatividade, um plug-in é considerado ocioso e é desligado.

## <a name="plugin-installation-and-discovery"></a>Instalação e descoberta do plug-in

Os plug-ins serão descobertos por meio de uma estrutura de diretório baseada em convenção.
Cenários de CI/CD e usuários avançados podem usar variáveis de ambiente para substituir o comportamento. Observe que `NUGET_NETFX_PLUGIN_PATHS` o `NUGET_NETCORE_PLUGIN_PATHS` e o estão disponíveis apenas com a versão 5.3 + das ferramentas do NuGet e posterior.

- `NUGET_NETFX_PLUGIN_PATHS`-define os plug-ins que serão usados pelas ferramentas baseadas em .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio). Tem precedência `NUGET_PLUGIN_PATHS`sobre. (Somente NuGet versão 5.3 +)
- `NUGET_NETCORE_PLUGIN_PATHS`-define os plug-ins que serão usados pelas ferramentas baseadas no .NET Core (dotNet. exe). Tem precedência `NUGET_PLUGIN_PATHS`sobre. (Somente NuGet versão 5.3 +)
- `NUGET_PLUGIN_PATHS`-define os plug-ins que serão usados para o processo NuGet, prioridade reservada. Se essa variável de ambiente for definida, ela substituirá a descoberta baseada em convenção. Ignorado se uma das variáveis específicas do Framework for especificada.
-  Local do usuário, o local inicial do NuGet `%UserProfile%/.nuget/plugins`em. Esse local não pode ser substituído. Um diretório raiz diferente será usado para os plug-ins .NET Core e .NET Framework.

| Framework | Local de descoberta raiz  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Cada plug-in deve ser instalado em sua própria pasta.
O ponto de entrada do plug-in será o nome da pasta instalada, com as extensões. dll para .NET Core e a extensão. exe para .NET Framework.

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
> No momento, não há nenhuma história de usuário para a instalação dos plug-ins. É tão simples quanto mover os arquivos necessários para o local predeterminado.

## <a name="supported-operations"></a>Operações com suporte

Há suporte para duas operações no novo protocolo de plugin.

| Nome da operação | Versão mínima do protocolo | Versão mínima do cliente NuGet |
| -------------- | ----------------------- | --------------------- |
| Baixar pacote | 1.0.0 | 4.3.0 |
| [Autenticação](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>Executando plug-ins no tempo de execução correto

Para o NuGet em cenários dotnet. exe, os plug-ins precisam ser capazes de executar sob esse tempo de execução específico do dotnet. exe.
Ele está no provedor de plug-in e no consumidor para garantir que uma combinação de dotnet. exe/plugin compatível seja usada.
Um problema potencial pode surgir com os plug-ins de localização do usuário quando, por exemplo, um dotnet. exe no tempo de execução 2,0 tentar usar um plug-in gravado para o tempo de execução 2,1.

## <a name="capabilities-caching"></a>Recursos de cache

A verificação de segurança e a instanciação dos plug-ins são dispendiosas. A operação de download ocorre de maneira mais frequente do que a operação de autenticação, no entanto, o usuário NuGet médio provavelmente terá um plug-in de autenticação.
Para melhorar a experiência, o NuGet armazenará em cache as declarações de operação para a solicitação especificada. Esse cache é por plug-in com a chave do plug-in sendo o caminho do plug-in e a expiração desse cache de recursos é de 30 dias. 

O cache está localizado em `%LocalAppData%/NuGet/plugins-cache` e é substituído pela variável `NUGET_PLUGINS_CACHE_PATH`de ambiente. Para limpar esse [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), é possível executar o comando local com a `plugins-cache` opção.
A `all` opção locais agora também excluirá o cache de plug-ins. 

## <a name="protocol-messages-index"></a>Índice de mensagens de protocolo

Mensagens da versão *1.0.0* do protocolo:

1.  Fechar
    * Direção da solicitação:  Plug-in > do NuGet
    * A solicitação não conterá nenhuma carga
    * Nenhuma resposta é esperada.  A resposta correta é para que o processo do plug-in seja fechado imediatamente.

2.  Copiar arquivos no pacote
    * Direção da solicitação:  Plug-in > do NuGet
    * A solicitação conterá:
        * a ID e a versão do pacote
        * o local do repositório de origem do pacote
        * caminho do diretório de destino
        * um enumerável de arquivos no pacote a ser copiado para o caminho do diretório de destino
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * um enumerável de caminhos completos para arquivos copiados no diretório de destino se a operação foi bem-sucedida

3.  Copiar arquivo de pacote (. nupkg)
    * Direção da solicitação:  Plug-in > do NuGet
    * A solicitação conterá:
        * a ID e a versão do pacote
        * o local do repositório de origem do pacote
        * o caminho do arquivo de destino
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação

4.  Obter credenciais
    * Direção da solicitação: > do plugin-NuGet
    * A solicitação conterá:
        * o local do repositório de origem do pacote
        * o código de status HTTP obtido do repositório de origem do pacote usando as credenciais atuais
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * um nome de usuário, se disponível
        * uma senha, se disponível

5.  Obter arquivos no pacote
    * Direção da solicitação:  Plug-in > do NuGet
    * A solicitação conterá:
        * a ID e a versão do pacote
        * o local do repositório de origem do pacote
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * um enumerável de caminhos de arquivo no pacote se a operação foi bem-sucedida

6.  Obter declarações de operação 
    * Direção da solicitação:  Plug-in > do NuGet
    * A solicitação conterá:
        * o Service index. JSON para uma origem de pacote
        * o local do repositório de origem do pacote
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * um enumerável de operações com suporte (por exemplo: download de pacote) se a operação foi bem-sucedida.  Se um plug-in não oferecer suporte à origem do pacote, o plug-in deverá retornar um conjunto vazio de operações com suporte.

> [!Note]
> Esta mensagem foi atualizada na versão *2.0.0*. Ele está no cliente para preservar a compatibilidade com versões anteriores.

7.  Obter hash do pacote
    * Direção da solicitação:  Plug-in > do NuGet
    * A solicitação conterá:
        * a ID e a versão do pacote
        * o local do repositório de origem do pacote
        * o algoritmo de hash
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * um hash de arquivo de pacote usando o algoritmo de hash solicitado se a operação foi bem-sucedida

8.  Obter versões do pacote
    * Direção da solicitação:  Plug-in > do NuGet
    * A solicitação conterá:
        * a ID do pacote
        * o local do repositório de origem do pacote
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * um enumerável de versões de pacote se a operação foi bem-sucedida

9.  Obter índice de serviço
    * Direção da solicitação: > do plugin-NuGet
    * A solicitação conterá:
        * o local do repositório de origem do pacote
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * o índice de serviço se a operação foi bem-sucedida

10.  Handshake
     * Direção da solicitação:  Plug-in < > do NuGet
     * A solicitação conterá:
         * a versão do protocolo do plugin atual
         * a versão mínima do protocolo de plug-in com suporte
     * Uma resposta conterá:
         * um código de resposta que indica o resultado da operação
         * a versão do protocolo negociado se a operação foi bem-sucedida.  Uma falha resultará no encerramento do plug-in.

11.  Initialize
     * Direção da solicitação:  Plug-in > do NuGet
     * A solicitação conterá:
         * a versão da ferramenta do cliente NuGet
         * o idioma efetivo da ferramenta de cliente NuGet.  Isso leva em consideração a configuração ForceEnglishOutput, se usada.
         * o tempo limite de solicitação padrão, que substitui o padrão de protocolo.
     * Uma resposta conterá:
         * um código de resposta que indica o resultado da operação.  Uma falha resultará no encerramento do plug-in.

12.  Log
     * Direção da solicitação: > do plugin-NuGet
     * A solicitação conterá:
         * o nível de log para a solicitação
         * uma mensagem a ser registrada
     * Uma resposta conterá:
         * um código de resposta que indica o resultado da operação.

13.  Monitorar a saída do processo NuGet
     * Direção da solicitação:  Plug-in > do NuGet
     * A solicitação conterá:
         * a ID do processo NuGet
     * Uma resposta conterá:
         * um código de resposta que indica o resultado da operação.

14.  Pacote de pré-busca
     * Direção da solicitação:  Plug-in > do NuGet
     * A solicitação conterá:
         * a ID e a versão do pacote
         * o local do repositório de origem do pacote
     * Uma resposta conterá:
         * um código de resposta que indica o resultado da operação

15.  Definir credenciais
     * Direção da solicitação:  Plug-in > do NuGet
     * A solicitação conterá:
         * o local do repositório de origem do pacote
         * o último nome de usuário de origem do pacote conhecido, se disponível
         * a última senha de origem do pacote conhecida, se disponível
         * o último nome de usuário de proxy conhecido, se disponível
         * a última senha de proxy conhecida, se disponível
     * Uma resposta conterá:
         * um código de resposta que indica o resultado da operação

16.  Definir nível de log
     * Direção da solicitação:  Plug-in > do NuGet
     * A solicitação conterá:
         * o nível de log padrão
     * Uma resposta conterá:
         * um código de resposta que indica o resultado da operação

Mensagens de *2.0.0* de versão de protocolo

17. Obter declarações de operação

* Direção da solicitação:  Plug-in > do NuGet
    * A solicitação conterá:
        * o Service index. JSON para uma origem de pacote
        * o local do repositório de origem do pacote
    * Uma resposta conterá:
        * um código de resposta que indica o resultado da operação
        * um enumerável de operações com suporte se a operação foi bem-sucedida.  Se um plug-in não oferecer suporte à origem do pacote, o plug-in deverá retornar um conjunto vazio de operações com suporte.

    Se o índice de serviço e a origem do pacote forem nulos, o plug-in poderá responder com a autenticação.

18. Obter credenciais de autenticação

* Direção da solicitação: Plug-in > do NuGet
* A solicitação conterá:
    * URI
    * isrepetir
    * NonInteractive
    * Canshowdialog
* Uma resposta conterá
    * Nome de usuário
    * Senha
    * Mensagem
    * Lista de tipos de autenticação
    * MessageResponseCode
