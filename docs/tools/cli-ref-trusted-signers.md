---
title: Comando de signatários confiáveis de CLI do NuGet
description: Referência do comando de signatários confiável nuget.exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ffd0cf5d50a2deed16e1722b32e43047bc81df2f
ms.sourcegitcommit: a1846edf70ddb2505d58e536e08e952d870931b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303682"
---
# <a name="trusted-signers-command-nuget-cli"></a>comando de signatários confiáveis (CLI do NuGet)

**Aplica-se a:** consumo do pacote &bullet; **versões com suporte:** 4.9 +

Obtém ou define os signatários confiáveis na configuração do NuGet. Para uso adicional, consulte [Configurando o comportamento do NuGet](../consume-packages/configuring-nuget-behavior.md). Para obter detalhes sobre como o esquema do NuGet. config se parece, consulte o [referência de arquivo de configuração do NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Uso

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Se nenhuma das `list|add|remove|sync` for especificado, o comando padrão será `list`.

## <a name="nuget-trusted-signers-list"></a>lista de signatários confiáveis do NuGet

Lista todos os signatários confiáveis na configuração. Essa opção incluirá todos os certificados (com a impressão digital e o algoritmo de impressão digital) tem cada assinante. Se um certificado tem precedidos `[U]`, isso significa que a entrada de certificado tiver `allowUntrustedRoot` definido como `true`.

Abaixo está um exemplo de saída deste comando:

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>NuGet signatários confiável add [Opções]

Adiciona um signatário confiável com o nome fornecido para o arquivo config. Essa opção tem diferentes gestos para adicionar um repositório ou autor confiável.

## <a name="options-for-add-based-on-a-package"></a>Opções para adicionar, com base em um pacote

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

em que `<package(s)>` é um ou mais `.nupkg` arquivos.

| Opção | Descrição |
| --- | --- |
| Autor | Especifica que a assinatura do autor do pacote (s) deve ser confiável. |
| Repositório | Especifica que a assinatura de repositório ou a referenda do pacote (s) deve ser confiável. |
| AllowUntrustedRoot | Especifica se o certificado do signatário confiável deve ter permissão de encadear para uma raiz não confiável. |
| Proprietários | Lista de ponto e vírgula separada de proprietários confiáveis para restringir ainda mais a relação de confiança de um repositório. Válido somente ao usar o `-Repository` opção. |

Fornecendo `-Author` e `-Repository` ao mesmo tempo não tem suporte.

## <a name="options-for-add-based-on-a-service-index"></a>Opções para adicionar, com base em um índice de serviço

```cli
nuget trusted-signers add -Name <name> [options]
```

_Observação_: essa opção só será adicionar repositórios confiáveis. 

| Opção | Descrição |
| --- | --- |
| ServiceIndex | Especifica o índice de serviço V3 do repositório para ser confiável. Esse repositório tem que oferecer suporte o recursos de assinaturas do repositório. Se não for fornecido, o comando irá procurar uma origem de pacote com o mesmo `-Name` e obter o índice de serviço a partir daí. |
| AllowUntrustedRoot | Especifica se o certificado do signatário confiável deve ter permissão de encadear para uma raiz não confiável. |
| Proprietários | Lista de ponto e vírgula separada de proprietários confiáveis para restringir ainda mais a relação de confiança de um repositório. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Opções para adicionar, com base nas informações de certificado

```cli
nuget trusted-signers add -Name <name> [options]
```

_Observação_: se um signatário confiável com o nome fornecido já existir, o item de certificado será adicionado para esse assinante. Caso contrário, um autor confiável será criado com um item de certificado de determinadas informações do certificado.

| Opção | Descrição |
| --- | --- |
| CertificateFingerprint | Especifica um certificado de impressões digitais de um certificado que pacotes assinados devem ser assinadas com. Uma impressão digital do certificado é um hash do certificado. Especifica o algoritmo de hash usado para calcular esse hash deve ser o `FingerprintAlgorithm` opção. |
| FingerprintAlgorithm | Especifica o algoritmo de hash usado para calcular a impressão digital do certificado. Assume o padrão de `SHA256`. Valores com suporte são `SHA256`, `SHA384` e `SHA512` |
| AllowUntrustedRoot | Especifica se o certificado do signatário confiável deve ter permissão de encadear para uma raiz não confiável. |

## <a name="nuget-trusted-signers-remove--name-name"></a>Remova o NuGet signatários confiáveis - nome <name>

Remove qualquer signatários confiáveis que correspondem ao nome fornecido.

## <a name="nuget-trusted-signers-sync--name-name"></a>NuGet signatários confiáveis de sincronização - nome <name>

Solicita a lista mais recente de certificados usados em um repositório confiável no momento para atualizar a lista de certificados existentes em um signatário confiável.

_Observação_: esse gesto excluirá a lista atual de certificados e substituí-los com uma lista atualizada do repositório.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| ForceEnglishOutput | Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

## <a name="examples"></a>Exemplos

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```