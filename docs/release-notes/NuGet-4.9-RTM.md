---
title: Notas sobre a versão do NuGet 4.9 RTM
description: Notas sobre a versão do NuGet 4.9, incluindo problemas conhecidos, correções de bugs, novas funcionalidades e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453765"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="81951-103">Notas sobre a versão do NuGet 4.9</span><span class="sxs-lookup"><span data-stu-id="81951-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="81951-104">O [Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com a funcionalidade do NuGet 4.9.0.</span><span class="sxs-lookup"><span data-stu-id="81951-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.9.0 functionality.</span></span>


<span data-ttu-id="81951-105">Versões de linha de comando da mesma funcionalidade também estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="81951-105">Command line versions of the same functionality are also available:</span></span>
* <span data-ttu-id="81951-106">NuGet.exe 4.9.x – [nuget.org/downloads](https://nuget.org/downloads)</span><span class="sxs-lookup"><span data-stu-id="81951-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span></span>
* <span data-ttu-id="81951-107">DotNet.exe – [SDK do .NET Core 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span><span class="sxs-lookup"><span data-stu-id="81951-107">dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span></span>


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="81951-108">Resumo: novidades no 4.9.0</span><span class="sxs-lookup"><span data-stu-id="81951-108">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="81951-109">Assinatura: habilite ClientPolicies para exigir o uso de um conjunto de Repositórios e Autores Confiáveis listados em NuGet.Config – [#6961](https://github.com/NuGet/Home/issues/6961)</span><span class="sxs-lookup"><span data-stu-id="81951-109">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961)</span></span>

* <span data-ttu-id="81951-110">crie arquivos ".snupkg" para conter símbolos no pacote – aprimore o envio por push para reconhecer o protocolo nuget para aceitar arquivos snupkg para o servidor de símbolos – [#6878](https://github.com/NuGet/Home/issues/6878)</span><span class="sxs-lookup"><span data-stu-id="81951-110">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878)</span></span>

* <span data-ttu-id="81951-111">Plug-in de credencial do NuGet V2 – [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="81951-111">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="81951-112">Pacotes NuGet autossuficientes – Licença – [#4628](https://github.com/NuGet/Home/issues/4628)</span><span class="sxs-lookup"><span data-stu-id="81951-112">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628)</span></span>

* <span data-ttu-id="81951-113">Habilitar a aceitação de metadados "GeneratePathProperty" em um PackageReference para gerar uma propriedade MSBuild por pacote para "Foo.Bar\1.0\" diretório – [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="81951-113">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="81951-114">Ampliar o sucesso do cliente com operações NuGet – [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="81951-114">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="81951-115">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="81951-115">Issues fixed in this release</span></span>

* <span data-ttu-id="81951-116">Avisos elevados a erros (por meio de WarnAsErrors) acionados por PackageExtraction não devem deixar para trás pacotes extraídos – [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="81951-116">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="81951-117">Pacotes assinados de forma inadequada não devem acabar na pasta de pacotes globais – [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="81951-117">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="81951-118">a associação da geração de redirecionamento não deve ignorar assemblies de fachada – [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="81951-118">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="81951-119">É igual a VersionRange não compara intervalos flutuantes – [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="81951-119">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="81951-120">Restaurar: regressão de desempenho usando a nova pilha HTTP .NET Core 2.1 – [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="81951-120">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="81951-121">A atualização de um Pacote não deve modificar os PrivateAssets de uma PackageReference – [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="81951-121">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="81951-122">Assinatura: a entrada deverá falhar se um pacote tiver muitas entradas de pacote (>65534) – [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="81951-122">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="81951-123">O caminho de código "dotnet nuget push" deve ser compatível com novas credenciais de provedor – [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="81951-123">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="81951-124">Suporte a plug-ins em execução com cultura invariável (como ocorre no docker) – [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="81951-124">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="81951-125">a adição das fontes de nuget não devem excluir credenciais de NuGet.config – [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="81951-125">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="81951-126">a instalação de um devDependency PackageReference deve ter como padrão excludeassets=compile – [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="81951-126">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="81951-127">corrigir a opção de migrador a ser exibida para todos os projetos e exibir uma mensagem de erro se o projeto for incompatível – [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="81951-127">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="81951-128">o "dotnet add package" deve confirmar a restauração que ele realiza para o arquivo de ativos – [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="81951-128">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="81951-129">Assinatura: melhorar as mensagens de erro relacionadas a assinaturas – [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="81951-129">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="81951-130">[Test Failure][zh-TW]A cadeia de caracteres "Package Manager Console" não é localizada no Console do Gerenciador de Pacotes – [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="81951-130">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="81951-131">Mensagem de erro em torno de "Não é possível encontrar informações sobre o projeto" deve ser um pouco mais específica no VS – [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="81951-131">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="81951-132">Mensagem de erro inútil ao usar incorretamente a marca de versão de nuspec do pacote nuget – [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="81951-132">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="81951-133">DCR – Assinatura:  suporte para o protocolo NuGet: recurso RepositorySignatures/4.9.0 – [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="81951-133">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="81951-134">DCR – O arquivo .nupkg.metadata será criado durante a extração do pacote – contém "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="81951-134">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="81951-135">DCR – Ignorar a verificação do código de autenticação de plug-ins durante a execução no Mono – [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="81951-135">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="81951-136">Lista de todos os problemas corrigidos na versão 4.9.0</span><span class="sxs-lookup"><span data-stu-id="81951-136">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="81951-137">Resumo: novidades na 4.9.1</span><span class="sxs-lookup"><span data-stu-id="81951-137">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="81951-138">Adição de suporte para leitura e gravação para o nuget.config por meio de um novo comando signatários-confiáveis – [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="81951-138">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="81951-139">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="81951-139">Issues fixed in this release</span></span>

* <span data-ttu-id="81951-140">Correção da geração de links de licença – [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="81951-140">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="81951-141">Regressão de códigos de erro para validação de assinaturas – [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="81951-141">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="81951-142">O pacote NuGet.Build.Tasks.Pack não contém informações de licença – [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="81951-142">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="81951-143">Lista de todas as correções da versão 4.9.1</span><span class="sxs-lookup"><span data-stu-id="81951-143">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="known-issues"></a><span data-ttu-id="81951-144">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="81951-144">Known issues</span></span>

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a><span data-ttu-id="81951-145">dotnet.exe/nuget.exe não usa as credenciais quando o nome de origem contém um espaço em branco – [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="81951-145">dotnet.exe/nuget.exe doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

#### <a name="issue"></a><span data-ttu-id="81951-146">Problema</span><span class="sxs-lookup"><span data-stu-id="81951-146">Issue</span></span>
<span data-ttu-id="81951-147">Quando há um espaço em branco no nome da origem, o nuget.exe gera um erro como `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span><span class="sxs-lookup"><span data-stu-id="81951-147">When there is a whitespace in the source name, nuget.exe throws an error like `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span></span>

#### <a name="workaround"></a><span data-ttu-id="81951-148">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="81951-148">Workaround</span></span>
<span data-ttu-id="81951-149">Altere o nome da origem, eliminando os espaços em branco.</span><span class="sxs-lookup"><span data-stu-id="81951-149">Change the name of the source to not contain a whitespace.</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="81951-150">dotnet nuget push –-a interatividade gera um erro no Mac.</span><span class="sxs-lookup"><span data-stu-id="81951-150">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="81951-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="81951-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="81951-152">Problema</span><span class="sxs-lookup"><span data-stu-id="81951-152">Issue</span></span>
<span data-ttu-id="81951-153">O argumento `--interactive` não está sendo encaminhado pela cli do dotnet, resultando no erro `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="81951-153">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="81951-154">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="81951-154">Workaround</span></span>
<span data-ttu-id="81951-155">Execute qualquer outro comando dotnet com a opção interativa, como `dotnet restore --interactive`, e autentique.</span><span class="sxs-lookup"><span data-stu-id="81951-155">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="81951-156">A autenticação deve ser armazenada em cache pelo provedor das credenciais.</span><span class="sxs-lookup"><span data-stu-id="81951-156">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="81951-157">Em seguida, execute `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="81951-157">Then run `dotnet nuget push`.</span></span>

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a><span data-ttu-id="81951-158">Problemas de acessibilidade LicenseAcceptanceWindow e LicenseFileWindow – [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="81951-158">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

#### <a name="issue"></a><span data-ttu-id="81951-159">Problema</span><span class="sxs-lookup"><span data-stu-id="81951-159">Issue</span></span>
<span data-ttu-id="81951-160">A janela de aceitação de licenças e a janela de arquivos de licença têm problemas de acessibilidade com a navegação por teclado e a narração com o leitor de tela e o JAWS.</span><span class="sxs-lookup"><span data-stu-id="81951-160">The license acceptance window and license file window have accessibility issues with keyboard navigation and narration with screen reader and JAWS.</span></span>

#### <a name="workaround"></a><span data-ttu-id="81951-161">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="81951-161">Workaround</span></span>
<span data-ttu-id="81951-162">Sem solução alternativa.</span><span class="sxs-lookup"><span data-stu-id="81951-162">No workaround.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="81951-163">Os pacotes em FallbackFolders instalados pelo SDK .NET Core são instalados de forma personalizada e falham ao validar a assinatura.</span><span class="sxs-lookup"><span data-stu-id="81951-163">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="81951-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="81951-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="81951-165">Problema</span><span class="sxs-lookup"><span data-stu-id="81951-165">Issue</span></span>
<span data-ttu-id="81951-166">Ao usar o dotnet.exe 2.x para restaurar um projeto que fará o direcionamento múltiplo para netcoreapp 1.x e netcoreapp 2.x, a pasta de fallback será tratada como um feed de arquivos.</span><span class="sxs-lookup"><span data-stu-id="81951-166">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="81951-167">Isso significa que, ao restaurar, o NuGet escolherá o pacote da pasta de fallback e tentará instalá-lo na pasta de pacotes globais e fazer a validação de assinatura usual que falha.</span><span class="sxs-lookup"><span data-stu-id="81951-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="81951-168">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="81951-168">Workaround</span></span>
<span data-ttu-id="81951-169">Desabilite a pasta de fallback configurando `RestoreAdditionalProjectSources` como nada.</span><span class="sxs-lookup"><span data-stu-id="81951-169">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="81951-170">`<RestoreAdditionalProjectSources/>` Use essa opção com cuidado porque ela pode fazer com que muitos dos pacotes sejam baixados do NuGet.org, os quais, normalmente, seriam restaurados da pasta de fallback.</span><span class="sxs-lookup"><span data-stu-id="81951-170">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
