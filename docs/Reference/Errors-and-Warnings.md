---
title: "Referência de erros e avisos a restauração do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: "Referência completa para avisos e erros emitidos durante a restauração do pacote do NuGet"
keywords: "NuGet erros, avisos do NuGet, diagnóstico"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53fccbb86f2920d870b5383070d043e25045a626
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="errors-and-warnings"></a>Erros e avisos

NuGet 4.3.0, erros e avisos são numerados conforme descrito neste tópico e fornecem informações detalhadas para ajudá-lo a resolver os problemas envolvidos. 

Os erros e avisos listados aqui estão disponíveis apenas com [com base em PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) NuGet 4.3.0 e projetos. NuGet também respeita propriedades MSBuild para suprimir avisos ou elevá-las a erros. Para obter mais informações, consulte [como: suprimir avisos do compilador](/visualstudio/ide/how-to-suppress-compiler-warnings) na documentação do Visual Studio.

**Erros**

| Grupo | Números de erro |
| --- | --- |
| [Erros de entrada inválidos](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [Erros de pacote e projeto ausentes](#missing-package-and-project-errors) | [NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (anteriormente NU1607) [NU1108](#nu1107) (anteriormente NU1606) |
| [Erros de compatibilidade](#compatibility-errors) | [NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401) |

**Avisos**

| Grupo | Números de aviso |
| --- | --- |
| [Avisos de entrada inválidos](#invalid-input-warnings) | [NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503) |
| [Avisos de versão de pacote inesperado](#unexpected-package-version-warnings) | [NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605) |
| [Avisos de conflito de resolução](#resolver-conflict-warnings) | [NU1608](#nu1608) |
| [Avisos de fallback do pacote](#package-fallback-warnings) | [NU1701](#nu1701) |
| [Avisos de feeds](#feed-warnings) | [NU1801](#nu1801) |
| [Avisos e erros internos do NuGet](#nuget-internal-errors-and-warnings) | [NU1000](#nu1000), [NU1500](#nu1500) |

## <a name="invalid-input-errors"></a>Erros de entrada inválidos

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **Problema** | O projeto não contém um ou mais frameworks. |
| **Causas comuns** | O projeto não contém um `TargetFramework` ou `TargetFrameworks` propriedade. |
| **Exemplo de mensagem** | *O projeto projA não especifica nenhuma estrutura de destino em c:\tmp\projA.csproj* |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **Problema** | Combinação inválida de entradas, junto com uma palavra-chave criptografada. |
| **Causas comuns** | CLEAR não pode ser combinado com outras entradas. |
| **Exemplo de mensagem** | *'CLEAR' não pode ser usado em conjunto com outros valores* |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **Problema** | `PackageTargetFallback`e `AssetTargetFallback` fornecem um comportamento diferente para a seleção de recursos e não podem ser usados juntos. |
| **Causas comuns** | Ambos `PackageTargetFallback` e `AssetTargetFallback` existe no projeto. |
| **Exemplo de mensagem** | *PackageTargetFallback e AssetTargetFallback não podem ser usados juntos. Remova as referências de PackageTargetFallback(deprecated) do ambiente do projeto.* |

## <a name="missing-package-and-project-errors"></a>Erros de pacote e projeto ausentes

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104 ](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **Problema** | Um grupo de dependência não ser resolvido. Esse é um problema genérico para tipos que não são pacotes ou projetos. |
| **Causas comuns** | O projeto contém uma dependência em um item que não existe. |
| **Exemplo de mensagem** | *Não é possível resolver System.Missing para net45* |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **Problema** | O pacote não foi encontrado em qualquer fonte. |
| **Causas comuns** | A origem do pacote correto está ausente ou o identificador de pacote está incorreto. |
| **Exemplo de mensagem** | *Não é possível encontrar o pacote System.Missing. Nenhum pacote existe com essa id na fonte (s): dotnet-core, dotnet roslyn, nuget.org* |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **Problema** | O identificador de pacote for encontrado, mas não é possível encontrar uma versão dentro do intervalo de dependência especificada em qualquer uma das fontes. |
| **Causas comuns** | A origem do pacote correto está ausente ou o intervalo de dependência está incorreto. O intervalo pode ser especificado por um pacote e não ao usuário. O usuário talvez precise alternar para uma versão disponível se esse pacote é referenciado pelo projeto diretamente. |
| **Exemplo de mensagem** | *Não é possível localizar o pacote NuGet.Versioning com a versão (> = 9.0.1)<br/> -versão (ões) de 30 encontrado em nuget.org [mais próximo de versão: 4.0.0]<br/> -versão (ões) de 10 encontrado em dotnet buildtools [mais próximo de versão: 4.0.0-rc-2129]<br/> -9 encontrado versão (ões) em NuGetVolatile [mais próximo de versão: 3.0.0-beta-00032]<br/> -encontrado versões 0 no núcleo do dotnet<br/> -encontrado versões 0 no roslyn dotnet* |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **Problema** | Nenhuma versão estável foram encontrado no intervalo de dependência. As versões de pré-lançamento foram encontradas, mas não são permitidas. |
| **Causas comuns** | O projeto especificado para o intervalo de dependência a uma versão estável. Os usuários precisam alterar o intervalo de versão para incluir as versões de pré-lançamento. |
| **Exemplo de mensagem** | *Não é possível localizar um pacote estável NuGet.Versioning com a versão (> = 3.0.0)<br/> -versão (ões) de 10 encontrado em dotnet buildtools [mais próximo de versão: 4.0.0-rc-2129]<br/> -versão (ões) de 9 encontrado em NuGetVolatile [mais próximo de versão: 3.0.0-beta-00032] <br/> -Encontrado versões 0 no núcleo do dotnet<br/> -encontrado versões 0 no roslyn dotnet* |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **Problema** | Um ProjectReference aponta para um arquivo que não existe. |
| **Causas comuns** | O arquivo de projeto está ausente do disco ou a referência está incorreta. |
| **Exemplo de mensagem** | *Referência de projeto não existe 'c:\a.csproj'. Verifique se a referência de projeto é válida e se existe o arquivo de projeto.* |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **Problema** | O arquivo de projeto existe, mas nenhuma informação de restauração foi fornecida para ele. |
| **Causas comuns** | No Visual Studio, isso pode significar que o projeto está descarregado. Na linha de comando, isso pode significar que o arquivo está corrompido ou que não contenha personalizado após o destino de importações necessário para restauração ler o projeto. |
| **Exemplo de mensagem** | *Não é possível ler as informações de projeto para 'c:\a.csproj'. O arquivo de projeto pode ser inválidos ou ausentes destinos necessários para a restauração.* |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **Problema** | Restrições de dependência não podem ser resolvidas. |
| **Causas comuns** | Os pacotes contêm dependência em versões exatas de um pacote em vez de intervalos abertos. |
| **Exemplo de mensagem** | *Não foi possível satisfazer solicitações conflitantes para {id}: {caminho conflito} Framework: {gráfico de destino}* |

< a name = "NU1107 ></a>

### <a name="nu1107-previously-nu1607"></a>NU1107 (anteriormente NU1607)

| | |
| --- | --- |
| **Problema** | Não é possível resolver as restrições de dependência entre pacotes. |
| **Causas comuns** | Pacotes com restrições de dependência em versões exatas não permitir que outros pacotes para aumentar a versão, se necessário. |
| **Exemplo de mensagem** | *Conflito de versão detectado para NuGet.Versioning. Referenciar o pacote diretamente do projeto para resolver esse problema.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)* |

< a name = "NU1108 ></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (anteriormente NU1606)

| | |
| --- | --- |
| **Problema** | Foi detectada uma dependência circular. |
| **Causas comuns** | Um pacote foi criado incorretamente. |
| **Exemplo de mensagem** | *Ciclo detectado: A -> B -> um* |

## <a name="compatibility-errors"></a>Erros de compatibilidade

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **Problema** | Um projeto de dependência não contém uma estrutura compatível com o projeto atual. |
| **Causas comuns** | Estrutura de destino do projeto é uma versão superior do projeto de consumo. |
| **Exemplo de mensagem** | *ServerWeb do projeto não é compatível com netstandard1.3 (. Identificadores de NETStandard, versão = v 1.3). Projeto suporta ServerWeb:<br/> -netstandard1.6 (. Identificadores de NETStandard, versão = v 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = v 1.0)* |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **Problema** | Um pacote de dependência não contém qualquer ativos compatíveis com o projeto. |
| **Causas comuns** | O pacote não dá suporte a estrutura de destino do projeto. |
| **Exemplo de mensagem** | *Pacote System.ComponentModel.EventBasedAsync 4.0.11 não é compatível com netstandard1.3 (. Identificadores de NETStandard, versão = v 1.3). Pacote suporta System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, versão = v 1.0)<br/> -monotouch10 (MonoTouch, versão = v 1.0)<br/> -net45 (. NETFramework, Version = v 4.5)<br/> -netcore50 (. NETCore, Version = v 5.0)<br/> -netstandard1.0 (. Identificadores de NETStandard, versão = v 1.0)<br/> -portátil net45 + win8 + wp8 + wpa81 (. NETPortable, Version = v0.0, perfil = Profile259)<br/> -win8 (Windows, versão = v 8.0)<br/> -wp8 (WindowsPhone, versão = v 8.0)<br/> -wpa81 (WindowsPhoneApp, versão = 8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **Problema** | O pacote não oferece suporte para o projeto `RuntimeIdentifier`. |
| **Causas comuns** | O pacote não dá suporte a atual `RuntimeIdentifier`. Alterar o `RuntimeIdentifier` valores usados no projeto, se necessário. |
| **Exemplo de mensagem** | *System.Example 1.0.0 fornece uma referência de tempo de compilação do assembly para o. dll em net461, mas não há nenhum tempo de execução do assembly compatível.* |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **Problema** | O pacote requer recursos ou estruturas atualmente não há suportadas à versão instalada do NuGet. |
| **Causas comuns** | Atualize o NuGet para corrigir o problema. |
| **Exemplo de mensagem** | *O pacote 'NuGet.Versioning' requer o NuGet versão de cliente '5.0.0' ou superior, mas a versão atual do NuGet é '4.3.0'. Para atualizar o NuGet, acesse http://docs.nuget.org/consume/installing-nuget.* |

## <a name="invalid-input-warnings"></a>Avisos de entrada inválidos

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **Problema** | A restauração do projeto está tentando operar em não foi encontrado. |
| **Causas comuns** | O projeto está ausente. |
| **Exemplo de mensagem** | *A pasta 'c:\projects\a' não contém um projeto para restaurar.* |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **Problema** | `RuntimeSupports`contém um perfil inválido. |
| **Causas comuns** | O dá suporte a perfil não foi encontrado em um `runtime.json` arquivo dos pacotes de dependência atual. |
| **Exemplo de mensagem** | *Perfil de compatibilidade desconhecido: aaa* |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **Problema** | Um projeto de dependência não importa destinos de restauração do NuGet. Isso é semelhante a NU1105, mas aqui o projeto será ignorado e ignorado em vez fazendo com que todos os de restauração falhe. Em soluções complexas geralmente há outros tipos de projetos que podem não oferecer suporte a restauração. |
| **Causas comuns** | Isso pode acontecer para projetos que não importar props/destinos comuns que importar automaticamente a restauração. Se o projeto não precisa ser restaurados isso pode ser ignorado. |
| **Exemplo de mensagem** | *Ignorando a restauração para o projeto 'c:\a.csproj'. O arquivo de projeto pode ser inválidos ou ausentes destinos necessários para a restauração.* |

## <a name="unexpected-package-version-warnings"></a>Avisos de versão de pacote inesperado

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **Problema** | Uma dependência de projeto foi aumentada para uma versão maior do que o projeto especificado. |
| **Causas comuns** | Outro pacote de dependência necessária uma versão mais recente e aumentado o pacote em. |
| **Exemplo de mensagem** | *Dependência especificada foi NuGet.Versioning (> = 3.5.0) mas acabou com NuGet.Versioning 4.0.0.* |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **Problema** | Uma dependência de pacote não tem um limite inferior. Isso não permite que a restauração localizar o *melhor correspondência*. Cada restauração flutua para baixo ao tentar encontrar uma versão inferior que pode ser usada. Isso significa que a restauração fica online para verificar se todas as fontes de cada vez em vez de usar os pacotes que já existem na pasta de pacote do usuário. |
| **Causas comuns** | Isso geralmente é um erro de criação de pacote. |
| **Exemplo de mensagem** | *NuGet. Packaging 4.0.0 não fornece um limite inferior inclusivo de dependência NuGet.Versioning (3.5.0 >). Uma melhor correspondência aproximada de 3.6.0 foi resolvida.* |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **Problema** | Uma dependência de pacote especificado de uma versão que não pôde ser encontrada. Uma versão mais recente foi usada em vez disso, o que é diferente do que o pacote foi criado.<br/><br/>Isso significa que a restauração não localizou o *melhor correspondência*. Cada restauração flutua para baixo ao tentar encontrar uma versão inferior que pode ser usada. Isso significa que a restauração fica online para verificar se todas as fontes de cada vez em vez de usar os pacotes que já existem na pasta de pacote do usuário. |
| **Causas comuns** | As fontes de pacote contém a versão inferior esperado. Se o pacote esperado não foi liberado, em seguida, isso pode ser um erro de criação de pacote. |
| **Exemplo de mensagem** | NuGet. Packaging 4.0.0 depende NuGet.Versioning (> = 4.0.0) mas 4.0.0 não foi encontrado. Uma melhor correspondência aproximada de 5.0.0 foi resolvida. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **Problema** | Uma dependência de projeto não define um limite inferior.<br/><br/>Isso significa que a restauração não localizou o *melhor correspondência*. Cada restauração flutua para baixo ao tentar encontrar uma versão inferior que pode ser usada. Isso significa que a restauração fica online para verificar se todas as fontes de cada vez em vez de usar os pacotes que já existem na pasta de pacote do usuário. |
| **Causas comuns** | O projeto *PackageReference* *versão* atributo deve ser atualizado para incluir um limite inferior. |
| **Exemplo de mensagem** | *Projeto dependência NuGet.Versioning (< = 9.0.0) doe não contêm um limite inferior inclusivo. Inclua um limite inferior na versão de dependência para garantir resultados consistentes de restauração.* |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **Problema** | Um pacote de dependência especificou uma restrição de versão em uma versão superior de um pacote de restauração finalmente resolvida. |
| **Causas comuns** | Wins mais próximos ao resolver pacotes. Um pacote distante pode ter substituído a um pacote mais próximo no gráfico. |
| **Exemplo de mensagem** | *Detectado o downgrade do pacote: NuGet.Versioning de 4.0.0 para 3.5.0. Referenciar o pacote diretamente do projeto para selecionar uma versão diferente.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0* |

## <a name="resolver-conflict-warnings"></a>Avisos de conflito de resolução

[NU1608](#nu1608)

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **Problema** | Um pacote de solução é maior do que permite que uma restrição de dependência. Em alguns casos, isso é intencional e o aviso pode ser suprimido. |
| **Causas comuns** | Um pacote referenciado diretamente por um projeto substituirão as restrições de dependência de outros pacotes.   |
| **Exemplo de mensagem** | *Versão do pacote detectado fora da restrição de dependência: x 1.0.0 requer y (= 1.0.0), mas a versão y 2.0.0 foi resolvido.* |

## <a name="package-fallback-warnings"></a>Avisos de fallback do pacote

[NU1701](#nu1701)

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **Problema** | *PackageTargetFallback/AssetTargetFallback* foi usado para selecionar os ativos de um pacote. Este é um aviso para informar o usuário que os ativos podem não ser 100% compatível. |
| **Causas comuns** | O pacote não dá suporte a estrutura do projeto. |
| **Exemplo de mensagem** | *Pacote 'NuGet.Versioning' foi restaurado usando 'portátil net45 + win8' em vez disso, a estrutura de destino do projeto 'netstandard1.5'. Esse pacote pode não ser totalmente compatível com o seu projeto.* |

## <a name="feed-warnings"></a>Avisos de feeds

[NU1801](#nu1801)

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **Problema** | Ocorreu um erro ao ler o feed quando `IgnoreFailedSources` está definido como true, convertendo-o para um aviso não fatal. Isso pode conter qualquer mensagem e é genérico. |
| **Causas comuns** | A fonte é inválida. |
| **Exemplo de mensagem** | N/D |

## <a name="nuget-internal-errors-and-warnings"></a>Avisos e erros internos do NuGet

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **Problema** | Um erro interno não específico do NuGet. |
| **Causas comuns** | Verifique os logs para obter mais informações |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **Problema** | Um aviso interno não específico do NuGet. |
| **Causas comuns** | Verifique os logs para obter mais informações |
