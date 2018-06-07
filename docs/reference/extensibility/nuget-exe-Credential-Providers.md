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
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="c23ee-103">Autenticando feeds com provedores de credenciais de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="c23ee-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="c23ee-104">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="c23ee-104">*NuGet 3.3+*</span></span>

<span data-ttu-id="c23ee-105">Quando `nuget.exe` precisa de credenciais para autenticar com um feed, ele procura-los da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c23ee-105">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="c23ee-106">NuGet primeiro procura por credenciais em `Nuget.Config` arquivos.</span><span class="sxs-lookup"><span data-stu-id="c23ee-106">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="c23ee-107">O NuGet, em seguida, usa provedores de credenciais de plug-in, sujeito à ordem especificada abaixo.</span><span class="sxs-lookup"><span data-stu-id="c23ee-107">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="c23ee-108">(E o exemplo é o [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="c23ee-108">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="c23ee-109">O NuGet, em seguida, solicita ao usuário credenciais na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="c23ee-109">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="c23ee-110">Observe que os provedores de credenciais descritos aqui funcionam somente em `nuget.exe` e não em 'dotnet restauração' ou o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c23ee-110">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="c23ee-111">Para provedores de credenciais com o Visual Studio, consulte [nuget.exe provedores de credenciais para o Visual Studio](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="c23ee-111">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="c23ee-112">provedores de credenciais de NuGet.exe podem ser usados em 3 maneiras:</span><span class="sxs-lookup"><span data-stu-id="c23ee-112">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="c23ee-113">**Globalmente**: para disponibilizar um provedor de credenciais para todas as instâncias de `nuget.exe` executados no perfil do usuário atual, adicione-o para `%LocalAppData%\NuGet\CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="c23ee-113">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="c23ee-114">Talvez seja necessário criar a `CredentialProviders` pasta.</span><span class="sxs-lookup"><span data-stu-id="c23ee-114">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="c23ee-115">Provedores de credenciais podem ser instalados na raiz de `CredentialProviders` pasta ou em uma subpasta.</span><span class="sxs-lookup"><span data-stu-id="c23ee-115">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="c23ee-116">Se um provedor de credenciais tiver vários arquivos/assemblies, você pode usar as subpastas para manter os provedores organizados.</span><span class="sxs-lookup"><span data-stu-id="c23ee-116">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="c23ee-117">**De uma variável de ambiente**: provedores de credenciais podem ser armazenados em qualquer lugar e tornar acessíveis para `nuget.exe` definindo o `%NUGET_CREDENTIALPROVIDERS_PATH%` variável de ambiente para o local do provedor.</span><span class="sxs-lookup"><span data-stu-id="c23ee-117">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="c23ee-118">Essa variável pode ser uma lista separada por ponto e vírgula (por exemplo, `path1;path2`) se você tiver vários locais.</span><span class="sxs-lookup"><span data-stu-id="c23ee-118">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="c23ee-119">**Ao lado de nuget.exe**: nuget.exe provedores de credenciais podem ser colocados na mesma pasta que `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="c23ee-119">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="c23ee-120">Ao carregar os provedores de credenciais, `nuget.exe` pesquisa os locais acima, em ordem, qualquer nomeado de arquivo `credentialprovider*.exe`, em seguida, carrega os arquivos na ordem encontradas.</span><span class="sxs-lookup"><span data-stu-id="c23ee-120">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="c23ee-121">Se existirem vários provedores de credenciais na mesma pasta, eles são carregados em ordem alfabética.</span><span class="sxs-lookup"><span data-stu-id="c23ee-121">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="c23ee-122">Criando um provedor de credenciais de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="c23ee-122">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="c23ee-123">Um provedor de credenciais é um executável de linha de comando, nomeado no formato `CredentialProvider*.exe`, que reúne entradas, adquire credenciais conforme apropriado e, em seguida, retorna a saída padrão e o código de status de saída apropriada.</span><span class="sxs-lookup"><span data-stu-id="c23ee-123">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="c23ee-124">Um provedor deve fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c23ee-124">A provider must do the following:</span></span>

- <span data-ttu-id="c23ee-125">Determine se ele pode fornecer credenciais para o URI de destino antes de iniciar a aquisição de credencial.</span><span class="sxs-lookup"><span data-stu-id="c23ee-125">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="c23ee-126">Caso contrário, ele deverá retornar um código de status 1 sem credenciais.</span><span class="sxs-lookup"><span data-stu-id="c23ee-126">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="c23ee-127">Não modifique `Nuget.Config` (como definir credenciais existe).</span><span class="sxs-lookup"><span data-stu-id="c23ee-127">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="c23ee-128">Configuração de proxy de identificador HTTP no seu próprio, como o NuGet não fornece informações de proxy para o plug-in.</span><span class="sxs-lookup"><span data-stu-id="c23ee-128">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="c23ee-129">Retornar as credenciais ou detalhes de erros para `nuget.exe` escrevendo um objeto de resposta JSON (veja abaixo) para stdout, usando a codificação UTF-8.</span><span class="sxs-lookup"><span data-stu-id="c23ee-129">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="c23ee-130">Se desejar emita o log de rastreamento adicional para stderr.</span><span class="sxs-lookup"><span data-stu-id="c23ee-130">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="c23ee-131">Nenhum segredos nunca devem ser gravados em stderr, pois nos níveis de verbosidade "normais" ou "detalhados" rastreamentos são exibidos pelo NuGet para o console.</span><span class="sxs-lookup"><span data-stu-id="c23ee-131">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="c23ee-132">Parâmetros inesperados devem ser ignorados, fornecendo a compatibilidade com versões futuras do NuGet.</span><span class="sxs-lookup"><span data-stu-id="c23ee-132">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c23ee-133">Parâmetros de entrada</span><span class="sxs-lookup"><span data-stu-id="c23ee-133">Input parameters</span></span>

| <span data-ttu-id="c23ee-134">Parâmetro/Switch</span><span class="sxs-lookup"><span data-stu-id="c23ee-134">Parameter/Switch</span></span> |<span data-ttu-id="c23ee-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="c23ee-135">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="c23ee-136">URI {value}</span><span class="sxs-lookup"><span data-stu-id="c23ee-136">Uri {value}</span></span> | <span data-ttu-id="c23ee-137">Os pacote URI que requerem credenciais de fonte.</span><span class="sxs-lookup"><span data-stu-id="c23ee-137">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="c23ee-138">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c23ee-138">NonInteractive</span></span> | <span data-ttu-id="c23ee-139">Se estiver presente, o provedor não emite prompts interativos.</span><span class="sxs-lookup"><span data-stu-id="c23ee-139">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="c23ee-140">IsRetry</span><span class="sxs-lookup"><span data-stu-id="c23ee-140">IsRetry</span></span> | <span data-ttu-id="c23ee-141">Se estiver presente, indica que essa tentativa é uma repetição de uma tentativa com falha anterior.</span><span class="sxs-lookup"><span data-stu-id="c23ee-141">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="c23ee-142">Os provedores costumam usar este sinalizador para garantir que eles ignoram qualquer cache existente e solicitar novas credenciais se possível.</span><span class="sxs-lookup"><span data-stu-id="c23ee-142">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="c23ee-143">Detalhamento {value}</span><span class="sxs-lookup"><span data-stu-id="c23ee-143">Verbosity {value}</span></span> | <span data-ttu-id="c23ee-144">Se estiver presente, um dos seguintes valores: "normal", "silenciosa" ou "detalhados".</span><span class="sxs-lookup"><span data-stu-id="c23ee-144">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="c23ee-145">Se nenhum valor for fornecido, o padrão será "normal".</span><span class="sxs-lookup"><span data-stu-id="c23ee-145">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="c23ee-146">Provedores devem usar isso como uma indicação do nível de log opcional para emitir o fluxo de erro padrão.</span><span class="sxs-lookup"><span data-stu-id="c23ee-146">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="c23ee-147">Códigos de saída</span><span class="sxs-lookup"><span data-stu-id="c23ee-147">Exit codes</span></span>

| <span data-ttu-id="c23ee-148">Código</span><span class="sxs-lookup"><span data-stu-id="c23ee-148">Code</span></span> |<span data-ttu-id="c23ee-149">Resultado</span><span class="sxs-lookup"><span data-stu-id="c23ee-149">Result</span></span> | <span data-ttu-id="c23ee-150">Descrição</span><span class="sxs-lookup"><span data-stu-id="c23ee-150">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="c23ee-151">0</span><span class="sxs-lookup"><span data-stu-id="c23ee-151">0</span></span> | <span data-ttu-id="c23ee-152">Êxito</span><span class="sxs-lookup"><span data-stu-id="c23ee-152">Success</span></span> | <span data-ttu-id="c23ee-153">As credenciais foram adquiridas com êxito e tiverem sido gravadas em stdout.</span><span class="sxs-lookup"><span data-stu-id="c23ee-153">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="c23ee-154">1</span><span class="sxs-lookup"><span data-stu-id="c23ee-154">1</span></span> | <span data-ttu-id="c23ee-155">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="c23ee-155">ProviderNotApplicable</span></span> | <span data-ttu-id="c23ee-156">O provedor atual não fornece credenciais para o URI fornecido.</span><span class="sxs-lookup"><span data-stu-id="c23ee-156">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="c23ee-157">2</span><span class="sxs-lookup"><span data-stu-id="c23ee-157">2</span></span> | <span data-ttu-id="c23ee-158">Falha</span><span class="sxs-lookup"><span data-stu-id="c23ee-158">Failure</span></span> | <span data-ttu-id="c23ee-159">O provedor é o provedor correto para o URI fornecido, mas não é possível fornecer credenciais.</span><span class="sxs-lookup"><span data-stu-id="c23ee-159">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="c23ee-160">Nesse caso, o nuget.exe não tentará novamente a autenticação e falhará.</span><span class="sxs-lookup"><span data-stu-id="c23ee-160">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="c23ee-161">Um exemplo típico é quando um usuário cancela um logon interativo.</span><span class="sxs-lookup"><span data-stu-id="c23ee-161">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="c23ee-162">Saída padrão</span><span class="sxs-lookup"><span data-stu-id="c23ee-162">Standard output</span></span>

| <span data-ttu-id="c23ee-163">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c23ee-163">Property</span></span> |<span data-ttu-id="c23ee-164">Observações</span><span class="sxs-lookup"><span data-stu-id="c23ee-164">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="c23ee-165">Nome de usuário</span><span class="sxs-lookup"><span data-stu-id="c23ee-165">Username</span></span> | <span data-ttu-id="c23ee-166">Nome de usuário para solicitações autenticadas.</span><span class="sxs-lookup"><span data-stu-id="c23ee-166">Username for authenticated requests.</span></span>|
| <span data-ttu-id="c23ee-167">Senha</span><span class="sxs-lookup"><span data-stu-id="c23ee-167">Password</span></span> | <span data-ttu-id="c23ee-168">Senha para solicitações autenticadas.</span><span class="sxs-lookup"><span data-stu-id="c23ee-168">Password for authenticated requests.</span></span>|
| <span data-ttu-id="c23ee-169">Mensagem</span><span class="sxs-lookup"><span data-stu-id="c23ee-169">Message</span></span> | <span data-ttu-id="c23ee-170">Detalhes opcionais sobre a resposta, usado somente para mostrar detalhes adicionais em casos de falha.</span><span class="sxs-lookup"><span data-stu-id="c23ee-170">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="c23ee-171">Stdout de exemplo:</span><span class="sxs-lookup"><span data-stu-id="c23ee-171">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="c23ee-172">Solucionando problemas de um provedor de credenciais</span><span class="sxs-lookup"><span data-stu-id="c23ee-172">Troubleshooting a credential provider</span></span>

<span data-ttu-id="c23ee-173">No momento, o NuGet não oferece muito suporte direto para depuração de provedores de credenciais personalizado; [emitir 4598](https://github.com/NuGet/Home/issues/4598) para acompanhar esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="c23ee-173">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="c23ee-174">Você também pode fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c23ee-174">You can also do the following:</span></span>

- <span data-ttu-id="c23ee-175">Executar nuget.exe com o `-verbosity` switch para inspecionar a saída detalhada.</span><span class="sxs-lookup"><span data-stu-id="c23ee-175">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="c23ee-176">Adicionar mensagens de depuração para `stdout` em locais apropriados.</span><span class="sxs-lookup"><span data-stu-id="c23ee-176">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="c23ee-177">Certifique-se de que você está usando nuget.exe 3.3 ou superior.</span><span class="sxs-lookup"><span data-stu-id="c23ee-177">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="c23ee-178">Anexe o depurador na inicialização com este trecho de código:</span><span class="sxs-lookup"><span data-stu-id="c23ee-178">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="c23ee-179">Para obter mais ajuda, [enviar uma solicitação de suporte um nuget.org](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="c23ee-179">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
