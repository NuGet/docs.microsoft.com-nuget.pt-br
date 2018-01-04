---
title: "Pacotes do NuGet e controle do código-fonte | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c874e6f-99eb-46dd-997f-f67d98d0237e
description: "Considerações sobre como tratar pacotes do NuGet nos sistemas de controle de versão e do código-fonte, e como omitir pacotes com git e TFVC."
keywords: "Controle de código-fonte do NuGet, controle de versão do NuGet, NuGet e git, NuGet e TFS, NuGet e TFVC, omitindo pacotes, repositórios de controle do código-fonte, repositórios de controle de versão"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c73dea74f2363f49fb476a5812c29de63fec89a3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="76d09-104">Omitindo pacotes do NuGet em sistemas de controle do código-fonte</span><span class="sxs-lookup"><span data-stu-id="76d09-104">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="76d09-105">Os desenvolvedores geralmente omitem pacotes do NuGet de seus repositórios de controle do código-fonte e, em vez disso, contam com a [restauração de pacote](../consume-packages/package-restore.md) para reinstalar as dependências de um projeto antes de um build.</span><span class="sxs-lookup"><span data-stu-id="76d09-105">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](../consume-packages/package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="76d09-106">Alguns dos motivos para contar com a restauração de pacote são:</span><span class="sxs-lookup"><span data-stu-id="76d09-106">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="76d09-107">Sistemas de controle de versão distribuídos, como Git, incluem cópias completas de todas as versões de cada arquivo dentro do repositório.</span><span class="sxs-lookup"><span data-stu-id="76d09-107">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="76d09-108">Arquivos binários que são atualizados com frequência levam a uma sobrecarga significativa e aumentam o tempo necessário para clonar o repositório.</span><span class="sxs-lookup"><span data-stu-id="76d09-108">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="76d09-109">Quando os pacotes são incluídos no repositório, os desenvolvedores são responsáveis por adicionar referências diretamente ao conteúdo do pacote no disco em vez de referenciar os pacotes por meio do NuGet, o que pode levar a nomes de caminho embutido em código no projeto.</span><span class="sxs-lookup"><span data-stu-id="76d09-109">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="76d09-110">Fica mais difícil limpar as pastas de pacote não utilizadas da solução, pois pode ser necessário garantir que você não exclua as pastas de pacote ainda em uso.</span><span class="sxs-lookup"><span data-stu-id="76d09-110">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="76d09-111">Ao omitir pacotes, você pode manter limites claros de propriedade entre o código e os pacotes de terceiros dos quais você depende.</span><span class="sxs-lookup"><span data-stu-id="76d09-111">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="76d09-112">Muitos pacotes do NuGet já são mantidos em seus próprios repositórios de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="76d09-112">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="76d09-113">Embora a restauração do pacote seja o comportamento padrão com o NuGet, é necessário certo trabalho manual para omitir pacotes&mdash;, ou seja, a pasta `packages` em seu projeto&mdash;do controle do código-fonte, conforme descrito nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="76d09-113">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in the following sections.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="76d09-114">Omitir pacotes com Git</span><span class="sxs-lookup"><span data-stu-id="76d09-114">Omitting packages with Git</span></span>

<span data-ttu-id="76d09-115">Use o [arquivo .gitignore](https://git-scm.com/docs/gitignore) evitar incluir a pasta `packages` no controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="76d09-115">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to avoid including the `packages` folder in source control.</span></span> <span data-ttu-id="76d09-116">Para referência, consulte o [exemplo `.gitignore` para projetos do Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="76d09-116">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="76d09-117">As partes importantes do arquivo `.gitignore` são:</span><span class="sxs-lookup"><span data-stu-id="76d09-117">The important parts of the `.gitignore` file are:</span></span>

```
# Ignore NuGet Packages
*.nupkg

# Ignore the packages folder
**/packages/*

# Include packages/build/, which is used as an MSBuild target
!**/packages/build/

# Uncomment if necessary; generally it's regenerated when needed
#!**/packages/repositories.config

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json; project.assets.json is used in conjunction with the PackageReference format.
project.lock.json
project.assets.json
*.nuget.props
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="76d09-118">Omitindo pacotes com o Controle de Versão do Team Foundation</span><span class="sxs-lookup"><span data-stu-id="76d09-118">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="76d09-119">Se possível, siga estas instruções *antes* de adicionar o projeto ao controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="76d09-119">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="76d09-120">Caso contrário, exclua a pasta `packages` manualmente do repositório e confirme essa alteração antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="76d09-120">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="76d09-121">Para desabilitar a integração de controle do código-fonte com TFVC para os arquivos selecionados:</span><span class="sxs-lookup"><span data-stu-id="76d09-121">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="76d09-122">Crie uma pasta chamada `.nuget` na pasta da sua solução (no qual o arquivo `.sln` está).</span><span class="sxs-lookup"><span data-stu-id="76d09-122">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="76d09-123">Dica: no Windows, para criar essa pasta no Windows Explorer, use o nome `.nuget.` *com* o ponto à direita.</span><span class="sxs-lookup"><span data-stu-id="76d09-123">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="76d09-124">Nessa pasta, crie um arquivo chamado `NuGet.Config` e abra-o para edição.</span><span class="sxs-lookup"><span data-stu-id="76d09-124">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="76d09-125">Adicione o texto a seguir no mínimo, em que a configuração [disableSourceControlIntegration](../Schema/nuget-config-file.md#solution-section) instrui o Visual Studio a ignorar tudo na pasta `packages`:</span><span class="sxs-lookup"><span data-stu-id="76d09-125">Add the following text as a minimum, where the [disableSourceControlIntegration](../Schema/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="76d09-126">Se você estiver usando o TFS 2010 ou anterior, encubra a pasta `packages` nos seus mapeamentos de espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="76d09-126">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="76d09-127">No TFS 2012 ou posterior, ou com o Visual Studio Team Services, crie um arquivo `.tfignore` conforme descrito em [AddFiles para o servidor](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore).</span><span class="sxs-lookup"><span data-stu-id="76d09-127">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore).</span></span> <span data-ttu-id="76d09-128">Nesse arquivo, inclua o conteúdo abaixo para ignorar explicitamente as modificações na pasta `\packages` no nível do repositório e alguns outros arquivos intermediários.</span><span class="sxs-lookup"><span data-stu-id="76d09-128">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="76d09-129">(Você pode criar o arquivo no Windows Explorer usando o nome de um `.tfignore.` com o ponto à direita, mas pode ser necessário desabilitar a opção “Ocultar extensões de arquivos conhecidos” primeiro.):</span><span class="sxs-lookup"><span data-stu-id="76d09-129">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```
   # Ignore NuGet Packages
   *.nupkg   

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Include package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="76d09-130">Adicione `NuGet.Config` e `.tfignore` ao controle do código-fonte e confirme suas alterações.</span><span class="sxs-lookup"><span data-stu-id="76d09-130">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
