---
title: Provedores de credenciais NuGet. exe
description: os provedores de credenciais NuGet. exe são autenticados com um feed e são implementados como executáveis de linha de comando que seguem convenções específicas.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428719"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="860b1-103">Autenticando feeds com provedores de credenciais NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="860b1-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="860b1-104">Na versão `3.3` suporte foi adicionado para `nuget.exe` provedores de credenciais específicos.</span><span class="sxs-lookup"><span data-stu-id="860b1-104">In version `3.3` support was added for `nuget.exe` specific credential providers.</span></span> <span data-ttu-id="860b1-105">Desde então, na versão `4.8` [suporte para provedores de credenciais](NuGet-Cross-Platform-Authentication-Plugin.md) que funcionam em todos os cenários de linha de comando (`nuget.exe`, `dotnet.exe``msbuild.exe`) foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="860b1-105">Since then, in version `4.8` [support for credential providers](NuGet-Cross-Platform-Authentication-Plugin.md) that work across all command line scenarios (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) was added.</span></span>

<span data-ttu-id="860b1-106">Consulte [consumindo pacotes de feeds autenticados](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) para obter mais detalhes sobre todas as abordagens de autenticação para `nuget.exe`</span><span class="sxs-lookup"><span data-stu-id="860b1-106">See [Consuming Packages from authenticated feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) for more details on all authentication approaches for `nuget.exe`</span></span>

## <a name="nugetexe-credential-provider-discovery"></a><span data-ttu-id="860b1-107">descoberta do provedor de credenciais NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="860b1-107">nuget.exe credential provider discovery</span></span>

<span data-ttu-id="860b1-108">os provedores de credenciais NuGet. exe podem ser usados de três maneiras:</span><span class="sxs-lookup"><span data-stu-id="860b1-108">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="860b1-109">**Globalmente**: para disponibilizar um provedor de credenciais para todas as instâncias do `nuget.exe` executado no perfil do usuário atual, adicione-o ao `%LocalAppData%\NuGet\CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="860b1-109">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="860b1-110">Talvez seja necessário criar a pasta `CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="860b1-110">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="860b1-111">Os provedores de credenciais podem ser instalados na raiz da pasta `CredentialProviders` ou em uma subpasta.</span><span class="sxs-lookup"><span data-stu-id="860b1-111">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="860b1-112">Se um provedor de credenciais tiver vários arquivos/assemblies, você poderá usar subpastas para manter os provedores organizados.</span><span class="sxs-lookup"><span data-stu-id="860b1-112">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="860b1-113">**De uma variável de ambiente**: os provedores de credenciais podem ser armazenados em qualquer lugar e acessíveis a `nuget.exe` Configurando a variável de ambiente `%NUGET_CREDENTIALPROVIDERS_PATH%` para o local do provedor.</span><span class="sxs-lookup"><span data-stu-id="860b1-113">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="860b1-114">Essa variável pode ser uma lista separada por ponto-e-vírgula (por exemplo, `path1;path2`) se você tiver vários locais.</span><span class="sxs-lookup"><span data-stu-id="860b1-114">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="860b1-115">**Junto com NuGet. exe**: os provedores de credenciais NuGet. exe podem ser colocados na mesma pasta que `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="860b1-115">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="860b1-116">Ao carregar provedores de credenciais, `nuget.exe` pesquisa os locais acima, em ordem, para qualquer arquivo chamado `credentialprovider*.exe`e, em seguida, carrega esses arquivos na ordem em que são encontrados.</span><span class="sxs-lookup"><span data-stu-id="860b1-116">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="860b1-117">Se houver vários provedores de credenciais na mesma pasta, eles serão carregados em ordem alfabética.</span><span class="sxs-lookup"><span data-stu-id="860b1-117">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="860b1-118">Criando um provedor de credenciais NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="860b1-118">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="860b1-119">Um provedor de credenciais é um executável de linha de comando, chamado no formulário `CredentialProvider*.exe`, que coleta entradas, adquire credenciais conforme apropriado e retorna o código de status de saída apropriado e a saída padrão.</span><span class="sxs-lookup"><span data-stu-id="860b1-119">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="860b1-120">Um provedor deve fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="860b1-120">A provider must do the following:</span></span>

- <span data-ttu-id="860b1-121">Determine se ele pode fornecer credenciais para o URI de destino antes de iniciar a aquisição de credencial.</span><span class="sxs-lookup"><span data-stu-id="860b1-121">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="860b1-122">Caso contrário, ele deve retornar o código de status 1 sem credenciais.</span><span class="sxs-lookup"><span data-stu-id="860b1-122">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="860b1-123">Não modifique `Nuget.Config` (como definir credenciais aqui).</span><span class="sxs-lookup"><span data-stu-id="860b1-123">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="860b1-124">Manipule a configuração de proxy HTTP por conta própria, pois o NuGet não fornece informações de proxy para o plug-in.</span><span class="sxs-lookup"><span data-stu-id="860b1-124">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="860b1-125">Retorne as credenciais ou os detalhes do erro para `nuget.exe` escrevendo um objeto de resposta JSON (veja abaixo) para stdout, usando a codificação UTF-8.</span><span class="sxs-lookup"><span data-stu-id="860b1-125">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="860b1-126">Opcionalmente, emita o log de rastreamento adicional para stderr.</span><span class="sxs-lookup"><span data-stu-id="860b1-126">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="860b1-127">Nenhum segredo deve ser gravado em stderr, já que, em níveis de detalhamento "normal" ou "detalhado", esses rastreamentos são ecoados pelo NuGet para o console.</span><span class="sxs-lookup"><span data-stu-id="860b1-127">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="860b1-128">Parâmetros inesperados devem ser ignorados, fornecendo compatibilidade com versões futuras do NuGet.</span><span class="sxs-lookup"><span data-stu-id="860b1-128">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="860b1-129">Parâmetros de entrada</span><span class="sxs-lookup"><span data-stu-id="860b1-129">Input parameters</span></span>

| <span data-ttu-id="860b1-130">Parâmetro/opção</span><span class="sxs-lookup"><span data-stu-id="860b1-130">Parameter/Switch</span></span> |<span data-ttu-id="860b1-131">Descrição</span><span class="sxs-lookup"><span data-stu-id="860b1-131">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="860b1-132">URI {Value}</span><span class="sxs-lookup"><span data-stu-id="860b1-132">Uri {value}</span></span> | <span data-ttu-id="860b1-133">O URI de origem do pacote que requer credenciais.</span><span class="sxs-lookup"><span data-stu-id="860b1-133">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="860b1-134">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="860b1-134">NonInteractive</span></span> | <span data-ttu-id="860b1-135">Se estiver presente, o provedor não emitirá prompts interativos.</span><span class="sxs-lookup"><span data-stu-id="860b1-135">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="860b1-136">Isrepetir</span><span class="sxs-lookup"><span data-stu-id="860b1-136">IsRetry</span></span> | <span data-ttu-id="860b1-137">Se presente, indica que essa tentativa é uma repetição de uma tentativa que falhou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="860b1-137">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="860b1-138">Os provedores normalmente usam esse sinalizador para garantir que eles ignorem qualquer cache existente e solicitem novas credenciais, se possível.</span><span class="sxs-lookup"><span data-stu-id="860b1-138">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="860b1-139">Detalhes {valor}</span><span class="sxs-lookup"><span data-stu-id="860b1-139">Verbosity {value}</span></span> | <span data-ttu-id="860b1-140">Se houver, um dos seguintes valores: "normal", "Quiet" ou "detailed".</span><span class="sxs-lookup"><span data-stu-id="860b1-140">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="860b1-141">Se nenhum valor for fornecido, o padrão será "normal".</span><span class="sxs-lookup"><span data-stu-id="860b1-141">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="860b1-142">Os provedores devem usar isso como uma indicação do nível de registro em log opcional para emitir para o fluxo de erro padrão.</span><span class="sxs-lookup"><span data-stu-id="860b1-142">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="860b1-143">Códigos de saída</span><span class="sxs-lookup"><span data-stu-id="860b1-143">Exit codes</span></span>

| <span data-ttu-id="860b1-144">Código</span><span class="sxs-lookup"><span data-stu-id="860b1-144">Code</span></span> |<span data-ttu-id="860b1-145">Resultado</span><span class="sxs-lookup"><span data-stu-id="860b1-145">Result</span></span> | <span data-ttu-id="860b1-146">Descrição</span><span class="sxs-lookup"><span data-stu-id="860b1-146">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="860b1-147">0</span><span class="sxs-lookup"><span data-stu-id="860b1-147">0</span></span> | <span data-ttu-id="860b1-148">Êxito</span><span class="sxs-lookup"><span data-stu-id="860b1-148">Success</span></span> | <span data-ttu-id="860b1-149">As credenciais foram adquiridas com êxito e foram gravadas em stdout.</span><span class="sxs-lookup"><span data-stu-id="860b1-149">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="860b1-150">1</span><span class="sxs-lookup"><span data-stu-id="860b1-150">1</span></span> | <span data-ttu-id="860b1-151">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="860b1-151">ProviderNotApplicable</span></span> | <span data-ttu-id="860b1-152">O provedor atual não fornece credenciais para o URI fornecido.</span><span class="sxs-lookup"><span data-stu-id="860b1-152">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="860b1-153">2</span><span class="sxs-lookup"><span data-stu-id="860b1-153">2</span></span> | <span data-ttu-id="860b1-154">Falha</span><span class="sxs-lookup"><span data-stu-id="860b1-154">Failure</span></span> | <span data-ttu-id="860b1-155">O provedor é o provedor correto para o URI fornecido, mas não pode fornecer credenciais.</span><span class="sxs-lookup"><span data-stu-id="860b1-155">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="860b1-156">Nesse caso, o NuGet. exe não tentará novamente a autenticação e falhará.</span><span class="sxs-lookup"><span data-stu-id="860b1-156">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="860b1-157">Um exemplo típico é quando um usuário cancela um logon interativo.</span><span class="sxs-lookup"><span data-stu-id="860b1-157">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="860b1-158">Saída padrão</span><span class="sxs-lookup"><span data-stu-id="860b1-158">Standard output</span></span>

| <span data-ttu-id="860b1-159">Propriedade</span><span class="sxs-lookup"><span data-stu-id="860b1-159">Property</span></span> |<span data-ttu-id="860b1-160">{1&gt;Observações&lt;1}</span><span class="sxs-lookup"><span data-stu-id="860b1-160">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="860b1-161">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="860b1-161">Username</span></span> | <span data-ttu-id="860b1-162">Nome de usuário para solicitações autenticadas.</span><span class="sxs-lookup"><span data-stu-id="860b1-162">Username for authenticated requests.</span></span>|
| <span data-ttu-id="860b1-163">Senha</span><span class="sxs-lookup"><span data-stu-id="860b1-163">Password</span></span> | <span data-ttu-id="860b1-164">Senha para solicitações autenticadas.</span><span class="sxs-lookup"><span data-stu-id="860b1-164">Password for authenticated requests.</span></span>|
| <span data-ttu-id="860b1-165">Mensagem</span><span class="sxs-lookup"><span data-stu-id="860b1-165">Message</span></span> | <span data-ttu-id="860b1-166">Detalhes opcionais sobre a resposta, usados apenas para mostrar detalhes adicionais em casos de falha.</span><span class="sxs-lookup"><span data-stu-id="860b1-166">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="860b1-167">Exemplo stdout:</span><span class="sxs-lookup"><span data-stu-id="860b1-167">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="860b1-168">Solucionando problemas de um provedor de credenciais</span><span class="sxs-lookup"><span data-stu-id="860b1-168">Troubleshooting a credential provider</span></span>

<span data-ttu-id="860b1-169">No momento, o NuGet não fornece suporte muito direto para depurar provedores de credenciais personalizados; o [problema 4598](https://github.com/NuGet/Home/issues/4598) está acompanhando esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="860b1-169">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="860b1-170">Você também pode fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="860b1-170">You can also do the following:</span></span>

- <span data-ttu-id="860b1-171">Execute NuGet. exe com a opção `-verbosity` para inspecionar a saída detalhada.</span><span class="sxs-lookup"><span data-stu-id="860b1-171">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="860b1-172">Adicione mensagens de depuração para `stdout` nos locais apropriados.</span><span class="sxs-lookup"><span data-stu-id="860b1-172">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="860b1-173">Certifique-se de que você está usando NuGet. exe 3,3 ou superior.</span><span class="sxs-lookup"><span data-stu-id="860b1-173">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="860b1-174">Anexar depurador na inicialização com este trecho de código:</span><span class="sxs-lookup"><span data-stu-id="860b1-174">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
