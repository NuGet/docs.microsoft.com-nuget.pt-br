---
title: Pacotes do NuGet e controle do código-fonte
description: Considerações sobre como tratar pacotes do NuGet nos sistemas de controle de versão e do código-fonte, e como omitir pacotes com git e TFVC.
author: JonDouglas
ms.author: jodou
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9bae65573ca49c68d07250228c1923890e0f14ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775018"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="93123-103">Omitindo pacotes do NuGet em sistemas de controle do código-fonte</span><span class="sxs-lookup"><span data-stu-id="93123-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="93123-104">Os desenvolvedores geralmente omitem pacotes do NuGet de seus repositórios de controle do código-fonte e, em vez disso, contam com a [restauração de pacote](package-restore.md) para reinstalar as dependências de um projeto antes de um build.</span><span class="sxs-lookup"><span data-stu-id="93123-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="93123-105">Alguns dos motivos para contar com a restauração de pacote são:</span><span class="sxs-lookup"><span data-stu-id="93123-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="93123-106">Sistemas de controle de versão distribuídos, como Git, incluem cópias completas de todas as versões de cada arquivo dentro do repositório.</span><span class="sxs-lookup"><span data-stu-id="93123-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="93123-107">Arquivos binários que são atualizados com frequência levam a uma sobrecarga significativa e aumentam o tempo necessário para clonar o repositório.</span><span class="sxs-lookup"><span data-stu-id="93123-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="93123-108">Quando os pacotes são incluídos no repositório, os desenvolvedores são responsáveis por adicionar referências diretamente ao conteúdo do pacote no disco em vez de referenciar os pacotes por meio do NuGet, o que pode levar a nomes de caminho embutido em código no projeto.</span><span class="sxs-lookup"><span data-stu-id="93123-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="93123-109">Fica mais difícil limpar as pastas de pacote não utilizadas da solução, pois pode ser necessário garantir que você não exclua as pastas de pacote ainda em uso.</span><span class="sxs-lookup"><span data-stu-id="93123-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="93123-110">Ao omitir pacotes, você pode manter limites claros de propriedade entre o código e os pacotes de terceiros dos quais você depende.</span><span class="sxs-lookup"><span data-stu-id="93123-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="93123-111">Muitos pacotes do NuGet já são mantidos em seus próprios repositórios de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="93123-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="93123-112">Embora a restauração de pacote seja o comportamento padrão no NuGet, é necessário certo trabalho manual para omitir pacotes &mdash; ou seja, a pasta `packages` em seu projeto &mdash; do controle do código-fonte, conforme descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="93123-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="93123-113">Omitir pacotes com Git</span><span class="sxs-lookup"><span data-stu-id="93123-113">Omitting packages with Git</span></span>

<span data-ttu-id="93123-114">Use o [arquivo .gitignore](https://git-scm.com/docs/gitignore) para ignorar pacotes do NuGet (`.nupkg`), a pasta `packages`, `project.assets.json`, entre outros itens.</span><span class="sxs-lookup"><span data-stu-id="93123-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="93123-115">Para referência, consulte o [exemplo `.gitignore` para projetos do Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span><span class="sxs-lookup"><span data-stu-id="93123-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="93123-116">As partes importantes do arquivo `.gitignore` são:</span><span class="sxs-lookup"><span data-stu-id="93123-116">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="93123-117">Omitindo pacotes com o Controle de Versão do Team Foundation</span><span class="sxs-lookup"><span data-stu-id="93123-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="93123-118">Se possível, siga estas instruções *antes* de adicionar o projeto ao controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="93123-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="93123-119">Caso contrário, exclua a pasta `packages` manualmente do repositório e confirme essa alteração antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="93123-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="93123-120">Para desabilitar a integração de controle do código-fonte com TFVC para os arquivos selecionados:</span><span class="sxs-lookup"><span data-stu-id="93123-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="93123-121">Crie uma pasta chamada `.nuget` na pasta da sua solução (no qual o arquivo `.sln` está).</span><span class="sxs-lookup"><span data-stu-id="93123-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="93123-122">Dica: no Windows, para criar essa pasta no Windows Explorer, use o nome `.nuget.` *com* o ponto à direita.</span><span class="sxs-lookup"><span data-stu-id="93123-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="93123-123">Nessa pasta, crie um arquivo chamado `NuGet.Config` e abra-o para edição.</span><span class="sxs-lookup"><span data-stu-id="93123-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="93123-124">Adicione o texto a seguir no mínimo, em que a configuração [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) instrui o Visual Studio a ignorar tudo na pasta `packages`:</span><span class="sxs-lookup"><span data-stu-id="93123-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="93123-125">Se você estiver usando o TFS 2010 ou anterior, encubra a pasta `packages` nos seus mapeamentos de workspace.</span><span class="sxs-lookup"><span data-stu-id="93123-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="93123-126">No TFS 2012 ou posterior, ou com o Visual Studio Team Services, crie um arquivo `.tfignore` conforme descrito em [Adicionar arquivos ao servidor](/vsts/tfvc/add-files-server?view=vsts#tfignore).</span><span class="sxs-lookup"><span data-stu-id="93123-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [Add Files to the Server](/vsts/tfvc/add-files-server?view=vsts#tfignore).</span></span> <span data-ttu-id="93123-127">Nesse arquivo, inclua o conteúdo abaixo para ignorar explicitamente as modificações na pasta `\packages` no nível do repositório e alguns outros arquivos intermediários.</span><span class="sxs-lookup"><span data-stu-id="93123-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="93123-128">(Você pode criar o arquivo no Windows Explorer usando o nome de um `.tfignore.` com o ponto à direita, mas pode ser necessário desabilitar a opção “Ocultar extensões de arquivos conhecidos” primeiro.):</span><span class="sxs-lookup"><span data-stu-id="93123-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="93123-129">Adicione `NuGet.Config` e `.tfignore` ao controle do código-fonte e confirme suas alterações.</span><span class="sxs-lookup"><span data-stu-id="93123-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
