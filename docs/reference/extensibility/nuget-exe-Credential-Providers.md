---
title: nuget.exe provedores de credenciais
description: nuget.exe provedores de credenciais autenticam com um feed e são implementados como executáveis de linha de comando que seguem convenções específicas.
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 4f0a5a2355b34c39a435d24691a3f8ea10ee9c00
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323824"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Autenticando feeds com provedores nuget.exe credenciais

O suporte `3.3` à versão foi adicionado para `nuget.exe` provedores de credenciais específicos. Desde então, o suporte de `4.8` [versão para provedores de credenciais](NuGet-Cross-Platform-Authentication-Plugin.md) que funcionam em todos os cenários de linha de comando ( , , ) foi `nuget.exe` `dotnet.exe` `msbuild.exe` adicionado.

Consulte [Consumindo pacotes de feeds autenticados para](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) obter mais detalhes sobre todas as abordagens de autenticação para `nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>nuget.exe do provedor de credenciais

nuget.exe provedores de credenciais podem ser usados de três maneiras:

- **Globalmente:** para disponibilizar um provedor de credenciais para todas as instâncias do executado no perfil do usuário `nuget.exe` atual, adicione-o ao `%LocalAppData%\NuGet\CredentialProviders` . Talvez seja necessário criar a `CredentialProviders` pasta. Os provedores de credenciais podem ser instalados na raiz `CredentialProviders`  da pasta ou em uma subpasta. Se um provedor de credenciais tiver vários arquivos/assemblies, você poderá usar subpastas para manter os provedores organizados.

- **De uma variável de ambiente:** os provedores de credenciais podem ser armazenados em qualquer lugar e ficam acessíveis ao definindo a variável de ambiente `nuget.exe` para o local do `%NUGET_CREDENTIALPROVIDERS_PATH%` provedor. Essa variável pode ser uma lista separada por ponto e vírgula (por exemplo, `path1;path2` ) se você tiver vários locais.

- **Juntamente nuget.exe**: nuget.exe provedores de credenciais podem ser colocados na mesma pasta que `nuget.exe` .

Ao carregar provedores de credenciais, pesquisa os locais acima, em ordem, para qualquer arquivo chamado , em seguida, carrega esses arquivos na ordem `nuget.exe` `credentialprovider*.exe` em que são encontrados. Se existirem vários provedores de credenciais na mesma pasta, eles serão carregados em ordem alfabética.

## <a name="creating-a-nugetexe-credential-provider"></a>Criando um provedor nuget.exe de credenciais

Um provedor de credenciais é um executável de linha de comando, chamado no formato , que coleta entradas, adquire credenciais conforme apropriado e retorna o código de status de saída apropriado e a saída `CredentialProvider*.exe` padrão.

Um provedor deve fazer o seguinte:

- Determine se ele pode fornecer credenciais para o URI de alvo antes de iniciar a aquisição de credenciais. Caso não, ele deverá retornar o código de status 1 sem credenciais.
- Não `NuGet.Config` modifique (como definir credenciais lá).
- Lidar com a configuração de proxy HTTP por conta própria, pois o NuGet não fornece informações de proxy para o plug-in.
- Retorne credenciais ou detalhes de erro para escrevendo um objeto de resposta `nuget.exe` JSON (veja abaixo) em stdout, usando a codificação UTF-8.
- Opcionalmente, emita registro em log de rastreamento adicional para stderr. Nenhum segredo deve ser gravado em stderr, pois, em níveis de detalhamento "normal" ou "detalhado", esses rastreamentos são ecoados pelo NuGet no console.
- Parâmetros inesperados devem ser ignorados, fornecendo compatibilidade com versões futuras do NuGet.

### <a name="input-parameters"></a>Parâmetros de entrada

| Parâmetro/opção |Descrição|
|----------------|-----------|
| Uri {value} | O URI de origem do pacote que exige credenciais.|
| NonInteractive | Se estiver presente, o provedor não emitirá prompts interativos. |
| IsRetry | Se presente, indica que essa tentativa é uma nova tentativa de uma tentativa com falha anterior. Os provedores normalmente usam esse sinalizador para garantir que ignorem qualquer cache existente e solicitam novas credenciais, se possível.|
| Verbosity {value} | Se estiver presente, um dos seguintes valores: "normal", "silencioso" ou "detalhado". Se nenhum valor for fornecido, o padrão será "normal". Os provedores devem usá-lo como uma indicação do nível de log opcional para emitir para o fluxo de erro padrão. |

### <a name="exit-codes"></a>Códigos de saída

| Código |Result | Descrição |
|----------------|-----------|-----------|
| 0 | Êxito | As credenciais foram adquiridas com êxito e foram escritas em stdout.|
| 1 | ProviderNotApplicable | O provedor atual não fornece credenciais para o URI determinado.|
| 2 | Falha | O provedor é o provedor correto para o URI determinado, mas não pode fornecer credenciais. Nesse caso, o nuget.exe não repetirá a autenticação e falhará. Um exemplo típico é quando um usuário cancela um logon interativo. |

### <a name="standard-output"></a>Saída padrão

| Propriedade |Observações|
|----------------|-----------|
| Nome de Usuário | Nome de usuário para solicitações autenticadas.|
| Senha | Senha para solicitações autenticadas.|
| Mensagem | Detalhes opcionais sobre a resposta, usados apenas para mostrar detalhes adicionais em casos de falha. |

Exemplo de stdout:

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a>Solução de problemas de um provedor de credenciais

No momento, o NuGet não oferece suporte direto para depurar provedores de credenciais personalizados; [O problema 4598](https://github.com/NuGet/Home/issues/4598) está acompanhando esse trabalho.

Você também pode fazer o seguinte:

- Execute nuget.exe com a opção `-verbosity` para inspecionar a saída detalhada.
- Adicione mensagens de depuração a `stdout` em locais apropriados.
- Certifique-se de que você está usando nuget.exe 3.3 ou superior.
- Anexe o depurador na inicialização com este snippet de código:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
