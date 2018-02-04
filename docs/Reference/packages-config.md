---
title: "Referência do arquivo packages.config do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Em alguns tipos de projeto, o packages.json mantém a lista de pacotes do NuGet usados no projeto."
keywords: "Arquivo packages.config do NuGet, referências de pacote do NuGet, dependências do NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1839ca4761f6f35d0a650cdc2e3cf36b1b08ef2d
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2018
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="43315-104">Referência de packages.config</span><span class="sxs-lookup"><span data-stu-id="43315-104">packages.config reference</span></span>

<span data-ttu-id="43315-105">O arquivo `packages.config` é usado em alguns tipos de projeto para manter a lista de pacotes referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="43315-105">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="43315-106">Isso permite que o NuGet restaure facilmente as dependências do projeto quando ele a ser transportado para um computador diferente, como um servidor de build, sem todos esses pacotes.</span><span class="sxs-lookup"><span data-stu-id="43315-106">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

## <a name="schema"></a><span data-ttu-id="43315-107">Esquema</span><span class="sxs-lookup"><span data-stu-id="43315-107">Schema</span></span>

<span data-ttu-id="43315-108">O esquema é simples: após o cabeçalho padrão de XML está um único nó `<packages>` que contém um ou mais elementos `<package>`, um para cada referência.</span><span class="sxs-lookup"><span data-stu-id="43315-108">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="43315-109">Cada elemento `<package>` pode ter os seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="43315-109">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="43315-110">Atributo</span><span class="sxs-lookup"><span data-stu-id="43315-110">Attribute</span></span> | <span data-ttu-id="43315-111">Necessária</span><span class="sxs-lookup"><span data-stu-id="43315-111">Required</span></span> | <span data-ttu-id="43315-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="43315-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="43315-113">id</span><span class="sxs-lookup"><span data-stu-id="43315-113">id</span></span> | <span data-ttu-id="43315-114">Sim</span><span class="sxs-lookup"><span data-stu-id="43315-114">Yes</span></span> | <span data-ttu-id="43315-115">O identificador do pacote, como Newtonsoft.json ou Microsoft.AspNet.Mvc.</span><span class="sxs-lookup"><span data-stu-id="43315-115">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="43315-116">version</span><span class="sxs-lookup"><span data-stu-id="43315-116">version</span></span> | <span data-ttu-id="43315-117">Sim</span><span class="sxs-lookup"><span data-stu-id="43315-117">Yes</span></span> | <span data-ttu-id="43315-118">A versão exata do pacote a ser instalado, como 3.1.1 ou 4.2.5.11-beta.</span><span class="sxs-lookup"><span data-stu-id="43315-118">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="43315-119">Uma cadeia de caracteres de versão precisa ter pelo menos três números; um quarto número é opcional, assim como um sufixo de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="43315-119">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="43315-120">Intervalos não são permitidos.</span><span class="sxs-lookup"><span data-stu-id="43315-120">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="43315-121">targetFramework</span><span class="sxs-lookup"><span data-stu-id="43315-121">targetFramework</span></span> | <span data-ttu-id="43315-122">Não</span><span class="sxs-lookup"><span data-stu-id="43315-122">No</span></span> | <span data-ttu-id="43315-123">O [TFM (moniker da estrutura de destino)](target-frameworks.md) a ser aplicado ao instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="43315-123">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="43315-124">Inicialmente, isso é definido para o destino do projeto quando um pacote é instalado.</span><span class="sxs-lookup"><span data-stu-id="43315-124">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="43315-125">Como resultado, diversos elementos `<package>` podem ter TFMs diferentes.</span><span class="sxs-lookup"><span data-stu-id="43315-125">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="43315-126">Por exemplo, se você criar um projeto direcionado ao .NET 4.5.2, os pacotes instalados nesse ponto usarão TFM do net452.</span><span class="sxs-lookup"><span data-stu-id="43315-126">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="43315-127">Mais tarde, se você redirecionar o projeto para .NET 4.6 e adicionar mais pacotes, eles usarão o TFM do net46.</span><span class="sxs-lookup"><span data-stu-id="43315-127">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="43315-128">Uma incompatibilidade entre o destino do projeto e os atributos `targetFramework` gerará avisos e, nesse caso, você pode reinstalar os pacotes afetados.</span><span class="sxs-lookup"><span data-stu-id="43315-128">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="43315-129">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="43315-129">allowedVersions</span></span> | <span data-ttu-id="43315-130">Não</span><span class="sxs-lookup"><span data-stu-id="43315-130">No</span></span> | <span data-ttu-id="43315-131">Um intervalo de versões permitidas para este pacote aplicado durante a atualização de pacote (consulte [Restrições de versões de upgrade](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="43315-131">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="43315-132">Ele *não* afeta quais pacotes são instalados durante a operação de instalação ou restauração.</span><span class="sxs-lookup"><span data-stu-id="43315-132">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="43315-133">Consulte [Controle de versão do pacote](../reference/package-versioning.md#version-ranges-and-wildcards) para ver a sintaxe.</span><span class="sxs-lookup"><span data-stu-id="43315-133">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="43315-134">A interface do usuário do PackageManager também desabilita todas as versões fora do intervalo permitido.</span><span class="sxs-lookup"><span data-stu-id="43315-134">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="43315-135">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="43315-135">developmentDependency</span></span> | <span data-ttu-id="43315-136">Não</span><span class="sxs-lookup"><span data-stu-id="43315-136">No</span></span> | <span data-ttu-id="43315-137">Se o próprio projeto consumidor criar um pacote do NuGet, definir isso como `true` para uma dependência evita que o pacote seja incluído quando o pacote consumidor for criado.</span><span class="sxs-lookup"><span data-stu-id="43315-137">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="43315-138">O padrão é `false`.</span><span class="sxs-lookup"><span data-stu-id="43315-138">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="43315-139">Exemplos</span><span class="sxs-lookup"><span data-stu-id="43315-139">Examples</span></span>

<span data-ttu-id="43315-140">O seguinte `packages.config` refere-se a duas dependências:</span><span class="sxs-lookup"><span data-stu-id="43315-140">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="43315-141">O `packages.config` a seguir refere-se a nove pacotes, mas `Microsoft.Net.Compilers` não será incluído ao compilar o pacote consumidor devido ao atributo `developmentDependency`.</span><span class="sxs-lookup"><span data-stu-id="43315-141">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="43315-142">A referência ao Newtonsoft.Json também restringe as atualizações somente às versões 8.x e 9.x.</span><span class="sxs-lookup"><span data-stu-id="43315-142">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
