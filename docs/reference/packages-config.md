---
title: Referência do arquivo NuGet Packages. config
description: Em alguns tipos de projeto, o packages.json mantém a lista de pacotes do NuGet usados no projeto.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: e10bc1625bc4cea7b7befe18caa22d33a876489b
ms.sourcegitcommit: f0b31af805183cf3a98eabb504e16d9b05223cfe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2018
---
# <a name="packagesconfig-reference"></a>Referência de packages.config

O arquivo `packages.config` é usado em alguns tipos de projeto para manter a lista de pacotes referenciados pelo projeto. Isso permite que o NuGet restaure facilmente as dependências do projeto quando ele a ser transportado para um computador diferente, como um servidor de build, sem todos esses pacotes.

Se usado, `packages.config` normalmente está localizado na raiz do projeto. Ela é criada automaticamente quando a primeira operação NuGet é executada, mas também pode ser criada manualmente antes de executar os comandos, como `nuget restore`.

Projetos que usam [PackageReference](../consume-packages/Package-References-in-Project-Files.md) não use `packages.config`.

## <a name="schema"></a>Esquema

O esquema é simples: após o cabeçalho padrão de XML está um único nó `<packages>` que contém um ou mais elementos `<package>`, um para cada referência. Cada elemento `<package>` pode ter os seguintes atributos:

| Atributo | Necessária | Descrição |
| --- | --- | --- |
| id | Sim | O identificador do pacote, como Newtonsoft.json ou Microsoft.AspNet.Mvc. | 
| version | Sim | A versão exata do pacote a ser instalado, como 3.1.1 ou 4.2.5.11-beta. Uma cadeia de caracteres de versão precisa ter pelo menos três números; um quarto número é opcional, assim como um sufixo de pré-lançamento. Intervalos não são permitidos. | 
| targetFramework | Não | O [TFM (moniker da estrutura de destino)](target-frameworks.md) a ser aplicado ao instalar o pacote. Inicialmente, isso é definido para o destino do projeto quando um pacote é instalado. Como resultado, diversos elementos `<package>` podem ter TFMs diferentes. Por exemplo, se você criar um projeto direcionado ao .NET 4.5.2, os pacotes instalados nesse ponto usarão TFM do net452. Mais tarde, se você redirecionar o projeto para .NET 4.6 e adicionar mais pacotes, eles usarão o TFM do net46. Uma incompatibilidade entre o destino do projeto e os atributos `targetFramework` gerará avisos e, nesse caso, você pode reinstalar os pacotes afetados. | 
| allowedVersions | Não | Um intervalo de versões permitidas para este pacote aplicado durante a atualização de pacote (consulte [Restrições de versões de upgrade](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Ele *não* afeta quais pacotes são instalados durante a operação de instalação ou restauração. Consulte [Controle de versão do pacote](../reference/package-versioning.md#version-ranges-and-wildcards) para ver a sintaxe. A interface do usuário do PackageManager também desabilita todas as versões fora do intervalo permitido. | 
| developmentDependency | Não | Se o próprio projeto consumidor criar um pacote do NuGet, definir isso como `true` para uma dependência evita que o pacote seja incluído quando o pacote consumidor for criado. O padrão é `false`. | 

## <a name="examples"></a>Exemplos

O seguinte `packages.config` refere-se a duas dependências:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

O `packages.config` a seguir refere-se a nove pacotes, mas `Microsoft.Net.Compilers` não será incluído ao compilar o pacote consumidor devido ao atributo `developmentDependency`. A referência ao Newtonsoft.Json também restringe as atualizações somente às versões 8.x e 9.x.

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
