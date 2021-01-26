---
title: Referência de arquivo NuGet packages.config
description: Em alguns tipos de projeto, o packages.json mantém a lista de pacotes do NuGet usados no projeto.
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 3e5db779f735cd42aa331f9f8a93496d32c8df54
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777623"
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="84463-103">Referência de packages.config</span><span class="sxs-lookup"><span data-stu-id="84463-103">packages.config reference</span></span>

<span data-ttu-id="84463-104">O arquivo `packages.config` é usado em alguns tipos de projeto para manter a lista de pacotes referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="84463-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="84463-105">Isso permite que o NuGet restaure facilmente as dependências do projeto quando ele a ser transportado para um computador diferente, como um servidor de build, sem todos esses pacotes.</span><span class="sxs-lookup"><span data-stu-id="84463-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

<span data-ttu-id="84463-106">Se usado, `packages.config` normalmente está localizado em uma raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="84463-106">If used, `packages.config` is typically located in a project root.</span></span> <span data-ttu-id="84463-107">Ele é criado automaticamente quando a primeira operação do NuGet é executada, mas também pode ser criado manualmente antes de executar qualquer comando, como `nuget restore` .</span><span class="sxs-lookup"><span data-stu-id="84463-107">It's automatically created when the first NuGet operation is run, but can also be created manually before running any commands such as `nuget restore`.</span></span>

<span data-ttu-id="84463-108">Projetos que usam [PackageReference](../consume-packages/Package-References-in-Project-Files.md) não usam `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="84463-108">Projects that use [PackageReference](../consume-packages/Package-References-in-Project-Files.md) do not use `packages.config`.</span></span>

## <a name="schema"></a><span data-ttu-id="84463-109">Esquema</span><span class="sxs-lookup"><span data-stu-id="84463-109">Schema</span></span>

<span data-ttu-id="84463-110">O esquema é simples: após o cabeçalho padrão de XML está um único nó `<packages>` que contém um ou mais elementos `<package>`, um para cada referência.</span><span class="sxs-lookup"><span data-stu-id="84463-110">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="84463-111">Cada elemento `<package>` pode ter os seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="84463-111">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="84463-112">Atributo</span><span class="sxs-lookup"><span data-stu-id="84463-112">Attribute</span></span> | <span data-ttu-id="84463-113">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="84463-113">Required</span></span> | <span data-ttu-id="84463-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="84463-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84463-115">id</span><span class="sxs-lookup"><span data-stu-id="84463-115">id</span></span> | <span data-ttu-id="84463-116">Sim</span><span class="sxs-lookup"><span data-stu-id="84463-116">Yes</span></span> | <span data-ttu-id="84463-117">O identificador do pacote, como Newtonsoft.json ou Microsoft.AspNet.Mvc.</span><span class="sxs-lookup"><span data-stu-id="84463-117">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="84463-118">version</span><span class="sxs-lookup"><span data-stu-id="84463-118">version</span></span> | <span data-ttu-id="84463-119">Sim</span><span class="sxs-lookup"><span data-stu-id="84463-119">Yes</span></span> | <span data-ttu-id="84463-120">A versão exata do pacote a ser instalado, como 3.1.1 ou 4.2.5.11-beta.</span><span class="sxs-lookup"><span data-stu-id="84463-120">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="84463-121">Uma cadeia de caracteres de versão precisa ter pelo menos três números; um quarto número é opcional, assim como um sufixo de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="84463-121">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="84463-122">Intervalos não são permitidos.</span><span class="sxs-lookup"><span data-stu-id="84463-122">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="84463-123">targetFramework</span><span class="sxs-lookup"><span data-stu-id="84463-123">targetFramework</span></span> | <span data-ttu-id="84463-124">Não</span><span class="sxs-lookup"><span data-stu-id="84463-124">No</span></span> | <span data-ttu-id="84463-125">O [TFM (moniker da estrutura de destino)](target-frameworks.md) a ser aplicado ao instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="84463-125">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="84463-126">Inicialmente, isso é definido para o destino do projeto quando um pacote é instalado.</span><span class="sxs-lookup"><span data-stu-id="84463-126">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="84463-127">Como resultado, diversos elementos `<package>` podem ter TFMs diferentes.</span><span class="sxs-lookup"><span data-stu-id="84463-127">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="84463-128">Por exemplo, se você criar um projeto direcionado ao .NET 4.5.2, os pacotes instalados nesse ponto usarão TFM do net452.</span><span class="sxs-lookup"><span data-stu-id="84463-128">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="84463-129">Mais tarde, se você redirecionar o projeto para .NET 4.6 e adicionar mais pacotes, eles usarão o TFM do net46.</span><span class="sxs-lookup"><span data-stu-id="84463-129">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="84463-130">Uma incompatibilidade entre o destino do projeto e os atributos `targetFramework` gerará avisos e, nesse caso, você pode reinstalar os pacotes afetados.</span><span class="sxs-lookup"><span data-stu-id="84463-130">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="84463-131">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="84463-131">allowedVersions</span></span> | <span data-ttu-id="84463-132">Não</span><span class="sxs-lookup"><span data-stu-id="84463-132">No</span></span> | <span data-ttu-id="84463-133">Um intervalo de versões permitidas para este pacote aplicado durante a atualização de pacote (consulte [Restrições de versões de upgrade](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="84463-133">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="84463-134">Ele *não* afeta quais pacotes são instalados durante a operação de instalação ou restauração.</span><span class="sxs-lookup"><span data-stu-id="84463-134">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="84463-135">Consulte [Controle de versão do pacote](../concepts/package-versioning.md#version-ranges) para ver a sintaxe.</span><span class="sxs-lookup"><span data-stu-id="84463-135">See [Package versioning](../concepts/package-versioning.md#version-ranges) for syntax.</span></span> <span data-ttu-id="84463-136">A interface do usuário do PackageManager também desabilita todas as versões fora do intervalo permitido.</span><span class="sxs-lookup"><span data-stu-id="84463-136">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="84463-137">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="84463-137">developmentDependency</span></span> | <span data-ttu-id="84463-138">Não</span><span class="sxs-lookup"><span data-stu-id="84463-138">No</span></span> | <span data-ttu-id="84463-139">Se o próprio projeto consumidor criar um pacote do NuGet, definir isso como `true` para uma dependência evita que o pacote seja incluído quando o pacote consumidor for criado.</span><span class="sxs-lookup"><span data-stu-id="84463-139">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="84463-140">O padrão é `false`.</span><span class="sxs-lookup"><span data-stu-id="84463-140">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="84463-141">Exemplos</span><span class="sxs-lookup"><span data-stu-id="84463-141">Examples</span></span>

<span data-ttu-id="84463-142">O seguinte `packages.config` refere-se a duas dependências:</span><span class="sxs-lookup"><span data-stu-id="84463-142">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="84463-143">O `packages.config` a seguir refere-se a nove pacotes, mas `Microsoft.Net.Compilers` não será incluído ao compilar o pacote consumidor devido ao atributo `developmentDependency`.</span><span class="sxs-lookup"><span data-stu-id="84463-143">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="84463-144">A referência ao Newtonsoft.Json também restringe as atualizações somente às versões 8.x e 9.x.</span><span class="sxs-lookup"><span data-stu-id="84463-144">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

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
