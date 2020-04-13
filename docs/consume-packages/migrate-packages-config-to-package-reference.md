---
title: Como migrar do package.config para os formatos PackageReference
description: Detalhes sobre como migrar um projeto do formato de gerenciamento package.config para PackageReference com suporte pelo NuGet 4.0+ e VS2017 e .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8e825410d621ff2946e23e80173292f24f9d21f2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428887"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrar de packages.config para PackageReference

O Visual Studio 2017 versão 15.7 e posterior oferece suporte à migração de um projeto do formato de gerenciamento [packages.config](../reference/packages-config.md) para o formato [PackageReference](../consume-packages/Package-References-in-Project-Files.md).

## <a name="benefits-of-using-packagereference"></a>Benefícios do uso de PackageReference

* **Gerencie todas as dependências do projeto em um só lugar**: Assim como o `PackageReference` projeto para projetar referências e referências de montagem, as referências do pacote NuGet (usando o nó) são gerenciadas diretamente dentro de arquivos de projeto, em vez de usar um arquivo de pacotes separados.config.
* **Visão desordenada de dependências de alto nível**: Ao contrário de packages.config, o PackageReference lista apenas os pacotes NuGet que você instalou diretamente no projeto. Como resultado, a interface do usuário do Gerenciador de Pacotes do NuGet e o arquivo de projeto não ficam cheios de dependências de baixo nível.
* **Melhorias de desempenho**: Ao usar o PackageReference, os pacotes são mantidos na pasta *de pacotes globais* (conforme descrito no [gerenciamento dos pacotes globais e pastas de cache,](../consume-packages/managing-the-global-packages-and-cache-folders.md) em vez de em uma `packages` pasta dentro da solução. Como resultado, PackageReference é executado mais rapidamente e consome menos espaço em disco.
* **Controle fino sobre dependências e fluxo**de conteúdo : O uso dos recursos existentes do MSBuild permite que você [consulte condicionalmente um pacote NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) e escolha referências de pacote por framework de destino, configuração, plataforma ou outros pivôs.
* **O PackageReference está em desenvolvimento ativo**: veja [problemas de referência do pacote no GitHub](https://aka.ms/nuget-pr-improvements). packages.config não está mais em desenvolvimento ativo.

### <a name="limitations"></a>Limitações

* O NuGet PackageReference não está disponível no Visual Studio 2015 e versões anteriores. Os projetos migrados podem ser abertos apenas no Visual Studio 2017 e posterior.
* Atualmente, a migração não está disponível para projetos C++ e ASP.NET.
* Alguns pacotes podem não ser totalmente compatíveis com o PackageReference. Para obter mais informações, confira [Problemas de compatibilidade de pacotes](#package-compatibility-issues).

Além disso, existem algumas diferenças em como o PackageReferences funciona em comparação com pacotes.config. Por exemplo , [restringir versões de upgrade](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) não é suppred pelo PackageReference, mas adicionar suporte para [versões flutuantes](../consume-packages/package-references-in-project-files.md#floating-versions).

### <a name="known-issues"></a>Problemas conhecidos

1. A opção `Migrate packages.config to PackageReference...` não está disponível no menu de contexto de clique com o botão direito do mouse 

#### <a name="issue"></a>Problema 
 
Quando um projeto é aberto pela primeira vez, o NuGet pode não ser inicializado até que uma operação do NuGet seja executada. Isso faz com que a opção de migração não apareça no menu de contexto com o botão direito do mouse em `packages.config` ou `References`. 

#### <a name="workaround"></a>Solução alternativa 

Execute qualquer uma das seguintes ações NuGet: 
* Abra a interface do usuário do Gerenciador de Pacotes, clique com o botão direito do mouse em `References` e selecione `Manage NuGet Packages...` 
* Abra o Console do Gerenciador de Pacotes em `Tools > NuGet Package Manager`, selecione `Package Manager Console` 
* Execute a restauração do NuGet, clique com o botão direito do mouse no nó de solução no Gerenciador de Soluções e selecione `Restore NuGet Packages` 
* Compile o projeto, o que também acionará a restauração do NuGet 

Agora você deve conseguir ver a opção de migração. Observe que essa opção não tem suporte e não será exibida para os tipos de projeto do ASP.NET e C++. 

## <a name="migration-steps"></a>Etapas da migração

> [!Note]
> Antes do início da migração, o Visual Studio cria um backup do projeto para permitir que você [reverta para packages.config](#how-to-roll-back-to-packagesconfig), se necessário.

1. Abra uma solução que contém um projeto que usa `packages.config`.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó **Referências** ou no arquivo `packages.config` e selecione **Migrar packages.config para PackageReference...**.

1. O migrador analisa as referências do pacote NuGet do projeto e tenta categorizá-las em **Dependências de nível superior** (pacotes NuGet instalados diretamente) e **Dependências transitivas** (pacotes instalados como dependências de pacotes de nível superior).

   > [!Note]
   > O PackageReference oferece suporte à restauração transitiva de pacotes e resolve dependências de modo dinâmico, o que significa que as dependências transitivas não precisam ser instaladas explicitamente.

1. (Opcional) Você pode tratar um pacote NuGet classificado como dependência transitiva como uma dependência de nível superior, selecionando a opção**Nível Superior** para o pacote. Essa opção é configurada automaticamente para pacotes contendo ativos que não fluem transitivamente (nas pastas `build`, `buildCrossTargeting`, `contentFiles` ou `analyzers`) e aqueles marcados como uma dependência de desenvolvimento (`developmentDependency = "true"`).

1. Analise quaisquer [problemas de compatibilidade de pacotes](#package-compatibility-issues).

1. Selecione **OK** para iniciar a migração.

1. No final da migração, o Visual Studio fornece um relatório com um caminho para o backup, a lista de pacotes instalados (dependências de nível superior), uma lista de pacotes referenciados como dependências transitivas e uma lista de problemas de compatibilidade identificados no início da migração. O relatório é salvo na pasta de backup.

1. Valide se a solução é compilada e executada. Se você encontrar problemas, [registre um problema no GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Como reverter para packages.config

1. Feche o projeto migrado.

1. Copie o arquivo do projeto e `packages.config` do backup (geralmente, `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) para a pasta do projeto. Exclua a pasta obj, se ela existir no diretório raiz do projeto.

1. Abra o projeto.

1. Abra o Console do Gerenciador de Pacotes usando o comando de menu **Ferramentas > Gerenciador de Pacotes NuGet > Console do Gerenciador de Pacotes**.

1. Execute o seguinte comando no console:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Criar um pacote após a migração

Quando a migração estiver concluída, recomendamos que você adicione uma referência ao pacote nuget [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) e use [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) para criar o pacote. Embora você possa usar `dotnet.exe pack` em vez de `msbuild -t:pack` em alguns cenários, isso não é recomendado.

## <a name="package-compatibility-issues"></a>Problemas de compatibilidade de pacotes

Alguns aspectos que tinham suporte em packages.config não têm suporte em PackageReference. O migrador analisa e detecta tais problemas. Qualquer pacote que tenha um ou mais dos problemas a seguir pode não se comportar conforme esperado após a migração.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>Os scripts "install.ps1" são ignorados quando o pacote é instalado após a migração

| | |
| --- | --- |
| **Descrição** | Com PackageReference, os scripts do PowerShell install.ps1 e uninstall.ps1 não são executados durante a instalação ou desinstalação de um pacote. |
| **Impacto potencial** | Pacotes que dependem desses scripts para configurar algum comportamento no projeto de destino podem não funcionar conforme o esperado. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>Os ativos "conteúdo" não estão disponíveis quando o pacote é instalado após a migração

| | |
| --- | --- |
| **Descrição** | Ativos na pasta `content` de um pacote não têm suporte com PackageReference e são ignorados. PackageReference adiciona suporte para `contentFiles` para ter um melhor suporte transitivo e conteúdo compartilhado.  |
| **Impacto potencial** | Os ativos em `content` não são copiados para o projeto e o código do projeto que depende da presença desses recursos requer refatoração.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Transformações XDT não são aplicadas quando o pacote é instalado após a atualização

| | |
| --- | --- |
| **Descrição** | As transformações XDT não têm suporte com PackageReference e os arquivos `.xdt` são ignorados durante a instalação ou desinstalação de um pacote.   |
| **Impacto potencial** | As transformações XDT não são aplicadas a nenhum arquivo XML de projeto, mais comumente, `web.config.install.xdt` e `web.config.uninstall.xdt`, o que significa que o arquivo ` web.config` do projeto não é atualizado quando o pacote é instalado ou desinstalado. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Assemblies na raiz lib são ignorados quando o pacote é instalado após a migração

| | |
| --- | --- |
| **Descrição** | Com PackageReference, os assemblies presentes na raiz da pasta `lib` sem uma subpasta específica da estrutura de destino são ignorados. O NuGet procura por uma subpasta correspondente ao TFM (moniker da estrutura de destino) que corresponde à estrutura de destino do projeto e instala os conjuntos correspondentes no projeto. |
| **Impacto potencial** | Os pacotes que não têm uma subpasta correspondente ao TFM (moniker da estrutura de destino) que corresponde à estrutura de destino do projeto podem não se comportar como esperado após a transição ou apresentar falha de instalação durante a migração |

## <a name="found-an-issue-report-it"></a>Encontrou um problema? Relate-o!

Se você tiver algum problema com a experiência de migração, [registre um problema no repositório GitHub do NuGet](https://github.com/NuGet/Home/issues/).
