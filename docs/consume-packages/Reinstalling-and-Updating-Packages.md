---
title: Reinstalando e atualizando pacotes do NuGet
description: Detalhes sobre quando é necessário reinstalar e atualizar pacotes, assim como acontece com referências de pacote interrompidas no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: c48980bc3f955a62962ca6e9619ce09f4a94a835
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488086"
---
# <a name="how-to-reinstall-and-update-packages"></a>Como reinstalar e atualizar pacotes

Há várias situações, descritas abaixo em [Quando reinstalar um pacote](#when-to-reinstall-a-package), em que as referências a um pacote podem ser interrompidas em um projeto do Visual Studio. Nesses casos, desinstalar e depois reinstalar a mesma versão do pacote fará com que essas referências voltem a funcionar corretamente. Atualizar um pacote simplesmente significa instalar uma versão atualizada, o que geralmente faz um pacote voltar a funcionar corretamente.

No Visual Studio, o Console do Gerenciador de Pacotes fornece muitas opções flexíveis para atualizar e reinstalar pacotes.

A atualização e reinstalação de pacotes é feita da seguinte maneira:

| Método | Atualização | Reinstalar |
| --- | --- | --- |
| Console do Gerenciador de Pacotes (descrito em [Usando Update-Package](#using-update-package)) | Comando `Update-Package` | Comando `Update-Package -reinstall` |
| Interface do usuário do Gerenciador de Pacotes | Na guia **Atualizações**, selecione um ou mais pacotes e escolha **Atualizar** | Na guia **Instalado**, selecione um pacote, registre seu nome e escolha **Desinstalar**. Mude para a guia **Procurar**, pesquise pelo nome do pacote, selecione-o e escolha **Instalar**). |
| CLI do nuget.exe | Comando `nuget update` | Para todos os pacotes, exclua a pasta do pacote e execute `nuget install`. Para um único pacote, exclua a pasta do pacote e usar `nuget install <id>` para reinstalar o mesmo. |

> [!NOTE]
> Para a CLI do dotnet, o procedimento equivalente não é necessário. Em um cenário semelhante, você pode [restaurar pacotes com a CLI do dotnet](package-restore.md#restore-using-the-dotnet-cli).

Neste artigo:

- [Quando reinstalar um pacote](#when-to-reinstall-a-package)
- [Restrições de versões de upgrade](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Quando reinstalar um pacote

1. **Referências com problemas após a restauração de pacote**: Se você abriu um projeto e restaurou pacotes NuGet, mas ainda está encontrando referências com problemas, tente reinstalar todos os pacotes.
1. **Projeto com problemas devido a arquivos excluídos**: O NuGet não impede que você remova itens adicionados de pacotes; portanto, é fácil modificar inadvertidamente o conteúdo instalado de um pacote e fazer com que o projeto fique com problemas. Para restaurar o projeto, reinstale os pacotes afetados.
1. **A atualização de pacote desfez o projeto**: Caso uma atualização de um pacote cause problemas em um projeto, a falha é geralmente causada por um pacote de dependência que também pode ter sido atualizado. Para restaurar o estado da dependência, reinstale o pacote específico.
1. **Redirecionamento ou atualização de projeto**: Isso pode ser útil quando um projeto foi redirecionado ou atualizado e se o pacote exige a reinstalação devido à alteração na estrutura de destino. O NuGet mostra um erro de build nesses casos imediatamente após o redirecionamento do projeto e os avisos de build subsequentes informam que o pacote pode precisar ser reinstalado. Para upgrade do projeto, o NuGet mostra um erro no Log de Upgrade de Projeto.
1. **Reinstalação de um pacote durante seu desenvolvimento**: Os autores de pacotes geralmente precisam reinstalar a mesma versão do pacote que está sendo desenvolvida para testar o comportamento. O comando `Install-Package` não oferece uma opção para forçar uma reinstalação, portanto, use `Update-Package -reinstall` em vez disso.

## <a name="constraining-upgrade-versions"></a>Restrições de versões de upgrade

Por padrão, reinstalar ou atualizar um pacote *sempre* instala a versão mais recente disponível da origem do pacote.

Em projetos que usam o formato `packages.config` de gerenciamento, no entanto, é possível restringir o intervalo de versão especificamente. Por exemplo, se você souber que o aplicativo funciona apenas com a versão 1.x de um pacote, mas não 2.0 e superior, talvez devido a uma alteração principal no pacote de API, pode ser útil restringir os upgrades para as versões 1.x. Isso impede atualizações acidentais que interromperiam o aplicativo.

Para definir uma restrição, abra `packages.config` em um editor de texto, localize a dependência em questão e adicione o atributo `allowedVersions` com um intervalo de versão. Por exemplo, para restringir atualizações para a versão 1.x, defina `allowedVersions` para `[1,2)`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

Em todo os casos, use a notação descrita em [Controle de versão do pacote](../concepts/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-update-package"></a>Usando o Update-Package

Lembre-se das [Considerações](#considerations) descritas abaixo. É possível reinstalar facilmente qualquer pacote usando o [comando Update-Package](../reference/ps-reference/ps-ref-update-package.md) no Console do Gerenciador de Pacotes do Visual Studio (**Ferramentas** > **Gerenciador de Pacotes NuGet** > **Console do Gerenciador de Pacotes**).

```ps
Update-Package -Id <package_name> –reinstall
```

Usar esse comando é muito mais fácil do que remover um pacote e, em seguida, tentar localizar o mesmo pacote na Galeria do NuGet com a mesma versão. Observe que a opção `-Id` é opcional.

O mesmo comando sem `-reinstall` atualiza um pacote para uma versão mais recente, se aplicável. O comando apresentará um erro se o pacote em questão ainda não tiver sido instalado em um projeto; ou seja, `Update-Package` não instala pacotes diretamente.

```ps
Update-Package <package_name>
```

Por padrão, `Update-Package` afeta todos os projetos em uma solução. Para limitar a ação a um projeto específico, use a opção `-ProjectName`, utilizando o nome do projeto como ele aparece no Gerenciador de Soluções:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

Para *atualizar* todos os pacotes em um projeto (ou reinstalá-los usando `-reinstall`), use `-ProjectName` sem especificar nenhum pacote específico:

```ps
Update-Package -ProjectName MyProject
```

Para atualizar todos os pacotes em uma solução, basta usar `Update-Package` sozinho sem argumentos nem opções. Use este formulário com cuidado, pois pode levar um tempo considerável para executar todas as atualizações:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

Atualizar pacotes em um projeto ou solução usando [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) sempre atualiza para a versão mais recente do pacote (excluindo pacotes de pré-lançamento). Projetos que usam `packages.config` podem, se desejado, limitar as versões de atualização conforme descrito abaixo em [Restrições de versões de upgrade](#constraining-upgrade-versions).

Para obter detalhes completos sobre o comando, consulte a referência de [Update-Package](../reference/ps-reference/ps-ref-update-package.md).

### <a name="considerations"></a>Considerações

O exemplo a seguir pode ser afetado ao reinstalar um pacote:

1. **Reinstalar os pacotes de acordo com redirecionamento de estrutura de destino do projeto**
    - Em um caso simples, apenas reinstalar um pacote usando `Update-Package –reinstall <package_name>` já funciona. Um pacote que está instalado em uma estrutura de destino antiga é desinstalado e o mesmo pacote é instalado na estrutura de destino atual do projeto.
    - Em alguns casos, pode haver um pacote não compatível com a nova estrutura de destino.
        - Se um pacote for compatível com PCLs (bibliotecas de classes portáteis) e o projeto for redirecionado para um conjunto de plataformas que não são mais compatíveis com o pacote, as referências ao pacote estarão ausentes após a reinstalação.
        - Isso pode surgir para pacotes que você está usando diretamente ou para pacotes instalados como dependências. É possível que o pacote que você está usando diretamente seja compatível com a nova estrutura de destino enquanto sua dependência não é.
        - Se reinstalar os pacotes depois de redirecionar seu aplicativo resultar em erros de build ou tempo de execução, poderá ser necessário reverter a estrutura de destino ou pesquisar pacotes alternativos com suporte adequado à sua estrutura de destino.

1. **O atributo requireReinstallation adicionado ao packages.config após o redirecionamento ou upgrade do projeto**
    - Se o NuGet detectar que pacotes foram afetados pelo redirecionamento ou upgrade de um projeto, ele adiciona um atributo `requireReinstallation="true"` em `packages.config` a todas as referências de pacote afetadas. Por isso, cada build subsequente no Visual Studio gera avisos de build para esses pacotes para que você se lembre de reinstalá-los.

1. **Reinstalar pacotes com dependências**
    - `Update-Package –reinstall` reinstala a mesma versão do pacote original, mas instala a versão mais recente das dependências, a menos que restrições específicas de versão sejam fornecidas. Isso permite atualizar apenas as dependências conforme necessário para corrigir um problema. No entanto, se isso reverter uma dependência para uma versão anterior, você pode usar `Update-Package <dependency_name>` para reinstalar essa dependência sem afetar o pacote dependente.
    - O `Update-Package –reinstall <packageName> -ignoreDependencies` reinstala a mesma versão do pacote original, mas não reinstale as dependências. Use esta opção ao atualizar as dependências do pacote pode resultar em um estado interrompido

1. **Reinstalar pacotes quando versões dependentes estão envolvidas**
    - Conforme explicado acima, reinstalar um pacote não altera as versões de outros pacotes instalados que dependem dele. É possível, em seguida, que reinstalar uma dependência poderia interromper o pacote dependente.
