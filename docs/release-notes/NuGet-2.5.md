---
title: Notas de versão do NuGet 2,5
description: Notas de versão do NuGet 2,5 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428712"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="13940-103">Notas de versão do NuGet 2,5</span><span class="sxs-lookup"><span data-stu-id="13940-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="13940-104">[Notas de versão do NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [notas de versão do NuGet 2,6](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="13940-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="13940-105">O NuGet 2,5 foi lançado em 25 de abril de 2013.</span><span class="sxs-lookup"><span data-stu-id="13940-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="13940-106">Essa versão foi tão grande, nós achamos obrigado a ignorar as versões 2,3 e 2,4!</span><span class="sxs-lookup"><span data-stu-id="13940-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="13940-107">Até o momento, esta é a maior versão que tínhamos para o NuGet, com mais de [160 itens de trabalho](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) na versão.</span><span class="sxs-lookup"><span data-stu-id="13940-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="13940-108">Agradecimentos</span><span class="sxs-lookup"><span data-stu-id="13940-108">Acknowledgements</span></span>

<span data-ttu-id="13940-109">Gostaríamos de agradecer aos seguintes colaboradores externos por suas contribuições significativas para o NuGet 2,5:</span><span class="sxs-lookup"><span data-stu-id="13940-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="13940-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="13940-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="13940-111">[#2847](https://nuget.codeplex.com/workitem/2847) -adicione o monoandroid, o MonoTouch e o MonoMac à lista de identificadores de estrutura de destino conhecidos.</span><span class="sxs-lookup"><span data-stu-id="13940-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="13940-112">[Andres G. aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="13940-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="13940-113">[#2865](https://nuget.codeplex.com/workitem/2865) -corrigir a ortografia de `NuGet.targets` para um sistema operacional que diferencia maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="13940-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="13940-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="13940-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="13940-115">Faça com que a solução seja criada no mono.</span><span class="sxs-lookup"><span data-stu-id="13940-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="13940-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="13940-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="13940-117">Corrigir testes de unidade com falha no mono.</span><span class="sxs-lookup"><span data-stu-id="13940-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="13940-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="13940-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="13940-119">[#2920](https://nuget.codeplex.com/workitem/2920) -o comando do pacote NuGet. exe não propaga as propriedades para o MSBuild</span><span class="sxs-lookup"><span data-stu-id="13940-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="13940-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="13940-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="13940-121">código de manipulação XML modificado [#1511](https://nuget.codeplex.com/workitem/1511) para preservar a formatação.</span><span class="sxs-lookup"><span data-stu-id="13940-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="13940-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="13940-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="13940-123">Palavras reconhecidas adicionadas ao dicionário personalizado para permitir que o Build. cmd tenha sucesso.</span><span class="sxs-lookup"><span data-stu-id="13940-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="13940-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="13940-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="13940-125">Corrigir testes de unidade durante a execução no localizado VS.</span><span class="sxs-lookup"><span data-stu-id="13940-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="13940-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="13940-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="13940-127">Interface extraída de PackageService</span><span class="sxs-lookup"><span data-stu-id="13940-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="13940-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="13940-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="13940-129">[#936](https://nuget.codeplex.com/workitem/936) -tratar dependências do projeto ao empacotar</span><span class="sxs-lookup"><span data-stu-id="13940-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="13940-130">[Xavier de descusto](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="13940-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="13940-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -dar suporte à senha de texto não criptografado ao armazenar as credenciais de origem do pacote em arquivos NuGet. cofig</span><span class="sxs-lookup"><span data-stu-id="13940-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="13940-132">[James Manning Publications](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="13940-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="13940-133">[#3190](http://nuget.codeplex.com/workitem/3190), descrição de ajuda do Get-Package do [#3191](http://nuget.codeplex.com/workitem/3191) -Fix</span><span class="sxs-lookup"><span data-stu-id="13940-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="13940-134">Também apreciamos os seguintes indivíduos para encontrar bugs com o NuGet 2,5 Beta/RC que foram aprovados e corrigidos antes da versão final:</span><span class="sxs-lookup"><span data-stu-id="13940-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="13940-135">[Tony parede](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="13940-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="13940-136">[#3200](https://nuget.codeplex.com/workitem/3200) -MSTest rompido com as compilações mais recentes do NuGet 2,4 e 2,5</span><span class="sxs-lookup"><span data-stu-id="13940-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="13940-137">Recursos notáveis na versão</span><span class="sxs-lookup"><span data-stu-id="13940-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="13940-138">Permitir que os usuários substituam os arquivos de conteúdo que já existem</span><span class="sxs-lookup"><span data-stu-id="13940-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="13940-139">Um dos recursos mais solicitados de todo o tempo foi a capacidade de substituir os arquivos de conteúdo que já existem no disco quando incluídos em um pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="13940-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="13940-140">A partir do NuGet 2,5, esses conflitos são identificados e você é solicitado a substituir os arquivos, enquanto anteriormente esses arquivos eram sempre ignorados.</span><span class="sxs-lookup"><span data-stu-id="13940-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Substituir arquivos de conteúdo](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="13940-142">"NuGet. exe update" e "Install-Package" agora têm uma nova opção "-fileconflitoaction" para definir um padrão para cenários de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="13940-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="13940-143">Defina uma ação padrão quando um arquivo de um pacote já existir no projeto de destino.</span><span class="sxs-lookup"><span data-stu-id="13940-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="13940-144">Defina como ' overwrite ' para sempre substituir arquivos.</span><span class="sxs-lookup"><span data-stu-id="13940-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="13940-145">Defina como ' ignorar ' para ignorar arquivos.</span><span class="sxs-lookup"><span data-stu-id="13940-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="13940-146">Se não for especificado, ele solicitará cada arquivo conflitante.</span><span class="sxs-lookup"><span data-stu-id="13940-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="13940-147">Importação automática de destinos do MSBuild e arquivos de props</span><span class="sxs-lookup"><span data-stu-id="13940-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="13940-148">Uma nova pasta convencional foi criada no nível superior do pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="13940-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="13940-149">Como um par para `\lib`, `\content`e `\tools`, agora você pode incluir uma pasta `\build` em seu pacote.</span><span class="sxs-lookup"><span data-stu-id="13940-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="13940-150">Nessa pasta, você pode posicionar dois arquivos com nomes fixos, `{packageid}.targets` ou `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="13940-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="13940-151">Esses dois arquivos podem ser diretamente sob `build` ou em pastas específicas da estrutura, assim como as outras pastas.</span><span class="sxs-lookup"><span data-stu-id="13940-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="13940-152">A regra para escolher a pasta de estrutura de melhor correspondência é exatamente a mesma daquela.</span><span class="sxs-lookup"><span data-stu-id="13940-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="13940-153">Quando o NuGet instala um pacote com arquivos \Build, ele adicionará um elemento de `<Import>` do MSBuild no arquivo de projeto apontando para os arquivos `.targets` e `.props`.</span><span class="sxs-lookup"><span data-stu-id="13940-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="13940-154">O arquivo de `.props` é adicionado na parte superior, enquanto o arquivo de `.targets` é adicionado à parte inferior.</span><span class="sxs-lookup"><span data-stu-id="13940-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="13940-155">Especificar referências diferentes por plataforma usando o elemento `<References/>`</span><span class="sxs-lookup"><span data-stu-id="13940-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="13940-156">Antes de 2,5, no arquivo `.nuspec`, o usuário só pode especificar os arquivos de referência para serem adicionados a todas as estruturas.</span><span class="sxs-lookup"><span data-stu-id="13940-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="13940-157">Agora, com esse novo recurso do 2,5, o usuário pode criar o elemento `<reference/>` para cada uma das plataformas com suporte, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="13940-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="13940-158">Este é o fluxo de como o NuGet adiciona referências a projetos com base no arquivo de `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="13940-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="13940-159">Localize a pasta `lib` apropriada para a estrutura de destino e obtenha a lista de assemblies dessa pasta</span><span class="sxs-lookup"><span data-stu-id="13940-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="13940-160">Localize separadamente o grupo de referências que é apropriado para a estrutura de destino e obtenha a lista de assemblies desse grupo.</span><span class="sxs-lookup"><span data-stu-id="13940-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="13940-161">O grupo de referência sem a estrutura de destino especificada é o grupo de fallback.</span><span class="sxs-lookup"><span data-stu-id="13940-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="13940-162">Localize a interseção das duas listas e use-a como as referências a serem adicionadas</span><span class="sxs-lookup"><span data-stu-id="13940-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="13940-163">Esse novo recurso permitirá que os autores de pacotes usem o recurso de referências para aplicar subconjuntos de assemblies a diferentes estruturas quando, de outra forma, precisariam executar assemblies duplicados em várias pastas de `lib`.</span><span class="sxs-lookup"><span data-stu-id="13940-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="13940-164">Observação: você deve usar atualmente o pacote NuGet. exe para usar esse recurso; O Gerenciador de pacotes NuGet ainda não dá suporte a ele.</span><span class="sxs-lookup"><span data-stu-id="13940-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="13940-165">Botão atualizar tudo para permitir a atualização de todos os pacotes ao mesmo tempo</span><span class="sxs-lookup"><span data-stu-id="13940-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="13940-166">Muitos de vocês sabem sobre o cmdlet "Update-Package" do PowerShell para atualizar todos os seus pacotes; Agora há uma maneira fácil de fazer isso por meio da interface do usuário também.</span><span class="sxs-lookup"><span data-stu-id="13940-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="13940-167">Para experimentar esse recurso:</span><span class="sxs-lookup"><span data-stu-id="13940-167">To try this feature out:</span></span>

1. <span data-ttu-id="13940-168">Criar um novo aplicativo ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="13940-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="13940-169">Iniciar a caixa de diálogo ' gerenciar pacotes NuGet '</span><span class="sxs-lookup"><span data-stu-id="13940-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="13940-170">Selecione ' atualizações '</span><span class="sxs-lookup"><span data-stu-id="13940-170">Select 'Updates'</span></span>
1. <span data-ttu-id="13940-171">Clique no botão ' atualizar tudo '</span><span class="sxs-lookup"><span data-stu-id="13940-171">Click the 'Update All' button</span></span>

![Botão atualizar tudo na caixa de diálogo](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="13940-173">Suporte de referência de projeto aprimorado para o pacote NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="13940-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="13940-174">Agora, o comando NuGet. exe Pack processa projetos referenciados com as seguintes regras:</span><span class="sxs-lookup"><span data-stu-id="13940-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="13940-175">Se o projeto referenciado tiver um arquivo `.nuspec` correspondente, por exemplo, há um arquivo chamado `proj1.nuspec` na mesma pasta que `proj1.csproj`, então esse projeto é adicionado como uma dependência ao pacote, usando a ID e a versão lidas do arquivo de `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="13940-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="13940-176">Caso contrário, os arquivos do projeto referenciado serão agrupados no pacote.</span><span class="sxs-lookup"><span data-stu-id="13940-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="13940-177">Em seguida, os projetos referenciados por este projeto serão processados usando as mesmas regras recursivamente.</span><span class="sxs-lookup"><span data-stu-id="13940-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="13940-178">Todos os arquivos DLL, `.pdb`e `.exe` são adicionados.</span><span class="sxs-lookup"><span data-stu-id="13940-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="13940-179">Todos os outros arquivos de conteúdo são adicionados.</span><span class="sxs-lookup"><span data-stu-id="13940-179">All other content files are added.</span></span>
1. <span data-ttu-id="13940-180">Todas as dependências são mescladas.</span><span class="sxs-lookup"><span data-stu-id="13940-180">All dependencies are merged.</span></span>

<span data-ttu-id="13940-181">Isso permite que um projeto referenciado seja tratado como uma dependência se houver um arquivo `.nuspec`, caso contrário, ele se tornará parte do pacote.</span><span class="sxs-lookup"><span data-stu-id="13940-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="13940-182">Mais detalhes aqui: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="13940-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="13940-183">Adicionar uma propriedade ' versão mínima do NuGet ' aos pacotes</span><span class="sxs-lookup"><span data-stu-id="13940-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="13940-184">Um novo atributo de metadados chamado ' minClientVersion ' agora pode indicar a versão mínima do cliente NuGet necessária para consumir um pacote.</span><span class="sxs-lookup"><span data-stu-id="13940-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="13940-185">Esse recurso ajuda o autor do pacote a especificar que um pacote só funcionará depois de uma versão específica do NuGet.</span><span class="sxs-lookup"><span data-stu-id="13940-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="13940-186">À medida que novos recursos de `.nuspec` são adicionados após o NuGet 2,5, os pacotes poderão declarar uma versão mínima do NuGet.</span><span class="sxs-lookup"><span data-stu-id="13940-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="13940-187">Se o usuário tiver o NuGet 2,5 instalado e um pacote for identificado como exigindo 2,6, as indicações visuais serão dadas ao usuário indicando que o pacote não poderá ser instalado.</span><span class="sxs-lookup"><span data-stu-id="13940-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="13940-188">O usuário será então guiado para atualizar sua versão do NuGet.</span><span class="sxs-lookup"><span data-stu-id="13940-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="13940-189">Isso melhorará a experiência existente em que os pacotes começam a ser instalados, mas falham indicando que uma versão de esquema não reconhecida foi identificada.</span><span class="sxs-lookup"><span data-stu-id="13940-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="13940-190">As dependências não são mais desnecessariamente atualizadas durante a instalação do pacote</span><span class="sxs-lookup"><span data-stu-id="13940-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="13940-191">Antes do NuGet 2,5, quando um pacote foi instalado que dependia de um pacote já instalado no projeto, a dependência seria atualizada como parte da nova instalação, mesmo que a versão existente esteja satisfeita na dependência.</span><span class="sxs-lookup"><span data-stu-id="13940-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="13940-192">A partir do NuGet 2,5, se uma versão de dependência já estiver satisfeita, a dependência não será atualizada durante outras instalações de pacote.</span><span class="sxs-lookup"><span data-stu-id="13940-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="13940-193">**O cenário:**</span><span class="sxs-lookup"><span data-stu-id="13940-193">**The scenario:**</span></span>

1. <span data-ttu-id="13940-194">O repositório de origem contém o pacote B com a versão 1.0.0 e 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="13940-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="13940-195">Ele também contém o pacote A que tem uma dependência em B (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="13940-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="13940-196">Suponha que o projeto atual já tenha a versão 1.0.0 do pacote B instalada.</span><span class="sxs-lookup"><span data-stu-id="13940-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="13940-197">Agora você deseja instalar o pacote A.</span><span class="sxs-lookup"><span data-stu-id="13940-197">Now you want to install package A.</span></span>

<span data-ttu-id="13940-198">**No NuGet 2,2 e mais antigo:**</span><span class="sxs-lookup"><span data-stu-id="13940-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="13940-199">Ao instalar o pacote A, o NuGet atualizará automaticamente B para 1.0.2, mesmo que a versão existente 1.0.0 já satisfaça a restrição de versão de dependência, que é > = 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="13940-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="13940-200">**No NuGet 2,5 e mais recente:**</span><span class="sxs-lookup"><span data-stu-id="13940-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="13940-201">O NuGet não atualizará mais B, pois detecta que a versão atual do 1.0.0 atende à restrição de versão de dependência.</span><span class="sxs-lookup"><span data-stu-id="13940-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="13940-202">Para obter mais informações sobre essa alteração, leia o [item de trabalho](http://nuget.codeplex.com/workitem/1681) detalhado, bem como o [thread de discussão](http://nuget.codeplex.com/discussions/436712)relacionado.</span><span class="sxs-lookup"><span data-stu-id="13940-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="13940-203">o NuGet. exe gera solicitações HTTP com detalhes detalhados</span><span class="sxs-lookup"><span data-stu-id="13940-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="13940-204">Se você estiver solucionando problemas do NuGet. exe ou apenas curioso quais solicitações HTTP são feitas durante as operações, a opção '-detalhamento detalhado ' gerará agora todas as solicitações HTTP feitas.</span><span class="sxs-lookup"><span data-stu-id="13940-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Saída HTTP do NuGet. exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="13940-206">o push NuGet. exe agora dá suporte a fontes UNC e de pasta</span><span class="sxs-lookup"><span data-stu-id="13940-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="13940-207">Antes do NuGet 2,5, se você tentou executar ' NuGet. exe push ' em uma origem de pacote com base em um caminho UNC ou em uma pasta local, o push falharia.</span><span class="sxs-lookup"><span data-stu-id="13940-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="13940-208">Com o recurso de configuração hierárquica adicionado recentemente, havia se tornado comum para o NuGet. exe precisar direcionar uma origem de UNC/pasta ou uma galeria de NuGet baseada em HTTP.</span><span class="sxs-lookup"><span data-stu-id="13940-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="13940-209">A partir do NuGet 2,5, se o NuGet. exe identificar uma origem UNC/pasta, ele executará a cópia do arquivo para a origem.</span><span class="sxs-lookup"><span data-stu-id="13940-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="13940-210">Agora, o seguinte comando funcionará:</span><span class="sxs-lookup"><span data-stu-id="13940-210">The following command will now work:</span></span>

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="13940-211">o NuGet. exe dá suporte a arquivos de configuração especificados explicitamente</span><span class="sxs-lookup"><span data-stu-id="13940-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="13940-212">os comandos NuGet. exe que acessam a configuração (tudo exceto ' spec ' e ' Pack ') agora oferecem suporte a uma nova opção '-ConfigFile ', que força um arquivo de configuração específico a ser usado no lugar do arquivo de configuração padrão em%AppData%\nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="13940-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="13940-213">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="13940-213">Example:</span></span>

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="13940-214">Suporte para projetos nativos</span><span class="sxs-lookup"><span data-stu-id="13940-214">Support for Native projects</span></span>

<span data-ttu-id="13940-215">Com o NuGet 2,5, as ferramentas do NuGet agora estão disponíveis para projetos nativos no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="13940-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="13940-216">Esperamos que a maioria dos pacotes nativos utilize o recurso de importações do MSBuild acima, usando uma ferramenta criada pelo [projeto CoApp](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="13940-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="13940-217">Para obter mais informações, leia [os detalhes sobre a ferramenta](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) no site do coapp.org.</span><span class="sxs-lookup"><span data-stu-id="13940-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="13940-218">O nome da estrutura de destino "Native" é introduzido para pacotes para incluir arquivos em \Build, \Content e \Tools quando o pacote é instalado em um projeto nativo.</span><span class="sxs-lookup"><span data-stu-id="13940-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="13940-219">A pasta \`lib ' não é usada para projetos nativos.</span><span class="sxs-lookup"><span data-stu-id="13940-219">The \`lib\` folder is not used for native projects.</span></span>
