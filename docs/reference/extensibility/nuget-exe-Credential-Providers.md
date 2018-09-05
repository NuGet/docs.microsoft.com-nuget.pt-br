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
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="2b3b1-103">Autenticando feeds com provedores de credenciais nuget.exe</span><span class="sxs-lookup"><span data-stu-id="2b3b1-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="2b3b1-104">*NuGet 3.3 ou superior*</span><span class="sxs-lookup"><span data-stu-id="2b3b1-104">*NuGet 3.3+*</span></span>

<span data-ttu-id="2b3b1-105">Quando `nuget.exe` precisa de credenciais para autenticar com um feed, ele procura-los da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="2b3b1-105">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="2b3b1-106">O NuGet primeiro examina as credenciais em `Nuget.Config` arquivos.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-106">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="2b3b1-107">Em seguida, o NuGet usa provedores de credenciais de plug-in, sujeito a ordem estabelecida abaixo.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-107">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="2b3b1-108">(E o exemplo é o [Visual Studio Team Services credencial Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="2b3b1-108">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="2b3b1-109">O NuGet, em seguida, solicita ao usuário as credenciais na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-109">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="2b3b1-110">Observe que os provedores de credenciais descritos aqui funcionam somente em `nuget.exe` e não em 'dotnet restore' ou o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-110">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="2b3b1-111">Para provedores de credenciais com o Visual Studio, consulte [nuget.exe provedores de credenciais para o Visual Studio](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="2b3b1-111">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="2b3b1-112">provedores de credenciais NuGet.exe podem ser usados em 3 maneiras:</span><span class="sxs-lookup"><span data-stu-id="2b3b1-112">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="2b3b1-113">**Globalmente**: para disponibilizar a todas as instâncias de um provedor de credenciais `nuget.exe` executado no perfil do usuário atual, adicioná-lo ao `%LocalAppData%\NuGet\CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-113">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="2b3b1-114">Talvez você precise criar o `CredentialProviders` pasta.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-114">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="2b3b1-115">Provedores de credenciais podem ser instalados na raiz do `CredentialProviders` pasta ou dentro de uma subpasta.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-115">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="2b3b1-116">Se um provedor de credenciais tiver vários arquivos/assemblies, você pode usar as subpastas para manter os provedores organizados.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-116">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="2b3b1-117">**De uma variável de ambiente**: provedores de credenciais podem ser armazenados em qualquer lugar e ficam acessíveis aos `nuget.exe` definindo o `%NUGET_CREDENTIALPROVIDERS_PATH%` variável de ambiente para o local do provedor.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-117">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="2b3b1-118">Essa variável pode ser uma lista separada por ponto e vírgula (por exemplo, `path1;path2`) se você tiver vários locais.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-118">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="2b3b1-119">**Juntamente com nuget.exe**: nuget.exe provedores de credenciais podem ser colocados na mesma pasta que `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-119">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="2b3b1-120">Ao carregar os provedores de credenciais `nuget.exe` pesquisa os locais acima, em ordem, para qualquer arquivo chamado `credentialprovider*.exe`, em seguida, carrega esses arquivos na ordem em que eles são encontrados.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-120">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="2b3b1-121">Se existirem vários provedores de credenciais na mesma pasta, eles são carregados em ordem alfabética.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-121">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="2b3b1-122">Criando um provedor de credenciais nuget.exe</span><span class="sxs-lookup"><span data-stu-id="2b3b1-122">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="2b3b1-123">Um provedor de credenciais é um executável de linha de comando, denominadas no formato `CredentialProvider*.exe`, que reúne as entradas, obtém as credenciais conforme apropriado e, em seguida, retorna o código de status de saída apropriada e a saída padrão.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-123">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="2b3b1-124">Um provedor deve fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2b3b1-124">A provider must do the following:</span></span>

- <span data-ttu-id="2b3b1-125">Determine se ele pode fornecer credenciais para o URI de destino antes de iniciar a aquisição de credencial.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-125">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="2b3b1-126">Caso contrário, ele deverá retornar o código de status 1 sem credenciais.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-126">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="2b3b1-127">Não modifique `Nuget.Config` (como definir credenciais lá).</span><span class="sxs-lookup"><span data-stu-id="2b3b1-127">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="2b3b1-128">Configuração de proxy HTTP do identificador no seu próprio, como o NuGet não fornece informações de proxy para o plug-in.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-128">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="2b3b1-129">Retornar as credenciais ou detalhes do erro `nuget.exe` escrevendo um objeto de resposta JSON (veja abaixo) para stdout, usando a codificação UTF-8.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-129">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="2b3b1-130">Opcionalmente, emita o registro em log de rastreamento adicionais para stderr.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-130">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="2b3b1-131">Nenhum segredo nunca deve ser escrito para stderr, já que nos níveis de detalhamento "normais" ou "detalhados" rastreamentos são exibidos com o NuGet para o console.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-131">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="2b3b1-132">Parâmetros inesperados devem ser ignorados, fornecendo a compatibilidade com versões futuras do NuGet.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-132">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2b3b1-133">Parâmetros de entrada</span><span class="sxs-lookup"><span data-stu-id="2b3b1-133">Input parameters</span></span>

| <span data-ttu-id="2b3b1-134">Parâmetro/Switch</span><span class="sxs-lookup"><span data-stu-id="2b3b1-134">Parameter/Switch</span></span> |<span data-ttu-id="2b3b1-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="2b3b1-135">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="2b3b1-136">URI {value}</span><span class="sxs-lookup"><span data-stu-id="2b3b1-136">Uri {value}</span></span> | <span data-ttu-id="2b3b1-137">O pacote de origem que exigem credenciais de URI.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-137">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="2b3b1-138">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2b3b1-138">NonInteractive</span></span> | <span data-ttu-id="2b3b1-139">Se estiver presente, o provedor não emite prompts interativos.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-139">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="2b3b1-140">isRetry</span><span class="sxs-lookup"><span data-stu-id="2b3b1-140">IsRetry</span></span> | <span data-ttu-id="2b3b1-141">Se estiver presente, indica que essa tentativa é uma nova tentativa de uma tentativa malsucedida anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-141">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="2b3b1-142">Provedores normalmente usam esse sinalizador para garantir que eles ignoram qualquer cache existente e solicita novas credenciais se possível.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-142">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="2b3b1-143">Detalhamento {value}</span><span class="sxs-lookup"><span data-stu-id="2b3b1-143">Verbosity {value}</span></span> | <span data-ttu-id="2b3b1-144">Se estiver presente, um dos seguintes valores: "normal", "silencioso" ou "detalhado".</span><span class="sxs-lookup"><span data-stu-id="2b3b1-144">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="2b3b1-145">Se nenhum valor for fornecido, padrão é "normal".</span><span class="sxs-lookup"><span data-stu-id="2b3b1-145">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="2b3b1-146">Provedores devem usar isso como uma indicação do nível de registro em log opcional para emitir o fluxo de erro padrão.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-146">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="2b3b1-147">Códigos de saída</span><span class="sxs-lookup"><span data-stu-id="2b3b1-147">Exit codes</span></span>

| <span data-ttu-id="2b3b1-148">Código</span><span class="sxs-lookup"><span data-stu-id="2b3b1-148">Code</span></span> |<span data-ttu-id="2b3b1-149">Resultado</span><span class="sxs-lookup"><span data-stu-id="2b3b1-149">Result</span></span> | <span data-ttu-id="2b3b1-150">Descrição</span><span class="sxs-lookup"><span data-stu-id="2b3b1-150">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="2b3b1-151">0</span><span class="sxs-lookup"><span data-stu-id="2b3b1-151">0</span></span> | <span data-ttu-id="2b3b1-152">Êxito</span><span class="sxs-lookup"><span data-stu-id="2b3b1-152">Success</span></span> | <span data-ttu-id="2b3b1-153">As credenciais foram adquiridas com êxito e foram gravadas em stdout.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-153">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="2b3b1-154">1</span><span class="sxs-lookup"><span data-stu-id="2b3b1-154">1</span></span> | <span data-ttu-id="2b3b1-155">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="2b3b1-155">ProviderNotApplicable</span></span> | <span data-ttu-id="2b3b1-156">O provedor atual não forneça credenciais para o URI fornecido.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-156">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="2b3b1-157">2</span><span class="sxs-lookup"><span data-stu-id="2b3b1-157">2</span></span> | <span data-ttu-id="2b3b1-158">Falha</span><span class="sxs-lookup"><span data-stu-id="2b3b1-158">Failure</span></span> | <span data-ttu-id="2b3b1-159">O provedor é o provedor correto para o URI fornecido, mas não é possível fornecer credenciais.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-159">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="2b3b1-160">Nesse caso, nuget.exe não tentará novamente a autenticação e falhará.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-160">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="2b3b1-161">Um exemplo típico é quando um usuário cancela um logon interativo.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-161">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="2b3b1-162">Saída padrão</span><span class="sxs-lookup"><span data-stu-id="2b3b1-162">Standard output</span></span>

| <span data-ttu-id="2b3b1-163">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2b3b1-163">Property</span></span> |<span data-ttu-id="2b3b1-164">Observações</span><span class="sxs-lookup"><span data-stu-id="2b3b1-164">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="2b3b1-165">Nome de usuário</span><span class="sxs-lookup"><span data-stu-id="2b3b1-165">Username</span></span> | <span data-ttu-id="2b3b1-166">Nome de usuário para solicitações autenticadas.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-166">Username for authenticated requests.</span></span>|
| <span data-ttu-id="2b3b1-167">Senha</span><span class="sxs-lookup"><span data-stu-id="2b3b1-167">Password</span></span> | <span data-ttu-id="2b3b1-168">Senha para solicitações autenticadas.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-168">Password for authenticated requests.</span></span>|
| <span data-ttu-id="2b3b1-169">Mensagem</span><span class="sxs-lookup"><span data-stu-id="2b3b1-169">Message</span></span> | <span data-ttu-id="2b3b1-170">Detalhes opcionais sobre a resposta, usado apenas para mostrar detalhes adicionais em casos de falha.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-170">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="2b3b1-171">Exemplo stdout:</span><span class="sxs-lookup"><span data-stu-id="2b3b1-171">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="2b3b1-172">Solução de problemas de um provedor de credenciais</span><span class="sxs-lookup"><span data-stu-id="2b3b1-172">Troubleshooting a credential provider</span></span>

<span data-ttu-id="2b3b1-173">No momento, o NuGet não oferece muito suporte direto para a depuração de provedores de credenciais personalizado; [emitir 4598](https://github.com/NuGet/Home/issues/4598) está acompanhando esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-173">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="2b3b1-174">Você também pode fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2b3b1-174">You can also do the following:</span></span>

- <span data-ttu-id="2b3b1-175">Executar nuget.exe com o `-verbosity` switch para inspecionar a saída detalhada.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-175">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="2b3b1-176">Adicionar mensagens de depuração para `stdout` em locais adequados.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-176">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="2b3b1-177">Certifique-se de que você esteja usando nuget.exe 3.3 ou superior.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-177">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="2b3b1-178">Anexe o depurador na inicialização com este trecho de código:</span><span class="sxs-lookup"><span data-stu-id="2b3b1-178">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="2b3b1-179">Para obter mais ajuda, [enviar uma solicitação de suporte um nuget.org](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="2b3b1-179">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
