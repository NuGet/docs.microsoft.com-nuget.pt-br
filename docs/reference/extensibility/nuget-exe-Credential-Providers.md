---
title: Provedores de credenciais de NuGet.exe
description: provedores de credenciais de NuGet.exe autenticam com um feed e são implementados como executáveis de linha de comando que seguem as convenções específicas.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: ebd3354c298eae8bc8158a987327374ac4a8d4f0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818754"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Autenticando feeds com provedores de credenciais de nuget.exe

*NuGet 3.3 +*

Quando `nuget.exe` precisa de credenciais para autenticar com um feed, ele procura-los da seguinte maneira:

1. NuGet primeiro procura por credenciais em `Nuget.Config` arquivos.
1. O NuGet, em seguida, usa provedores de credenciais de plug-in, sujeito à ordem especificada abaixo. (E o exemplo é o [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. O NuGet, em seguida, solicita ao usuário credenciais na linha de comando.

Observe que os provedores de credenciais descritos aqui funcionam somente em `nuget.exe` e não em 'dotnet restauração' ou o Visual Studio. Para provedores de credenciais com o Visual Studio, consulte [nuget.exe provedores de credenciais para o Visual Studio](nuget-credential-providers-for-visual-studio.md)

provedores de credenciais de NuGet.exe podem ser usados em 3 maneiras:

- **Globalmente**: para disponibilizar um provedor de credenciais para todas as instâncias de `nuget.exe` executados no perfil do usuário atual, adicione-o para `%LocalAppData%\NuGet\CredentialProviders`. Talvez seja necessário criar a `CredentialProviders` pasta. Provedores de credenciais podem ser instalados na raiz de `CredentialProviders` pasta ou em uma subpasta. Se um provedor de credenciais tiver vários arquivos/assemblies, você pode usar as subpastas para manter os provedores organizados.

- **De uma variável de ambiente**: provedores de credenciais podem ser armazenados em qualquer lugar e tornar acessíveis para `nuget.exe` definindo o `%NUGET_CREDENTIALPROVIDERS_PATH%` variável de ambiente para o local do provedor. Essa variável pode ser uma lista separada por ponto e vírgula (por exemplo, `path1;path2`) se você tiver vários locais.

- **Ao lado de nuget.exe**: nuget.exe provedores de credenciais podem ser colocados na mesma pasta que `nuget.exe`.

Ao carregar os provedores de credenciais, `nuget.exe` pesquisa os locais acima, em ordem, qualquer nomeado de arquivo `credentialprovider*.exe`, em seguida, carrega os arquivos na ordem encontradas. Se existirem vários provedores de credenciais na mesma pasta, eles são carregados em ordem alfabética.

## <a name="creating-a-nugetexe-credential-provider"></a>Criando um provedor de credenciais de nuget.exe

Um provedor de credenciais é um executável de linha de comando, nomeado no formato `CredentialProvider*.exe`, que reúne entradas, adquire credenciais conforme apropriado e, em seguida, retorna a saída padrão e o código de status de saída apropriada.

Um provedor deve fazer o seguinte:

- Determine se ele pode fornecer credenciais para o URI de destino antes de iniciar a aquisição de credencial. Caso contrário, ele deverá retornar um código de status 1 sem credenciais.
- Não modifique `Nuget.Config` (como definir credenciais existe).
- Configuração de proxy de identificador HTTP no seu próprio, como o NuGet não fornece informações de proxy para o plug-in.
- Retornar as credenciais ou detalhes de erros para `nuget.exe` escrevendo um objeto de resposta JSON (veja abaixo) para stdout, usando a codificação UTF-8.
- Se desejar emita o log de rastreamento adicional para stderr. Nenhum segredos nunca devem ser gravados em stderr, pois nos níveis de verbosidade "normais" ou "detalhados" rastreamentos são exibidos pelo NuGet para o console.
- Parâmetros inesperados devem ser ignorados, fornecendo a compatibilidade com versões futuras do NuGet.

### <a name="input-parameters"></a>Parâmetros de entrada

| Parâmetro/Switch |Descrição|
|----------------|-----------|
| URI {value} | Os pacote URI que requerem credenciais de fonte.|
| NonInteractive | Se estiver presente, o provedor não emite prompts interativos. |
| IsRetry | Se estiver presente, indica que essa tentativa é uma repetição de uma tentativa com falha anterior. Os provedores costumam usar este sinalizador para garantir que eles ignoram qualquer cache existente e solicitar novas credenciais se possível.|
| Detalhamento {value} | Se estiver presente, um dos seguintes valores: "normal", "silenciosa" ou "detalhados". Se nenhum valor for fornecido, o padrão será "normal". Provedores devem usar isso como uma indicação do nível de log opcional para emitir o fluxo de erro padrão. |

### <a name="exit-codes"></a>Códigos de saída

| Código |Resultado | Descrição |
|----------------|-----------|-----------|
| 0 | Êxito | As credenciais foram adquiridas com êxito e tiverem sido gravadas em stdout.|
| 1 | ProviderNotApplicable | O provedor atual não fornece credenciais para o URI fornecido.|
| 2 | Falha | O provedor é o provedor correto para o URI fornecido, mas não é possível fornecer credenciais. Nesse caso, o nuget.exe não tentará novamente a autenticação e falhará. Um exemplo típico é quando um usuário cancela um logon interativo. |

### <a name="standard-output"></a>Saída padrão

| Propriedade |Observações|
|----------------|-----------|
| Nome de usuário | Nome de usuário para solicitações autenticadas.|
| Senha | Senha para solicitações autenticadas.|
| Mensagem | Detalhes opcionais sobre a resposta, usado somente para mostrar detalhes adicionais em casos de falha. |

Stdout de exemplo:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Solucionando problemas de um provedor de credenciais

No momento, o NuGet não oferece muito suporte direto para depuração de provedores de credenciais personalizado; [emitir 4598](https://github.com/NuGet/Home/issues/4598) para acompanhar esse trabalho.

Você também pode fazer o seguinte:

- Executar nuget.exe com o `-verbosity` switch para inspecionar a saída detalhada.
- Adicionar mensagens de depuração para `stdout` em locais apropriados.
- Certifique-se de que você está usando nuget.exe 3.3 ou superior.
- Anexe o depurador na inicialização com este trecho de código:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

Para obter mais ajuda, [enviar uma solicitação de suporte um nuget.org](https://www.nuget.org/policies/Contact).
