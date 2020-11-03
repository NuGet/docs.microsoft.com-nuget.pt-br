---
title: Comando Verify da CLI do NuGet
description: Referência para o comando nuget.exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238134"
---
# <a name="verify-command-nuget-cli"></a>comando VERIFY (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** do consumo do pacote: 4.6 +

Verifica um pacote.

A verificação de pacotes assinados ainda não tem suporte no mono.

## <a name="usage"></a>Uso

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

onde `<package(s)>` é um ou mais `.nupkg` arquivos.

## <a name="nuget-verify--all"></a>verificar NuGet-todos

Especifica que todas as verificações possíveis devem ser executadas nos pacotes.

## <a name="nuget-verify--signatures"></a>verificação de NuGet-assinaturas

Especifica que a verificação de assinatura do pacote deve ser executada.

## <a name="options-for-verify--signatures"></a>Opções para "Verify-Signatures"

- **`-CertificateFingerprint`**

  Especifica uma ou mais impressões digitais do certificado SHA-256 de certificados com os quais os pacotes assinados devem ser assinados. Uma impressão digital SHA-256 do certificado é um hash SHA-256 do certificado. Várias entradas devem ser separadas por ponto e vírgula.

## <a name="options"></a>Opções

- **`-ConfigFile`**

  O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.

- **`-ForceEnglishOutput`**

  Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.

- **`-?|-help`**

  Exibe informações de ajuda para o comando.

- **`-NonInteractive`**

  Suprime prompts de entrada ou confirmações do usuário.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .

## <a name="examples"></a>Exemplos

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```