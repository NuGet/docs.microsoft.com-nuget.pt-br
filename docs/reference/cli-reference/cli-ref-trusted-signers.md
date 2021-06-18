---
title: Comando de assinantes confiáveis da CLI do NuGet
description: Referência para o nuget.exe comando de assinantes confiáveis
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: a5f3564af8b96dfa673d2252aea2e77a79c184a4
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323584"
---
# <a name="trusted-signers-command-nuget-cli"></a>comando de assinantes confiáveis (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** de consumo de pacote: 4.9.1 +

Obtém ou define os assinantes confiáveis para a configuração do NuGet. Para uso adicional, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md). Para obter detalhes sobre como o esquema de nuget.config se parece, consulte a [referência do arquivo de configuração do NuGet](../nuget-config-file.md).

## <a name="usage"></a>Uso

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Se nenhum `list|add|remove|sync` for especificado, o comando usará como padrão `list` .

## <a name="nuget-trusted-signers-list"></a>lista de assinantes confiáveis do NuGet

Lista todos os assinantes confiáveis na configuração. Essa opção incluirá todos os certificados (com o algoritmo de impressão digital e de impressão digital) que cada signatário tem. Se um certificado tiver um anterior `[U]` , isso significará que a entrada do certificado foi `allowUntrustedRoot` definida como `true` .

Veja abaixo um exemplo de saída deste comando:

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>NuGet confiável-os assinantes adicionam [opções]

Adiciona um signatário confiável com o nome fornecido para a configuração. Esta opção tem gestos diferentes para adicionar um autor ou um repositório confiável.

## <a name="options-for-add-based-on-a-package"></a>Opções para adicionar com base em um pacote

```cli
nuget trusted-signers add <package> -Name <name> [options]
```

onde `<package>` é um `.nupkg` arquivo assinado.

- **`-Author`**

  Especifica que a assinatura de autor do pacote assinado deve ser confiável.

- **`-AllowUntrustedRoot`**

  Especifica se o certificado para o assinante confiável deve ter permissão para se encadear a uma raiz não confiável.

- **`-Owners`**

  Lista separada por ponto e vírgula de proprietários confiáveis para restringir ainda mais a confiança de um repositório. Válido somente ao usar a `-Repository` opção.

- **`-Repository`**

  Especifica que a assinatura de repositório ou a referenda do pacote assinado deve ser confiável.

Fornecer `-Author` e `-Repository` ao mesmo tempo não é suportado.

## <a name="options-for-add-based-on-a-service-index"></a>Opções para adicionar com base em um índice de serviço

```cli
nuget trusted-signers add -Name <name> [options]
```

_Observação_: esta opção adicionará somente Repositórios confiáveis. 

- **`-AllowUntrustedRoot`**

  Especifica se o certificado para o assinante confiável deve ter permissão para se encadear a uma raiz não confiável.

- **`-Owners`**

  Lista separada por ponto e vírgula de proprietários confiáveis para restringir ainda mais a confiança de um repositório.

- **`-ServiceIndex`**

  Especifica o índice de serviço V3 do repositório a ser confiável. Este repositório tem que oferecer suporte ao recurso de assinaturas de repositório. Se não for fornecido, o comando procurará uma origem de pacote com o mesmo `-Name` e obterá o índice de serviço a partir daí.

## <a name="options-for-add-based-on-the-certificate-information"></a>Opções para adicionar com base nas informações do certificado

```cli
nuget trusted-signers add -Name <name> [options]
```

_Observação_: se um signatário confiável com o nome fornecido já existir, o item de certificado será adicionado a esse signatário. Caso contrário, um autor confiável será criado com um item de certificado de informações de certificado fornecidas.


- **`-AllowUntrustedRoot`**

  Especifica se o certificado para o assinante confiável deve ter permissão para se encadear a uma raiz não confiável.

- **`-CertificateFingerprint`**

  Especifica um certificado de impressões digitais de um certificado com o qual os pacotes assinados devem ser assinados. Uma impressão digital de certificado é um hash do certificado. O algoritmo de hash usado para calcular esse hash deve ser especificado na `FingerprintAlgorithm` opção.

- **`-FingerprintAlgorithm`**

  Especifica o algoritmo de hash usado para calcular a impressão digital do certificado. Assume o padrão de `SHA256`. Os valores com suporte são `SHA256` `SHA384` e `SHA512` .

## <a name="nuget-trusted-signers-remove--name-name"></a>NuGet confiável-os assinantes removem-Name \<name\>

Remove os assinantes confiáveis que correspondem ao nome fornecido.

## <a name="nuget-trusted-signers-sync--name-name"></a>NuGet confiável-autenticadores Sync-Name \<name\>

Solicita a lista mais recente de certificados usados em um repositório atualmente confiável para atualizar a lista de certificados existentes no Assinante confiável.

_Observação_: esse gesto excluirá a lista atual de certificados e os substituirá por uma lista atualizada do repositório.

## <a name="options"></a>Opções

- **`-ConfigFile`**

  O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.

- **`-ForceEnglishOutput`**

  Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.

- **`-?|-help`**

  Exibe informações de ajuda para o comando.

- **`-Name`**

  Nome do signatário confiável.

- **`-NonInteractive`**

  Suprime prompts de entrada ou confirmações do usuário.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .


## <a name="examples"></a>Exemplos

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
