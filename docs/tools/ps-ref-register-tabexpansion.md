---
title: Referência do PowerShell NuGet Register-TabExpansion
description: Referência do comando Register-TabExpansion PowerShell no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 98171c598bd4a3468bd23e2d6060e267c38021b4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546599"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Registre-se-TabExpansion (Package Manager Console no Visual Studio)

*Disponível somente dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*

Registra uma expansão da tabulação para os parâmetros do comando especificado, de modo que quando a guia é usada ao inserir um comando, os valores expandidos aparecem como opções disponíveis para o parâmetro em questão. Qualquer expansões anteriores para o comando são substituídos.

## <a name="syntax"></a>Sintaxe

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Nome | (Obrigatório) O comando para o qual registrar expansões. -Nome do comutador em si é opcional. |
| Definição | (Obrigatório) Um objeto que descreve o argumento na sintaxe `@{'<parameter>' = {'<value1>', '<value2>', ...}}` onde `<parameter>` é o nome do parâmetro para modificar e cada `<value>` fornece uma expansão específica. Aspas simples e duplas são aceitos. |

Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Register-TabExpansion` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.

## <a name="examples"></a>Exemplos

Considere uma solução que contém três nomes de projetos EventManager, utilitários e SpecialParser. O desenvolvedor usa com frequência o `Update-Package` comando em momentos diferentes com cada um desses projetos. Ela localiza conveniente fazer com que o `Update-Package` comando fornecer expansões de preenchimento automático para o `-ProjectName` argumento para que ela não precisa digitar um nome de projeto cada vez. 

O comando a seguir, em seguida, registra esses nomes de três projetos como uma expansão para o `-ProjectName` parâmetro:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

O desenvolvedor pode, em seguida, digite `Update-Package -ProjectName `, pressione a tecla Tab e veja as expansões oferecidas como opções de preenchimento automático:

![Exemplo de como usar o registro TabExpansion](media/Register-TabExpansion-Example.png)
