---
title: Como gerenciar as pastas de pacotes globais, de cache e temporárias no NuGet
description: Como gerenciar a pasta de instalação de pacote global, o cache de pacote e as pastas temporárias que existem em um computador, usados durante a instalação, restauração e atualização de pacotes.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825212"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Como gerenciar as pastas de pacotes globais, de cache e temporárias

Sempre que você instala, atualiza ou restaura um pacote, o NuGet gerencia pacotes e informações do pacote em várias pastas fora da estrutura do seu projeto:

| Name | Descrição e localização (por usuário)|
| --- | --- |
| global&#8209;packages | A pasta *global-packages* é onde o NuGet instala qualquer pacote baixado. Cada pacote é totalmente expandido em uma subpasta que corresponde ao identificador de pacote e ao número de versão. Os projetos que usam o formato [PackageReference](package-references-in-project-files.md) sempre usam pacotes diretamente dessa pasta. Ao usar o [packages.config](../reference/packages-config.md), os pacotes são instalados na pasta *global-packages*, depois são copiados para a pasta `packages` do projeto.<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>Substitua usando a variável de ambiente NUGET_PACKAGES, as [definições de configuração](../reference/nuget-config-file.md#config-section) de `globalPackagesFolder` ou `repositoryPath` (ao usar PackageReference e `packages.config`, respectivamente) ou a propriedade do MSBuild `RestorePackagesPath` (somente MSBuild). A variável de ambiente tem precedência sobre a definição de configuração.</li></ul> |
| http&#8209;cache | O Gerenciador de Pacotes do Visual Studio (NuGet 3.x ou posterior) e a ferramenta `dotnet` armazenam cópias de pacotes baixados nesse cache (salvos como arquivos `.dat`), organizados em subpastas para cada origem de pacote. Os pacotes não são expandidos, e o cache tem um tempo de expiração de 30 minutos.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>Substitua usando a variável de ambiente NUGET_HTTP_CACHE_PATH.</li></ul> |
| temp | Uma pasta em que o NuGet armazena arquivos temporários durante suas várias operações.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |
| plugins-cache **4.8+** | Uma pasta na qual o NuGet armazena os resultados da solicitação de declarações de operação.<br/><ul><li>Windows: `%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/plugins-cache`</li><li>Substitua usando a variável de ambiente NUGET_PLUGINS_CACHE_PATH.</li></ul> |

> [!Note]
> O NuGet 3.5 e versões anteriores usam *packages-cache* em vez de *http-cache*, que está localizado em `%localappdata%\NuGet\Cache`.

Ao usar as pastas de cache e *global-packages*, geralmente o NuGet evita o download de pacotes que já existem no computador, melhorando o desempenho da instalação, atualização e restauração de operações. Quando PackageReference é usado, a pasta *global-packages* também evita o armazenamento de pacotes baixados dentro das pastas de projeto, onde eles podem ser inadvertidamente adicionados ao controle do código-fonte, e reduz o impacto geral do NuGet no armazenamento do computador.

Quando solicitado a recuperar um pacote, o NuGet primeiro examina a pasta *global-packages*. Se a versão exata do pacote não estiver lá, o NuGet verificará todas as origens de pacote não HTTP. Se ainda assim o pacote não for encontrado, o NuGet procurará o pacote no *http-cache*, a menos que você especifique `--no-cache` com comandos `dotnet.exe` ou `-NoCache` com comandos `nuget.exe`. Se o pacote não estiver no cache ou se o cache não for usado, o NuGet recuperará o pacote via HTTP.

Para obter mais informações, confira [O que acontece quando um pacote é instalado?](../concepts/package-installation-process.md).

## <a name="viewing-folder-locations"></a>Exibir os locais de pastas

É possível exibir os locais usando o [comando nuget locals](../reference/cli-reference/cli-ref-locals.md):

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

Saída típica (Windows; "user1" é o nome de usuário atual):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

(`package-cache` é usado no NuGet 2.x e aparece no NuGet 3.5 e versões anteriores).

Também é possível exibir os locais de pasta usando o [comando dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals):

```dotnetcli
dotnet nuget locals all --list
```

Saída típica (Mac/Linux; "user1" é o nome de usuário atual):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

Para exibir a localização de uma única pasta, use `http-cache`, `global-packages`, `temp` ou `plugins-cache` em vez de `all`.

## <a name="clearing-local-folders"></a>Limpar pastas locais

Se você encontrar problemas de instalação do pacote ou se desejar garantir que esteja instalando pacotes de uma galeria remota, use a opção `locals --clear` (dotnet.exe) ou `locals -clear` (nuget.exe), especificando a pasta a ser limpa, ou `all` para limpar todas as pastas:

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

Todos os pacotes usados por projetos que estejam abertos no momento no Visual Studio não serão apagados da pasta *global-packages*.

No Visual Studio 2017 em diante, use o comando de menu **Ferramentas > Gerenciador de Pacotes NuGet > Configurações do Gerenciador de Pacotes** e, em seguida, selecione **Limpar Todos os Caches do NuGet**. O gerenciamento de cache não está disponível atualmente por meio do Console do Gerenciador de Pacotes. No Visual Studio 2015, use os comandos da CLI.

![Comando de opção do NuGet para limpar caches](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Solução de problemas de erros

Os seguintes erros podem ocorrer ao usar `nuget locals` ou `dotnet nuget locals`:

- *Erro: o processo não pode acessar o arquivo <package> porque ele está sendo usado por outro processo* ou *Falha ao limpar os recursos locais: não é possível excluir um ou mais arquivos*

    Um ou mais arquivos da pasta estão em uso por outro processo. Por exemplo, um projeto do Visual Studio está aberto e se refere aos pacotes da pasta *global-packages*. Feche os processos e tente novamente.

- *Erro: o acesso ao caminho <path> foi negado* ou *O diretório não está vazio*

    Você não tem permissão para excluir arquivos no cache. Altere as permissões de pasta, se possível, e tente novamente. Senão, entre em contato com o administrador do sistema.

- *Erro: o caminho especificado, o nome do arquivo ou ambos são muito longos. O nome de arquivo totalmente qualificado deve ter menos de 260 caracteres e o nome do diretório deve ter menos de 248 caracteres.*

    Reduza os nomes de pasta e tente novamente.
