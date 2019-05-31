---
title: Configurando o comportamento do NuGet
description: Arquivos NuGet.Config controlam o comportamento do NuGet tanto globalmente quanto em cada projeto e são modificados com o comando nuget config.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 963d1d59ea7e65e3d75bc7105b8864e3e4045938
ms.sourcegitcommit: ef08f376688f0191a8d3d873b6a4386afd799373
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266347"
---
# <a name="configuring-nuget-behavior"></a><span data-ttu-id="da425-103">Configurando o comportamento de NuGet</span><span class="sxs-lookup"><span data-stu-id="da425-103">Configuring NuGet behavior</span></span>

<span data-ttu-id="da425-104">O comportamento do NuGet é controlado pelas configurações acumuladas em um ou mais arquivos `NuGet.Config` (XML) que podem existir no nível de projeto, usuário e computador.</span><span class="sxs-lookup"><span data-stu-id="da425-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="da425-105">Um arquivo global `NuGetDefaults.Config` também configura as origens de pacote especificamente.</span><span class="sxs-lookup"><span data-stu-id="da425-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="da425-106">As configurações se aplicam a todos os comandos emitidos na CLI, no Console do Gerenciador de Pacotes e na interface do usuário do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="da425-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="da425-107">Usos e locais do arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="da425-107">Config file locations and uses</span></span>

| <span data-ttu-id="da425-108">Escopo</span><span class="sxs-lookup"><span data-stu-id="da425-108">Scope</span></span> | <span data-ttu-id="da425-109">Local do arquivo NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="da425-109">NuGet.Config file location</span></span> | <span data-ttu-id="da425-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="da425-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="da425-111">Solução</span><span class="sxs-lookup"><span data-stu-id="da425-111">Solution</span></span> | <span data-ttu-id="da425-112">A pasta atual (também conhecida como pasta de solução) ou qualquer pasta até a raiz da unidade.</span><span class="sxs-lookup"><span data-stu-id="da425-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="da425-113">Em uma pasta de solução, as configurações se aplicam a todos os projetos nas subpastas.</span><span class="sxs-lookup"><span data-stu-id="da425-113">In a solution folder, settings apply apply to all projects in subfolders.</span></span> <span data-ttu-id="da425-114">Observe que, se um arquivo de configuração for colocado em uma pasta de projeto, ele não causará nenhum efeito nesse projeto.</span><span class="sxs-lookup"><span data-stu-id="da425-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="da425-115">User</span><span class="sxs-lookup"><span data-stu-id="da425-115">User</span></span> | <span data-ttu-id="da425-116">Windows: `%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="da425-116">Windows: `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="da425-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` ou `~/.nuget/NuGet/NuGet.Config` (varia de acordo com a distribuição do SO)</span><span class="sxs-lookup"><span data-stu-id="da425-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> | <span data-ttu-id="da425-118">As configurações se aplicam a todas as operações, mas são substituídas por quaisquer configurações de nível de projeto.</span><span class="sxs-lookup"><span data-stu-id="da425-118">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="da425-119">Computador</span><span class="sxs-lookup"><span data-stu-id="da425-119">Computer</span></span> | <span data-ttu-id="da425-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="da425-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="da425-121">Mac/Linux: `$XDG_DATA_HOME`.</span><span class="sxs-lookup"><span data-stu-id="da425-121">Mac/Linux: `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="da425-122">Se `$XDG_DATA_HOME` for nulo ou vazio, `~/.local/share` ou `/usr/local/share` será usado (varia de acordo com a distribuição do SO)</span><span class="sxs-lookup"><span data-stu-id="da425-122">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="da425-123">As configurações se aplicam a todas as operações, mas são substituídas por qualquer usuário ou por configurações de nível de projeto.</span><span class="sxs-lookup"><span data-stu-id="da425-123">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="da425-124">Observações para versões anteriores do NuGet:</span><span class="sxs-lookup"><span data-stu-id="da425-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="da425-125">O NuGet 3.3 e versões anteriores usavam uma pasta `.nuget` para configurações de toda a solução.</span><span class="sxs-lookup"><span data-stu-id="da425-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="da425-126">Este arquivo não é usado no NuGet 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="da425-126">This file is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="da425-127">Para o NuGet 2.6 a 3.x, o arquivo de configuração de nível de computador no Windows encontra-se em %ProgramData%\NuGet\Config [\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, em que *{IDE}* pode ser *VisualStudio*, *{Version}* é a versão do Visual Studio como *14.0* e *{SKU}* é *Community*, *Pro* ou *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="da425-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="da425-128">Para migrar as configurações para o NuGet 4.0 ou superior, simplesmente copie o arquivo de configuração para %ProgramFiles(x86)%\NuGet\Config. No Linux, esse local anterior era /etc/opt e no Mac era /Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="da425-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="da425-129">Alterar as definições da configuração</span><span class="sxs-lookup"><span data-stu-id="da425-129">Changing config settings</span></span>

<span data-ttu-id="da425-130">Um arquivo `NuGet.Config` é um arquivo de texto XML simples que contém pares chave-valor, conforme descrito no tópico [Definições de configuração do NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="da425-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="da425-131">As configurações são gerenciadas usando o [comando config](../tools/cli-ref-config.md) da CLI do NuGet:</span><span class="sxs-lookup"><span data-stu-id="da425-131">Settings are managed using the NuGet CLI [config command](../tools/cli-ref-config.md):</span></span>
- <span data-ttu-id="da425-132">Por padrão, as alterações são feitas no arquivo de configuração de nível de usuário.</span><span class="sxs-lookup"><span data-stu-id="da425-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="da425-133">Para alterar as configurações em um arquivo diferente, use a opção `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="da425-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="da425-134">Nesse caso, os arquivos podem usar qualquer nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="da425-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="da425-135">As chaves sempre diferenciam maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="da425-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="da425-136">A elevação é necessária para alterar as configurações no arquivo de configurações no nível do computador.</span><span class="sxs-lookup"><span data-stu-id="da425-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="da425-137">Embora você possa modificar o arquivo em qualquer editor de texto, o NuGet (v3.4.3 e posterior) ignorará silenciosamente todo o arquivo de configuração se ele contiver XML malformado (marcas não correspondidas, aspas inválidas, etc.).</span><span class="sxs-lookup"><span data-stu-id="da425-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="da425-138">É por isso que é preferível gerenciar a configuração usando `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="da425-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="da425-139">Definindo um valor</span><span class="sxs-lookup"><span data-stu-id="da425-139">Setting a value</span></span>

<span data-ttu-id="da425-140">Windows:</span><span class="sxs-lookup"><span data-stu-id="da425-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="da425-141">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="da425-141">Mac/Linux:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> <span data-ttu-id="da425-142">No NuGet 3.4 e posterior, você pode usar as variáveis de ambiente em qualquer valor, como no `repositoryPath=%PACKAGEHOME%` (Windows) e `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="da425-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="da425-143">Removendo um valor</span><span class="sxs-lookup"><span data-stu-id="da425-143">Removing a value</span></span>

<span data-ttu-id="da425-144">Para remover um valor, especifique uma chave com um valor vazio.</span><span class="sxs-lookup"><span data-stu-id="da425-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="da425-145">Criar um novo arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="da425-145">Creating a new config file</span></span>

<span data-ttu-id="da425-146">Copie o modelo abaixo para o novo arquivo e, em seguida, use `nuget config -configFile <filename>` para definir os valores:</span><span class="sxs-lookup"><span data-stu-id="da425-146">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="da425-147">Como as configurações são aplicadas</span><span class="sxs-lookup"><span data-stu-id="da425-147">How settings are applied</span></span>

<span data-ttu-id="da425-148">Vários arquivos `NuGet.Config` permitem que você armazene as configurações em locais diferentes, para que elas se apliquem a um único projeto, um grupo de projetos ou todos os projetos.</span><span class="sxs-lookup"><span data-stu-id="da425-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="da425-149">Coletivamente, essas configurações se aplicam a qualquer operação do NuGet invocada na linha de comando ou do Visual Studio, com as configurações existentes “mais próximas” para um projeto ou a pasta atual tendo precedência.</span><span class="sxs-lookup"><span data-stu-id="da425-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="da425-150">Especificamente, o NuGet carrega as configurações dos arquivos de configuração diferente na seguinte ordem:</span><span class="sxs-lookup"><span data-stu-id="da425-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="da425-151">O [arquivo NuGetDefaults.Config](#nuget-defaults-file), que contém as configurações relacionadas somente às origens de pacotes.</span><span class="sxs-lookup"><span data-stu-id="da425-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="da425-152">O arquivo de nível de computador.</span><span class="sxs-lookup"><span data-stu-id="da425-152">The computer-level file.</span></span>
1. <span data-ttu-id="da425-153">O arquivo de nível de usuário.</span><span class="sxs-lookup"><span data-stu-id="da425-153">The user-level file.</span></span>
1. <span data-ttu-id="da425-154">O arquivo especificado com `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="da425-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="da425-155">Arquivos encontrados em todas as pastas no caminho da raiz de unidade para a pasta atual (em que nuget.exe é invocado ou a pasta que contém o projeto do Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="da425-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="da425-156">Por exemplo, se um comando for invocado em c:\A\B\C, o NuGet procura e carrega os arquivos de configuração em c:\,, c:\A, c:\A\B e, finalmente, c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="da425-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="da425-157">À medida que o NuGet encontra configurações nesses arquivos, eles são aplicados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="da425-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="da425-158">Para elementos de item único, o NuGet substituiu qualquer valor encontrado anteriormente pela mesma chave.</span><span class="sxs-lookup"><span data-stu-id="da425-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="da425-159">Isso significa que as configurações que são “mais próximas” da pasta ou projeto atual substituem quaisquer outras encontradas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="da425-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="da425-160">Por exemplo, a definição `defaultPushSource` em `NuGetDefaults.Config` será substituída se ela existir em qualquer outro arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="da425-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="da425-161">Para elementos de coleta (como `<packageSources>`), o NuGet combina os valores de todos os arquivos de configuração em uma única coleção.</span><span class="sxs-lookup"><span data-stu-id="da425-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="da425-162">Quando `<clear />` está presente para um nó específico, o NuGet ignora os valores de configuração definidos anteriormente para esse nó.</span><span class="sxs-lookup"><span data-stu-id="da425-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="da425-163">Explicação passo a passo das configurações</span><span class="sxs-lookup"><span data-stu-id="da425-163">Settings walkthrough</span></span>

<span data-ttu-id="da425-164">Digamos que você tem a seguinte estrutura de pasta em duas unidades separadas:</span><span class="sxs-lookup"><span data-stu-id="da425-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="da425-165">Dessa forma, você terá quatro arquivos `NuGet.Config` nos seguintes locais com o conteúdo em questão.</span><span class="sxs-lookup"><span data-stu-id="da425-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="da425-166">(O arquivo no nível de computador não está incluído neste exemplo, mas se comportaria da mesma forma que o arquivo de nível de usuário.)</span><span class="sxs-lookup"><span data-stu-id="da425-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="da425-167">Arquivo A. Arquivo de nível de usuário, (`%appdata%\NuGet\NuGet.Config` no Windows e `~/.config/NuGet/NuGet.Config` no Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="da425-167">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="da425-168">Arquivo B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="da425-168">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="da425-169">Arquivo C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="da425-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="da425-170">Arquivo D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="da425-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="da425-171">O NuGet, em seguida, carrega e aplica as configurações como mostrado a seguir, dependendo de onde ele é chamado:</span><span class="sxs-lookup"><span data-stu-id="da425-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="da425-172">**Invocado de disk_drive_1/users**: somente o repositório padrão listado no arquivo de configuração de nível do usuário (A) é usado, pois esse é o único arquivo encontrado em disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="da425-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="da425-173">**Invocado de disk_drive_2/ ou disk_drive_ /tmp**: o arquivo no nível do usuário (A) é carregado primeiro, depois o NuGet acessa a raiz de disk_drive_2 e descobre o arquivo (B).</span><span class="sxs-lookup"><span data-stu-id="da425-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="da425-174">O NuGet também procura um arquivo de configuração em /tmp, mas não o encontra.</span><span class="sxs-lookup"><span data-stu-id="da425-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="da425-175">Como resultado, o repositório padrão no nuget.org é usado, a restauração de pacote é habilitada e os pacotes são expandidos em disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="da425-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="da425-176">**Invocado de disk_drive_2/Project1 ou disk_drive_2/Project1/Source**: o arquivo de nível do usuário (A) é carregado primeiro, depois o NuGet carrega o arquivo (B) da raiz de disk_drive_2, seguido pelo arquivo (C).</span><span class="sxs-lookup"><span data-stu-id="da425-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="da425-177">As configurações em (C) substituirão as de (B) e (A), portanto, o `repositoryPath` em que os pacotes são instalados são disk_drive_2/Project1/External/Packages em vez de *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="da425-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="da425-178">Além disso, como (C) limpa o `<packageSources>`, o nuget.org não está mais disponível como uma origem, restando apenas `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="da425-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="da425-179">**Invocado de disk_drive_2/Project2 ou disk_drive_2/Project2/Source**: O arquivo de nível de usuário (A) é carregado primeiro, seguido pelos arquivo (B) e (D).</span><span class="sxs-lookup"><span data-stu-id="da425-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="da425-180">Como `packageSources` não foi apagado, ambos `nuget.org` e `https://MyPrivateRepo/DQ/nuget` estão disponíveis como origens.</span><span class="sxs-lookup"><span data-stu-id="da425-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="da425-181">Pacotes são expandidos em disk_drive_2/tmp conforme especificado em (B).</span><span class="sxs-lookup"><span data-stu-id="da425-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="da425-182">Arquivo de padrões do NuGet</span><span class="sxs-lookup"><span data-stu-id="da425-182">NuGet defaults file</span></span>

<span data-ttu-id="da425-183">O arquivo `NuGetDefaults.Config` existe para especificar origens de pacote do qual os pacotes são instalados e atualizados, e para controlar o destino padrão para publicar pacotes com `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="da425-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="da425-184">Como os administradores podem implantar com conveniência (usando a Política de Grupo, por exemplo) arquivos `NuGetDefaults.Config` consistentes em computadores de desenvolvedor e de build, eles podem garantir que todos na organização estejam usando as origens de pacotes corretas, em vez do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="da425-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="da425-185">O arquivo `NuGetDefaults.Config` nunca faz com que a origem do pacote seja removida da configuração do NuGet do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="da425-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="da425-186">Isso significa que, se o desenvolvedor já tiver usado o NuGet e, portanto, a origem do pacote no nuget.org está registrada, ele não será removido após a criação de um arquivo `NuGetDefaults.Config`.</span><span class="sxs-lookup"><span data-stu-id="da425-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="da425-187">Além disso, nem o `NuGetDefaults.Config` nem nenhum outro mecanismo no NuGet pode impedir o acesso às origens de pacote como nuget.org. Se uma organização desejar bloquear esse acesso, ela usará outros meios, como firewalls, para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="da425-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="da425-188">Local do NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="da425-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="da425-189">A tabela a seguir descreve onde o arquivo `NuGetDefaults.Config` deve ser armazenado, dependendo do sistema operacional de destino:</span><span class="sxs-lookup"><span data-stu-id="da425-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="da425-190">Plataforma do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="da425-190">OS Platform</span></span>  | <span data-ttu-id="da425-191">Local de NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="da425-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="da425-192">Windows</span><span class="sxs-lookup"><span data-stu-id="da425-192">Windows</span></span>      | <span data-ttu-id="da425-193">**Visual Studio 2017 ou NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="da425-193">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="da425-194">**Visual Studio 2015 e anteriores ou NuGet 3.x e anteriores:** `%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="da425-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="da425-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="da425-195">Mac/Linux</span></span>    | <span data-ttu-id="da425-196">`$XDG_DATA_HOME` (normalmente `~/.local/share` ou `/usr/local/share`, dependendo da distribuição do SO)</span><span class="sxs-lookup"><span data-stu-id="da425-196">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="da425-197">Configurações do NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="da425-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="da425-198">`packageSources`: esta coleção tem o mesmo significado que `packageSources` em arquivos de configuração regulares e especifica as origens padrão.</span><span class="sxs-lookup"><span data-stu-id="da425-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="da425-199">O NuGet usa as origens em ordem ao instalar ou atualizar pacotes em projetos usando o formato de gerenciamento `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="da425-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="da425-200">Para projetos usando o formato PackageReference, o NuGet usa origens locais primeiro e, em seguida, origens em compartilhamentos de rede e origens em HTTP, independentemente da ordem dos arquivos de configuração.</span><span class="sxs-lookup"><span data-stu-id="da425-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="da425-201">O NuGet sempre ignora a ordem de origens com operações de restauração.</span><span class="sxs-lookup"><span data-stu-id="da425-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="da425-202">`disabledPackageSources`: esta coleção também tem o mesmo significado que arquivos `NuGet.Config`, em que cada origem afetada é listada por seu nome e um valor true/false que indica se ela está desabilitada.</span><span class="sxs-lookup"><span data-stu-id="da425-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="da425-203">Isso permite que o nome de origem e a URL permaneçam em `packageSources` sem que ele seja ativado por padrão.</span><span class="sxs-lookup"><span data-stu-id="da425-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="da425-204">Desenvolvedores individuais podem reabilitar a origem definindo o valor dela para falso em outros arquivos `NuGet.Config` sem a necessidade de localizar a URL correta novamente.</span><span class="sxs-lookup"><span data-stu-id="da425-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="da425-205">Isso também é útil para fornecer aos desenvolvedores uma lista completa de URLs de origem interna para uma organização, permitindo somente a origem de uma equipe individual por padrão.</span><span class="sxs-lookup"><span data-stu-id="da425-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="da425-206">`defaultPushSource`: especifica o destino padrão para operações `nuget push`, substituindo o padrão interno do nuget.org. Os administradores podem implantar essa configuração para evitar publicar pacotes internos para o nuget.org público por acidente, visto que os desenvolvedores precisam usar `nuget push -Source` especificamente para publicar no nuget.org.</span><span class="sxs-lookup"><span data-stu-id="da425-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="da425-207">Exemplo de NuGetDefaults.Config e aplicativo</span><span class="sxs-lookup"><span data-stu-id="da425-207">Example NuGetDefaults.Config and application</span></span>

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
