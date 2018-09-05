---
title: Notas de versão 2.5 do NuGet
description: Notas de versão do NuGet 2.5, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550477"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="b1df9-103">Notas de versão 2.5 do NuGet</span><span class="sxs-lookup"><span data-stu-id="b1df9-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="b1df9-104">[Notas de versão do NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [notas de versão do NuGet 2.6](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="b1df9-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="b1df9-105">O NuGet 2.5 foi lançado em 25 de abril de 2013.</span><span class="sxs-lookup"><span data-stu-id="b1df9-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="b1df9-106">Esta versão era tão grande, constatamos forçadas ignorar as versões 2.3 e 2.4!</span><span class="sxs-lookup"><span data-stu-id="b1df9-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="b1df9-107">Até o momento, esta é a versão de maior que tivemos para o NuGet, com failover [itens de trabalho de 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) na versão.</span><span class="sxs-lookup"><span data-stu-id="b1df9-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="b1df9-108">Confirmações</span><span class="sxs-lookup"><span data-stu-id="b1df9-108">Acknowledgements</span></span>

<span data-ttu-id="b1df9-109">Gostaríamos de agradecer os seguintes colaboradores externos por suas contribuições significativas para o NuGet 2.5:</span><span class="sxs-lookup"><span data-stu-id="b1df9-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="b1df9-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="b1df9-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="b1df9-111">[#2847](https://nuget.codeplex.com/workitem/2847) -adicionar MonoAndroid, MonoTouch e MonoMac à lista de identificadores de estrutura de destino conhecidos.</span><span class="sxs-lookup"><span data-stu-id="b1df9-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="b1df9-112">[Aragoneses de g. Andres](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="b1df9-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="b1df9-113">[#2865](https://nuget.codeplex.com/workitem/2865) -corrigir a ortografia do `NuGet.targets` para um sistema de operacional diferencia maiusculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="b1df9-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="b1df9-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="b1df9-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="b1df9-115">Verifique a solução de build no Mono.</span><span class="sxs-lookup"><span data-stu-id="b1df9-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="b1df9-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="b1df9-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="b1df9-117">Corrija os testes de unidade com falha no Mono.</span><span class="sxs-lookup"><span data-stu-id="b1df9-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="b1df9-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="b1df9-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="b1df9-119">[#2920](https://nuget.codeplex.com/workitem/2920) -comando de pacote nuget.exe não propaga as propriedades para o MSBuild</span><span class="sxs-lookup"><span data-stu-id="b1df9-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="b1df9-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="b1df9-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="b1df9-121">[#1511](https://nuget.codeplex.com/workitem/1511) - XML modificado código de tratamento para preservar a formatação.</span><span class="sxs-lookup"><span data-stu-id="b1df9-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="b1df9-122">[ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="b1df9-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="b1df9-123">Palavras reconhecidas adicionadas ao dicionário personalizado para permitir que o build. cmd seja bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="b1df9-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="b1df9-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="b1df9-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="b1df9-125">Corrija os testes de unidade durante a execução no VS localizadas.</span><span class="sxs-lookup"><span data-stu-id="b1df9-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="b1df9-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="b1df9-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="b1df9-127">Interface extraído do PackageService</span><span class="sxs-lookup"><span data-stu-id="b1df9-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="b1df9-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="b1df9-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="b1df9-129">[#936](https://nuget.codeplex.com/workitem/936) -lidar com as dependências do projeto quando o empacotamento</span><span class="sxs-lookup"><span data-stu-id="b1df9-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="b1df9-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="b1df9-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="b1df9-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -suporte senha com texto não criptografado ao armazenar credenciais de origem do pacote em arquivos de nuget.cofig</span><span class="sxs-lookup"><span data-stu-id="b1df9-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="b1df9-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="b1df9-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="b1df9-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -descrição de Ajuda do Get-Package corrigir</span><span class="sxs-lookup"><span data-stu-id="b1df9-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="b1df9-134">Também Agradecemos os indivíduos a seguir para localizar bugs com o NuGet 2.5 Beta/RC que foram aprovados e corrigido antes do lançamento final:</span><span class="sxs-lookup"><span data-stu-id="b1df9-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="b1df9-135">[Tony parede](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="b1df9-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="b1df9-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest dividido com mais recente NuGet 2.4 e 2.5 compilações</span><span class="sxs-lookup"><span data-stu-id="b1df9-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="b1df9-137">Recursos importantes da versão</span><span class="sxs-lookup"><span data-stu-id="b1df9-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="b1df9-138">Permitir que os usuários substituir os arquivos de conteúdo que já existe</span><span class="sxs-lookup"><span data-stu-id="b1df9-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="b1df9-139">Um dos recursos mais solicitados de todo o tempo foi a capacidade de substituir os arquivos de conteúdo que já existem no disco quando incluído em um pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="b1df9-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="b1df9-140">Começando com o NuGet 2.5, os conflitos são identificados e você será solicitado a substituir os arquivos, enquanto que anteriormente esses arquivos sempre foram ignorados.</span><span class="sxs-lookup"><span data-stu-id="b1df9-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Substituir arquivos de conteúdo](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="b1df9-142">'nuget.exe update' e 'Install-Package' agora têm uma nova opção '-FileConflictAction' para definir alguns padrão para cenários de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="b1df9-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="b1df9-143">Defina uma ação padrão quando já existe um arquivo de um pacote no projeto de destino.</span><span class="sxs-lookup"><span data-stu-id="b1df9-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="b1df9-144">Definido como 'Substituição' para substituir os arquivos sempre.</span><span class="sxs-lookup"><span data-stu-id="b1df9-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="b1df9-145">Defina como 'Ignorar' para ignorar arquivos.</span><span class="sxs-lookup"><span data-stu-id="b1df9-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="b1df9-146">Se não for especificado, ele solicitará para cada arquivo conflitante.</span><span class="sxs-lookup"><span data-stu-id="b1df9-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="b1df9-147">Importação automática de arquivos de destinos e objetos do MSBuild</span><span class="sxs-lookup"><span data-stu-id="b1df9-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="b1df9-148">Uma nova pasta convencional foi criada no nível superior do pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="b1df9-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="b1df9-149">Como um par `\lib`, `\content`, e `\tools`, agora você pode incluir um `\build` pasta em seu pacote.</span><span class="sxs-lookup"><span data-stu-id="b1df9-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="b1df9-150">Nesta pasta, você pode colocar dois arquivos com nomes fixos, `{packageid}.targets` ou `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="b1df9-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="b1df9-151">Esses dois arquivos podem ser diretamente em `build` ou em pastas específicas do framework assim como as outras pastas.</span><span class="sxs-lookup"><span data-stu-id="b1df9-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="b1df9-152">A regra para a pasta de framework melhor correspondentes de separação é exatamente o mesmo aqueles.</span><span class="sxs-lookup"><span data-stu-id="b1df9-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="b1df9-153">Quando o NuGet instala um pacote com arquivos \build, ele adicionará um MSBuild `<Import>` elemento no arquivo de projeto que aponta para o `.targets` e `.props` arquivos.</span><span class="sxs-lookup"><span data-stu-id="b1df9-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="b1df9-154">O `.props` arquivo for adicionado na parte superior, enquanto o `.targets` arquivo é adicionado à parte inferior.</span><span class="sxs-lookup"><span data-stu-id="b1df9-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="b1df9-155">Especifique as referências de diferentes por plataforma usando `<References/>` elemento</span><span class="sxs-lookup"><span data-stu-id="b1df9-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="b1df9-156">Antes de 2.5, em `.nuspec` arquivo, o usuário só pode especificar os arquivos de referência, a ser adicionada para todos os framework.</span><span class="sxs-lookup"><span data-stu-id="b1df9-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="b1df9-157">Agora, com esse novo recurso no 2.5, o usuário pode criar o `<reference/>` elemento para cada plataforma suportada, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b1df9-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="b1df9-158">Aqui está o fluxo para como o NuGet adiciona referências a projetos com base no `.nuspec` arquivo:</span><span class="sxs-lookup"><span data-stu-id="b1df9-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="b1df9-159">Encontre o `lib` pasta que é apropriado para a estrutura de destino e obter a lista de assemblies da pasta</span><span class="sxs-lookup"><span data-stu-id="b1df9-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="b1df9-160">Separadamente, localize o grupo de referências que é apropriado para a estrutura de destino e obter a lista de assemblies do grupo.</span><span class="sxs-lookup"><span data-stu-id="b1df9-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="b1df9-161">Grupo de referência sem a estrutura de destino especificado é o fallback.</span><span class="sxs-lookup"><span data-stu-id="b1df9-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="b1df9-162">Localize a interseção das duas listas e usá-lo como as referências para adicionar</span><span class="sxs-lookup"><span data-stu-id="b1df9-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="b1df9-163">Esse novo recurso permitirá que os autores de pacote usar o recurso de referências para aplicar a subconjuntos de assemblies para estruturas diferentes quando eles precisariam executar assemblies duplicados em vários `lib` pastas.</span><span class="sxs-lookup"><span data-stu-id="b1df9-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="b1df9-164">Observação: você deve, no momento usar nuget.exe pack para usar esse recurso; Explorador de pacotes NuGet ainda não dá suporte-lo.</span><span class="sxs-lookup"><span data-stu-id="b1df9-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="b1df9-165">Atualizar todos os botões para permitir a atualização de todos os pacotes ao mesmo tempo</span><span class="sxs-lookup"><span data-stu-id="b1df9-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="b1df9-166">Muitos de vocês sabem sobre o cmdlet do PowerShell "Update-Package" para atualizar todos os seus pacotes; Agora há uma maneira fácil de fazer isso por meio da interface do usuário também.</span><span class="sxs-lookup"><span data-stu-id="b1df9-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="b1df9-167">Para experimentar este recurso:</span><span class="sxs-lookup"><span data-stu-id="b1df9-167">To try this feature out:</span></span>

1. <span data-ttu-id="b1df9-168">Criar um novo aplicativo ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="b1df9-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="b1df9-169">Iniciar a caixa de diálogo 'Gerenciar pacotes do NuGet'</span><span class="sxs-lookup"><span data-stu-id="b1df9-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="b1df9-170">Selecione 'Atualizações'</span><span class="sxs-lookup"><span data-stu-id="b1df9-170">Select 'Updates'</span></span>
1. <span data-ttu-id="b1df9-171">Clique no botão 'Atualizar tudo'</span><span class="sxs-lookup"><span data-stu-id="b1df9-171">Click the 'Update All' button</span></span>

![Botão tudo na caixa de diálogo de atualização](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="b1df9-173">Suporte de referência de projeto aprimorado para nuget.exe Pack</span><span class="sxs-lookup"><span data-stu-id="b1df9-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="b1df9-174">Agora nuget.exe processos de comando de pacote referenciado em projetos com as seguintes regras:</span><span class="sxs-lookup"><span data-stu-id="b1df9-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="b1df9-175">Se o projeto referenciado tem correspondente `.nuspec` do arquivo, por exemplo, há um arquivo chamado `proj1.nuspec` na mesma pasta que `proj1.csproj`, este projeto é adicionado como uma dependência ao pacote, usando a id e versão leia o `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="b1df9-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="b1df9-176">Caso contrário, os arquivos do projeto referenciado são empacotados em pacote.</span><span class="sxs-lookup"><span data-stu-id="b1df9-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="b1df9-177">Em seguida, projetos referenciados por este projeto serão processados usando o mesmos regras recursivamente.</span><span class="sxs-lookup"><span data-stu-id="b1df9-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="b1df9-178">DLL de todos os `.pdb`, e `.exe` arquivos são adicionados.</span><span class="sxs-lookup"><span data-stu-id="b1df9-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="b1df9-179">Todos os outros arquivos de conteúdo são adicionados.</span><span class="sxs-lookup"><span data-stu-id="b1df9-179">All other content files are added.</span></span>
1. <span data-ttu-id="b1df9-180">Todas as dependências são mescladas.</span><span class="sxs-lookup"><span data-stu-id="b1df9-180">All dependencies are merged.</span></span>

<span data-ttu-id="b1df9-181">Isso permite que um projeto referenciado deve ser tratada como uma dependência, se houver um `.nuspec` de arquivos, caso contrário, ele se torna parte do pacote.</span><span class="sxs-lookup"><span data-stu-id="b1df9-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="b1df9-182">Mais detalhes aqui: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="b1df9-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="b1df9-183">Adicionar uma propriedade 'Mínimo a versão do NuGet' aos pacotes</span><span class="sxs-lookup"><span data-stu-id="b1df9-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="b1df9-184">Um novo atributo de metadados chamado 'minClientVersion' agora pode indicar a versão de cliente do NuGet mínima necessária para consumir um pacote.</span><span class="sxs-lookup"><span data-stu-id="b1df9-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="b1df9-185">Esse recurso ajuda o autor do pacote para especificar que um pacote funcionará apenas depois de uma versão específica do NuGet.</span><span class="sxs-lookup"><span data-stu-id="b1df9-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="b1df9-186">Como novos `.nuspec` recursos são adicionados após o NuGet 2.5, pacotes serão possível reivindicar uma versão mínima do NuGet.</span><span class="sxs-lookup"><span data-stu-id="b1df9-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="b1df9-187">Se o usuário tem o NuGet 2.5 instalado e um pacote é identificado como exigindo 2.6, indicações visuais serão fornecidas para o usuário indicando que o pacote não será instalado.</span><span class="sxs-lookup"><span data-stu-id="b1df9-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="b1df9-188">Em seguida, o usuário será orientado para atualizar sua versão do NuGet.</span><span class="sxs-lookup"><span data-stu-id="b1df9-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="b1df9-189">Isso melhora na experiência existente no qual começam a pacotes para instalar, mas falhar, em seguida, o que indica que uma versão de esquema não reconhecido foi identificada.</span><span class="sxs-lookup"><span data-stu-id="b1df9-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="b1df9-190">Dependências não desnecessariamente são atualizadas durante a instalação do pacote</span><span class="sxs-lookup"><span data-stu-id="b1df9-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="b1df9-191">Antes do NuGet 2.5, quando um pacote foi instalado que depende de um pacote já instalado no projeto, a dependência será atualizada como parte da nova instalação, mesmo se a versão existente satisfez a dependência.</span><span class="sxs-lookup"><span data-stu-id="b1df9-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="b1df9-192">Começando com o NuGet 2.5, se uma versão de dependência já for atendida, a dependência não será atualizada durante outras instalações de pacote.</span><span class="sxs-lookup"><span data-stu-id="b1df9-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="b1df9-193">**Cenário:**</span><span class="sxs-lookup"><span data-stu-id="b1df9-193">**The scenario:**</span></span>

1. <span data-ttu-id="b1df9-194">O repositório de origem contém o pacote B com a versão 1.0.0 e 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="b1df9-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="b1df9-195">Ele também contém o pacote a, que tem uma dependência em B (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="b1df9-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="b1df9-196">Suponha que o projeto atual já tem a versão do pacote B 1.0.0 instalado.</span><span class="sxs-lookup"><span data-stu-id="b1df9-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="b1df9-197">Agora que você deseja instalar a pacote.</span><span class="sxs-lookup"><span data-stu-id="b1df9-197">Now you want to install package A.</span></span>

<span data-ttu-id="b1df9-198">**No NuGet 2.2 e anteriores:**</span><span class="sxs-lookup"><span data-stu-id="b1df9-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="b1df9-199">Ao instalar um pacote, o NuGet será atualizado automaticamente B à 1.0.2, mesmo que a versão existente 1.0.0 já atende à restrição de versão de dependência, que é > = 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="b1df9-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="b1df9-200">**No NuGet 2.5 e mais recente:**</span><span class="sxs-lookup"><span data-stu-id="b1df9-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="b1df9-201">O NuGet não será mais atualizado B, pois detecta que a versão existente 1.0.0 satisfaz a restrição de versão de dependência.</span><span class="sxs-lookup"><span data-stu-id="b1df9-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="b1df9-202">Para obter mais informações sobre essa alteração, leia a página detalhada [item de trabalho](http://nuget.codeplex.com/workitem/1681) , bem como os relacionados [thread de discussão](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="b1df9-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="b1df9-203">NuGet.exe gera solicitações http detalhado</span><span class="sxs-lookup"><span data-stu-id="b1df9-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="b1df9-204">Se você estiver solucionando problemas de nuget.exe ou apenas curioso quais solicitações HTTP são feitas durante as operações, o '-detalhamento detalhada ' switch agora produzirá todas as solicitações HTTP feitas.</span><span class="sxs-lookup"><span data-stu-id="b1df9-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Saída HTTP do nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="b1df9-206">push NuGet.exe agora dá suporte a fontes de UNC e pasta</span><span class="sxs-lookup"><span data-stu-id="b1df9-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="b1df9-207">Antes do NuGet 2.5, se você tentou executar 'nuget.exe push' para uma origem de pacote com base em um caminho UNC ou uma pasta local, o envio por push falharia.</span><span class="sxs-lookup"><span data-stu-id="b1df9-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="b1df9-208">Com o recurso de configuração hierárquicos adicionados recentemente, tornou-se comum para nuget.exe precisar direcionar para uma fonte de pasta/UNC ou uma galeria do NuGet com base em HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1df9-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="b1df9-209">Começando com o NuGet 2.5 se nuget.exe identifica uma fonte UNC/pasta, ele fará a cópia do arquivo para a fonte.</span><span class="sxs-lookup"><span data-stu-id="b1df9-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="b1df9-210">O comando a seguir funcionará:</span><span class="sxs-lookup"><span data-stu-id="b1df9-210">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="b1df9-211">NuGet.exe dá suporte a arquivos de configuração especificado explicitamente</span><span class="sxs-lookup"><span data-stu-id="b1df9-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="b1df9-212">comandos de NuGet.exe que acessar a configuração (todos, exceto 'especificação' e 'pack') agora dão suporte a um novo '-ConfigFile' opção, o que força a um arquivo de configuração específico a ser usado no lugar do arquivo de configuração padrão em % AppData%\nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="b1df9-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="b1df9-213">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="b1df9-213">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="b1df9-214">Suporte para projetos nativos</span><span class="sxs-lookup"><span data-stu-id="b1df9-214">Support for Native projects</span></span>

<span data-ttu-id="b1df9-215">Com o NuGet 2.5, as ferramentas do NuGet agora estão disponível para projetos nativos no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b1df9-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="b1df9-216">Esperamos que mais pacotes nativos utilizarão o recurso de importações do MSBuild acima, usando uma ferramenta criada pela [CoApp projeto](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="b1df9-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="b1df9-217">Para obter mais informações, leia [os detalhes sobre a ferramenta](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) no site da coapp.org.</span><span class="sxs-lookup"><span data-stu-id="b1df9-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="b1df9-218">O nome da estrutura de destino de "nativo" é introduzido para pacotes incluir arquivos \build, \content e \tools quando o pacote é instalado em um projeto nativo.</span><span class="sxs-lookup"><span data-stu-id="b1df9-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="b1df9-219">O \`lib' pasta não é usada para projetos nativos.</span><span class="sxs-lookup"><span data-stu-id="b1df9-219">The \`lib` folder is not used for native projects.</span></span>
