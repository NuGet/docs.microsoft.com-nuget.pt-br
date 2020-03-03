---
title: Provedores de credenciais NuGet. exe
description: os provedores de credenciais NuGet. exe são autenticados com um feed e são implementados como executáveis de linha de comando que seguem convenções específicas.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230779"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Autenticando feeds com provedores de credenciais NuGet. exe

Na versão `3.3` suporte foi adicionado para `nuget.exe` provedores de credenciais específicos. Desde então, na versão `4.8` [suporte para provedores de credenciais](NuGet-Cross-Platform-Authentication-Plugin.md) que funcionam em todos os cenários de linha de comando (`nuget.exe`, `dotnet.exe``msbuild.exe`) foi adicionado.

Consulte [consumindo pacotes de feeds autenticados](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) para obter mais detalhes sobre todas as abordagens de autenticação para `nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>descoberta do provedor de credenciais NuGet. exe

os provedores de credenciais NuGet. exe podem ser usados de três maneiras:

- **Globalmente**: para disponibilizar um provedor de credenciais para todas as instâncias do `nuget.exe` executado no perfil do usuário atual, adicione-o ao `%LocalAppData%\NuGet\CredentialProviders`. Talvez seja necessário criar a pasta `CredentialProviders`. Os provedores de credenciais podem ser instalados na raiz da pasta `CredentialProviders` ou em uma subpasta. Se um provedor de credenciais tiver vários arquivos/assemblies, você poderá usar subpastas para manter os provedores organizados.

- **De uma variável de ambiente**: os provedores de credenciais podem ser armazenados em qualquer lugar e acessíveis a `nuget.exe` Configurando a variável de ambiente `%NUGET_CREDENTIALPROVIDERS_PATH%` para o local do provedor. Essa variável pode ser uma lista separada por ponto-e-vírgula (por exemplo, `path1;path2`) se você tiver vários locais.

- **Junto com NuGet. exe**: os provedores de credenciais NuGet. exe podem ser colocados na mesma pasta que `nuget.exe`.

Ao carregar provedores de credenciais, `nuget.exe` pesquisa os locais acima, em ordem, para qualquer arquivo chamado `credentialprovider*.exe`e, em seguida, carrega esses arquivos na ordem em que são encontrados. Se houver vários provedores de credenciais na mesma pasta, eles serão carregados em ordem alfabética.

## <a name="creating-a-nugetexe-credential-provider"></a>Criando um provedor de credenciais NuGet. exe

Um provedor de credenciais é um executável de linha de comando, chamado no formulário `CredentialProvider*.exe`, que coleta entradas, adquire credenciais conforme apropriado e retorna o código de status de saída apropriado e a saída padrão.

Um provedor deve fazer o seguinte:

- Determine se ele pode fornecer credenciais para o URI de destino antes de iniciar a aquisição de credencial. Caso contrário, ele deve retornar o código de status 1 sem credenciais.
- Não modifique `Nuget.Config` (como definir credenciais aqui).
- Manipule a configuração de proxy HTTP por conta própria, pois o NuGet não fornece informações de proxy para o plug-in.
- Retorne as credenciais ou os detalhes do erro para `nuget.exe` escrevendo um objeto de resposta JSON (veja abaixo) para stdout, usando a codificação UTF-8.
- Opcionalmente, emita o log de rastreamento adicional para stderr. Nenhum segredo deve ser gravado em stderr, já que, em níveis de detalhamento "normal" ou "detalhado", esses rastreamentos são ecoados pelo NuGet para o console.
- Parâmetros inesperados devem ser ignorados, fornecendo compatibilidade com versões futuras do NuGet.

### <a name="input-parameters"></a>Parâmetros de entrada

| Parâmetro/opção |DESCRIÇÃO|
|----------------|-----------|
| URI {Value} | O URI de origem do pacote que requer credenciais.|
| NonInteractive | Se estiver presente, o provedor não emitirá prompts interativos. |
| Isrepetir | Se presente, indica que essa tentativa é uma repetição de uma tentativa que falhou anteriormente. Os provedores normalmente usam esse sinalizador para garantir que eles ignorem qualquer cache existente e solicitem novas credenciais, se possível.|
| Detalhes {valor} | Se houver, um dos seguintes valores: "normal", "Quiet" ou "detailed". Se nenhum valor for fornecido, o padrão será "normal". Os provedores devem usar isso como uma indicação do nível de registro em log opcional para emitir para o fluxo de erro padrão. |

### <a name="exit-codes"></a>Códigos de saída

| Código |Result | DESCRIÇÃO |
|----------------|-----------|-----------|
| 0 | Sucesso | As credenciais foram adquiridas com êxito e foram gravadas em stdout.|
| 1 | ProviderNotApplicable | O provedor atual não fornece credenciais para o URI fornecido.|
| 2 | Falha | O provedor é o provedor correto para o URI fornecido, mas não pode fornecer credenciais. Nesse caso, o NuGet. exe não tentará novamente a autenticação e falhará. Um exemplo típico é quando um usuário cancela um logon interativo. |

### <a name="standard-output"></a>Saída padrão

| Propriedade |Observações|
|----------------|-----------|
| Nome de Usuário | Nome de usuário para solicitações autenticadas.|
| Senha | Senha para solicitações autenticadas.|
| Mensagem | Detalhes opcionais sobre a resposta, usados apenas para mostrar detalhes adicionais em casos de falha. |

Exemplo stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Solucionando problemas de um provedor de credenciais

No momento, o NuGet não fornece suporte muito direto para depurar provedores de credenciais personalizados; o [problema 4598](https://github.com/NuGet/Home/issues/4598) está acompanhando esse trabalho.

Você também pode fazer o seguinte:

- Execute NuGet. exe com a opção `-verbosity` para inspecionar a saída detalhada.
- Adicione mensagens de depuração para `stdout` nos locais apropriados.
- Certifique-se de que você está usando NuGet. exe 3,3 ou superior.
- Anexar depurador na inicialização com este trecho de código:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
