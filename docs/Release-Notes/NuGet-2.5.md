---
title: Notas de versão do NuGet 2.5 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Notas de versão do NuGet 2.5, incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs.
keywords: Notas de versão 2.5 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4495e1ea9cc4ec13ef330e56d12de1320cf10b24
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="05c31-104">Notas de versão 2.5 do NuGet</span><span class="sxs-lookup"><span data-stu-id="05c31-104">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="05c31-105">[Notas de versão do NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [notas de versão 2.6 do NuGet](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="05c31-105">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="05c31-106">O NuGet 2.5 foi lançado em 25 de abril de 2013.</span><span class="sxs-lookup"><span data-stu-id="05c31-106">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="05c31-107">Esta versão foi tão grande, percebemos forçadas ignorar as versões 2.3 e 2.4!</span><span class="sxs-lookup"><span data-stu-id="05c31-107">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="05c31-108">Até agora, isso é a versão maior que tivemos para NuGet, com failover [itens de trabalho de 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) na versão.</span><span class="sxs-lookup"><span data-stu-id="05c31-108">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="05c31-109">Confirmações</span><span class="sxs-lookup"><span data-stu-id="05c31-109">Acknowledgements</span></span>

<span data-ttu-id="05c31-110">Gostaríamos de agradecer os seguintes colaboradores externos por suas contribuições significativas para o NuGet 2.5:</span><span class="sxs-lookup"><span data-stu-id="05c31-110">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="05c31-111">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="05c31-111">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="05c31-112">[#2847](https://nuget.codeplex.com/workitem/2847) -adicionar MonoAndroid, MonoTouch e MonoMac à lista de identificadores do framework de destino conhecidos.</span><span class="sxs-lookup"><span data-stu-id="05c31-112">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
1. <span data-ttu-id="05c31-113">[Aragoneses g. Andres](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="05c31-113">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="05c31-114">[#2865](https://nuget.codeplex.com/workitem/2865) -corrija a grafia de `NuGet.targets` para um sistema operacional diferencia maiusculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="05c31-114">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
1. <span data-ttu-id="05c31-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="05c31-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="05c31-116">Verifique a solução Mono de compilação.</span><span class="sxs-lookup"><span data-stu-id="05c31-116">Make the solution build on Mono.</span></span>
1. <span data-ttu-id="05c31-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="05c31-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="05c31-118">Corrija os testes de unidade com falha em Mono.</span><span class="sxs-lookup"><span data-stu-id="05c31-118">Fix unit tests failing on Mono.</span></span>
1. <span data-ttu-id="05c31-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="05c31-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="05c31-120">[#2920](https://nuget.codeplex.com/workitem/2920) -comando de pacote nuget.exe não propaga propriedades para o MSBuild</span><span class="sxs-lookup"><span data-stu-id="05c31-120">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
1. <span data-ttu-id="05c31-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="05c31-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="05c31-122">[#1511](https://nuget.codeplex.com/workitem/1511) - XML modificado código de tratamento para preservar a formatação.</span><span class="sxs-lookup"><span data-stu-id="05c31-122">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
1. <span data-ttu-id="05c31-123">[ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="05c31-123">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="05c31-124">Palavras reconhecidas adicionadas ao dicionário personalizado para permitir que build.cmd seja bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="05c31-124">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
1. [<span data-ttu-id="05c31-125">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="05c31-125">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="05c31-126">Corrija os testes de unidade durante a execução no VS localizadas.</span><span class="sxs-lookup"><span data-stu-id="05c31-126">Fix unit tests when running in localized VS.</span></span>
1. [<span data-ttu-id="05c31-127">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="05c31-127">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="05c31-128">Interface extraído da PackageService</span><span class="sxs-lookup"><span data-stu-id="05c31-128">Extracted interface from PackageService</span></span>
1. <span data-ttu-id="05c31-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="05c31-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
    - <span data-ttu-id="05c31-130">[#936](https://nuget.codeplex.com/workitem/936) -lidar com dependências do projeto quando de remessa</span><span class="sxs-lookup"><span data-stu-id="05c31-130">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
1. <span data-ttu-id="05c31-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="05c31-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
    - <span data-ttu-id="05c31-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -suporte senha com texto não criptografado ao armazenar credenciais de origem do pacote em arquivos de nuget.cofig</span><span class="sxs-lookup"><span data-stu-id="05c31-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
1. <span data-ttu-id="05c31-133">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="05c31-133">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
    - <span data-ttu-id="05c31-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -descrição de Ajuda do Get-Package corrigir</span><span class="sxs-lookup"><span data-stu-id="05c31-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="05c31-135">Agradecemos também as pessoas a seguir para localizar os bugs com o NuGet 2.5 Beta/RC que foram aprovadas e corrigido antes da versão final:</span><span class="sxs-lookup"><span data-stu-id="05c31-135">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="05c31-136">[Parede Tony](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="05c31-136">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="05c31-137">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest dividido com mais recente NuGet 2.4 e 2.5 compilações</span><span class="sxs-lookup"><span data-stu-id="05c31-137">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="05c31-138">Recursos importantes da versão</span><span class="sxs-lookup"><span data-stu-id="05c31-138">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="05c31-139">Permitir que os usuários substituir os arquivos de conteúdo que já existe</span><span class="sxs-lookup"><span data-stu-id="05c31-139">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="05c31-140">Um dos recursos mais solicitados de todo o tempo foi a capacidade de substituir os arquivos de conteúdo que já existem no disco quando incluídos em um pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="05c31-140">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="05c31-141">Começando com o NuGet 2.5, esses conflitos são identificados e você será solicitado a substituir os arquivos, enquanto que anteriormente esses arquivos sempre foram ignorados.</span><span class="sxs-lookup"><span data-stu-id="05c31-141">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Substituir os arquivos de conteúdo](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="05c31-143">'nuget.exe update' e 'Install-Package' agora têm uma nova opção '-FileConflictAction' para definir alguns padrão para cenários de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="05c31-143">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="05c31-144">Defina uma ação padrão quando já existe um arquivo de um pacote no projeto de destino.</span><span class="sxs-lookup"><span data-stu-id="05c31-144">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="05c31-145">Definido como 'Sobrescrever' para substituir os arquivos sempre.</span><span class="sxs-lookup"><span data-stu-id="05c31-145">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="05c31-146">Defina como 'Ignorar' para ignorar arquivos.</span><span class="sxs-lookup"><span data-stu-id="05c31-146">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="05c31-147">Se não for especificado, ele solicitará para cada arquivo conflitante.</span><span class="sxs-lookup"><span data-stu-id="05c31-147">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="05c31-148">Importação automática de arquivos de destino e destinos do MSBuild</span><span class="sxs-lookup"><span data-stu-id="05c31-148">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="05c31-149">Foi criada uma nova pasta convencional no nível superior do pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="05c31-149">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="05c31-150">Como um par de `\lib`, `\content`, e `\tools`, você pode incluir um `\build` pasta em seu pacote.</span><span class="sxs-lookup"><span data-stu-id="05c31-150">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="05c31-151">Nesta pasta, você pode colocar dois arquivos com nomes fixos, `{packageid}.targets` ou `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="05c31-151">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="05c31-152">Esses dois arquivos podem ser diretamente em `build` ou em pastas específicas do framework assim como as outras pastas.</span><span class="sxs-lookup"><span data-stu-id="05c31-152">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="05c31-153">A regra para a pasta de estrutura melhor correspondência de separação é exatamente o mesmo que os.</span><span class="sxs-lookup"><span data-stu-id="05c31-153">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="05c31-154">Quando o NuGet instala um pacote com arquivos \build, ele adicionará um MSBuild `<Import>` elemento no arquivo de projeto apontando para o `.targets` e `.props` arquivos.</span><span class="sxs-lookup"><span data-stu-id="05c31-154">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="05c31-155">O `.props` arquivo é adicionado na parte superior, enquanto o `.targets` é adicionado à parte inferior.</span><span class="sxs-lookup"><span data-stu-id="05c31-155">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="05c31-156">Especifique referências diferentes por plataforma usando `<References/>` elemento</span><span class="sxs-lookup"><span data-stu-id="05c31-156">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="05c31-157">Antes de 2.5, no `.nuspec` arquivo, o usuário só pode especificar os arquivos de referência, a ser adicionada para todos os framework.</span><span class="sxs-lookup"><span data-stu-id="05c31-157">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="05c31-158">Agora com esse novo recurso no 2.5, o usuário pode criar o `<reference/>` elemento para cada plataforma suportada, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05c31-158">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

<span data-ttu-id="05c31-159">Aqui está o fluxo como NuGet adiciona referências a projetos com base no `.nuspec` arquivo:</span><span class="sxs-lookup"><span data-stu-id="05c31-159">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="05c31-160">Localizar o `lib` pasta que é apropriado para a estrutura de destino e obter a lista de assemblies da pasta</span><span class="sxs-lookup"><span data-stu-id="05c31-160">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="05c31-161">Separadamente, localizar o grupo de referências que é apropriado para a estrutura de destino e obter a lista de assemblies do grupo.</span><span class="sxs-lookup"><span data-stu-id="05c31-161">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="05c31-162">Referência sem framework de destino especificado é o grupo de fallback.</span><span class="sxs-lookup"><span data-stu-id="05c31-162">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="05c31-163">Localize a interseção das duas listas e usá-lo como as referências para adicionar</span><span class="sxs-lookup"><span data-stu-id="05c31-163">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="05c31-164">Esse novo recurso permitirá que os autores de pacote usar o recurso de referências para aplicar subconjuntos de assemblies para estruturas diferentes quando eles precisaria executar assemblies duplicados em vários `lib` pastas.</span><span class="sxs-lookup"><span data-stu-id="05c31-164">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="05c31-165">Observação: você deve atualmente usar pacote de nuget.exe para usar esse recurso; Explorador de pacotes do NuGet ainda não suporta-lo.</span><span class="sxs-lookup"><span data-stu-id="05c31-165">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="05c31-166">Atualizar todos os botões para permitir que todos os pacotes de atualização de uma vez</span><span class="sxs-lookup"><span data-stu-id="05c31-166">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="05c31-167">Muitos de vocês sabem sobre o cmdlet do PowerShell "Pacote de atualização" para atualizar todos os pacotes; Agora há uma maneira fácil de fazer isso por meio de interface de usuário.</span><span class="sxs-lookup"><span data-stu-id="05c31-167">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="05c31-168">Para experimentar esse recurso:</span><span class="sxs-lookup"><span data-stu-id="05c31-168">To try this feature out:</span></span>

1. <span data-ttu-id="05c31-169">Criar um novo aplicativo ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="05c31-169">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="05c31-170">Iniciar a caixa de diálogo 'Gerenciar pacotes do NuGet'</span><span class="sxs-lookup"><span data-stu-id="05c31-170">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="05c31-171">Selecione 'Atualizações'</span><span class="sxs-lookup"><span data-stu-id="05c31-171">Select 'Updates'</span></span>
1. <span data-ttu-id="05c31-172">Clique no botão 'Atualizar tudo'</span><span class="sxs-lookup"><span data-stu-id="05c31-172">Click the 'Update All' button</span></span>

![Atualizar todos os botões na caixa de diálogo](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="05c31-174">Suporte de referência de projeto aprimorado para nuget.exe Pack</span><span class="sxs-lookup"><span data-stu-id="05c31-174">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="05c31-175">Agora a processos de comando do pacote de nuget.exe referenciada projetos com as seguintes regras:</span><span class="sxs-lookup"><span data-stu-id="05c31-175">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="05c31-176">Se o projeto referenciado tem correspondente `.nuspec` de arquivos, por exemplo, há um arquivo chamado `proj1.nuspec` na mesma pasta que `proj1.csproj`, este projeto é adicionado como uma dependência no pacote, usando a id e ler a versão do `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="05c31-176">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="05c31-177">Caso contrário, os arquivos do projeto referenciado são incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="05c31-177">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="05c31-178">Em seguida, projetos referenciados por este projeto serão processados usando o mesmos regras recursivamente.</span><span class="sxs-lookup"><span data-stu-id="05c31-178">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="05c31-179">DLL de todos os `.pdb`, e `.exe` arquivos são adicionados.</span><span class="sxs-lookup"><span data-stu-id="05c31-179">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="05c31-180">Todos os outros arquivos de conteúdo são adicionados.</span><span class="sxs-lookup"><span data-stu-id="05c31-180">All other content files are added.</span></span>
1. <span data-ttu-id="05c31-181">Todas as dependências são mescladas.</span><span class="sxs-lookup"><span data-stu-id="05c31-181">All dependencies are merged.</span></span>

<span data-ttu-id="05c31-182">Isso permite que um projeto referenciado deve ser tratada como uma dependência, se houver um `.nuspec` de arquivos, caso contrário, ele se torna parte do pacote.</span><span class="sxs-lookup"><span data-stu-id="05c31-182">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="05c31-183">Mais detalhes aqui: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="05c31-183">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="05c31-184">Adicionar uma propriedade de 'Mínimo a versão do NuGet' para pacotes</span><span class="sxs-lookup"><span data-stu-id="05c31-184">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="05c31-185">Um novo atributo de metadados chamado 'minClientVersion' agora pode indicar a versão de cliente NuGet mínima necessária para consumir um pacote.</span><span class="sxs-lookup"><span data-stu-id="05c31-185">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="05c31-186">Esse recurso ajuda o autor do pacote para especificar que um pacote funcionará somente depois de uma versão específica do NuGet.</span><span class="sxs-lookup"><span data-stu-id="05c31-186">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="05c31-187">Como novo `.nuspec` recursos foram adicionados após o NuGet 2.5 pacotes será capazes de declaração de uma versão mínima do NuGet.</span><span class="sxs-lookup"><span data-stu-id="05c31-187">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="05c31-188">Se o usuário tem o NuGet 2.5 instalado e um pacote é identificado como exigir 2.6, indicações visuais terá para o usuário indicando que o pacote não será instalado.</span><span class="sxs-lookup"><span data-stu-id="05c31-188">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="05c31-189">Em seguida, o usuário será orientado para atualizar sua versão do NuGet.</span><span class="sxs-lookup"><span data-stu-id="05c31-189">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="05c31-190">Isso será aprimoram a experiência existente onde os pacotes de começam a instalar, mas não que indica que uma versão de esquema não reconhecido foi identificada.</span><span class="sxs-lookup"><span data-stu-id="05c31-190">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="05c31-191">Dependências não desnecessariamente são atualizadas durante a instalação do pacote</span><span class="sxs-lookup"><span data-stu-id="05c31-191">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="05c31-192">Antes do NuGet 2.5, quando foi instalado um pacote que depende de um pacote já instalado no projeto, a dependência será atualizada como parte da instalação do novo, mesmo se a versão existente atendidas a dependência.</span><span class="sxs-lookup"><span data-stu-id="05c31-192">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="05c31-193">Começando com o NuGet 2.5, se uma versão de dependência já for atendida, a dependência não será atualizada durante as outras instalações de pacote.</span><span class="sxs-lookup"><span data-stu-id="05c31-193">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="05c31-194">**Cenário:**</span><span class="sxs-lookup"><span data-stu-id="05c31-194">**The scenario:**</span></span>

1. <span data-ttu-id="05c31-195">O repositório de origem contém o pacote B com a versão 1.0.0 e 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="05c31-195">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="05c31-196">Ele também contém o pacote que tem uma dependência em B (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="05c31-196">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="05c31-197">Suponha que o projeto atual já tem a versão do pacote B 1.0.0 instalado.</span><span class="sxs-lookup"><span data-stu-id="05c31-197">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="05c31-198">Agora você deseja instalar a pacote.</span><span class="sxs-lookup"><span data-stu-id="05c31-198">Now you want to install package A.</span></span>

<span data-ttu-id="05c31-199">**No NuGet 2.2 e anterior:**</span><span class="sxs-lookup"><span data-stu-id="05c31-199">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="05c31-200">Ao instalar um pacote, o NuGet será atualizado automaticamente B à 1.0.2, mesmo que a versão existente 1.0.0 já atende à restrição de versão de dependência, que é > = 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="05c31-200">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="05c31-201">**No NuGet 2.5 e mais recente:**</span><span class="sxs-lookup"><span data-stu-id="05c31-201">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="05c31-202">O NuGet não serão mais atualizados B, pois detecta que a versão existente 1.0.0 satisfaz a restrição de versão de dependência.</span><span class="sxs-lookup"><span data-stu-id="05c31-202">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="05c31-203">Para obter mais informações sobre essa alteração, leia o detalhado [item de trabalho](http://nuget.codeplex.com/workitem/1681) , bem como os relacionados [segmento de discussão](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="05c31-203">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="05c31-204">NuGet.exe produz solicitações http com detalhamento detalhado</span><span class="sxs-lookup"><span data-stu-id="05c31-204">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="05c31-205">Se você estiver solucionando problemas de nuget.exe ou apenas curioso que são feitas solicitações HTTP durante operações, o '-detalhes detalhadas ' switch agora mostrará todas as solicitações HTTP feitas.</span><span class="sxs-lookup"><span data-stu-id="05c31-205">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Saída HTTP de nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="05c31-207">push NuGet.exe agora dá suporte a fontes de UNC e pasta</span><span class="sxs-lookup"><span data-stu-id="05c31-207">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="05c31-208">Antes do NuGet 2.5, se você tentou executar 'nuget.exe push' para uma origem de pacote com base em um caminho UNC ou uma pasta local, o envio falhará.</span><span class="sxs-lookup"><span data-stu-id="05c31-208">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="05c31-209">Com o recurso de configuração hierárquica adicionado recentemente, tornou-se comum de nuget.exe para precisa direcionar uma fonte UNC/pasta ou uma galeria do NuGet com base em HTTP.</span><span class="sxs-lookup"><span data-stu-id="05c31-209">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="05c31-210">Começando com o NuGet 2.5 se nuget.exe identifica uma fonte de pasta/UNC, ela executará a cópia do arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="05c31-210">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="05c31-211">O comando a seguir agora funcionará:</span><span class="sxs-lookup"><span data-stu-id="05c31-211">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="05c31-212">NuGet.exe oferece suporte a arquivos de configuração especificado explicitamente</span><span class="sxs-lookup"><span data-stu-id="05c31-212">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="05c31-213">suportam a comandos de NuGet.exe que acessar configuração (todos exceto 'especificação' e 'pacote') agora um novo '-ConfigFile' opção, o que força um arquivo de configuração específico a ser usado no lugar do arquivo de configuração padrão em % AppData%\nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="05c31-213">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="05c31-214">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="05c31-214">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="05c31-215">Suporte para projetos nativos</span><span class="sxs-lookup"><span data-stu-id="05c31-215">Support for Native projects</span></span>

<span data-ttu-id="05c31-216">Com o NuGet 2.5, a NuGet ferramentas agora está disponível para projetos nativos no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="05c31-216">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="05c31-217">Esperamos que mais pacotes nativos utilizará o recurso de importações do MSBuild acima, usando uma ferramenta criada pelo [CoApp projeto](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="05c31-217">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="05c31-218">Para obter mais informações, leia [os detalhes sobre a ferramenta](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) no site da coapp.org.</span><span class="sxs-lookup"><span data-stu-id="05c31-218">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="05c31-219">O nome da estrutura de destino de "nativo" é introduzido para pacotes incluir arquivos no \build \content e \tools quando o pacote for instalado em um projeto nativo.</span><span class="sxs-lookup"><span data-stu-id="05c31-219">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="05c31-220">O \`lib' pasta não é usada para projetos nativos.</span><span class="sxs-lookup"><span data-stu-id="05c31-220">The \`lib` folder is not used for native projects.</span></span>
