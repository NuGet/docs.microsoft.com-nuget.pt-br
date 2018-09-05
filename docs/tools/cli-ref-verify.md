---
title: CLI do NuGet verifique se o comando
description: Referência para o nuget.exe Verifique se o comando
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545207"
---
# <a name="verify-command-nuget-cli"></a>Commando verify (NuGet CLI)

**Aplica-se a:** consumo do pacote &bullet; **versões com suporte:** 4.6 +

Verifica um pacote.

Verificação de pacotes assinados ainda não é suportada no .NET Core, em Mono, ou em plataformas não Windows.

## <a name="usage"></a>Uso

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

em que `<package(s)>` é um ou mais `.nupkg` arquivos.

## <a name="nuget-verify--all"></a>Verifique se o NuGet - todos

Especifica que todas as verificações de possíveis devem ser executadas sobre o pacote (s).

## <a name="nuget-verify--signatures"></a>Verifique se o NuGet - assinaturas

Especifica que a verificação de assinatura de pacote deve ser executada.

## <a name="options-for-verify--signatures"></a>Opções para "verificar - assinaturas"

| Opção | Descrição |
| --- | --- |
| CertificateFingerprint | Especifica um ou mais SHA-256 certificado impressões digitais de certificados (s) quais pacotes assinados devem ser assinados com. Uma impressão digital de certificado SHA-256 é um hash SHA-256 do certificado. Várias entradas devem ser separada de ponto e vírgula. |

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| ForceEnglishOutput | Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

## <a name="examples"></a>Exemplos

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```