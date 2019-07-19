---
title: Referência do PowerShell do NuGet
description: A referência completa aos comandos do PowerShell disponíveis no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 142af9c4f7d25c3b0d986524313851cceb1e4c60
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327923"
---
# <a name="powershell-reference"></a>Referência do PowerShell

O console do Gerenciador de pacotes fornece uma interface do PowerShell no Visual Studio no Windows para interagir com o NuGet por meio dos comandos específicos listados abaixo. (O console não está disponível atualmente no Visual Studio para Mac.) Para obter um guia sobre como usar o console do, consulte o tópico [instalar e gerenciar pacotes usando o console do Gerenciador de pacotes](../consume-packages/install-use-packages-powershell.md) .

> [!Tip]
> Todos os comandos do PowerShell se relacionam apenas com o consumo do pacote. Nenhum comando do PowerShell está relacionado à criação e publicação de pacotes, exceto na medida em que um pacote também pode ser um consumidor de outros pacotes.

> [!Important]
> Os comandos listados aqui são específicos do console do Gerenciador de pacotes no Visual Studio e são diferentes dos [comandos do módulo gerenciamento de pacotes](/powershell/module/packagemanagement/?view=powershell-6) que estão disponíveis em um ambiente geral do PowerShell. Especificamente, cada ambiente tem comandos que não estão disponíveis no outro, e comandos com o mesmo nome também podem diferir em seus argumentos específicos. Ao usar o console do Gerenciamento de Pacotes no Visual Studio, os comandos e argumentos documentados neste tópico atual se aplicam.

| Comandos comuns | Descrição | Versão do NuGet |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | Instala um pacote e suas dependências no projeto. | Todos |
| [Update-Package](ps-reference/ps-ref-update-package.md) | Atualiza um pacote e suas dependências ou todos os pacotes em um projeto. | Todos |
| [Find-Package](ps-reference/ps-ref-find-package.md) | Pesquisa uma origem de pacote usando uma ID de pacote ou palavras-chave. | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | Recupera a lista de pacotes instalados no repositório local ou lista os pacotes disponíveis de uma origem de pacote. | Todos |

| Comandos secundários | Descrição | Versão do NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | Examina todos os assemblies no caminho de saída de um projeto e adiciona redirecionamentos de associação ao `app.config` ou `web.config` quando necessário. | Todos |
| [Get-Project](ps-reference/ps-ref-get-project.md) | Exibe informações sobre o projeto padrão ou especificado. | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | Inicia o navegador padrão com o projeto, a licença ou a URL de abuso de relatório para o pacote especificado. | Preterido em 3.0 + |
| [Register-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | Registra uma expansão de tabulação para os parâmetros de um comando, permitindo que você crie expansões personalizadas para valores de parâmetro usados com frequência. | Todos |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | Obtenha a versão do pacote instalado do projeto especificado e sincronize a versão para o restante dos projetos na solução. | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | Remove um pacote de um projeto, removendo opcionalmente suas dependências. | Todos |

Para obter ajuda completa e detalhada sobre qualquer um desses comandos no console do, basta executar o seguinte com o nome do comando em questão:

```ps
Get-Help <command> -full
```

Todos os comandos do console do Gerenciador de pacotes dão suporte aos seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):

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
