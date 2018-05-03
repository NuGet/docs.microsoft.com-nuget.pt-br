---
title: Migrando do package.config para formatos de PackageReference
description: Obter detalhes sobre como migrar um projeto do formato de gerenciamento package.config para PackageReference com suporte pelo NuGet 4.0 + e VS2017 e .NET Core 2.0
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: 2b15d60d4f71fb2777e36c6a948ad72b4e2bc594
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrar de Packages. config para PackageReference

Visual Studio 2017 versão 15,7 Preview 3 e posterior oferece suporte a migração de um projeto a partir de [Packages](./packages-config.md) formato de gerenciamento para o [PackageReference](../consume-packages/Package-References-in-Project-Files.md) formato.

## <a name="benefits-of-using-packagereference"></a>Benefícios do uso de PackageReference

* **Gerenciar todas as dependências de projeto em um só lugar**: assim como referências de projeto ao projeto e referências de assembly, o pacote NuGet faz referência (usando o `PackageReference` nó) são gerenciados diretamente nos arquivos de projeto em vez de usar um separado arquivo Packages. config.
* **Uma exibição organizada de dependências de nível superior**: diferentemente Packages, PackageReference lista somente os pacotes do NuGet instalados diretamente no projeto. Como resultado, o NuGet Package Manager UI e o arquivo de projeto não são organizadas com dependências de nível inferior.
* **Melhorias de desempenho**: ao usar PackageReference, os pacotes são mantidos no *pacotes global* pasta (conforme descrito em [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md) em vez de em um `packages` pasta dentro da solução. Como resultado, PackageReference desempenho mais rápido e consome menos espaço em disco.
* **Problema controle sobre as dependências e fluxo de conteúdo**: usando os recursos existentes do MSBuild permite que você [condicionalmente fazem referência a um pacote do NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) e escolha as referências de pacote por estrutura de destino, configuração, plataforma ou outros pontos.
* **PackageReference está em desenvolvimento ativo**: consulte [PackageReference problemas no GitHub](https://aka.ms/nuget-pr-improvements). Packages. config não está mais em desenvolvimento ativo.

### <a name="limitations"></a>Limitações

* NuGet PackageReference não está disponível no Visual Studio 2015 e anteriores. Migrado de projetos pode ser aberto apenas no Visual Studio de 2017.
* Migração não está disponível atualmente para o projeto C++ e ASP.NET.
* Alguns pacotes podem não ser totalmente compatíveis com PackageReference. Para obter mais informações, consulte [problemas de compatibilidade do pacote](#package-compatibility-issues).

## <a name="migration-steps"></a>Etapas de migração

> [!Note]
> Antes de inicia a migração, o Visual Studio cria um backup do projeto para permitir que você [reverta a Packages](#how-to-roll-back-to-packagesconfig) se necessário.

1. Abrir uma solução que contém o projeto usando `packages.config`.

1. Em **Solution Explorer**, com o botão direito no **referências** nó ou o `packages.config` de arquivo e selecione **migrar Packages para PackageReference...** .

1. O migrator analisa as referências do pacote NuGet do projeto e tenta categorizá-los em **dependências de nível superior** (diretório você instalou pacotes do NuGet) e **dependências transitivas**(pacotes que foram instalados como dependências dos pacotes de nível superior).

   > [!Note]
   > PackageReference dá suporte à restauração do pacote transitiva e resolve dependências dinamicamente, que significa que as dependências transitivas não precisam ser instaladas explicitamente.

1. (Opcional) Você pode optar por tratar de um pacote do NuGet classificado como uma dependência transitiva como uma dependência de nível superior, selecionando o **nível superior** opção para o pacote. Essa opção é automaticamente definida para pacotes que contêm ativos que não fluem transitivamente (aqueles no `build`, `buildCrossTargeting`, `contentFiles`, ou `analyzers` pastas) e aqueles marcado como uma dependência de desenvolvimento (`developmentDependency = "true"`).

1. Analise qualquer [problemas de compatibilidade do pacote](#package-compatibility-issues).

1. Selecione **Okey** para iniciar a migração.

1. No final da migração, o Visual Studio fornece um relatório com um caminho para o backup, a lista de pacotes instalados (dependências de nível superior), uma lista de pacotes referenciados como dependências transitivas e uma lista de problemas de compatibilidade identificado no início de migração. O relatório é salvo na pasta de backup.

1. Valide que a solução é compilado e executado. Se você encontrar problemas, [um problema de arquivo no GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Como reverter para Packages. config

1. Feche o projeto migrado.

1. Copie o arquivo de projeto e `packages.config` do backup (geralmente `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) para a pasta do projeto.

1. Abra o projeto.

1. Abra o Console do Gerenciador de pacote usando o **Ferramentas > Gerenciador de pacotes do NuGet > Package Manager Console** comando de menu.

1. Execute o seguinte comando no Console:

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>Problemas de compatibilidade de pacote

Não há suporte para alguns aspectos que tinham suporte em Packages. config em PackageReference. O migrator analisa e detecta esses problemas. Qualquer pacote que tem um ou mais dos seguintes problemas pode não se comportar conforme o esperado após a migração.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>scripts "install.ps1" são ignorados quando o pacote for instalado depois da migração

| | |
| --- | --- |
| **Descrição** | Com PackageReference, install.ps1 e uninstall.ps1 scripts do PowerShell não são executadas durante a instalação ou desinstalação de um pacote. |
| **Impacto potencial** | Pacotes que dependem desses scripts para configurar o comportamento de alguns no projeto de destino podem não funcionar conforme o esperado. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>ativos de "conteúdo" não estão disponíveis quando o pacote for instalado depois da migração

| | |
| --- | --- |
| **Descrição** | Ativos em um pacote `content` pasta não são compatíveis com PackageReference e são ignorados. PackageReference adiciona suporte para `contentFiles` ter um suporte melhor transitivo e conteúdo compartilhado.  |
| **Impacto potencial** | Ativos em `content` não são copiados para o projeto e o projeto de código que depende da presença desses ativos requer a refatoração.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Transformações XDT não são aplicadas quando o pacote for instalado depois da atualização

| | |
| --- | --- |
| **Descrição** | Não há suporte para transformações XDT com PackageReference e `.xdt` arquivos são ignorados ao instalar ou desinstalar um pacote.   |
| **Impacto potencial** | Transformações XDT não são aplicadas para os arquivos XML de projeto, geralmente, `web.config.install.xdt` e `web.config.uninstall.xdt`, que significa que o projeto` web.config` arquivo não é atualizado quando o pacote for instalado ou desinstalado. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Assemblies na raiz da biblioteca são ignorados quando o pacote for instalado depois da migração

| | |
| --- | --- |
| **Descrição** | Com PackageReference, assemblies presentes na raiz da `lib` pasta sem uma destino do framework subpasta específica são ignorados. NuGet procura uma subpasta, o moniker da estrutura de destino (TFM) correspondente para o framework de destino do projeto de correspondência e instala os assemblies de correspondência no projeto. |
| **Impacto potencial** | Pacotes que não têm uma subpasta correspondente o moniker da estrutura de destino (TFM) correspondente para o framework de destino do projeto não podem se comportar conforme o esperado após a transição ou falha de instalação durante a migração |

## <a name="found-an-issue-report-it"></a>Encontrado um problema? Relatá-lo!

Se você tiver um problema com a experiência de migração, [um problema de arquivo no repositório do NuGet GitHub](https://github.com/NuGet/Home/issues/).
