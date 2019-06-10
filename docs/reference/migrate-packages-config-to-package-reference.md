---
title: Migrando do Package para formatos de PackageReference
description: Obter detalhes sobre como migrar um projeto do formato de gerenciamento do Package para PackageReference com suporte do NuGet 4.0 ou superior e o VS2017 e .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 09d132aeaf00d2a1d095b9638b455cc23de91f2c
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812883"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrar de Packages. config para PackageReference

Visual Studio 2017 versão 15.7 e posteriores dão suporte para migrar um projeto a partir de [Packages. config](./packages-config.md) formato de gerenciamento para o [PackageReference](../consume-packages/Package-References-in-Project-Files.md) formato.

## <a name="benefits-of-using-packagereference"></a>Benefícios de usar PackageReference

* **Gerenciar todas as dependências do projeto em um só lugar**: Assim como referências projeto a projeto e referências de assembly, o pacote NuGet faz referência (usando o `PackageReference` nó) são gerenciados diretamente nos arquivos de projeto em vez de usar um arquivo Packages. config separados.
* **Modo de exibição organizado de dependências de nível superior**: Ao contrário de Packages. config, o PackageReference lista somente os pacotes NuGet instalados diretamente no projeto. Como resultado, a UI do Gerenciador de pacotes NuGet e o arquivo de projeto não são desorganizados com dependências de nível inferior.
* **Melhorias de desempenho**: Ao usar PackageReference, os pacotes são mantidos na *global-packages* pasta (conforme descrito em [gerenciar os pacotes globais e as pastas de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md) em vez de em um `packages` pasta dentro de solução. Como resultado, o PackageReference desempenho mais rápido e consome menos espaço em disco.
* **Um controle refinado sobre as dependências e fluxo de conteúdo**: Usando os recursos existentes do MSBuild permite que você [condicionalmente fazer referência a um pacote do NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) e escolher as referências de pacote por estrutura de destino, configuração, plataforma ou outras tabelas dinâmicas.
* **PackageReference está em desenvolvimento ativo**: Ver [PackageReference problemas no GitHub](https://aka.ms/nuget-pr-improvements). Packages. config não está mais sob desenvolvimento ativo.

### <a name="limitations"></a>Limitações

* PackageReference do NuGet não está disponível no Visual Studio 2015 e anteriores. Projetos migrados podem ser abertos apenas no Visual Studio 2017.
* Migração não está atualmente disponível para projetos C++ e ASP.NET.
* Alguns pacotes podem não ser totalmente compatíveis com o PackageReference. Para obter mais informações, consulte [problemas de compatibilidade de pacote](#package-compatibility-issues).

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
> Antes de começar a migração, o Visual Studio cria um backup do projeto para permitir que você [reversão para Packages. config](#how-to-roll-back-to-packagesconfig) se necessário.

1. Abra uma solução que contém o projeto usando `packages.config`.

1. No **Gerenciador de soluções**, clique com botão direito no **referências** nó ou o `packages.config` arquivo e selecione **Migrovat Packages. config na PackageReference...** .

1. O migrator analisa as referências do pacote NuGet do projeto e tenta categorize-as em **dependências de nível superior** (pacotes do NuGet que você instalou diretamente) e **dependências transitivas** (pacotes que foram instalados como dependências de pacotes de nível superior).

   > [!Note]
   > PackageReference dá suporte à restauração de pacote transitivo e resolve as dependências dinamicamente, que significa que dependências transitivas não precisam ser instaladas explicitamente.

1. (Opcional) Você pode optar por se tratar de um pacote do NuGet classificado como uma dependência transitiva como uma dependência de nível superior, selecionando o **nível superior** opção para o pacote. Essa opção é automaticamente definida para pacotes que contêm os ativos que não fluem transitivamente (aqueles na `build`, `buildCrossTargeting`, `contentFiles`, ou `analyzers` pastas) e aqueles marcados como uma dependência de desenvolvimento (`developmentDependency = "true"`).

1. Revisar qualquer [problemas de compatibilidade de pacote](#package-compatibility-issues).

1. Selecione **Okey** para iniciar a migração.

1. No final da migração, o Visual Studio fornece um relatório com um caminho para o backup, a lista de pacotes instalados (dependências de nível superior), uma lista de pacotes referenciados como dependências transitivas e uma lista de problemas de compatibilidade identificados no início do migração. O relatório é salvo na pasta de backup.

1. Valide que a solução compila e executa. Se você encontrar problemas, [arquivar um problema no GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Como reverter para Packages. config

1. Feche o projeto migrado.

1. Copie o arquivo de projeto e `packages.config` do backup (normalmente `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) para a pasta do projeto. Exclua a pasta obj se ele existir no diretório raiz do projeto.

1. Abra o projeto.

1. Abra o Console do Gerenciador de pacotes usando o **Ferramentas > Gerenciador de pacotes NuGet > Console do Gerenciador de pacotes** comando de menu.

1. Execute o seguinte comando no Console:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Criar um pacote após a migração

Depois que a migração for concluída, é recomendável que você adicione uma referência para o [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget do pacote e, em seguida, use [pacote msbuild](../reference/msbuild-targets.md#pack-target) para criar o pacote. Embora em alguns cenários, você pode usar `dotnet.exe pack` em vez de `msbuild pack`, não é recomendável.

## <a name="package-compatibility-issues"></a>Problemas de compatibilidade de pacote

Não há suporte para alguns aspectos que tinham suporte em Packages. config na PackageReference. O migrator analisa e detecta esses problemas. Qualquer pacote que tem um ou mais dos seguintes problemas pode não se comportar conforme o esperado após a migração.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>scripts de "install.ps1" são ignorados quando o pacote for instalado após a migração

| | |
| --- | --- |
| **Descrição** | Com o PackageReference, install.ps1 e uninstall.ps1 scripts do PowerShell não são executadas durante a instalação ou desinstalação de um pacote. |
| **Impacto potencial** | Pacotes que dependem desses scripts para configurar alguns comportamentos no projeto de destino podem não funcionar conforme o esperado. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>ativos de "conteúdo" não estão disponíveis quando o pacote for instalado após a migração

| | |
| --- | --- |
| **Descrição** | Ativos em um pacote `content` pasta não são compatíveis com PackageReference e são ignorados. Adiciona o suporte para PackageReference `contentFiles` ter melhor suporte transitivo e conteúdo compartilhado.  |
| **Impacto potencial** | Ativos no `content` não são copiados para o projeto e o projeto de código que depende da presença desses ativos exige a refatoração.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Transformações XDT não são aplicadas quando o pacote for instalado após a atualização

| | |
| --- | --- |
| **Descrição** | Não há suporte para transformações XDT com PackageReference e `.xdt` arquivos são ignorados ao instalar ou desinstalar um pacote.   |
| **Impacto potencial** | Transformações XDT não são aplicadas nos arquivos de projeto XML, mais comumente, `web.config.install.xdt` e `web.config.uninstall.xdt`, que significa que o projeto` web.config` arquivo não é atualizado quando o pacote é instalado ou desinstalado. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Assemblies na raiz lib são ignorados quando o pacote for instalado após a migração

| | |
| --- | --- |
| **Descrição** | Com o PackageReference, assemblies presente na raiz do `lib` pasta sem uma target framework subpasta específica são ignoradas. O NuGet procura uma subpasta, o moniker da estrutura de destino (TFM) correspondente a estrutura de destino do projeto de correspondência e instala os assemblies correspondentes no projeto. |
| **Impacto potencial** | Pacotes que não têm uma subpasta, o moniker da estrutura de destino (TFM) correspondente a estrutura de destino do projeto de correspondência não podem se comportar como esperado após a transição ou falha na instalação durante a migração |

## <a name="found-an-issue-report-it"></a>Encontramos um problema? Relatá-lo!

Se você tiver um problema com a experiência de migração, faça [arquivar um problema no repositório do GitHub do NuGet](https://github.com/NuGet/Home/issues/).
