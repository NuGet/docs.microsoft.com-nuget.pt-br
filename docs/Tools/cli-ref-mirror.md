---
title: Comando de espelho do NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o comando de espelho nuget.exe"
keywords: "referência de espelho do NuGet, comando de espelho"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff5f1c1a915943e8a2eb9c6d6ab09a850968371
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="mirror-command-nuget-cli"></a>comando de espelho (NuGet CLI)

**Aplica-se a:** pacote publicação &bullet; **versões com suporte:** preterido no 3.2 +

Reflete um pacote e suas dependências de repositórios de origem especificado para o repositório de destino.

> [!NOTE]
> Para habilitar esse comando para versões do NuGet antes 3.2, vá para [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), selecione a versão estável mais recente, baixe `NuGet.ServerExtensions.dll` e `Nuget-Signed.exe` para seu disco local e renomear `Nuget-Signed.exe` para `nuget.exe`.

## <a name="usage"></a>Uso

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

onde `<packageID>` é o pacote para o espelho, ou `<configFilePath>` identifica o `packages.config` arquivo que lista os pacotes para espelhar.

O `<listUrlTarget>` Especifica o repositório de origem e `<publishUrlTarget>` Especifica o repositório de destino.

Se o repositório de destino estiver em `https://machine/repo` que está executando o [NuGet.Server](../hosting-packages/NuGet-Server.md), as urls de lista e enviar por push será `https://machine/repo/nuget` e `https://machine/repo/api/v2/package`, respectivamente.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| apiKey | A chave de API para o repositório de destino. Se não estiverem presentes, especificada na *%AppData%\NuGet\NuGet.Config* é usado. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NoCache | Impede que o NuGet usando pacotes de caches de computador local. |
| NOOP | Registra o que deve ser feito, mas não executa as ações; assume o sucesso para operações de envio por push. |
| Versão de pré-lançamento | Inclui pacotes pré-lançados na operação de espelhamento. |
| Origem | Uma lista de fontes de pacote para espelhar. Se nenhuma fonte for especificada, aqueles definidos no *%AppData%\NuGet\NuGet.Config* forem usados, padronizando para nuget.org se nenhum for especificado. |
| Tempo limite | Especifica o tempo limite, em segundos, para enviar por push para um servidor. O padrão é 300 segundos (5 minutos). |
| Versão | A versão do pacote para instalação. Se não for especificado, a versão mais recente é espelhada. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
