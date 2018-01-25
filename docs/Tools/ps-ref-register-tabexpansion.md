---
title: "Referência do PowerShell do NuGet Register-TabExpansion | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência de comando do PowerShell do registro TabExpansion no Console do Gerenciador de pacotes do NuGet no Visual Studio."
keywords: "Console do Gerenciador, comandos do Powershell do NuGet, referência do Powershell do NuGet, TabExpansion de registro do pacote NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5691c07f9efef4bfd12680421f3b02c5a523eb6f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (Console de Gerenciador de pacotes no Visual Studio)

*Disponível apenas dentro de [NuGet Package Manager Console](Package-Manager-Console.md) no Visual Studio no Windows.*

Registra uma expansão de guia para os parâmetros do comando especificado, que quando a guia é usada ao inserir um comando, os valores expandidos aparecem como opções disponíveis para o parâmetro em questão. Qualquer expansões anteriores para o comando são substituídos.

## <a name="syntax"></a>Sintaxe

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Nome | (Obrigatório) O comando para o qual registrar expansões. -Nome do comutador em si é opcional. |
| Definição | (Obrigatório) Um objeto que descreve o argumento na sintaxe `@{'<parameter>' = {'<value1>', '<value2>', ...}}` onde `<parameter>` é o nome do parâmetro para modificar e cada `<value>` fornece uma expansão específica. Aspas simples e duplas são aceitas. |

Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Register-TabExpansion`suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.

## <a name="examples"></a>Exemplos

Considere uma solução que contém três nomes de projetos EventManager, utilitários e SpecialParser. O desenvolvedor usa com frequência o `Update-Package` comando em momentos diferentes com cada um desses projetos. Ela localiza conveniente ter o `Update-Package` comando fornecem expansões de preenchimento automático para o `-ProjectName` argumento para que ela não precisa digitar um nome de projeto cada vez. 

O comando a seguir, em seguida, registra esses nomes de três projeto como uma expansão para o `-ProjectName` parâmetro:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

O desenvolvedor pode, em seguida, digite `Update-Package -ProjectName `, pressione a tecla Tab e ver as expansões oferecidas como opções de conclusão automática:

![Exemplo de como usar o registro TabExpansion](media/Register-TabExpansion-Example.png)
