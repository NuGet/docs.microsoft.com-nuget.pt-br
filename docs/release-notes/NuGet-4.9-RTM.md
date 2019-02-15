---
title: Notas sobre a versão do NuGet 4.9 RTM
description: Notas sobre a versão do NuGet 4.9, incluindo problemas conhecidos, correções de bugs, novas funcionalidades e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: aa9bf87504477506dbb1e9ac10d5c1d5841c224f
ms.sourcegitcommit: 885973352d31808e3ddbb45da6d6e54d1e4fca9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56224938"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="ada80-103">Notas sobre a versão do NuGet 4.9</span><span class="sxs-lookup"><span data-stu-id="ada80-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="ada80-104">Veículos de distribuição do NuGet:</span><span class="sxs-lookup"><span data-stu-id="ada80-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="ada80-105">Versão do NuGet</span><span class="sxs-lookup"><span data-stu-id="ada80-105">NuGet version</span></span> | <span data-ttu-id="ada80-106">Disponível na versão do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ada80-106">Available in Visual Studio version</span></span>| <span data-ttu-id="ada80-107">Disponível em SDKs do .NET</span><span class="sxs-lookup"><span data-stu-id="ada80-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="ada80-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="ada80-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="ada80-109">Visual Studio 2017 versão 15.9.0</span><span class="sxs-lookup"><span data-stu-id="ada80-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="ada80-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="ada80-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="ada80-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="ada80-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="ada80-112">N/D</span><span class="sxs-lookup"><span data-stu-id="ada80-112">n/a</span></span> | <span data-ttu-id="ada80-113">N/D</span><span class="sxs-lookup"><span data-stu-id="ada80-113">n/a</span></span> |
| [<span data-ttu-id="ada80-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="ada80-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="ada80-115">Versão 15.9.4 do Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ada80-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="ada80-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="ada80-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="ada80-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="ada80-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="ada80-118">Visual Studio 2017 versão 15.9.6</span><span class="sxs-lookup"><span data-stu-id="ada80-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="ada80-119">2.1.504, 2.2.104</span><span class="sxs-lookup"><span data-stu-id="ada80-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="ada80-120">Resumo: Novidades no 4.9.0</span><span class="sxs-lookup"><span data-stu-id="ada80-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="ada80-121">Assinatura: Habilite ClientPolicies para exigir o uso de um conjunto de Repositórios e Autores Confiáveis listados em NuGet.Config – [#6961](https://github.com/NuGet/Home/issues/6961), [postagem no blog](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="ada80-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="ada80-122">Crie arquivos ".snupkg" para conter símbolos no pacote – aprimore o envio por push para reconhecer o protocolo nuget para aceitar arquivos snupkg para o servidor de símbolos – [#6878](https://github.com/NuGet/Home/issues/6878), [postagem no blog](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="ada80-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="ada80-123">Plug-in de credencial do NuGet V2 – [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="ada80-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="ada80-124">Pacotes NuGet autossuficientes – Licença – [#4628](https://github.com/NuGet/Home/issues/4628), [comunicado](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="ada80-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="ada80-125">Habilitar a aceitação de metadados "GeneratePathProperty" em um PackageReference para gerar uma propriedade MSBuild por pacote para "Foo.Bar\1.0\" diretório – [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="ada80-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="ada80-126">Ampliar o sucesso do cliente com operações NuGet – [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="ada80-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="ada80-127">Habilitar restaurações de pacote repetitivo usando um arquivo de bloqueio – [#5602](https://github.com/NuGet/Home/issues/5602), [comunicado](https://github.com/NuGet/Announcements/issues/28), [postagem no blog](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="ada80-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ada80-128">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="ada80-128">Issues fixed in this release</span></span>

* <span data-ttu-id="ada80-129">Avisos elevados a erros (por meio de WarnAsErrors) acionados por PackageExtraction não devem deixar para trás pacotes extraídos – [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="ada80-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="ada80-130">Pacotes assinados de forma inadequada não devem acabar na pasta de pacotes globais – [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="ada80-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="ada80-131">a associação da geração de redirecionamento não deve ignorar assemblies de fachada – [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="ada80-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="ada80-132">É igual a VersionRange não compara intervalos flutuantes – [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="ada80-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="ada80-133">Restaurar: regressão de desempenho usando a nova pilha HTTP .NET Core 2.1 – [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="ada80-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="ada80-134">A atualização de um Pacote não deve modificar os PrivateAssets de uma PackageReference – [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="ada80-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="ada80-135">Assinatura: a entrada deverá falhar se um pacote tiver muitas entradas de pacote (>65534) – [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="ada80-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="ada80-136">O caminho de código "dotnet nuget push" deve ser compatível com novas credenciais de provedor – [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="ada80-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="ada80-137">Suporte a plug-ins em execução com cultura invariável (como ocorre no docker) – [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="ada80-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="ada80-138">a adição das fontes de nuget não devem excluir credenciais de NuGet.config – [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="ada80-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="ada80-139">a instalação de um devDependency PackageReference deve ter como padrão excludeassets=compile – [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="ada80-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="ada80-140">corrigir a opção de migrador a ser exibida para todos os projetos e exibir uma mensagem de erro se o projeto for incompatível – [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="ada80-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="ada80-141">o "dotnet add package" deve confirmar a restauração que ele realiza para o arquivo de ativos – [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="ada80-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="ada80-142">Assinatura: melhorar as mensagens de erro relacionadas a assinaturas – [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="ada80-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="ada80-143">[Test Failure][zh-TW]A cadeia de caracteres "Package Manager Console" não é localizada no Console do Gerenciador de Pacotes – [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="ada80-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="ada80-144">Mensagem de erro em torno de "Não é possível encontrar informações sobre o projeto" deve ser um pouco mais específica no VS – [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="ada80-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="ada80-145">Mensagem de erro inútil ao usar incorretamente a marca de versão de nuspec do pacote nuget – [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="ada80-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="ada80-146">DCR – Assinatura; oferece suporte ao protocolo NuGet: recurso RepositorySignatures/4.9.0 – [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="ada80-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="ada80-147">DCR – O arquivo .nupkg.metadata será criado durante a extração do pacote – contém "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="ada80-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="ada80-148">DCR – Ignorar a verificação do código de autenticação de plug-ins durante a execução no Mono – [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="ada80-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="ada80-149">Lista de todos os problemas corrigidos na versão 4.9.0</span><span class="sxs-lookup"><span data-stu-id="ada80-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="ada80-150">Resumo: Novidades no 4.9.1</span><span class="sxs-lookup"><span data-stu-id="ada80-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="ada80-151">Adição de suporte para leitura e gravação para o nuget.config por meio de um novo comando signatários-confiáveis – [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="ada80-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ada80-152">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="ada80-152">Issues fixed in this release</span></span>

* <span data-ttu-id="ada80-153">Correção da geração de links de licença – [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="ada80-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="ada80-154">Regressão de códigos de erro para validação de assinaturas – [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="ada80-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="ada80-155">O pacote NuGet.Build.Tasks.Pack não contém informações de licença – [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="ada80-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="ada80-156">Lista de todas as correções da versão 4.9.1</span><span class="sxs-lookup"><span data-stu-id="ada80-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="ada80-157">Resumo: Novidades no 4.9.2</span><span class="sxs-lookup"><span data-stu-id="ada80-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ada80-158">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="ada80-158">Issues fixed in this release</span></span>

* <span data-ttu-id="ada80-159">O recurso VS/dotnet.exe/nuget.exe/msbuild.exe não usa as credenciais quando o nome de origem contém um espaço em branco – [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="ada80-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="ada80-160">Problemas de acessibilidade LicenseAcceptanceWindow e LicenseFileWindow – [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="ada80-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="ada80-161">Correção de FormatException em DateTime.Parse do DateTimeConverter – [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="ada80-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="ada80-162">Lista de todas as correções da versão 4.9.2</span><span class="sxs-lookup"><span data-stu-id="ada80-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="ada80-163">Resumo: Novidades no 4.9.3</span><span class="sxs-lookup"><span data-stu-id="ada80-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ada80-164">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="ada80-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="ada80-165">Problemas de "restaurações de pacote repetitivo usando um arquivo de bloqueio"</span><span class="sxs-lookup"><span data-stu-id="ada80-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="ada80-166">O modo de bloqueio que não funciona como hash é calculado incorretamente para pacotes armazenados em cache anteriormente – [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="ada80-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="ada80-167">A restauração é resolvida para uma versão diferente da definida no arquivo `packages.lock.json` – [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="ada80-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="ada80-168">'--locked-mode / RestoreLockedMode' causa falhas espúrias de restauração quando ProjectReferences estão envolvidas – [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="ada80-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="ada80-169">O resolvedor MSBuild SDK tenta validar o SHA para um pacote do SDK que falha na restauração ao usar o packages.lock.json – [#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="ada80-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="ada80-170">Problemas de "bloqueio de dependências usando políticas de confiança configuráveis"</span><span class="sxs-lookup"><span data-stu-id="ada80-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="ada80-171">O dotnet.exe não deverá avaliar assinantes confiáveis enquanto não houver suporte a pacotes assinados – [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="ada80-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="ada80-172">A ordem de trustedSigners no arquivo de configuração afeta a avaliação de confiança – [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="ada80-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="ada80-173">Não é possível implementar ISettings [causado pela refatoração de APIs de configurações para dar suporte ao recurso de políticas de confiança] – [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="ada80-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="ada80-174">Problemas de "melhor experiência de depuração"</span><span class="sxs-lookup"><span data-stu-id="ada80-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="ada80-175">Não é possível publicar o pacote de símbolos para .NET Core Global Tool – [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="ada80-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="ada80-176">Problemas de "pacotes NuGet autossuficientes – Licença"</span><span class="sxs-lookup"><span data-stu-id="ada80-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="ada80-177">Erro na criação do pacote .snupkg do símbolo ao usar o arquivo de licença incorporado – [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="ada80-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="ada80-178">Lista de todas as correções da versão 4.9.3</span><span class="sxs-lookup"><span data-stu-id="ada80-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")
## <a name="known-issues"></a><span data-ttu-id="ada80-179">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="ada80-179">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="ada80-180">dotnet nuget push –-a interatividade gera um erro no Mac.</span><span class="sxs-lookup"><span data-stu-id="ada80-180">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="ada80-181"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="ada80-181"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="ada80-182">Problema</span><span class="sxs-lookup"><span data-stu-id="ada80-182">Issue</span></span>
<span data-ttu-id="ada80-183">O argumento `--interactive` não está sendo encaminhado pela cli do dotnet, resultando no erro `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="ada80-183">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="ada80-184">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="ada80-184">Workaround</span></span>
<span data-ttu-id="ada80-185">Execute qualquer outro comando dotnet com a opção interativa, como `dotnet restore --interactive`, e autentique.</span><span class="sxs-lookup"><span data-stu-id="ada80-185">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="ada80-186">A autenticação deve ser armazenada em cache pelo provedor das credenciais.</span><span class="sxs-lookup"><span data-stu-id="ada80-186">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="ada80-187">Em seguida, execute `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="ada80-187">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="ada80-188">Os pacotes em FallbackFolders instalados pelo SDK .NET Core são instalados de forma personalizada e falham ao validar a assinatura.</span><span class="sxs-lookup"><span data-stu-id="ada80-188">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="ada80-189"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="ada80-189"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="ada80-190">Problema</span><span class="sxs-lookup"><span data-stu-id="ada80-190">Issue</span></span>
<span data-ttu-id="ada80-191">Ao usar o dotnet.exe 2.x para restaurar um projeto que fará o direcionamento múltiplo para netcoreapp 1.x e netcoreapp 2.x, a pasta de fallback será tratada como um feed de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ada80-191">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="ada80-192">Isso significa que, ao restaurar, o NuGet escolherá o pacote da pasta de fallback e tentará instalá-lo na pasta de pacotes globais e fazer a validação de assinatura usual que falha.</span><span class="sxs-lookup"><span data-stu-id="ada80-192">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="ada80-193">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="ada80-193">Workaround</span></span>
<span data-ttu-id="ada80-194">Desabilite a pasta de fallback configurando `RestoreAdditionalProjectSources` como nada.</span><span class="sxs-lookup"><span data-stu-id="ada80-194">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="ada80-195">`<RestoreAdditionalProjectSources/>` Use essa opção com cuidado porque ela pode fazer com que muitos dos pacotes sejam baixados do NuGet.org, os quais, normalmente, seriam restaurados da pasta de fallback.</span><span class="sxs-lookup"><span data-stu-id="ada80-195">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
