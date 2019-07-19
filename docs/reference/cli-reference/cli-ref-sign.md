---
title: Comando de assinatura do NuGet CLI
description: Referência para o comando de assinatura NuGet. exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327583"
---
# <a name="sign-command-nuget-cli"></a>Commando Commando sign (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** para criação de pacote: 4.6 +

Assina todos os pacotes que correspondem ao primeiro argumento com um certificado. O certificado com a chave privada pode ser obtido de um arquivo ou de um certificado instalado em um repositório de certificados, fornecendo um nome de entidade ou uma impressão digital.

A assinatura de pacote ainda não tem suporte no .NET Core, em mono ou em plataformas que não são do Windows.

## <a name="usage"></a>Uso

```cli
nuget sign <package(s)> [options]
```

onde `<package(s)>` é um ou mais `.nupkg` arquivos.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| CertificateFingerprint | Especifica a impressão digital SHA-1 do certificado usado para pesquisar um repositório de certificados local para o certificado. |
| certificatePassword | Especifica a senha do certificado, se necessário. Se um certificado for protegido por senha, mas nenhuma senha for fornecida, o comando solicitará uma senha em tempo de execução, a menos que a opção-não interativa seja passada. |
| CertificatePath | Especifica o caminho do arquivo para o certificado a ser usado na assinatura do pacote. |
| CertificateStoreLocation | Especifica o nome do repositório de certificados X. 509 usado para pesquisar o certificado. O padrão é "CurrentUser", o repositório de certificados X. 509 usado pelo usuário atual. Essa opção deve ser usada ao especificar o certificado por meio de opções-CertificateSubjectName ou-CertificateFingerprint. |
| CertificateStoreName | Especifica o nome do repositório de certificados X. 509 a ser usado para pesquisar o certificado. O padrão é "My", o repositório de certificados X. 509 para certificados pessoais. Essa opção deve ser usada ao especificar o certificado por meio de opções-CertificateSubjectName ou-CertificateFingerprint. |
| CertificateSubjectName | Especifica o nome da entidade do certificado usado para pesquisar um repositório de certificados local para o certificado.  A pesquisa é uma comparação de cadeias de caracteres que não diferencia maiúsculas de minúsculas usando o valor fornecido, que encontrará todos os certificados com o nome da entidade que contém essa cadeia de caracteres, independentemente de outros valores de entidade.  O repositório de certificados pode ser especificado por opções-CertificateStoreName e-CertificateStoreLocation. |
| ConfigFile | O arquivo de configuração do NuGet a ser aplicado. Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.|
| ForceEnglishOutput | Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| HashAlgorithm | Algoritmo de hash a ser usado para assinar o pacote. O padrão é SHA256. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| OutputDirectory | Especifica o diretório em que o pacote assinado deve ser salvo. Por padrão, o pacote original é substituído pelo pacote assinado. |
| Substituir | Alterne para indicar se a assinatura atual deve ser substituída. Por padrão, o comando falhará se o pacote já tiver uma assinatura. |
| Timestamper | URL para um servidor de carimbo de data/hora RFC 3161. |
| TimestampHashAlgorithm | Algoritmo de hash a ser usado pelo servidor de carimbo de data/hora RFC 3161. O padrão é SHA256. |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |

## <a name="examples"></a>Exemplos

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```