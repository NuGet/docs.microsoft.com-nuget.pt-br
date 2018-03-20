---
title: "Solução de problemas da restauração de pacote do NuGet no Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Uma descrição de erros de restauração de NuGet comuns no Visual Studio e como solucioná-los."
keywords: "Restauração de pacote do NuGet, restaurando pacotes, solucionando problemas, solução de problemas"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a>Solução de problemas de erros de restauração de pacote

Este artigo aborda os erros comuns ao restaurar pacotes e as etapas para resolvê-los. Para obter detalhes completos sobre a restauração de pacotes, veja [Restauração de pacote](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Se estas instruções não funcionarem para você, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para examinarmos o cenário mais cuidadosamente. Não use o controle "Esta página é útil?" que pode aparecer nesta página, pois ele não nos possibilita contatar você para obter mais informações.

## <a name="quick-solution-for-visual-studio-users"></a>Solução rápida para usuários do Visual Studio

Se você estiver usando o Visual Studio, primeiro habilite a restauração de pacote da maneira descrita a seguir. Caso contrário, prossiga para as seções seguintes.

1. Selecione o comando de menu **Ferramentas > Gerenciador de Pacotes do NuGet > Configurações do Gerenciador de Pacotes**.
1. Marque as duas opções em **Restauração de Pacote**.
1. Selecione **OK**.
1. Compile o projeto novamente.

![Habilitar a restauração de pacote do NuGet em Ferramenta/Opções](../consume-packages/media/restore-01-autorestoreoptions.png)

Essas configurações também podem ser alteradas no arquivo `NuGet.config`; veja a seção de [consentimento](#consent).

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Este projeto faz referência a pacotes NuGet ausentes neste computador

Mensagem de erro completa:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Esse erro ocorre ao tentar compilar um projeto com referências a um ou mais pacotes do NuGet, mas, no momento, esses pacotes não estão armazenados em cache no projeto. (Os pacotes são armazenados em cache em uma pasta `packages` na raiz da solução se o projeto usa `packages.config` ou no arquivo `obj/project.assets.json` se o projeto usa o formato PackageReference.)

Essa situação geralmente ocorre ao obter o código-fonte do projeto por meio do controle do código-fonte ou de outro download. Os pacotes normalmente são omitidos do controle do código-fonte ou dos downloads, uma vez que podem ser restaurados de feeds de pacotes, como o nuget.org (veja [Pacotes e controle do código-fonte](Packages-and-Source-Control.md)). Por outro lado, a inclusão deles sobrecarregaria o repositório ou criaria arquivos .zip desnecessariamente grandes.

Use um dos seguintes métodos para restaurar os pacotes:

- No Visual Studio, habilite a restauração de pacote selecionando o comando de menu **Ferramentas > Gerenciador de Pacotes do NuGet > Configurações do Gerenciador de Pacotes** marcando ambas as opções em **Restauração de Pacote** e selecionando **OK**. Em seguida, compile a solução novamente.
- Para projetos do .NET Core, execute `dotnet restore` ou `dotnet build` (que executa automaticamente a restauração).
- Na linha de comando, execute `nuget restore` (exceto para projetos criados com `dotnet`, caso em que `dotnet restore` deverá ser usado).
- Na linha de comando com projetos usando o formato PackageReference, execute `msbuild /t:restore`.

Após uma restauração bem-sucedida, você deverá ver uma pasta `packages` (ao usar `packages.config`) ou o arquivo `obj/project.assets.json` (ao usar PackageReference). Nesse momento, o projeto deverá ser compilado com êxito. Caso contrário, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que possamos acompanhá-lo com você.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Arquivo de ativos project.assets.json não encontrado

Mensagem de erro completa:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Esse erro ocorre pelos mesmos motivos que os explicados na [seção anterior](#missing) e apresentam as mesmas soluções. Por exemplo, executar `msbuild` em um projeto do .NET Core obtido por meio do controle do código-fonte não restaurará automaticamente os pacotes. Nesse caso, execute `msbuild /t:restore` seguido por `msbuild` ou use `dotnet build` (que restaura automaticamente os pacotes).

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

Observe que, se você editar as configurações de `packageRestore` diretamente em `nuget.config`, reinicie o Visual Studio para que a caixa de diálogo de opções mostre os valores atuais.

## <a name="other-potential-conditions"></a>Outras condições possíveis

- Você pode encontrar erros de build devido a arquivos ausentes, com uma mensagem indicando para usar a restauração do NuGet para baixá-los. No entanto, ao executar uma restauração, a seguinte mensagem poderá aparecer: "Todos os pacotes já estão instalados e não há nada para ser restaurado". Nesse caso, exclua a pasta `packages` (ao usar `packages.config`) ou o arquivo `obj/project.assets.json` (ao usar PackageReference) e execute a restauração novamente.

- Ao obter um projeto por meio do controle do código-fonte, as pastas do projeto poderão ser definidas como somente leitura. Altere as permissões de pasta e tente restaurar os pacotes novamente.

- Talvez você esteja usando uma versão antiga do NuGet. Acesse [nuget.org/downloads](https://www.nuget.org/downloads) para obter as versões mais recentes recomendadas. Para o Visual Studio 2015, recomendamos a versão 3.6.0.

Se você encontrar outros problemas, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que possamos obter mais detalhes.