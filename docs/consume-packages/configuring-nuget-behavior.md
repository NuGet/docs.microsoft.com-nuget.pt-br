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
# <a name="common-nuget-configurations"></a>Configurações comuns do NuGet

O comportamento do NuGet é controlado pelas configurações acumuladas em um ou mais arquivos `NuGet.Config` (XML) que podem existir no nível de projeto, usuário e computador. Um arquivo global `NuGetDefaults.Config` também configura as origens de pacote especificamente. As configurações se aplicam a todos os comandos emitidos na CLI, no Console do Gerenciador de Pacotes e na interface do usuário do Gerenciador de Pacotes.

## <a name="config-file-locations-and-uses"></a>Usos e locais do arquivo de configuração

| Escopo | `NuGet.Config` local do arquivo | Descrição |
| --- | --- | --- |
| Solução | A pasta atual (também conhecida como pasta de solução) ou qualquer pasta até a raiz da unidade.| Em uma pasta de solução, as configurações se aplicam a todos os projetos nas subpastas. Observe que, se um arquivo de configuração for colocado em uma pasta de projeto, ele não causará nenhum efeito nesse projeto. |
| Usuário | **Windows:**`%appdata%\NuGet\NuGet.Config`<br/>**Mac/Linux:** `~/.config/NuGet/NuGet.Config` ou `~/.nuget/NuGet/NuGet.Config` (varia de acordo com a distribuição do sistema operacional) <br/>Configurações adicionais têm suporte em todas as plataformas. Essas configurações não podem ser editadas pelas ferramentas. </br> **Windows:**`%appdata%\NuGet\config\*.Config` <br/>**Mac/Linux:** `~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config` | As configurações se aplicam a todas as operações, mas são substituídas por quaisquer configurações de nível de projeto. |
| Computador | **Windows:**`%ProgramFiles(x86)%\NuGet\Config`<br/>**Mac/Linux:** `$XDG_DATA_HOME` . Se `$XDG_DATA_HOME` for nulo ou vazio, `~/.local/share` ou `/usr/local/share` será usado (varia de acordo com a distribuição do SO)  | As configurações se aplicam a todas as operações, mas são substituídas por qualquer usuário ou por configurações de nível de projeto. |

Observações para versões anteriores do NuGet:
- O NuGet 3.3 e versões anteriores usavam uma pasta `.nuget` para configurações de toda a solução. Esta pasta não é usada no NuGet 3.4 +.
- Para o NuGet 2,6 a 3. x, o arquivo de configuração no nível do computador no Windows estava localizado em `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]\NuGet.Config` , onde `{IDE}` pode ser `VisualStudio` , `{Version}` a versão do Visual Studio, como, `14.0` e `{SKU}` é `Community` , `Pro` ou `Enterprise` . Para migrar as configurações para o NuGet 4.0 +, basta copiar o arquivo de configuração para `%ProgramFiles(x86)%\NuGet\Config` . No Linux, esse local anterior era `/etc/opt` , e no Mac, `/Library/Application Support` .

## <a name="changing-config-settings"></a>Alterar as definições da configuração

Um arquivo `NuGet.Config` é um arquivo de texto XML simples que contém pares chave-valor, conforme descrito no tópico [Definições de configuração do NuGet](../reference/nuget-config-file.md).

As configurações são gerenciadas usando o [comando config](../reference/cli-reference/cli-ref-config.md) da CLI do NuGet:
- Por padrão, as alterações são feitas no arquivo de configuração de nível de usuário.
- Para alterar as configurações em um arquivo diferente, use a opção `-configFile`. Nesse caso, os arquivos podem usar qualquer nome de arquivo.
- As chaves sempre diferenciam maiúsculas e minúsculas.
- A elevação é necessária para alterar as configurações no arquivo de configurações no nível do computador.

> [!Warning]
> Embora você possa modificar o arquivo em qualquer editor de texto, o NuGet (v3.4.3 e posterior) ignorará silenciosamente todo o arquivo de configuração se ele contiver XML malformado (marcas não correspondidas, aspas inválidas, etc.). É por isso que é preferível gerenciar a configuração usando `nuget config`.

### <a name="setting-a-value"></a>Definindo um valor

Windows:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

Mac/Linux:

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
> No NuGet 3.4 e posterior, você pode usar as variáveis de ambiente em qualquer valor, como no `repositoryPath=%PACKAGEHOME%` (Windows) e `repositoryPath=$PACKAGEHOME` (Mac/Linux).

### <a name="removing-a-value"></a>Removendo um valor

Para remover um valor, especifique uma chave com um valor vazio.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Criar um novo arquivo de configuração

Copie o modelo abaixo para o novo arquivo e, em seguida, use `nuget config -configFile <filename>` para definir os valores:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Como as configurações são aplicadas

Vários arquivos `NuGet.Config` permitem que você armazene as configurações em locais diferentes, para que elas se apliquem a um único projeto, um grupo de projetos ou todos os projetos. Coletivamente, essas configurações se aplicam a qualquer operação do NuGet invocada na linha de comando ou do Visual Studio, com as configurações existentes “mais próximas” para um projeto ou a pasta atual tendo precedência.

Especificamente, o NuGet carrega as configurações dos arquivos de configuração diferente na seguinte ordem:

1. O [ `NuGetDefaults.Config` arquivo](#nuget-defaults-file), que contém configurações relacionadas apenas às origens do pacote.
1. O arquivo de nível de computador.
1. O arquivo de nível de usuário.
1. O arquivo especificado com `-configFile`.
1. Arquivos encontrados em todas as pastas no caminho da raiz da unidade para a pasta atual (onde `nuget.exe` é invocado ou a pasta que contém o projeto do Visual Studio). Por exemplo, se um comando for invocado no `c:\A\B\C` , o NuGet procurará e carregará os arquivos de configuração em `c:\` , depois, `c:\A` `c:\A\B` e finalmente `c:\A\B\C` .

À medida que o NuGet encontra configurações nesses arquivos, eles são aplicados da seguinte maneira:

1. Para elementos de item único, o NuGet substituiu qualquer valor encontrado anteriormente pela mesma chave. Isso significa que as configurações que são “mais próximas” da pasta ou projeto atual substituem quaisquer outras encontradas anteriormente. Por exemplo, a definição `defaultPushSource` em `NuGetDefaults.Config` será substituída se ela existir em qualquer outro arquivo de configuração.
1. Para elementos de coleta (como `<packageSources>`), o NuGet combina os valores de todos os arquivos de configuração em uma única coleção.
1. Quando `<clear />` está presente para um nó específico, o NuGet ignora os valores de configuração definidos anteriormente para esse nó.

### <a name="settings-walkthrough"></a>Explicação passo a passo das configurações

Digamos que você tem a seguinte estrutura de pasta em duas unidades separadas:

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

Dessa forma, você terá quatro arquivos `NuGet.Config` nos seguintes locais com o conteúdo em questão. (O arquivo no nível de computador não está incluído neste exemplo, mas se comportaria da mesma forma que o arquivo de nível de usuário.)

Arquivo A. Arquivo de nível de usuário, (`%appdata%\NuGet\NuGet.Config` no Windows e `~/.config/NuGet/NuGet.Config` no Mac/Linux):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

Arquivo B. `disk_drive_2/NuGet.Config` :

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

Arquivo C. `disk_drive_2/Project1/NuGet.Config` :

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

Arquivo D. `disk_drive_2/Project2/NuGet.Config` :

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

O NuGet, em seguida, carrega e aplica as configurações como mostrado a seguir, dependendo de onde ele é chamado:

- **Chamado de `disk_drive_1/users`**: somente o repositório padrão listado no arquivo de configuração de nível de usuário (A) é usado, pois esse é o único arquivo encontrado em `disk_drive_1` .

- **Invocado `disk_drive_2/` de `disk_drive_/tmp` ou**: o arquivo de nível de usuário (a) é carregado primeiro, então o NuGet vai para a raiz de `disk_drive_2` e localiza o arquivo (B). O NuGet também procura um arquivo de configuração no `/tmp` , mas não localiza um. Como resultado, o repositório padrão no `nuget.org` é usado, a restauração de pacote é habilitada e os pacotes são expandidos no `disk_drive_2/tmp` .

- **Invocado `disk_drive_2/Project1` de `disk_drive_2/Project1/Source` ou**: o arquivo de nível de usuário (a) é carregado primeiro, em seguida, o NuGet carrega o arquivo (B) da raiz de `disk_drive_2` , seguido por arquivo (C). As configurações em (C) substituem aquelas em (B) e (A), de modo que os `repositoryPath` pacotes de onde são instalados são, `disk_drive_2/Project1/External/Packages` em vez de `disk_drive_2/tmp` . Além disso, como (C) limpa o `<packageSources>`, o nuget.org não está mais disponível como uma origem, restando apenas `https://MyPrivateRepo/ES/nuget`.

- **Invocado `disk_drive_2/Project2` de `disk_drive_2/Project2/Source` ou**: o arquivo de nível de usuário (a) é carregado primeiro seguido pelo arquivo (B) e arquivo (D). Como `packageSources` não foi apagado, ambos `nuget.org` e `https://MyPrivateRepo/DQ/nuget` estão disponíveis como origens. Os pacotes são expandidos no `disk_drive_2/tmp` conforme especificado em (B).

## <a name="additional-user-wide-configuration"></a>Configuração de todo o usuário adicional

A partir do 5,7, o NuGet adicionou suporte para arquivos adicionais de configuração de todo o usuário. Isso permite que fornecedores de terceiros adicionem arquivos de configuração de usuário adicionais sem elevação.
Esses arquivos de configuração são encontrados na pasta de configuração de usuário padrão em uma `config` subpasta.
Todos os arquivos que terminam com `.config` ou `.Config` serão considerados.
Esses arquivos não podem ser editados pelas ferramentas padrão.

| Plataforma do SO  | Configurações adicionais |
| --- | --- |
| Windows      | `%appdata%\NuGet\config\*.Config` |
| Mac/Linux    | `~/.config/NuGet/config/*.config` ou `~/.nuget/config/*.config` |

## <a name="nuget-defaults-file"></a>Arquivo de padrões do NuGet

O arquivo `NuGetDefaults.Config` existe para especificar origens de pacote do qual os pacotes são instalados e atualizados, e para controlar o destino padrão para publicar pacotes com `nuget push`. Como os administradores podem implantar com conveniência (usando a Política de Grupo, por exemplo) arquivos `NuGetDefaults.Config` consistentes em computadores de desenvolvedor e de build, eles podem garantir que todos na organização estejam usando as origens de pacotes corretas, em vez do nuget.org.

> [!Important]
> O arquivo `NuGetDefaults.Config` nunca faz com que a origem do pacote seja removida da configuração do NuGet do desenvolvedor. Isso significa que, se o desenvolvedor já tiver usado o NuGet e, portanto, a origem do pacote no nuget.org está registrada, ele não será removido após a criação de um arquivo `NuGetDefaults.Config`.
>
> Além disso, nem `NuGetDefaults.Config` qualquer outro mecanismo no NuGet pode impedir o acesso a fontes de pacote como NuGet.org. Se uma organização quiser bloquear tal acesso, ela deverá usar outros meios, como firewalls para fazer isso.

### <a name="nugetdefaultsconfig-location"></a>`NuGetDefaults.Config` local

A tabela a seguir descreve onde o arquivo `NuGetDefaults.Config` deve ser armazenado, dependendo do sistema operacional de destino:

| Plataforma do SO  | `NuGetDefaults.Config` Local |
| --- | --- |
| Windows      | **Visual Studio 2017 ou NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 e anteriores ou NuGet 3.x e anteriores:** `%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME` (normalmente `~/.local/share` ou `/usr/local/share`, dependendo da distribuição do SO)|

### <a name="nugetdefaultsconfig-settings"></a>Configurações do NuGetDefaults.Config

- `packageSources`: esta coleção tem o mesmo significado que `packageSources` em arquivos de configuração regulares e especifica as origens padrão. O NuGet usa as origens em ordem ao instalar ou atualizar pacotes em projetos usando o formato de gerenciamento `packages.config`. Para projetos usando o formato PackageReference, o NuGet usa origens locais primeiro e, em seguida, origens em compartilhamentos de rede e origens em HTTP, independentemente da ordem dos arquivos de configuração. O NuGet sempre ignora a ordem de origens com operações de restauração.

- `disabledPackageSources`: essa coleção também tem o mesmo significado que nos `NuGet.Config` arquivos, onde cada fonte afetada é listada por seu nome e um `true` / `false` valor que indica se ele está desabilitado. Isso permite que o nome de origem e a URL permaneçam em `packageSources` sem que ele seja ativado por padrão. Os desenvolvedores individuais podem reabilitar a origem definindo o valor da origem como `false` em outros `NuGet.Config` arquivos sem precisar encontrar a URL correta novamente. Isso também é útil para fornecer aos desenvolvedores uma lista completa de URLs de origem interna para uma organização, permitindo somente a origem de uma equipe individual por padrão.

- `defaultPushSource`: especifica o destino padrão para `nuget push` operações, substituindo o padrão interno de `nuget.org` . Os administradores podem implantar essa configuração para evitar a publicação de pacotes internos para o público `nuget.org` por acidente, pois os desenvolvedores precisam usar especificamente `nuget push -Source` para publicar no `nuget.org` .

### <a name="example-nugetdefaultsconfig-and-application"></a>Exemplo de NuGetDefaults.Config e aplicativo

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
