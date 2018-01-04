---
title: Configurar o comportamento do NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c1e34826-d07d-4609-a0fd-123459ae89c5
description: "Arquivos NuGet.Config controlam o comportamento do NuGet tanto globalmente quanto em cada projeto e são modificados com o comando nuget config."
keywords: "Arquivos de configuração do NuGet, configuração do NuGet, configurações de comportamento do NuGet, configurações de comportamento do NuGet, configurações do NuGet, NuGet.Config, NuGetDefaults.Config, padrões"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f9e56b68f70387435cdaa1537db503abb912fd2a
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="configuring-nuget-behavior"></a><span data-ttu-id="01c1a-104">Configurando o comportamento de NuGet</span><span class="sxs-lookup"><span data-stu-id="01c1a-104">Configuring NuGet behavior</span></span>

<span data-ttu-id="01c1a-105">O comportamento do NuGet é controlado pelas configurações acumuladas em um ou mais arquivos `NuGet.Config` (XML) que podem existir no nível de projeto, usuário e computador.</span><span class="sxs-lookup"><span data-stu-id="01c1a-105">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="01c1a-106">Um arquivo global `NuGetDefaults.Config` (2.7 ou superior) também configura as origens de pacote especificamente.</span><span class="sxs-lookup"><span data-stu-id="01c1a-106">A global `NuGetDefaults.Config` file (2.7+) also specifically configures package sources.</span></span> <span data-ttu-id="01c1a-107">As configurações se aplicam a todos os comandos emitidos na CLI, no Console do Gerenciador de Pacotes e na interface do usuário do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="01c1a-107">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

<span data-ttu-id="01c1a-108">Neste tópico:</span><span class="sxs-lookup"><span data-stu-id="01c1a-108">In this topic:</span></span>

- [<span data-ttu-id="01c1a-109">Usos e locais do arquivo NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="01c1a-109">NuGet.Config file locations and uses</span></span>](#config-file-locations-and-uses)
- [<span data-ttu-id="01c1a-110">Alterando configurações</span><span class="sxs-lookup"><span data-stu-id="01c1a-110">Changing settings</span></span>](#changing-config-settings)
- [<span data-ttu-id="01c1a-111">Como as configurações são aplicadas</span><span class="sxs-lookup"><span data-stu-id="01c1a-111">How settings are applied</span></span>](#how-settings-are-applied)
- [<span data-ttu-id="01c1a-112">Arquivo NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="01c1a-112">NuGetDefaults.Config file</span></span>](#nuget-defaults-file)

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="01c1a-113">Usos e locais do arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="01c1a-113">Config file locations and uses</span></span>

| <span data-ttu-id="01c1a-114">Escopo</span><span class="sxs-lookup"><span data-stu-id="01c1a-114">Scope</span></span> | <span data-ttu-id="01c1a-115">Local do arquivo NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="01c1a-115">NuGet.Config file location</span></span> | <span data-ttu-id="01c1a-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="01c1a-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="01c1a-117">Projeto</span><span class="sxs-lookup"><span data-stu-id="01c1a-117">Project</span></span> | <span data-ttu-id="01c1a-118">Pasta do projeto ou qualquer pasta até a raiz da unidade</span><span class="sxs-lookup"><span data-stu-id="01c1a-118">Project folder or any folder up to the drive root</span></span> | <span data-ttu-id="01c1a-119">Em uma pasta de projeto, as configurações se aplicam apenas a esse projeto.</span><span class="sxs-lookup"><span data-stu-id="01c1a-119">In a project folder, settings apply only to that project.</span></span> <span data-ttu-id="01c1a-120">Em pastas pai que contém várias subpastas de projetos, as configurações se aplicam a todos os projetos nas subpastas.</span><span class="sxs-lookup"><span data-stu-id="01c1a-120">In parent folders that contain multiple projects subfolders, settings apply to all projects in those subfolders.</span></span> |
| <span data-ttu-id="01c1a-121">User</span><span class="sxs-lookup"><span data-stu-id="01c1a-121">User</span></span> | <span data-ttu-id="01c1a-122">Windows: %APPDATA%\NuGet\NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="01c1a-122">Windows: %APPDATA%\NuGet\NuGet.Config</span></span><br/><span data-ttu-id="01c1a-123">Mac/Linux: ~/.nuget/NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="01c1a-123">Mac/Linux: ~/.nuget/NuGet.Config</span></span> | <span data-ttu-id="01c1a-124">As configurações se aplicam a todas as operações, mas são substituídas por quaisquer configurações de nível de projeto.</span><span class="sxs-lookup"><span data-stu-id="01c1a-124">Settings apply to all operations, but are overridden by any project-level settings.</span></span> <span data-ttu-id="01c1a-125">Usando comandos da CLI, é possível especificar um arquivo de configuração diferente usando a opção `-configFile` para ignorar as configurações no arquivo no nível do usuário padrão.</span><span class="sxs-lookup"><span data-stu-id="01c1a-125">When using CLI commands, you can specify a different config file using the `-configFile` switch to ignore any settings in the default user-level file.</span></span> |
| <span data-ttu-id="01c1a-126">Computador</span><span class="sxs-lookup"><span data-stu-id="01c1a-126">Computer</span></span> | <span data-ttu-id="01c1a-127">Windows: %ProgramFiles(x86)%\NuGet\Config</span><span class="sxs-lookup"><span data-stu-id="01c1a-127">Windows: %ProgramFiles(x86)%\NuGet\Config</span></span><br/><span data-ttu-id="01c1a-128">Mac/Linux: $XDG_DATA_HOME (geralmente ~/.local/share)</span><span class="sxs-lookup"><span data-stu-id="01c1a-128">Mac/Linux: $XDG_DATA_HOME (typically ~/.local/share)</span></span> | <span data-ttu-id="01c1a-129">As configurações se aplicam a todas as operações, mas são substituídas por qualquer usuário configurações de nível de projeto.</span><span class="sxs-lookup"><span data-stu-id="01c1a-129">Settings apply to all operations on the computer, but are overriden by any user- or project-level settings.</span></span> |

<span data-ttu-id="01c1a-130">Observações para versões anteriores do NuGet:</span><span class="sxs-lookup"><span data-stu-id="01c1a-130">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="01c1a-131">O NuGet 3.3 e versões anteriores usavam uma pasta `.nuget` para configurações de toda a solução.</span><span class="sxs-lookup"><span data-stu-id="01c1a-131">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="01c1a-132">Este arquivo não é usado no NuGet 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="01c1a-132">This file not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="01c1a-133">Para o NuGet 2.6 a 3.x, o arquivo de configuração de nível de computador no Windows encontra-se em %ProgramData%\NuGet\Config [\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, em que *{IDE}* pode ser *VisualStudio*, *{Version}* é a versão do Visual Studio como *14.0* e *{SKU}* é *Community*, *Pro* ou *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="01c1a-133">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="01c1a-134">Para migrar as configurações para o NuGet 4.0 ou superior, simplesmente copie o arquivo de configuração para %ProgramFiles(x86)%\NuGet\Config. No Linux, esse local anterior era /etc/opt e no Mac era /Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="01c1a-134">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linus, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="01c1a-135">Alterar as definições da configuração</span><span class="sxs-lookup"><span data-stu-id="01c1a-135">Changing config settings</span></span>

<span data-ttu-id="01c1a-136">Um arquivo `NuGet.Config` é um arquivo de texto XML simples que contém pares chave-valor, conforme descrito no tópico [Definições de configuração do NuGet](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="01c1a-136">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../Schema/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="01c1a-137">As configurações são gerenciadas usando o [comando config](../tools/cli-ref-config.md) da CLI do NuGet:</span><span class="sxs-lookup"><span data-stu-id="01c1a-137">Settings are managed using the NuGet CLI [config command](../tools/cli-ref-config.md):</span></span>
- <span data-ttu-id="01c1a-138">Por padrão, as alterações são feitas no arquivo de configuração de nível de usuário.</span><span class="sxs-lookup"><span data-stu-id="01c1a-138">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="01c1a-139">Para alterar as configurações em um arquivo diferente, use a opção `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="01c1a-139">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="01c1a-140">Nesse caso, os arquivos podem usar qualquer nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="01c1a-140">In this case files can use any filename.</span></span>
- <span data-ttu-id="01c1a-141">As chaves sempre diferenciam maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="01c1a-141">Keys are always case sensitive.</span></span>
- <span data-ttu-id="01c1a-142">A elevação é necessária para alterar as configurações no arquivo de configurações no nível do computador.</span><span class="sxs-lookup"><span data-stu-id="01c1a-142">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="01c1a-143">Embora você possa modificar o arquivo em qualquer editor de texto, o NuGet (v3.4.3 e posterior) ignorará silenciosamente todo o arquivo de configuração se ele contiver XML malformado (marcas não correspondidas, aspas inválidas, etc.).</span><span class="sxs-lookup"><span data-stu-id="01c1a-143">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="01c1a-144">É por isso que é preferível gerenciar a configuração usando `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="01c1a-144">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="01c1a-145">Definindo um valor</span><span class="sxs-lookup"><span data-stu-id="01c1a-145">Setting a value</span></span>

<span data-ttu-id="01c1a-146">Windows:</span><span class="sxs-lookup"><span data-stu-id="01c1a-146">Windows:</span></span>

```
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\NuGet.Config
```

<span data-ttu-id="01c1a-147">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="01c1a-147">Mac/Linux:</span></span>

```
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> <span data-ttu-id="01c1a-148">No NuGet 3.4 e posterior, você pode usar as variáveis de ambiente em qualquer valor, como no `repositoryPath=%PACKAGEHOME%` (Windows) e `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="01c1a-148">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="01c1a-149">Removendo um valor</span><span class="sxs-lookup"><span data-stu-id="01c1a-149">Removing a value</span></span>

<span data-ttu-id="01c1a-150">Para remover um valor, especifique uma chave com um valor vazio.</span><span class="sxs-lookup"><span data-stu-id="01c1a-150">To remove a value, specify a key with an empty value.</span></span>

```
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="01c1a-151">Criar um novo arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="01c1a-151">Creating a new config file</span></span>

<span data-ttu-id="01c1a-152">Copie o modelo abaixo para o novo arquivo e, em seguida, use `nuget config --configFile <filename>` para definir os valores:</span><span class="sxs-lookup"><span data-stu-id="01c1a-152">Copy the template below into the new file and then use `nuget config --configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

<br/>

## <a name="how-settings-are-applied"></a><span data-ttu-id="01c1a-153">Como as configurações são aplicadas</span><span class="sxs-lookup"><span data-stu-id="01c1a-153">How settings are applied</span></span>

<span data-ttu-id="01c1a-154">Vários arquivos `NuGet.Config` permitem que você armazene as configurações em locais diferentes, para que elas se apliquem a um único projeto, um grupo de projetos ou todos os projetos.</span><span class="sxs-lookup"><span data-stu-id="01c1a-154">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="01c1a-155">Coletivamente, essas configurações se aplicam a qualquer operação do NuGet invocada na linha de comando ou do Visual Studio, com as configurações existentes “mais próximas” para um projeto ou a pasta atual tendo precedência.</span><span class="sxs-lookup"><span data-stu-id="01c1a-155">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="01c1a-156">Especificamente, o NuGet carrega as configurações dos arquivos de configuração diferente na seguinte ordem:</span><span class="sxs-lookup"><span data-stu-id="01c1a-156">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="01c1a-157">O [arquivo NuGetDefaults.Config](#nuget-defaults-file), que contém as configurações relacionadas somente às origens de pacotes.</span><span class="sxs-lookup"><span data-stu-id="01c1a-157">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="01c1a-158">O arquivo de nível de computador.</span><span class="sxs-lookup"><span data-stu-id="01c1a-158">The computer-level file.</span></span>
1. <span data-ttu-id="01c1a-159">O arquivo de nível de usuário.</span><span class="sxs-lookup"><span data-stu-id="01c1a-159">The user-level file.</span></span>
1. <span data-ttu-id="01c1a-160">O arquivo especificado com `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="01c1a-160">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="01c1a-161">Arquivos encontrados em todas as pastas no caminho da raiz de unidade para a pasta atual (em que nuget.exe é invocado ou a pasta que contém o projeto do Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="01c1a-161">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="01c1a-162">Por exemplo, se um comando for invocado em c:\A\B\C, o NuGet procura e carrega os arquivos de configuração em c:\,, c:\A, c:\A\B e, finalmente, c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="01c1a-162">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="01c1a-163">À medida que o NuGet encontra configurações nesses arquivos, eles são aplicados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="01c1a-163">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="01c1a-164">Para elementos de item único, o NuGet substituiu qualquer valor encontrado anteriormente pela mesma chave.</span><span class="sxs-lookup"><span data-stu-id="01c1a-164">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="01c1a-165">Isso significa que as configurações que são “mais próximas” da pasta ou projeto atual substituem quaisquer outras encontradas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="01c1a-165">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="01c1a-166">Por exemplo, a definição `defaultPushSource` em `NuGetDefaults.Config` será substituída se ela existir em qualquer outro arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="01c1a-166">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="01c1a-167">Para elementos de coleta (como `<packageSources>`), o NuGet combina os valores de todos os arquivos de configuração em uma única coleção.</span><span class="sxs-lookup"><span data-stu-id="01c1a-167">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="01c1a-168">Quando `<clear />` está presente para um nó específico, o NuGet ignora os valores de configuração definidos anteriormente para esse nó.</span><span class="sxs-lookup"><span data-stu-id="01c1a-168">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="01c1a-169">Explicação passo a passo das configurações</span><span class="sxs-lookup"><span data-stu-id="01c1a-169">Settings walkthrough</span></span>

<span data-ttu-id="01c1a-170">Digamos que você tem a seguinte estrutura de pasta em duas unidades separadas:</span><span class="sxs-lookup"><span data-stu-id="01c1a-170">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="01c1a-171">Dessa forma, você terá quatro arquivos `NuGet.Config` nos seguintes locais com o conteúdo em questão.</span><span class="sxs-lookup"><span data-stu-id="01c1a-171">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="01c1a-172">(O arquivo no nível de computador não está incluído neste exemplo, mas se comportaria da mesma forma que o arquivo de nível de usuário.)</span><span class="sxs-lookup"><span data-stu-id="01c1a-172">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="01c1a-173">Arquivo A. Arquivo no nível do usuário, (%APPDATA%\NuGet\NuGet.Config no Windows, ~/.nuget/NuGet.Config no Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="01c1a-173">File A. User-level file, (%APPDATA%\NuGet\NuGet.Config on Windows, ~/.nuget/NuGet.Config on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="01c1a-174">Arquivo B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="01c1a-174">File B. disk_drive_2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>        
        <add key="repositoryPath" value="disk_drive_2/tmp" />
    </config>
    <packageRestore>
        <add key="enabled" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="01c1a-175">Arquivo C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="01c1a-175">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="External/Packages" />
        <add key="defaultPushSource" value="https://MyPrivateRepo/ES/api/v2/package" />
    </config>
    <packageSources>
        <clear /> <!-- ensure only the sources defined below are used -->
        <add key="MyPrivateRepo - ES" value="https://MyPrivateRepo/ES/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="01c1a-176">Arquivo D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="01c1a-176">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="01c1a-177">O NuGet, em seguida, carrega e aplica as configurações como mostrado a seguir, dependendo de onde ele é chamado:</span><span class="sxs-lookup"><span data-stu-id="01c1a-177">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="01c1a-178">**Invocado de disk_drive_1/users**: somente o repositório padrão listado no arquivo de configuração de nível do usuário (A) é usado, pois esse é o único arquivo encontrado em disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="01c1a-178">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="01c1a-179">**Invocado de disk_drive_2/ ou disk_drive_/tmp**: o arquivo no nível do usuário (A) é carregado primeiro, depois o NuGet acessa a raiz de disk_drive_2 e descobre o arquivo (B).</span><span class="sxs-lookup"><span data-stu-id="01c1a-179">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="01c1a-180">O NuGet também procura um arquivo de configuração em /tmp, mas não o encontra.</span><span class="sxs-lookup"><span data-stu-id="01c1a-180">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="01c1a-181">Como resultado, o repositório padrão no nuget.org é usado, a restauração de pacote é habilitada e os pacotes são expandidos em disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="01c1a-181">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="01c1a-182">**Invocado de disk_drive_2/Project1 ou disk_drive_2/Project1/Source**: o arquivo de nível do usuário (A) é carregado primeiro e então, o NuGet carrega o arquivo (B) da raiz de disk_drive_2, seguido pelo arquivo (C).</span><span class="sxs-lookup"><span data-stu-id="01c1a-182">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="01c1a-183">As configurações em (C) substituirão as de (B) e (A), portanto, o `repositoryPath` em que os pacotes são instalados são disk_drive_2/Project1/External/Packages em vez de *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="01c1a-183">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="01c1a-184">Além disso, como (C) limpa o `<packageSources>`, o nuget.org não está mais disponível como uma origem, restando apenas `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="01c1a-184">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="01c1a-185">**Invocado de disk_drive_2/Project2 ou disk_drive_2/Project2/Source**: o arquivo de nível de usuário (A) é carregado primeiro e seguido pelos arquivos (B) e (D).</span><span class="sxs-lookup"><span data-stu-id="01c1a-185">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="01c1a-186">Como `packageSources` não foi apagado, ambos `nuget.org` e `https://MyPrivateRepo/DQ/nuget` estão disponíveis como origens.</span><span class="sxs-lookup"><span data-stu-id="01c1a-186">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="01c1a-187">Pacotes são expandidos em disk_drive_2/tmp conforme especificado em (B).</span><span class="sxs-lookup"><span data-stu-id="01c1a-187">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="01c1a-188">Arquivo de padrões do NuGet</span><span class="sxs-lookup"><span data-stu-id="01c1a-188">NuGet defaults file</span></span>

<span data-ttu-id="01c1a-189">O arquivo `NuGetDefaults.Config` existe para especificar origens de pacote do qual os pacotes são instalados e atualizados, e para controlar o destino padrão para publicar pacotes com `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="01c1a-189">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="01c1a-190">Como os administradores podem implantar convenientemente (usando a Política de Grupo, por exemplo) arquivos `NuGetDefaults.Config` consistentes em computadores de desenvolvedor e de build, eles podem garantir que todos na organização estejam usando as origens de pacotes corretas, em vez do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="01c1a-190">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensuring that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="01c1a-191">O arquivo `NuGetDefaults.Config` nunca faz com que a origem do pacote seja removida da configuração do NuGet do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="01c1a-191">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="01c1a-192">Isso significa que, se o desenvolvedor já tiver usado o NuGet e, portanto, a origem do pacote no nuget.org está registrada, ele não será removido após a criação de um arquivo `NuGetDefaults.Config`.</span><span class="sxs-lookup"><span data-stu-id="01c1a-192">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="01c1a-193">Além disso, nem o `NuGetDefaults.Config` nem nenhum outro mecanismo no NuGet pode impedir o acesso às origens de pacote como nuget.org. Se uma organização desejar bloquear esse acesso, ela usará outros meios, como firewalls, para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="01c1a-193">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it much use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="01c1a-194">Local do NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="01c1a-194">NuGetDefaults.Config location</span></span>

<span data-ttu-id="01c1a-195">Windows: %ProgramFiles(x86)%\NuGet\Config (NuGet 2.7 para NuGet 3.x: %PROGRAMDATA%\NuGet\NuGetDefaults.Config) Mac/Linux: $XDG_DATA_HOME (geralmente ~/.local/share)</span><span class="sxs-lookup"><span data-stu-id="01c1a-195">Windows: %ProgramFiles(x86)%\NuGet\Config (NuGet 2.7 to NuGet 3.x: %PROGRAMDATA%\NuGet\NuGetDefaults.Config) Mac/Linux: $XDG_DATA_HOME (typically ~/.local/share)</span></span> 

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="01c1a-196">Configurações do NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="01c1a-196">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="01c1a-197">`packageSources`: esta coleção tem o mesmo significado que `packageSources` em arquivos de configuração regulares e especifica as origens padrão na ordem preferencial.</span><span class="sxs-lookup"><span data-stu-id="01c1a-197">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources in their preferred order.</span></span> <span data-ttu-id="01c1a-198">Se essa configuração existir em `NuGetDefaults.Config`, em seguida, o NuGet não usa nuget.org como uma origem de pacote padrão.</span><span class="sxs-lookup"><span data-stu-id="01c1a-198">If this setting exists in `NuGetDefaults.Config`, then NuGet doesn't use nuget.org as a default package source.</span></span> <span data-ttu-id="01c1a-199">Dessa forma, um administrador pode verificar se todos aqueles que usam este arquivo estão trabalhando com as mesmas origens e evita o uso do nuget.org, se desejado.</span><span class="sxs-lookup"><span data-stu-id="01c1a-199">An administrator can thus make sure that everyone using this file is working with the same sources and avoids using nuget.org if desired.</span></span>

- <span data-ttu-id="01c1a-200">`disabledPackageSources`: esta coleção também tem o mesmo significado que arquivos `NuGet.Config`, em que cada origem afetada é listada por seu nome e um valor true/false que indica se ela está desabilitada.</span><span class="sxs-lookup"><span data-stu-id="01c1a-200">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="01c1a-201">Isso permite que o nome de origem e a URL permaneçam em `packageSources` sem que ele seja ativado por padrão.</span><span class="sxs-lookup"><span data-stu-id="01c1a-201">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="01c1a-202">Desenvolvedores individuais podem reabilitar a origem definindo o valor dela para falso em outros arquivos `NuGet.Config` sem a necessidade de localizar a URL correta novamente.</span><span class="sxs-lookup"><span data-stu-id="01c1a-202">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="01c1a-203">Isso também é útil para fornecer aos desenvolvedores uma lista completa de URLs de origem interna para uma organização, permitindo somente a origem de uma equipe individual por padrão.</span><span class="sxs-lookup"><span data-stu-id="01c1a-203">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="01c1a-204">`defaultPushSource`: especifica o destino padrão para operações `nuget push`, substituindo o padrão interno do nuget.org. Os administradores podem implantar essa configuração para evitar publicar pacotes internos para o nuget.org público por acidente, visto que os desenvolvedores precisam usar `nuget push -Source` especificamente para publicar no nuget.org.</span><span class="sxs-lookup"><span data-stu-id="01c1a-204">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="01c1a-205">Exemplo de NuGetDefaults.Config e aplicativo</span><span class="sxs-lookup"><span data-stu-id="01c1a-205">Example NuGetDefaults.Config and application</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- defaultPushSource key works like the 'defaultPushSource' key of NuGet.Config files. -->
    <!-- This can be used by administrators to prevent accidental publishing of packages to nuget.org. -->
    <config>
        <add key="defaultPushSource" value="https://contoso.com/packages/" />
    </config>

    <!-- Default Package Sources; works like the 'packageSources' section of NuGet.Config files. -->
    <!-- This collection cannot be deleted or modified but can be disabled/enabled by users. -->
    <packageSources>
        <add key="Contoso Package Source" value="https://contoso.com/packages/" />
        <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    </packageSources>

    <!-- Default Package Sources that are disabled by default. -->
    <!-- Works like the 'disabledPackageSources' section of NuGet.Config files. -->
    <!-- Sources cannot be modified or deleted either but can be enabled/disabled by users. -->
    <disabledPackageSources>
        <add key="nuget.org" value="true" />
    </disabledPackageSources>
</configuration>
```
