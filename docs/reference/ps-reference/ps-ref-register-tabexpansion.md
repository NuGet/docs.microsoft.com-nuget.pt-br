---
title: Referência do PowerShell de registro do NuGet-TabExpansion
description: Referência para o comando Register-TabExpansion do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384448"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (console do Gerenciador de pacotes no Visual Studio)

*Disponível somente dentro do [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*

Registra uma expansão de tabulação para os parâmetros do comando especificado, de modo que, quando a guia é usada ao inserir um comando, os valores expandidos aparecem como opções disponíveis para o parâmetro em questão. Todas as expansões anteriores para o comando são substituídas.

## <a name="syntax"></a>Sintaxe

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Name | Necessária O comando para o qual registrar expansões. A opção-Name em si é opcional. |
| Definição | Necessária Um objeto que descreve o argumento na sintaxe `@{'<parameter>' = {'<value1>', '<value2>', ...}}` em que `<parameter>` é o nome do parâmetro a ser modificado e cada `<value>` fornece uma expansão específica. Aspas simples e duplas são aceitas. |

Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.

## <a name="common-parameters"></a>Parâmetros comuns

o `Register-TabExpansion` dá suporte aos seguintes [parâmetros comuns do PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Exemplos

Considere uma solução que contenha três nomes de projectmanager, utilitários e SpecialParser. O desenvolvedor frequentemente usa o comando `Update-Package` em momentos diferentes com cada um desses projetos. Ela descobre que é conveniente fazer com que o comando `Update-Package` forneça expansões de preenchimento automático para o argumento `-ProjectName` para que ela não precise digitar um nome de projeto a cada vez. 

O comando a seguir, em seguida, registra esses três nomes de projeto como uma expansão para o parâmetro `-ProjectName`:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

O desenvolvedor pode digitar `Update-Package -ProjectName `, pressionar Tab e ver as expansões oferecidas como opções de preenchimento automático:

![Exemplo de uso de Register-TabExpansion](media/Register-TabExpansion-Example.png)
