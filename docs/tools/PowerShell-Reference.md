---
title: Referência do NuGet PowerShell
description: A referência completa de comandos do PowerShell disponíveis no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 45c8be9956ceaab844bdcd89f1b96adc256f805c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546658"
---
# <a name="powershell-reference"></a>Referência do PowerShell

O Package Manager Console fornece uma interface do PowerShell no Visual Studio no Windows para interagir com o NuGet por meio dos comandos específicos listados abaixo. (O console não está disponível atualmente no Visual Studio para Mac.) Para um guia para usar o console, consulte o [Package Manager Console](../tools/package-manager-console.md) tópico.

> [!Tip]
> Todos os comandos do PowerShell referem-se apenas ao consumo de pacote. Nenhum comando do PowerShell estão relacionadas à criação e publicação de pacotes, exceto na medida em que um pacote também pode ser um consumidor de outros pacotes.

> [!Important]
> Os comandos listados aqui são específicos para o Package Manager Console no Visual Studio e diferem da [comandos do módulo de gerenciamento de pacotes](/powershell/module/packagemanagement/?view=powershell-6) que estão disponíveis em um ambiente do PowerShell geral. Especificamente, cada ambiente tem comandos que não estão disponíveis no outro, e também podem ser diferentes comandos com o mesmo nome em seus argumentos específicos. Ao usar o Console de gerenciamento de pacotes no Visual Studio, os comandos e argumentos documentados neste tópico presente se aplicam.

| Comandos comuns | Descrição | Versão do NuGet |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | Instala um pacote e suas dependências no projeto. | Todos |
| [Update-Package](ps-ref-update-package.md) | Atualiza um pacote e suas dependências ou todos os pacotes em um projeto. | Todos |
| [Find-Package](ps-ref-find-package.md) | Pesquisa uma origem de pacote usando uma ID de pacote ou palavras-chave. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Recupera a lista de pacotes instalados no repositório local, ou lista os pacotes disponíveis a partir de uma origem de pacote. | Todos |

| Comandos secundários | Descrição | Versão do NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | Examina todos os assemblies no caminho de saída para um projeto e adiciona redirecionamentos de associação para o `app.config` ou `web.config` onde for necessário. | Todos |
| [Get-Project](ps-ref-get-project.md) | Exibe informações sobre o padrão ou o projeto especificado. | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | Inicia o navegador padrão com o projeto, a licença ou a URL para relatar abuso para o pacote especificado. | Preterido no 3.0 ou superior |
| [Registre-se TabExpansion](ps-ref-register-tabexpansion.md) | Registra uma expansão da tabulação para os parâmetros de um comando, permitindo que você crie expansões personalizados para valores de parâmetro usados. | Todos |
| [Sync-Package](ps-ref-sync-package.md) | Obter a versão do pacote a partir de instalada especificada do projeto e sincroniza a versão para o restante dos projetos na solução. | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | Remove um pacote de um projeto, opcionalmente, removendo suas dependências. | Todos |

Para obter ajuda completa e detalhada sobre qualquer um desses comandos dentro do console do, execute o seguinte com o nome do comando em questão:

```ps
Get-Help <command> -full
```

Todos os comandos do Console do Gerenciador de pacote de suporte aos seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):

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
