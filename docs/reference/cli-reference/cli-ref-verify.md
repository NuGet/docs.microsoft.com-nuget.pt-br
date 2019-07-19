---
title: Comando Verify da CLI do NuGet
description: Referência para o comando de verificação NuGet. exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327493"
---
# <a name="verify-command-nuget-cli"></a>Commando verify (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** de consumo de pacote: 4.6 +

Verifica um pacote.

A verificação de pacotes assinados ainda não tem suporte no .NET Core, em mono ou em plataformas que não são do Windows.

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

| Opção | Descrição |
| --- | --- |
| CertificateFingerprint | Especifica uma ou mais impressões digitais do certificado SHA-256 de certificados com os quais os pacotes assinados devem ser assinados. Uma impressão digital SHA-256 do certificado é um hash SHA-256 do certificado. Várias entradas devem ser separadas por ponto e vírgula. |

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet a ser aplicado. Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.|
| ForceEnglishOutput | Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |

## <a name="examples"></a>Exemplos

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```