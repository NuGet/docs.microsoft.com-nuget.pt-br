---
title: Configurações comuns do NuGet
description: Arquivos NuGet.Config controlam o comportamento do NuGet tanto globalmente quanto em cada projeto e são modificados com o comando nuget config.
author: JonDouglas
ms.author: jodou
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 18e3af7145495b5753b5900915ffb4b07942b856
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901467"
---
# <a name="common-nuget-configurations"></a><span data-ttu-id="21261-103">Configurações comuns do NuGet</span><span class="sxs-lookup"><span data-stu-id="21261-103">Common NuGet configurations</span></span>

<span data-ttu-id="21261-104">O comportamento do NuGet é controlado pelas configurações acumuladas em um ou mais arquivos `NuGet.Config` (XML) que podem existir no nível de projeto, usuário e computador.</span><span class="sxs-lookup"><span data-stu-id="21261-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="21261-105">Um arquivo global `NuGetDefaults.Config` também configura as origens de pacote especificamente.</span><span class="sxs-lookup"><span data-stu-id="21261-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="21261-106">As configurações se aplicam a todos os comandos emitidos na CLI, no Console do Gerenciador de Pacotes e na interface do usuário do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="21261-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="21261-107">Usos e locais do arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="21261-107">Config file locations and uses</span></span>

| <span data-ttu-id="21261-108">Escopo</span><span class="sxs-lookup"><span data-stu-id="21261-108">Scope</span></span> | <span data-ttu-id="21261-109">`NuGet.Config` local do arquivo</span><span class="sxs-lookup"><span data-stu-id="21261-109">`NuGet.Config` file location</span></span> | <span data-ttu-id="21261-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="21261-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21261-111">Solução</span><span class="sxs-lookup"><span data-stu-id="21261-111">Solution</span></span> | <span data-ttu-id="21261-112">A pasta atual (também conhecida como pasta de solução) ou qualquer pasta até a raiz da unidade.</span><span class="sxs-lookup"><span data-stu-id="21261-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="21261-113">Em uma pasta de solução, as configurações se aplicam a todos os projetos nas subpastas.</span><span class="sxs-lookup"><span data-stu-id="21261-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="21261-114">Observe que, se um arquivo de configuração for colocado em uma pasta de projeto, ele não causará nenhum efeito nesse projeto.</span><span class="sxs-lookup"><span data-stu-id="21261-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="21261-115">Usuário</span><span class="sxs-lookup"><span data-stu-id="21261-115">User</span></span> | <span data-ttu-id="21261-116">**Windows:**`%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="21261-116">**Windows:** `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="21261-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` ou `~/.nuget/NuGet/NuGet.Config` (varia de acordo com a distribuição do sistema operacional)</span><span class="sxs-lookup"><span data-stu-id="21261-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> <br/><span data-ttu-id="21261-118">Configurações adicionais têm suporte em todas as plataformas.</span><span class="sxs-lookup"><span data-stu-id="21261-118">Additional configs are supported on all platforms.</span></span> <span data-ttu-id="21261-119">Essas configurações não podem ser editadas pelas ferramentas.</span><span class="sxs-lookup"><span data-stu-id="21261-119">These configs cannot be edited by the tooling.</span></span> </br> <span data-ttu-id="21261-120">**Windows:**`%appdata%\NuGet\config\*.Config`</span><span class="sxs-lookup"><span data-stu-id="21261-120">**Windows:** `%appdata%\NuGet\config\*.Config`</span></span> <br/><span data-ttu-id="21261-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="21261-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> | <span data-ttu-id="21261-122">As configurações se aplicam a todas as operações, mas são substituídas por quaisquer configurações de nível de projeto.</span><span class="sxs-lookup"><span data-stu-id="21261-122">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="21261-123">Computador</span><span class="sxs-lookup"><span data-stu-id="21261-123">Computer</span></span> | <span data-ttu-id="21261-124">**Windows:**`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="21261-124">**Windows:** `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="21261-125">**Mac/Linux:** `$XDG_DATA_HOME` .</span><span class="sxs-lookup"><span data-stu-id="21261-125">**Mac/Linux:** `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="21261-126">Se `$XDG_DATA_HOME` for nulo ou vazio, `~/.local/share` ou `/usr/local/share` será usado (varia de acordo com a distribuição do SO)</span><span class="sxs-lookup"><span data-stu-id="21261-126">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="21261-127">As configurações se aplicam a todas as operações, mas são substituídas por qualquer usuário ou por configurações de nível de projeto.</span><span class="sxs-lookup"><span data-stu-id="21261-127">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="21261-128">Observações para versões anteriores do NuGet:</span><span class="sxs-lookup"><span data-stu-id="21261-128">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="21261-129">O NuGet 3.3 e versões anteriores usavam uma pasta `.nuget` para configurações de toda a solução.</span><span class="sxs-lookup"><span data-stu-id="21261-129">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="21261-130">Esta pasta não é usada no NuGet 3.4 +.</span><span class="sxs-lookup"><span data-stu-id="21261-130">This folder is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="21261-131">Para o NuGet 2,6 a 3. x, o arquivo de configuração no nível do computador no Windows estava localizado em `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]\NuGet.Config` , onde `{IDE}` pode ser `VisualStudio` , `{Version}` a versão do Visual Studio, como, `14.0` e `{SKU}` é `Community` , `Pro` ou `Enterprise` .</span><span class="sxs-lookup"><span data-stu-id="21261-131">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]\NuGet.Config`, where `{IDE}` can be `VisualStudio`, `{Version}` was the Visual Studio version such as `14.0`, and `{SKU}` is either `Community`, `Pro`, or `Enterprise`.</span></span> <span data-ttu-id="21261-132">Para migrar as configurações para o NuGet 4.0 +, basta copiar o arquivo de configuração para `%ProgramFiles(x86)%\NuGet\Config` .</span><span class="sxs-lookup"><span data-stu-id="21261-132">To migrate settings to NuGet 4.0+, simply copy the config file to `%ProgramFiles(x86)%\NuGet\Config`.</span></span> <span data-ttu-id="21261-133">No Linux, esse local anterior era `/etc/opt` , e no Mac, `/Library/Application Support` .</span><span class="sxs-lookup"><span data-stu-id="21261-133">On Linux, this previous location was `/etc/opt`, and on Mac, `/Library/Application Support`.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="21261-134">Alterar as definições da configuração</span><span class="sxs-lookup"><span data-stu-id="21261-134">Changing config settings</span></span>

<span data-ttu-id="21261-135">Um arquivo `NuGet.Config` é um arquivo de texto XML simples que contém pares chave-valor, conforme descrito no tópico [Definições de configuração do NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="21261-135">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="21261-136">As configurações são gerenciadas usando o [comando config](../reference/cli-reference/cli-ref-config.md) da CLI do NuGet:</span><span class="sxs-lookup"><span data-stu-id="21261-136">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="21261-137">Por padrão, as alterações são feitas no arquivo de configuração de nível de usuário.</span><span class="sxs-lookup"><span data-stu-id="21261-137">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="21261-138">Para alterar as configurações em um arquivo diferente, use a opção `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="21261-138">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="21261-139">Nesse caso, os arquivos podem usar qualquer nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="21261-139">In this case files can use any filename.</span></span>
- <span data-ttu-id="21261-140">As chaves sempre diferenciam maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="21261-140">Keys are always case sensitive.</span></span>
- <span data-ttu-id="21261-141">A elevação é necessária para alterar as configurações no arquivo de configurações no nível do computador.</span><span class="sxs-lookup"><span data-stu-id="21261-141">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="21261-142">Embora você possa modificar o arquivo em qualquer editor de texto, o NuGet (v3.4.3 e posterior) ignorará silenciosamente todo o arquivo de configuração se ele contiver XML malformado (marcas não correspondidas, aspas inválidas, etc.).</span><span class="sxs-lookup"><span data-stu-id="21261-142">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="21261-143">É por isso que é preferível gerenciar a configuração usando `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="21261-143">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="21261-144">Definindo um valor</span><span class="sxs-lookup"><span data-stu-id="21261-144">Setting a value</span></span>

<span data-ttu-id="21261-145">Windows:</span><span class="sxs-lookup"><span data-stu-id="21261-145">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="21261-146">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="21261-146">Mac/Linux:</span></span>

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
> <span data-ttu-id="21261-147">No NuGet 3.4 e posterior, você pode usar as variáveis de ambiente em qualquer valor, como no `repositoryPath=%PACKAGEHOME%` (Windows) e `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="21261-147">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="21261-148">Removendo um valor</span><span class="sxs-lookup"><span data-stu-id="21261-148">Removing a value</span></span>

<span data-ttu-id="21261-149">Para remover um valor, especifique uma chave com um valor vazio.</span><span class="sxs-lookup"><span data-stu-id="21261-149">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="21261-150">Criar um novo arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="21261-150">Creating a new config file</span></span>

<span data-ttu-id="21261-151">Copie o modelo abaixo para o novo arquivo e, em seguida, use `nuget config -configFile <filename>` para definir os valores:</span><span class="sxs-lookup"><span data-stu-id="21261-151">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="21261-152">Como as configurações são aplicadas</span><span class="sxs-lookup"><span data-stu-id="21261-152">How settings are applied</span></span>

<span data-ttu-id="21261-153">Vários arquivos `NuGet.Config` permitem que você armazene as configurações em locais diferentes, para que elas se apliquem a um único projeto, um grupo de projetos ou todos os projetos.</span><span class="sxs-lookup"><span data-stu-id="21261-153">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="21261-154">Coletivamente, essas configurações se aplicam a qualquer operação do NuGet invocada na linha de comando ou do Visual Studio, com as configurações existentes “mais próximas” para um projeto ou a pasta atual tendo precedência.</span><span class="sxs-lookup"><span data-stu-id="21261-154">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="21261-155">Especificamente, o NuGet carrega as configurações dos arquivos de configuração diferente na seguinte ordem:</span><span class="sxs-lookup"><span data-stu-id="21261-155">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="21261-156">O [ `NuGetDefaults.Config` arquivo](#nuget-defaults-file), que contém configurações relacionadas apenas às origens do pacote.</span><span class="sxs-lookup"><span data-stu-id="21261-156">The [`NuGetDefaults.Config` file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="21261-157">O arquivo de nível de computador.</span><span class="sxs-lookup"><span data-stu-id="21261-157">The computer-level file.</span></span>
1. <span data-ttu-id="21261-158">O arquivo de nível de usuário.</span><span class="sxs-lookup"><span data-stu-id="21261-158">The user-level file.</span></span>
1. <span data-ttu-id="21261-159">O arquivo especificado com `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="21261-159">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="21261-160">Arquivos encontrados em todas as pastas no caminho da raiz da unidade para a pasta atual (onde `nuget.exe` é invocado ou a pasta que contém o projeto do Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="21261-160">Files found in every folder in the path from the drive root to the current folder (where `nuget.exe` is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="21261-161">Por exemplo, se um comando for invocado no `c:\A\B\C` , o NuGet procurará e carregará os arquivos de configuração em `c:\` , depois, `c:\A` `c:\A\B` e finalmente `c:\A\B\C` .</span><span class="sxs-lookup"><span data-stu-id="21261-161">For example, if a command is invoked in `c:\A\B\C`, NuGet looks for and loads config files in `c:\`, then `c:\A`, then `c:\A\B`, and finally `c:\A\B\C`.</span></span>

<span data-ttu-id="21261-162">À medida que o NuGet encontra configurações nesses arquivos, eles são aplicados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="21261-162">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="21261-163">Para elementos de item único, o NuGet substituiu qualquer valor encontrado anteriormente pela mesma chave.</span><span class="sxs-lookup"><span data-stu-id="21261-163">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="21261-164">Isso significa que as configurações que são “mais próximas” da pasta ou projeto atual substituem quaisquer outras encontradas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="21261-164">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="21261-165">Por exemplo, a definição `defaultPushSource` em `NuGetDefaults.Config` será substituída se ela existir em qualquer outro arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="21261-165">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>
1. <span data-ttu-id="21261-166">Para elementos de coleta (como `<packageSources>`), o NuGet combina os valores de todos os arquivos de configuração em uma única coleção.</span><span class="sxs-lookup"><span data-stu-id="21261-166">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>
1. <span data-ttu-id="21261-167">Quando `<clear />` está presente para um nó específico, o NuGet ignora os valores de configuração definidos anteriormente para esse nó.</span><span class="sxs-lookup"><span data-stu-id="21261-167">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="21261-168">Explicação passo a passo das configurações</span><span class="sxs-lookup"><span data-stu-id="21261-168">Settings walkthrough</span></span>

<span data-ttu-id="21261-169">Digamos que você tem a seguinte estrutura de pasta em duas unidades separadas:</span><span class="sxs-lookup"><span data-stu-id="21261-169">Let's say you have the following folder structure on two separate drives:</span></span>

```
disk_drive_1
    User
disk_drive_2
    Project1
        Source
    Project2
        Source
    tmp
```

<span data-ttu-id="21261-170">Dessa forma, você terá quatro arquivos `NuGet.Config` nos seguintes locais com o conteúdo em questão.</span><span class="sxs-lookup"><span data-stu-id="21261-170">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="21261-171">(O arquivo no nível de computador não está incluído neste exemplo, mas se comportaria da mesma forma que o arquivo de nível de usuário.)</span><span class="sxs-lookup"><span data-stu-id="21261-171">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="21261-172">Arquivo A. Arquivo de nível de usuário, (`%appdata%\NuGet\NuGet.Config` no Windows e `~/.config/NuGet/NuGet.Config` no Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="21261-172">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="21261-173">Arquivo B. `disk_drive_2/NuGet.Config` :</span><span class="sxs-lookup"><span data-stu-id="21261-173">File B. `disk_drive_2/NuGet.Config`:</span></span>

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

<span data-ttu-id="21261-174">Arquivo C. `disk_drive_2/Project1/NuGet.Config` :</span><span class="sxs-lookup"><span data-stu-id="21261-174">File C. `disk_drive_2/Project1/NuGet.Config`:</span></span>

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

<span data-ttu-id="21261-175">Arquivo D. `disk_drive_2/Project2/NuGet.Config` :</span><span class="sxs-lookup"><span data-stu-id="21261-175">File D. `disk_drive_2/Project2/NuGet.Config`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="21261-176">O NuGet, em seguida, carrega e aplica as configurações como mostrado a seguir, dependendo de onde ele é chamado:</span><span class="sxs-lookup"><span data-stu-id="21261-176">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="21261-177">**Chamado de `disk_drive_1/users`**: somente o repositório padrão listado no arquivo de configuração de nível de usuário (A) é usado, pois esse é o único arquivo encontrado em `disk_drive_1` .</span><span class="sxs-lookup"><span data-stu-id="21261-177">**Invoked from `disk_drive_1/users`**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on `disk_drive_1`.</span></span>

- <span data-ttu-id="21261-178">**Invocado `disk_drive_2/` de `disk_drive_/tmp` ou**: o arquivo de nível de usuário (a) é carregado primeiro, então o NuGet vai para a raiz de `disk_drive_2` e localiza o arquivo (B).</span><span class="sxs-lookup"><span data-stu-id="21261-178">**Invoked from `disk_drive_2/` or `disk_drive_/tmp`**: The user-level file (A) is loaded first, then NuGet goes to the root of `disk_drive_2` and finds file (B).</span></span> <span data-ttu-id="21261-179">O NuGet também procura um arquivo de configuração no `/tmp` , mas não localiza um.</span><span class="sxs-lookup"><span data-stu-id="21261-179">NuGet also looks for a configuration file in `/tmp` but does not find one.</span></span> <span data-ttu-id="21261-180">Como resultado, o repositório padrão no `nuget.org` é usado, a restauração de pacote é habilitada e os pacotes são expandidos no `disk_drive_2/tmp` .</span><span class="sxs-lookup"><span data-stu-id="21261-180">As a result, the default repository on `nuget.org` is used, package restore is enabled, and packages get expanded in `disk_drive_2/tmp`.</span></span>

- <span data-ttu-id="21261-181">**Invocado `disk_drive_2/Project1` de `disk_drive_2/Project1/Source` ou**: o arquivo de nível de usuário (a) é carregado primeiro, em seguida, o NuGet carrega o arquivo (B) da raiz de `disk_drive_2` , seguido por arquivo (C).</span><span class="sxs-lookup"><span data-stu-id="21261-181">**Invoked from `disk_drive_2/Project1` or `disk_drive_2/Project1/Source`**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of `disk_drive_2`, followed by file (C).</span></span> <span data-ttu-id="21261-182">As configurações em (C) substituem aquelas em (B) e (A), de modo que os `repositoryPath` pacotes de onde são instalados são, `disk_drive_2/Project1/External/Packages` em vez de `disk_drive_2/tmp` .</span><span class="sxs-lookup"><span data-stu-id="21261-182">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is `disk_drive_2/Project1/External/Packages` instead of `disk_drive_2/tmp`.</span></span> <span data-ttu-id="21261-183">Além disso, como (C) limpa o `<packageSources>`, o nuget.org não está mais disponível como uma origem, restando apenas `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="21261-183">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="21261-184">**Invocado `disk_drive_2/Project2` de `disk_drive_2/Project2/Source` ou**: o arquivo de nível de usuário (a) é carregado primeiro seguido pelo arquivo (B) e arquivo (D).</span><span class="sxs-lookup"><span data-stu-id="21261-184">**Invoked from `disk_drive_2/Project2` or `disk_drive_2/Project2/Source`**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="21261-185">Como `packageSources` não foi apagado, ambos `nuget.org` e `https://MyPrivateRepo/DQ/nuget` estão disponíveis como origens.</span><span class="sxs-lookup"><span data-stu-id="21261-185">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="21261-186">Os pacotes são expandidos no `disk_drive_2/tmp` conforme especificado em (B).</span><span class="sxs-lookup"><span data-stu-id="21261-186">Packages get expanded in `disk_drive_2/tmp` as specified in (B).</span></span>

## <a name="additional-user-wide-configuration"></a><span data-ttu-id="21261-187">Configuração de todo o usuário adicional</span><span class="sxs-lookup"><span data-stu-id="21261-187">Additional user wide configuration</span></span>

<span data-ttu-id="21261-188">A partir do 5,7, o NuGet adicionou suporte para arquivos adicionais de configuração de todo o usuário.</span><span class="sxs-lookup"><span data-stu-id="21261-188">Starting with 5.7, NuGet has added support for additional user wide configuration files.</span></span> <span data-ttu-id="21261-189">Isso permite que fornecedores de terceiros adicionem arquivos de configuração de usuário adicionais sem elevação.</span><span class="sxs-lookup"><span data-stu-id="21261-189">This allows third-party vendors to add additional user configuration files without elevation.</span></span>
<span data-ttu-id="21261-190">Esses arquivos de configuração são encontrados na pasta de configuração de usuário padrão em uma `config` subpasta.</span><span class="sxs-lookup"><span data-stu-id="21261-190">These configuration files are found in the standard user wide configuration folder within a `config` subfolder.</span></span>
<span data-ttu-id="21261-191">Todos os arquivos que terminam com `.config` ou `.Config` serão considerados.</span><span class="sxs-lookup"><span data-stu-id="21261-191">All files ending with `.config` or `.Config` will be considered.</span></span>
<span data-ttu-id="21261-192">Esses arquivos não podem ser editados pelas ferramentas padrão.</span><span class="sxs-lookup"><span data-stu-id="21261-192">These files cannot be edited by the standard tooling.</span></span>

| <span data-ttu-id="21261-193">Plataforma do SO</span><span class="sxs-lookup"><span data-stu-id="21261-193">OS Platform</span></span>  | <span data-ttu-id="21261-194">Configurações adicionais</span><span class="sxs-lookup"><span data-stu-id="21261-194">Additional Configurations</span></span> |
| --- | --- |
| <span data-ttu-id="21261-195">Windows</span><span class="sxs-lookup"><span data-stu-id="21261-195">Windows</span></span>      | `%appdata%\NuGet\config\*.Config` |
| <span data-ttu-id="21261-196">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="21261-196">Mac/Linux</span></span>    | <span data-ttu-id="21261-197">`~/.config/NuGet/config/*.config` ou `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="21261-197">`~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> |

## <a name="nuget-defaults-file"></a><span data-ttu-id="21261-198">Arquivo de padrões do NuGet</span><span class="sxs-lookup"><span data-stu-id="21261-198">NuGet defaults file</span></span>

<span data-ttu-id="21261-199">O arquivo `NuGetDefaults.Config` existe para especificar origens de pacote do qual os pacotes são instalados e atualizados, e para controlar o destino padrão para publicar pacotes com `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="21261-199">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="21261-200">Como os administradores podem implantar com conveniência (usando a Política de Grupo, por exemplo) arquivos `NuGetDefaults.Config` consistentes em computadores de desenvolvedor e de build, eles podem garantir que todos na organização estejam usando as origens de pacotes corretas, em vez do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="21261-200">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="21261-201">O arquivo `NuGetDefaults.Config` nunca faz com que a origem do pacote seja removida da configuração do NuGet do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="21261-201">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="21261-202">Isso significa que, se o desenvolvedor já tiver usado o NuGet e, portanto, a origem do pacote no nuget.org está registrada, ele não será removido após a criação de um arquivo `NuGetDefaults.Config`.</span><span class="sxs-lookup"><span data-stu-id="21261-202">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="21261-203">Além disso, nem `NuGetDefaults.Config` qualquer outro mecanismo no NuGet pode impedir o acesso a fontes de pacote como NuGet.org. Se uma organização quiser bloquear tal acesso, ela deverá usar outros meios, como firewalls para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="21261-203">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="21261-204">`NuGetDefaults.Config` local</span><span class="sxs-lookup"><span data-stu-id="21261-204">`NuGetDefaults.Config` location</span></span>

<span data-ttu-id="21261-205">A tabela a seguir descreve onde o arquivo `NuGetDefaults.Config` deve ser armazenado, dependendo do sistema operacional de destino:</span><span class="sxs-lookup"><span data-stu-id="21261-205">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="21261-206">Plataforma do SO</span><span class="sxs-lookup"><span data-stu-id="21261-206">OS Platform</span></span>  | <span data-ttu-id="21261-207">`NuGetDefaults.Config` Local</span><span class="sxs-lookup"><span data-stu-id="21261-207">`NuGetDefaults.Config` Location</span></span> |
| --- | --- |
| <span data-ttu-id="21261-208">Windows</span><span class="sxs-lookup"><span data-stu-id="21261-208">Windows</span></span>      | <span data-ttu-id="21261-209">**Visual Studio 2017 ou NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="21261-209">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="21261-210">**Visual Studio 2015 e anteriores ou NuGet 3.x e anteriores:** `%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="21261-210">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="21261-211">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="21261-211">Mac/Linux</span></span>    | <span data-ttu-id="21261-212">`$XDG_DATA_HOME` (normalmente `~/.local/share` ou `/usr/local/share`, dependendo da distribuição do SO)</span><span class="sxs-lookup"><span data-stu-id="21261-212">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="21261-213">Configurações do NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="21261-213">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="21261-214">`packageSources`: esta coleção tem o mesmo significado que `packageSources` em arquivos de configuração regulares e especifica as origens padrão.</span><span class="sxs-lookup"><span data-stu-id="21261-214">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="21261-215">O NuGet usa as origens em ordem ao instalar ou atualizar pacotes em projetos usando o formato de gerenciamento `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="21261-215">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="21261-216">Para projetos usando o formato PackageReference, o NuGet usa origens locais primeiro e, em seguida, origens em compartilhamentos de rede e origens em HTTP, independentemente da ordem dos arquivos de configuração.</span><span class="sxs-lookup"><span data-stu-id="21261-216">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="21261-217">O NuGet sempre ignora a ordem de origens com operações de restauração.</span><span class="sxs-lookup"><span data-stu-id="21261-217">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="21261-218">`disabledPackageSources`: essa coleção também tem o mesmo significado que nos `NuGet.Config` arquivos, onde cada fonte afetada é listada por seu nome e um `true` / `false` valor que indica se ele está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="21261-218">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a `true`/`false` value indicating whether it's disabled.</span></span> <span data-ttu-id="21261-219">Isso permite que o nome de origem e a URL permaneçam em `packageSources` sem que ele seja ativado por padrão.</span><span class="sxs-lookup"><span data-stu-id="21261-219">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="21261-220">Os desenvolvedores individuais podem reabilitar a origem definindo o valor da origem como `false` em outros `NuGet.Config` arquivos sem precisar encontrar a URL correta novamente.</span><span class="sxs-lookup"><span data-stu-id="21261-220">Individual developers can then re-enable the source by setting the source's value to `false` in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="21261-221">Isso também é útil para fornecer aos desenvolvedores uma lista completa de URLs de origem interna para uma organização, permitindo somente a origem de uma equipe individual por padrão.</span><span class="sxs-lookup"><span data-stu-id="21261-221">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="21261-222">`defaultPushSource`: especifica o destino padrão para `nuget push` operações, substituindo o padrão interno de `nuget.org` .</span><span class="sxs-lookup"><span data-stu-id="21261-222">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of `nuget.org`.</span></span> <span data-ttu-id="21261-223">Os administradores podem implantar essa configuração para evitar a publicação de pacotes internos para o público `nuget.org` por acidente, pois os desenvolvedores precisam usar especificamente `nuget push -Source` para publicar no `nuget.org` .</span><span class="sxs-lookup"><span data-stu-id="21261-223">Administrators can deploy this setting to avoid publishing internal packages to the public `nuget.org` by accident, as developers specifically need to use `nuget push -Source` to publish to `nuget.org`.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="21261-224">Exemplo de NuGetDefaults.Config e aplicativo</span><span class="sxs-lookup"><span data-stu-id="21261-224">Example NuGetDefaults.Config and application</span></span>

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
