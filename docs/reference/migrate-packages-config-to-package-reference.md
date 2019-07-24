---
title: Migrando do Package. config para formatos PackageReference
description: Detalhes sobre como migrar um projeto do formato de gerenciamento Package. config para PackageReference com suporte pelo NuGet 4.0 + e VS2017 e .NET Core 2,0
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: d1c32f4a926f1f688db3ea6a9ca2eed1a21b2dec
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433284"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrar de Packages. config para PackageReference

O Visual Studio 2017 versão 15,7 e posterior dá suporte à migração de um projeto do formato de gerenciamento [Packages. config](./packages-config.md) para o formato [PackageReference](../consume-packages/Package-References-in-Project-Files.md) .

## <a name="benefits-of-using-packagereference"></a>Benefícios do uso do PackageReference

* **Gerenciar todas as dependências de projeto em um único local**: Assim como as referências de projeto para projeto e referências de assembly, as referências de `PackageReference` pacote NuGet (usando o nó) são gerenciadas diretamente em arquivos de projeto em vez de usar um arquivo Packages. config separado.
* **Exibição organizada de dependências de nível superior**: Ao contrário de Packages. config, o PackageReference lista apenas os pacotes NuGet que você instalou diretamente no projeto. Como resultado, a interface do usuário do Gerenciador de pacotes NuGet e o arquivo de projeto não ficam confusos com dependências de nível inferior.
* **Aprimoramentos de desempenho**: Ao usar o PackageReference, os pacotes são mantidos na pasta *global-Packages* (conforme descrito em [Gerenciando os pacotes globais e pastas](../consume-packages/managing-the-global-packages-and-cache-folders.md) de cache `packages` em vez de em uma pasta dentro da solução. Como resultado, o PackageReference é executado mais rapidamente e consome menos espaço em disco.
* **Controle fino sobre dependências e fluxo de conteúdo**: Usar os recursos existentes do MSBuild permite referenciar [condicionalmente um pacote NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) e escolher referências de pacote por estrutura de destino, configuração, plataforma ou outras tabelas dinâmicas.
* O **PackageReference está em desenvolvimento ativo**: Consulte [problemas de PackageReference no GitHub](https://aka.ms/nuget-pr-improvements). Packages. config não está mais em desenvolvimento ativo.

### <a name="limitations"></a>Limitações

* O NuGet PackageReference não está disponível no Visual Studio 2015 e versões anteriores. Projetos migrados podem ser abertos somente no Visual Studio 2017 e posterior.
* Atualmente, a migração não está disponível para projetos C++ e ASP.NET.
* Alguns pacotes podem não ser totalmente compatíveis com PackageReference. Para obter mais informações, consulte [problemas de compatibilidade do pacote](#package-compatibility-issues).

### <a name="known-issues"></a>Problemas Conhecidos

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

## <a name="migration-steps"></a>Etapas de migração

> [!Note]
> Antes de iniciar a migração, o Visual Studio cria um backup do projeto para permitir que você reverta [para Packages. config](#how-to-roll-back-to-packagesconfig) , se necessário.

1. Abra uma solução que contém o `packages.config`projeto usando.

1. Em **Gerenciador de soluções**, clique com o botão direito  do mouse no nó `packages.config` referências ou no arquivo e selecione **migrar Packages. config para PackageReference...** .

1. O migrador analisa as referências de pacote NuGet do projeto e tenta categorizá-las em dependências de **nível superior** (pacotes NuGet que você instalou diretamente) e **dependências transitivas** (pacotes que foram instalados como dependências de pacotes de nível superior).

   > [!Note]
   > O PackageReference dá suporte à restauração de pacote transitiva e resolve dependências de forma dinâmica, o que significa que as dependências transitivas não precisam ser instaladas explicitamente.

1. Adicional Você pode optar por tratar um pacote NuGet classificado como uma dependência transitiva como uma dependência de nível superior selecionando a opção de **nível superior** para o pacote. Essa opção é definida automaticamente para pacotes que contêm ativos que não fluem de forma transitiva (aquelas nas `build`pastas `buildCrossTargeting`, `contentFiles`, ou `analyzers` ) e aquelas marcadas como uma dependência de desenvolvimento`developmentDependency = "true"`().

1. Examine os [problemas de compatibilidade do pacote](#package-compatibility-issues).

1. Selecione **OK** para iniciar a migração.

1. No final da migração, o Visual Studio fornece um relatório com um caminho para o backup, a lista de pacotes instalados (dependências de nível superior), uma lista de pacotes referenciados como dependências transitivas e uma lista de problemas de compatibilidade identificados no início de as. O relatório é salvo na pasta de backup.

1. Valide se a solução é compilada e executada. Se você encontrar problemas, [Execute um problema no GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Como reverter para Packages. config

1. Feche o projeto migrado.

1. Copie o arquivo de projeto `packages.config` e do backup (normalmente `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) para a pasta do projeto. Exclua a pasta obj se ela existir no diretório raiz do projeto.

1. Abra o projeto.

1. Abra o console do Gerenciador de pacotes usando as **ferramentas > o Gerenciador de pacotes NuGet >** comando de menu do console do Gerenciador de pacotes.

1. Execute o seguinte comando no console do:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Criar um pacote após a migração

Depois que a migração for concluída, recomendamos que você adicione uma referência ao pacote NuGet [NuGet. Build. Tasks. Pack](https://www.nuget.org/packages/nuget.build.tasks.pack) e, em seguida, use o [MSBuild-t:Pack](../reference/msbuild-targets.md#pack-target) para criar o pacote. Embora em alguns cenários você possa usar `dotnet.exe pack` em vez `msbuild -t:pack`de, não é recomendável.

## <a name="package-compatibility-issues"></a>Problemas de compatibilidade do pacote

Não há suporte para alguns aspectos que tenham suporte em Packages. config em PackageReference. O migrador analisa e detecta esses problemas. Qualquer pacote que tenha um ou mais dos seguintes problemas pode não se comportar conforme o esperado após a migração.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>os scripts "install. ps1" são ignorados quando o pacote é instalado após a migração

| | |
| --- | --- |
| **Descrição** | Com o PackageReference, os scripts do PowerShell Install. ps1 e Uninstall. ps1 não são executados durante a instalação ou desinstalação de um pacote. |
| **Impacto potencial** | Os pacotes que dependem desses scripts para configurar algum comportamento no projeto de destino podem não funcionar conforme o esperado. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>os ativos de "conteúdo" não estão disponíveis quando o pacote é instalado após a migração

| | |
| --- | --- |
| **Descrição** | Os ativos na `content` pasta de um pacote não têm suporte com PackageReference e são ignorados. O PackageReference adiciona suporte `contentFiles` para para ter um melhor suporte transitivo e conteúdo compartilhado.  |
| **Impacto potencial** | Os ativos `content` no não são copiados para o projeto e o código do projeto que depende da presença desses ativos requer refatoração.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Transformações de XDT não são aplicadas quando o pacote é instalado após a atualização

| | |
| --- | --- |
| **Descrição** | As transformações xdt não têm suporte com PackageReference `.xdt` e os arquivos são ignorados durante a instalação ou desinstalação de um pacote.   |
| **Impacto potencial** | As transformações de xdt não são aplicadas a nenhum arquivo XML de projeto, `web.config.install.xdt` mais `web.config.uninstall.xdt`comumente e, o que significa` web.config` que o arquivo do projeto não é atualizado quando o pacote é instalado ou desinstalado. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Os assemblies na raiz lib são ignorados quando o pacote é instalado após a migração

| | |
| --- | --- |
| **Descrição** | Com PackageReference, os assemblies presentes na raiz da `lib` pasta sem uma subpasta específica da estrutura de destino são ignorados. O NuGet procura uma subpasta correspondente ao moniker da estrutura de destino (TFM) correspondente à estrutura de destino do projeto e instala os assemblies correspondentes no projeto. |
| **Impacto potencial** | Os pacotes que não têm uma subpasta correspondente ao moniker da estrutura de destino (TFM) correspondentes à estrutura de destino do projeto podem não se comportar conforme o esperado após a transição ou falha na instalação durante a migração |

## <a name="found-an-issue-report-it"></a>Encontrou um problema? Relatório!

Se você encontrar um problema com a experiência de migração, registre [um problema no repositório GitHub do NuGet](https://github.com/NuGet/Home/issues/).
