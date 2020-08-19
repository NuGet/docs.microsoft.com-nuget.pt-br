---
title: Comando de assinatura do NuGet CLI
description: Referência para o comando de assinatura de nuget.exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622766"
---
# <a name="sign-command-nuget-cli"></a>comando Sign (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** para criação de pacote: 4.6 +

Assina todos os pacotes que correspondem ao primeiro argumento com um certificado. O certificado com a chave privada pode ser obtido de um arquivo ou de um certificado instalado em um repositório de certificados, fornecendo um nome de entidade ou uma impressão digital.

> [!Note]
> A assinatura de pacote ainda não tem suporte no .NET Core, em mono ou em plataformas que não são do Windows.

## <a name="usage"></a>Uso

```cli
nuget sign <package(s)> [options]
```

onde `<package(s)>` é um ou mais `.nupkg` arquivos.

## <a name="options"></a>Opções

- **`-CertificateFingerprint`**

  Especifica a impressão digital SHA-1 do certificado usado para pesquisar um repositório de certificados local para o certificado.

- **`-CertificatePassword`**

  Especifica a senha do certificado, se necessário. Se um certificado for protegido por senha, mas nenhuma senha for fornecida, o comando solicitará uma senha em tempo de execução, a menos que a `-NonInteractive` opção seja passada.

- **`-CertificatePath`**

  Especifica o caminho do arquivo para o certificado a ser usado na assinatura do pacote.

- **`-CertificateStoreLocation`**

  Especifica o nome do repositório de certificados X. 509 usado para pesquisar o certificado. O padrão é "CurrentUser", o repositório de certificados X. 509 usado pelo usuário atual. Essa opção deve ser usada ao especificar o certificado por meio de `-CertificateSubjectName` `-CertificateFingerprint` Opções ou.

- **`-CertificateStoreName`**

  Especifica o nome do repositório de certificados X. 509 a ser usado para pesquisar o certificado. O padrão é "My", o repositório de certificados X. 509 para certificados pessoais. Essa opção deve ser usada ao especificar o certificado por meio de `-CertificateSubjectName` `-CertificateFingerprint` Opções ou.

- **`-CertificateSubjectName`**

  Especifica o nome da entidade do certificado usado para pesquisar um repositório de certificados local para o certificado.  A pesquisa é uma comparação de cadeias de caracteres que não diferencia maiúsculas de minúsculas usando o valor fornecido, que encontrará todos os certificados com o nome da entidade que contém essa cadeia de caracteres, independentemente de outros valores de entidade.  O repositório de certificados pode ser especificado por `-CertificateStoreName` e `-CertificateStoreLocation` opções.

- **`-ConfigFile`**

  O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.

- **`-ForceEnglishOutput`**

  Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.

- **`-HashAlgorithm`**

  Algoritmo de hash a ser usado para assinar o pacote. O padrão é SHA256. Os valores possíveis são SHA256, SHA384 e SHA512.

- **`-?|-help`**

  Exibe informações de ajuda para o comando.

- **`-NonInteractive`**

  Suprime prompts de entrada ou confirmações do usuário.

- **`-OutputDirectory`**

  Especifica o diretório em que o pacote assinado deve ser salvo. Por padrão, o pacote original é substituído pelo pacote assinado.

- **`-Overwrite`**

  Alterne para indicar se a assinatura atual deve ser substituída. Por padrão, o comando falhará se o pacote já tiver uma assinatura.

- **`-Timestamper`**

  URL para um servidor de carimbo de data/hora RFC 3161.

- **`-TimestampHashAlgorithm`**

  Algoritmo de hash a ser usado pelo servidor de carimbo de data/hora RFC 3161. O padrão é SHA256.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .

## <a name="examples"></a>Exemplos

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
