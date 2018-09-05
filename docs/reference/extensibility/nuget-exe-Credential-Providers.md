---
title: Provedores de credenciais NuGet.exe
description: provedores de credenciais NuGet.exe autenticam com um feed e são implementados como executáveis de linha de comando que seguem as convenções específicas.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550183"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Autenticando feeds com provedores de credenciais nuget.exe

*NuGet 3.3 ou superior*

Quando `nuget.exe` precisa de credenciais para autenticar com um feed, ele procura-los da seguinte maneira:

1. O NuGet primeiro examina as credenciais em `Nuget.Config` arquivos.
1. Em seguida, o NuGet usa provedores de credenciais de plug-in, sujeito a ordem estabelecida abaixo. (E o exemplo é o [Visual Studio Team Services credencial Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. O NuGet, em seguida, solicita ao usuário as credenciais na linha de comando.

Observe que os provedores de credenciais descritos aqui funcionam somente em `nuget.exe` e não em 'dotnet restore' ou o Visual Studio. Para provedores de credenciais com o Visual Studio, consulte [nuget.exe provedores de credenciais para o Visual Studio](nuget-credential-providers-for-visual-studio.md)

provedores de credenciais NuGet.exe podem ser usados em 3 maneiras:

- **Globalmente**: para disponibilizar a todas as instâncias de um provedor de credenciais `nuget.exe` executado no perfil do usuário atual, adicioná-lo ao `%LocalAppData%\NuGet\CredentialProviders`. Talvez você precise criar o `CredentialProviders` pasta. Provedores de credenciais podem ser instalados na raiz do `CredentialProviders` pasta ou dentro de uma subpasta. Se um provedor de credenciais tiver vários arquivos/assemblies, você pode usar as subpastas para manter os provedores organizados.

- **De uma variável de ambiente**: provedores de credenciais podem ser armazenados em qualquer lugar e ficam acessíveis aos `nuget.exe` definindo o `%NUGET_CREDENTIALPROVIDERS_PATH%` variável de ambiente para o local do provedor. Essa variável pode ser uma lista separada por ponto e vírgula (por exemplo, `path1;path2`) se você tiver vários locais.

- **Juntamente com nuget.exe**: nuget.exe provedores de credenciais podem ser colocados na mesma pasta que `nuget.exe`.

Ao carregar os provedores de credenciais `nuget.exe` pesquisa os locais acima, em ordem, para qualquer arquivo chamado `credentialprovider*.exe`, em seguida, carrega esses arquivos na ordem em que eles são encontrados. Se existirem vários provedores de credenciais na mesma pasta, eles são carregados em ordem alfabética.

## <a name="creating-a-nugetexe-credential-provider"></a>Criando um provedor de credenciais nuget.exe

Um provedor de credenciais é um executável de linha de comando, denominadas no formato `CredentialProvider*.exe`, que reúne as entradas, obtém as credenciais conforme apropriado e, em seguida, retorna o código de status de saída apropriada e a saída padrão.

Um provedor deve fazer o seguinte:

- Determine se ele pode fornecer credenciais para o URI de destino antes de iniciar a aquisição de credencial. Caso contrário, ele deverá retornar o código de status 1 sem credenciais.
- Não modifique `Nuget.Config` (como definir credenciais lá).
- Configuração de proxy HTTP do identificador no seu próprio, como o NuGet não fornece informações de proxy para o plug-in.
- Retornar as credenciais ou detalhes do erro `nuget.exe` escrevendo um objeto de resposta JSON (veja abaixo) para stdout, usando a codificação UTF-8.
- Opcionalmente, emita o registro em log de rastreamento adicionais para stderr. Nenhum segredo nunca deve ser escrito para stderr, já que nos níveis de detalhamento "normais" ou "detalhados" rastreamentos são exibidos com o NuGet para o console.
- Parâmetros inesperados devem ser ignorados, fornecendo a compatibilidade com versões futuras do NuGet.

### <a name="input-parameters"></a>Parâmetros de entrada

| Parâmetro/Switch |Descrição|
|----------------|-----------|
| URI {value} | O pacote de origem que exigem credenciais de URI.|
| NonInteractive | Se estiver presente, o provedor não emite prompts interativos. |
| isRetry | Se estiver presente, indica que essa tentativa é uma nova tentativa de uma tentativa malsucedida anteriormente. Provedores normalmente usam esse sinalizador para garantir que eles ignoram qualquer cache existente e solicita novas credenciais se possível.|
| Detalhamento {value} | Se estiver presente, um dos seguintes valores: "normal", "silencioso" ou "detalhado". Se nenhum valor for fornecido, padrão é "normal". Provedores devem usar isso como uma indicação do nível de registro em log opcional para emitir o fluxo de erro padrão. |

### <a name="exit-codes"></a>Códigos de saída

| Código |Resultado | Descrição |
|----------------|-----------|-----------|
| 0 | Êxito | As credenciais foram adquiridas com êxito e foram gravadas em stdout.|
| 1 | ProviderNotApplicable | O provedor atual não forneça credenciais para o URI fornecido.|
| 2 | Falha | O provedor é o provedor correto para o URI fornecido, mas não é possível fornecer credenciais. Nesse caso, nuget.exe não tentará novamente a autenticação e falhará. Um exemplo típico é quando um usuário cancela um logon interativo. |

### <a name="standard-output"></a>Saída padrão

| Propriedade |Observações|
|----------------|-----------|
| Nome de usuário | Nome de usuário para solicitações autenticadas.|
| Senha | Senha para solicitações autenticadas.|
| Mensagem | Detalhes opcionais sobre a resposta, usado apenas para mostrar detalhes adicionais em casos de falha. |

Exemplo stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Solução de problemas de um provedor de credenciais

No momento, o NuGet não oferece muito suporte direto para a depuração de provedores de credenciais personalizado; [emitir 4598](https://github.com/NuGet/Home/issues/4598) está acompanhando esse trabalho.

Você também pode fazer o seguinte:

- Executar nuget.exe com o `-verbosity` switch para inspecionar a saída detalhada.
- Adicionar mensagens de depuração para `stdout` em locais adequados.
- Certifique-se de que você esteja usando nuget.exe 3.3 ou superior.
- Anexe o depurador na inicialização com este trecho de código:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

Para obter mais ajuda, [enviar uma solicitação de suporte um nuget.org](https://www.nuget.org/policies/Contact).
