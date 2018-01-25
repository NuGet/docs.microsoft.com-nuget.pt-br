---
title: "Referência do PowerShell do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "A referência completa de comandos do PowerShell disponíveis no Console do Gerenciador de pacotes do NuGet no Visual Studio."
keywords: "NuGet pacote manager console, comandos do Powershell do NuGet, referência do Powershell do NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0cbd9b13b34bd93fea6c6684c03bca9cff5d9e5e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="powershell-reference"></a>Referência do PowerShell

O Package Manager Console fornece uma interface do PowerShell dentro do Visual Studio no Windows para interagir com o NuGet por meio de comandos específicos listados abaixo. (O console não está atualmente disponível no Visual Studio para Mac.) Para um guia para usar o console, consulte o [Package Manager Console](../tools/package-manager-console.md) tópico.

> [!Tip]
> Todos os comandos do PowerShell referem-se somente para o consumo de pacote. Não há comandos do PowerShell relacionam para criar e publicar pacotes exceto nos casos em que um pacote também pode ser um consumidor de outros pacotes.

> [!Important]
> Os comandos listados aqui são específicos para o Console do Gerenciador de pacotes no Visual Studio e diferem do [comandos do módulo de gerenciamento de pacotes](/powershell/module/packagemanagement/?view=powershell-6) que estão disponíveis em um ambiente do PowerShell geral. Especificamente, cada ambiente tem comandos que não estão disponíveis nos outros e comandos com o mesmo nome também podem ser diferentes em seus argumentos específicos. Ao usar o Console de gerenciamento de pacote no Visual Studio, os comandos e os argumentos documentados neste tópico presente se aplicam.

| Comandos comuns | Descrição | Versão do NuGet |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | Instala um pacote e suas dependências no projeto. | Todos |
| [Update-Package](ps-ref-update-package.md) | Atualiza um pacote e suas dependências ou todos os pacotes em um projeto. | Todos |
| [Find-Package](ps-ref-find-package.md) | Pesquisa uma origem de pacote usando uma ID de pacote ou palavras-chave. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Recupera a lista de pacotes instalados no repositório local, ou lista de pacotes disponíveis a partir de uma origem do pacote. | Todos |

| Comandos secundários | Descrição | Versão do NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | Examina todos os assemblies no caminho de saída para um projeto e adiciona redirecionamentos de associação a `app.config` ou `web.config` quando necessário. | Todos |
| [Get-Project](ps-ref-get-project.md) | Exibe informações sobre o padrão ou o projeto especificado. | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | Inicia o navegador padrão com o projeto, a licença ou a URL para o pacote especificado abuso. | Preterido no 3.0 + |
| [Register-TabExpansion](ps-ref-register-tabexpansion.md) | Registra uma expansão de guia para os parâmetros de um comando, permitindo que você crie expansões personalizados para valores de parâmetro usados com frequência. | Todos |
| [Sync-Package](ps-ref-sync-package.md) | Obter a versão do instalada pacote de especificado do projeto e sincroniza a versão para o restante dos projetos na solução. | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | Remove um pacote de um projeto, opcionalmente, a remoção de suas dependências. | Todos |

Para obter ajuda completa, detalhada em qualquer um desses comandos dentro do console, execute o seguinte com o nome do comando em questão:

```ps
Get-Help <command> -full
```

Todos os comandos do Console do Gerenciador de pacote de suportam as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):

- Depurar
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Detalhado
- WarningAction
- WarningVariable

Para obter detalhes, consulte [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) na documentação do PowerShell.
