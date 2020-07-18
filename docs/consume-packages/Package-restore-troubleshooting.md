---
title: Solucionando problemas de restauração de pacote do NuGet no Visual Studio
description: Uma descrição de erros de restauração de NuGet comuns no Visual Studio e como solucioná-los.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: b162990eae2160961f560b6c6ee73e47cb4121d6
ms.sourcegitcommit: f29fa9b93fd59e679fab50d7413bbf67da3ea5b3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451145"
---
# <a name="troubleshooting-package-restore-errors"></a>Solução de problemas de erros de restauração de pacote

Este artigo aborda os erros comuns ao restaurar pacotes e as etapas para resolvê-los. 

A Restauração de Pacote tenta instalar todas as dependências de pacotes no estado correto correspondente às referências de pacote do arquivo de projeto (*.csproj*) ou do arquivo *packages.config*. (No Visual Studio, as referências aparecem em Gerenciador de Soluções sob as **dependências \ NuGet** ou o nó **References** .) Para seguir as etapas necessárias para restaurar pacotes, consulte [restaurar pacotes](../consume-packages/package-restore.md#restore-packages). Se as referências de pacote no arquivo de projeto (*.csproj*) ou no arquivo *packages.config* estiverem incorretas (não corresponderem ao estado desejado após a Restauração de Pacote), instale ou atualize os pacotes em vez de usar a Restauração de Pacote.

Se estas instruções não funcionarem para você, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para examinarmos o cenário mais cuidadosamente. Não use o controle “Esta página é útil?” que pode aparecer nesta página, pois ele não nos permite entrar em contato com você para obter mais informações.

## <a name="quick-solution-for-visual-studio-users"></a>Solução rápida para usuários do Visual Studio

Se você estiver usando o Visual Studio, primeiro habilite a restauração de pacote da maneira descrita a seguir. Caso contrário, prossiga para as seções seguintes.

1. Selecione o comando de menu **Ferramentas > Gerenciador de Pacotes do NuGet > Configurações do Gerenciador de Pacotes**.
1. Marque as duas opções em **Restauração de Pacote**.
1. Selecione **OK**.
1. Compile o projeto novamente.

![Habilitar a restauração de pacote do NuGet em Ferramenta/Opções](../consume-packages/media/restore-01-autorestoreoptions.png)

Essas configurações também podem ser alteradas no arquivo `NuGet.config`; veja a seção de [consentimento](#consent). Se seu projeto for um projeto mais antigo que usa a restauração de pacote integrada ao MSBuild, talvez seja [necessário](package-restore.md#migrate-to-automatic-package-restore-visual-studio) migrar para a restauração automática de pacote.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Este projeto faz referência a pacotes NuGet ausentes neste computador

Mensagem de erro completa:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Esse erro ocorre ao tentar compilar um projeto com referências a um ou mais pacotes do NuGet, mas, no momento, esses pacotes não estão instalados no computador ou no projeto.

- Ao usar o formato de gerenciamento [PackageReference](package-references-in-project-files.md) , o erro significa que o pacote não está instalado na pasta *global-Packages* , conforme descrito em [Gerenciando os pacotes globais e as pastas de cache](managing-the-global-packages-and-cache-folders.md).
- Ao usar o [packages.config](../reference/packages-config.md), o erro significa que o pacote não está instalado na pasta `packages` na raiz da solução.

Essa situação geralmente ocorre ao obter o código-fonte do projeto por meio do controle do código-fonte ou de outro download. Os pacotes normalmente são omitidos do controle do código-fonte ou dos downloads, uma vez que podem ser restaurados de feeds de pacotes, como o nuget.org (veja [Pacotes e controle do código-fonte](Packages-and-Source-Control.md)). Por outro lado, a inclusão deles sobrecarregaria o repositório ou criaria arquivos .zip desnecessariamente grandes.

O erro também poderá ocorrer se o arquivo de projeto contiver caminhos absolutos para locais de pacote e você mover o projeto.

Use um dos seguintes métodos para restaurar os pacotes:

- Se você moveu o arquivo de projeto, edite o arquivo diretamente para atualizar as referências do pacote.
- [Visual Studio](package-restore.md#restore-using-visual-studio) ([restauração automática](package-restore.md#restore-packages-automatically-using-visual-studio) ou [restauração manual](package-restore.md#restore-packages-manually-using-visual-studio))
- [CLI do dotnet](package-restore.md#restore-using-the-dotnet-cli)
- [CLI do nuget.exe](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

Após uma restauração bem-sucedida, o pacote deve estar presente na pasta *global-packages*. Em caso de projetos que usam PackageReference, uma restauração deve recriar o arquivo `obj/project.assets.json`; em projetos que usam `packages.config`, o pacote deve aparecer na pasta `packages` do projeto. Nesse momento, o projeto deverá ser compilado com êxito. Caso contrário, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que possamos acompanhá-lo com você.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Arquivo de ativos project.assets.json não encontrado

Mensagem de erro completa:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

O arquivo `project.assets.json` mantém um grafo de dependência do projeto quando ocorre o uso do formato de gerenciamento PackageReference, que é usado para garantir que todos os pacotes necessários sejam instalados no computador. Como esse arquivo é gerado de modo dinâmico por meio da restauração do pacote, ele geralmente não é adicionado ao controle do código-fonte. Como resultado, esse erro ocorre ao compilar um projeto com uma ferramenta como o `msbuild`, que não restaura os pacotes automaticamente.

Nesse caso, execute `msbuild -t:restore` seguido por `msbuild` ou use `dotnet build` (que restaura automaticamente os pacotes). Também é possível usar algum dos métodos de restauração de pacote descritos na [seção anterior](#missing).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Um ou mais pacotes NuGet precisam ser restaurados, mas não foi possível porque o consentimento não foi concedido

Mensagem de erro completa:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Esse erro indica que a restauração de pacote está desabilitada na configuração do NuGet.

Você pode alterar as configurações aplicáveis no Visual Studio, conforme descrito anteriormente em [Solução rápida para usuários do Visual Studio](#quick-solution-for-visual-studio-users).

Você também pode editar essas configurações diretamente no arquivo `nuget.config` aplicável (normalmente `%AppData%\NuGet\NuGet.Config` no Windows e `~/.nuget/NuGet/NuGet.Config` no Linux/Mac). Verifique se as chaves `enabled` e `automatic` em `packageRestore` estão definidas como True:

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> Se você editar as configurações de `packageRestore` diretamente em `nuget.config`, reinicie o Visual Studio para que a caixa de diálogo de opções mostre os valores atuais.

## <a name="other-potential-conditions"></a>Outras condições possíveis

- Você pode encontrar erros de build devido a arquivos ausentes, com uma mensagem indicando para usar a restauração do NuGet para baixá-los. No entanto, ao executar uma restauração, a seguinte mensagem poderá aparecer: "Todos os pacotes já estão instalados e não há nada para ser restaurado". Nesse caso, exclua a pasta `packages` (ao usar `packages.config`) ou o arquivo `obj/project.assets.json` (ao usar PackageReference) e execute a restauração novamente. Se o erro continuar, use `nuget locals all -clear` ou `dotnet nuget locals all --clear` pela linha de comando para limpar as pastas *global-packages* e de cache, conforme descrito em [Como gerenciar as pastas de pacotes globais e de cache](managing-the-global-packages-and-cache-folders.md).

- Ao obter um projeto por meio do controle do código-fonte, as pastas do projeto poderão ser definidas como somente leitura. Altere as permissões de pasta e tente restaurar os pacotes novamente.

- Talvez você esteja usando uma versão antiga do NuGet. Acesse [nuget.org/downloads](https://www.nuget.org/downloads) para obter as versões mais recentes recomendadas. Para o Visual Studio 2015, recomendamos a versão 3.6.0.

Se você encontrar outros problemas, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que possamos obter mais detalhes.
