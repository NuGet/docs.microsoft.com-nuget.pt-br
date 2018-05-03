---
title: Comando de sinal de CLI do NuGet
description: Referência para o comando de sinal de nuget.exe
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7e84d794b802cfd69c785f720280fd5c022a46f6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="sign-command-nuget-cli"></a>comando de sinal (NuGet CLI)

**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** 4.6 +

Assina todos os pacotes que o primeiro argumento com um certificado de correspondência. O certificado com a chave privada pode ser obtido de um arquivo ou de um certificado instalado em um repositório de certificados, fornecendo um nome de entidade ou uma impressão digital.

Assinatura do pacote ainda não é suportada no núcleo do .NET, em Mono ou em plataformas não Windows.

## <a name="usage"></a>Uso

```cli
nuget sign <package(s)> [options]
```

onde `<package(s)>` é uma ou mais `.nupkg` arquivos.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| CertificateFingerprint | Especifica a impressão digital de SHA-1 do certificado usado para pesquisar um repositório de certificados local para o certificado. |
| CertificatePassword | Especifica a senha do certificado, se necessário. Se um certificado é protegido por senha, mas nenhuma senha for fornecida, o comando solicitará uma senha em tempo de execução, a menos que o - opção interativa é passado. |
| CertificatePath | Especifica o caminho do arquivo para o certificado a ser usado na assinatura do pacote. |
| CertificateStoreLocation | Especifica o nome do uso de repositório de certificado x. 509 para pesquisar o certificado. O padrão é "CurrentUser", o repositório de certificados x. 509 usado pelo usuário atual. Essa opção deve ser usada ao especificar o certificado usando as opções de CertificateSubjectName - ou - CertificateFingerprint. |
| CertificateStoreName | Especifica o nome do repositório de certificados x. 509 a ser usado para pesquisar o certificado. O padrão é "My", o repositório de certificados x. 509 certificados pessoais. Essa opção deve ser usada ao especificar o certificado usando as opções de CertificateSubjectName - ou - CertificateFingerprint. |
| CertificateSubjectName | Especifica o nome da entidade do certificado usado para pesquisar um repositório de certificados local para o certificado.  A pesquisa é uma comparação de cadeia de caracteres de maiusculas e minúsculas usando o valor fornecido, o que encontrará todos os certificados com o nome da entidade que contém essa cadeia de caracteres, independentemente de outros valores de assunto.  O repositório de certificados pode ser especificado pelas opções CertificateStoreName - e - CertificateStoreLocation. |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| ForceEnglishOutput | Força o nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| HashAlgorithm | Algoritmo de hash a ser usado para assinar o pacote. O padrão é SHA256. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime avisos para a entrada do usuário ou confirmações. |
| OutputDirectory | Especifica o diretório onde o pacote assinado deve ser salvo. Por padrão, o pacote original é substituído pelo pacote assinado. |
| Substituir | Opção para indicar se a assinatura atual deve ser substituída. Por padrão o comando falhará se o pacote já tiver uma assinatura. |
| Timestamper | URL para um servidor de carimbo de hora do RFC 3161. |
| TimestampHashAlgorithm | Algoritmo de hash a ser usado pelo servidor de carimbo de hora do RFC 3161. O padrão é SHA256. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

## <a name="examples"></a>Exemplos

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```