---
title: NuGet referência de erros e avisos
description: Referência completa de avisos e erros emitidos do NuGet durante várias operações do NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 368a9554c5caf92b709f9b29e16b8a7cdb264eec
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818510"
---
# <a name="errors-and-warnings"></a>Erros e avisos

NuGet 4.3.0+, erros e avisos são numerados conforme descrito neste tópico e fornecem informações detalhadas para ajudá-lo a resolver os problemas envolvidos.

Os erros e avisos listados aqui estão disponíveis apenas com [com base em PackageReference](../consume-packages/package-references-in-project-files.md) 4.3.0+ NuGet e projetos. NuGet também respeita propriedades MSBuild para suprimir avisos ou elevá-las a erros. Para obter mais informações, consulte [como: suprimir avisos do compilador](/visualstudio/ide/how-to-suppress-compiler-warnings) na documentação do Visual Studio.

**Erros**

| Grupo | Números de erro |
| --- | --- |
| [Erros de entrada inválidos](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [Erros de pacote e projeto ausentes](#missing-package-and-project-errors) | [NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (anteriormente NU1607) [NU1108](#nu1108) (anteriormente NU1606) |
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
| [Pacotes assinados (criação e verificação)](#signed-packages-creation-and-verification)| [NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028) |

## <a name="invalid-input-errors"></a>Erros de entrada inválidos

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **Problema** | O projeto não contém um ou mais frameworks. |
| **Exemplo de mensagem** | *O projeto projA não especifica nenhuma estrutura de destino em c:\tmp\projA.csproj* |
| **Solução** | Adicionar um `TargetFramework` ou `TargetFrameworks` propriedade para o arquivo de projeto especificado. |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **Problema** | Combinação inválida de entradas, junto com uma palavra-chave criptografada. |
| **Exemplo de mensagem** | *'CLEAR' não pode ser usado em conjunto com outros valores* |
| **Solução** | Use limpar por si só e omitir todas as outras entradas. |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **Problema** | `PackageTargetFallback` e `AssetTargetFallback` fornecem um comportamento diferente para a seleção de recursos e não podem ser usados juntos. |
| **Exemplo de mensagem** | *PackageTargetFallback e AssetTargetFallback não podem ser usados juntos. Remova as referências de PackageTargetFallback(deprecated) do ambiente do projeto.* |
| **Solução** | Remover preterido `PackageTargetFallback` elemento do projeto. |

## <a name="missing-package-and-project-errors"></a>Erros de pacote e projeto ausentes

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **Problema** | Um grupo de dependência não ser resolvido. Esse é um problema genérico para tipos que não são pacotes ou projetos. |
| **Exemplo de mensagem** | *Não é possível resolver System.Missing para net45* |
| **Solução** | Abra o arquivo de projeto e examine a lista de suas dependências. Verifique se cada dependência existe nas fontes de pacote que você está usando, e o pacote dá suporte à estrutura de destino do projeto. |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **Problema** | O pacote não foi encontrado em qualquer fonte. |
| **Exemplo de mensagem** | *Não é possível encontrar o pacote System.Missing. Nenhum pacote existe com essa id na fonte (s): dotnet-core, dotnet roslyn, nuget.org* |
| **Solução** | Examine as dependências do projeto no Visual Studio para certificar-se de que você está usando o número de versão e de identificador de pacote correto. Também verifique se o [configuração NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica as origens do pacote seu pretende usar. Se você usar pacotes que tenham [o controle de versão semântico 2.0.0](../reference/package-versioning.md#semantic-versioning-200), certifique-se de que você está usando o V3 feed, `https://api.nuget.org/v3/index.json`, no [configuração NuGet](../consume-packages/Configuring-NuGet-Behavior.md). |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **Problema** | O identificador de pacote for encontrado, mas não é possível encontrar uma versão dentro do intervalo de dependência especificada em qualquer uma das fontes. O intervalo pode ser especificado por um pacote e não ao usuário. |
| **Exemplo de mensagem** | *Não é possível localizar o pacote NuGet.Versioning com a versão (> = 9.0.1)<br/> -versão (ões) de 30 encontrado em nuget.org [mais próximo de versão: 4.0.0]<br/> -versão (ões) de 10 encontrado em dotnet buildtools [mais próximo de versão: 4.0.0-rc-2129]<br/> -9 encontrado versão (ões) em NuGetVolatile [mais próximo de versão: 3.0.0-beta-00032]<br/> -encontrado versões 0 no núcleo do dotnet<br/> -encontrado versões 0 no roslyn dotnet* |
| **Solução** | Edite o arquivo de projeto para corrigir a versão do pacote. Também verifique se o [configuração NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica as origens do pacote seu pretende usar. Talvez seja necessário alterar a versão de requeted se esse pacote é referenciado pelo projeto diretamente. |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **Problema** | O projeto especificado para o intervalo de dependência a uma versão estável, mas nenhuma versão estável foram encontrado nesse intervalo. As versões de pré-lançamento foram encontradas, mas não são permitidas. |
| **Exemplo de mensagem** | *Não é possível localizar um pacote estável NuGet.Versioning com a versão (> = 3.0.0)<br/> -versão (ões) de 10 encontrado em dotnet buildtools [mais próximo de versão: 4.0.0-rc-2129]<br/> -versão (ões) de 9 encontrado em NuGetVolatile [mais próximo de versão: 3.0.0-beta-00032] <br/> -Encontrado versões 0 no núcleo do dotnet<br/> -encontrado versões 0 no roslyn dotnet* |
| **Solução** |  Edite o intervalo de versão no arquivo de projeto para incluir as versões de pré-lançamento. Consulte [controle de versão do pacote](../reference/Package-Versioning.md). |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **Problema** | Um ProjectReference aponta para um arquivo que não existe. |
| **Exemplo de mensagem** | *Referência de projeto não existe 'c:\a.csproj'. Verifique se a referência de projeto é válida e se existe o arquivo de projeto.* |
| **Solução** | Edite o arquivo de projeto para corrigir o caminho para o projeto referenciado ou para remover a referência ao mesmo tempo, se ele não for mais necessário. |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **Problema** | O arquivo de projeto existe, mas nenhuma informação de restauração foi fornecida para ele. |
| **Exemplo de mensagem** | *Não é possível ler as informações de projeto para 'c:\a.csproj'. O arquivo de projeto pode ser inválidos ou ausentes destinos necessários para a restauração.* |
| **Solução** | No Visual Studio, o erro pode significar que o projeto é descarregado, em cujo caso recarregar o projeto. Na linha de comando, isso pode significar que o arquivo está corrompido ou que não contenha personalizado "após imports" necessário para restauração ler o projeto de destino. Verifique se o arquivo de projeto é válido e contém um destino de "depois imports". |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **Problema** | Restrições de dependência não podem ser resolvidas. |
| **Exemplo de mensagem** | *Não foi possível satisfazer solicitações conflitantes para {id}: {caminho conflito} Framework: {gráfico de destino}* |
| **Solução** | Edite o arquivo de projeto para especificar intervalos mais abertos para a dependência em vez de uma versão exata. |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a>NU1107 (anteriormente NU1607)

| | |
| --- | --- |
| **Problema** | Não é possível resolver as restrições de dependência entre pacotes. |
| **Exemplo de mensagem** | *Conflito de versão detectado para NuGet.Versioning. Referenciar o pacote diretamente do projeto para resolver esse problema.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)* |
| **Solução** | Pacotes com restrições de dependência em versões exatas não permitir que outros pacotes para aumentar a versão, se necessário. Adicione uma referência para o pacote diretamente (no arquivo de projeto) com a versão exata necessária. |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (anteriormente NU1606)

| | |
| --- | --- |
| **Problema** | Foi detectada uma dependência circular. |
| **Exemplo de mensagem** | *Ciclo detectado: A -> B -> um* |
| **Solução** | O pacote foi criado incorretamente. entre em contato com o proprietário do pacote para corrigir o erro. |

## <a name="compatibility-errors"></a>Erros de compatibilidade

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **Problema** | Um projeto de dependência não contém uma estrutura compatível com o projeto atual. Normalmente, a estrutura de destino do projeto é uma versão superior do projeto de consumo. |
| **Exemplo de mensagem** | *ServerWeb do projeto não é compatível com netstandard1.3 (. Identificadores de NETStandard, versão = v 1.3). Projeto suporta ServerWeb:<br/> -netstandard1.6 (. Identificadores de NETStandard, versão = v 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = v 1.0)* |
| **Solução** | Altere a estrutura de destino do projeto para uma versão igual ou menor que o projeto de consumo. |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **Problema** | Um pacote de dependência não contém qualquer ativos compatíveis com o projeto. |
| **Exemplo de mensagem** | *Pacote System.ComponentModel.EventBasedAsync 4.0.11 não é compatível com netstandard1.3 (. Identificadores de NETStandard, versão = v 1.3). Pacote suporta System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, versão = v 1.0)<br/> -monotouch10 (MonoTouch, versão = v 1.0)<br/> -net45 (. NETFramework, Version = v 4.5)<br/> -netcore50 (. NETCore, Version = v 5.0)<br/> -netstandard1.0 (. Identificadores de NETStandard, versão = v 1.0)<br/> -portátil net45 + win8 + wp8 + wpa81 (. NETPortable, Version = v0.0, perfil = Profile259)<br/> -win8 (Windows, versão = v 8.0)<br/> -wp8 (WindowsPhone, versão = v 8.0)<br/> -wpa81 (WindowsPhoneApp, versão = 8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|
| **Solução** | Altere a estrutura de destino do projeto para um com suporte no pacote. |

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **Problema** | O pacote não oferece suporte para o projeto `RuntimeIdentifier`. |
| **Exemplo de mensagem** | *System.Example 1.0.0 fornece uma referência de tempo de compilação do assembly para o. dll em net461, mas não há nenhum tempo de execução do assembly compatível.* |
| **Solução** | Alterar o `RuntimeIdentifier` valores usados no projeto, conforme necessário. |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **Problema** | O pacote requer recursos ou estruturas atualmente não há suportadas à versão instalada do NuGet. |
| **Exemplo de mensagem** | *O pacote 'NuGet.Versioning' requer o NuGet versão de cliente '5.0.0' ou superior, mas a versão atual do NuGet é '4.3.0'.* |
| **Solução** | Instale uma versão mais recente do NuGet. Consulte [ferramentas de cliente de instalar o NuGet](../install-nuget-client-tools.md). |

## <a name="invalid-input-warnings"></a>Avisos de entrada inválidos

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **Problema** | A restauração do projeto está tentando operar em não foi encontrado. |
| **Exemplo de mensagem** | *A pasta 'c:\projects\a' não contém um projeto para restaurar.* |
| **Solução** | Execute a restauração do nuget em uma pasta que contém um projeto. |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **Problema** | `RuntimeSupports` contém um perfil inválido. Normalmente, o oferece suporte a perfil não foi encontrado em um `runtime.json` arquivo dos pacotes de dependência atual.|
| **Exemplo de mensagem** | *Perfil de compatibilidade desconhecido: aaa* |
| **Solução** | Verifique o `RuntimeSupports` valor em seu projeto. |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **Problema** | Um projeto de dependência não importa destinos de restauração do NuGet. Isso é semelhante a NU1105, mas aqui o projeto será ignorado e ignorado em vez fazendo com que todos os de restauração falhe. Em soluções complexas geralmente há outros tipos de projetos que podem não oferecer suporte a restauração. |
| **Exemplo de mensagem** | *Ignorando a restauração para o projeto 'c:\a.csproj'. O arquivo de projeto pode ser inválidos ou ausentes destinos necessários para a restauração.* |
| **Solução** | Isso pode acontecer para projetos que não importar props/destinos comuns que importar automaticamente a restauração. Se o projeto não precisa ser restaurados isso pode ser ignorado. Caso contrário, edite o projeto afetado para adicionar destinos de restauração. |

## <a name="unexpected-package-version-warnings"></a>Avisos de versão de pacote inesperado

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **Problema** | Uma dependência de projeto foi aumentada para uma versão maior do que o projeto especificado. |
| **Exemplo de mensagem** | *Dependência especificada foi NuGet.Versioning (> = 3.5.0) mas acabou com NuGet.Versioning 4.0.0.* |
| **Solução** | Atualize a dependência no projeto para uma versão apropriada. |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **Problema** | Uma dependência de pacote não tem um limite inferior. Isso não permite que a restauração localizar o *melhor correspondência*. Cada restauração flutua para baixo ao tentar encontrar uma versão inferior que pode ser usada. Isso significa que a restauração fica online para verificar se todas as fontes de cada vez em vez de usar os pacotes que já existem na pasta de pacote do usuário. |
| **Exemplo de mensagem** | *NuGet. Packaging 4.0.0 não fornece um limite inferior inclusivo de dependência NuGet.Versioning (3.5.0 >). Uma melhor correspondência aproximada de 3.6.0 foi resolvida.* |
| **Solução** | Isso geralmente é um erro de criação de pacote. Entre em contato com o autor do pacote para resolver o problema. |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **Problema** | Uma dependência de pacote especificado de uma versão que não pôde ser encontrada. Normalmente, as origens do pacote contém a versão inferior esperado. Uma versão mais recente foi usada em vez disso, o que é diferente do que o pacote foi criado.<br/><br/>Isso significa que a restauração não localizou o *melhor correspondência*. Cada restauração flutua para baixo ao tentar encontrar uma versão inferior que pode ser usada. Isso significa que a restauração fica online para verificar se todas as fontes de cada vez em vez de usar os pacotes que já existem na pasta de pacote do usuário. |
| **Exemplo de mensagem** | NuGet. Packaging 4.0.0 depende NuGet.Versioning (> = 4.0.0) mas 4.0.0 não foi encontrado. Uma melhor correspondência aproximada de 5.0.0 foi resolvida. |
| **Solução** | Se o pacote esperado não foi liberado, em seguida, isso pode ser um erro de criação de pacote. Entre em contato com o autor do pacote para resolver o problema. Se o pacote foi liberado, verifique se ela está disponível nas fontes de pacote que você está usando. Se usar uma fonte particular, você precisará atualizar o pacote em que o feed. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **Problema** | Uma dependência de projeto não define um limite inferior.<br/><br/>Isso significa que a restauração não localizou o *melhor correspondência*. Cada restauração flutua para baixo ao tentar encontrar uma versão inferior que pode ser usada. Isso significa que a restauração fica online para verificar se todas as fontes de cada vez em vez de usar os pacotes que já existem na pasta de pacote do usuário. |
| **Exemplo de mensagem** | *Projeto dependência NuGet.Versioning (< = 9.0.0) doe não contêm um limite inferior inclusivo. Inclua um limite inferior na versão de dependência para garantir resultados consistentes de restauração.* |
| **Solução** | Atualize o projeto `PackageReference` `Version` atributo para incluir um limite inferior. |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **Problema** | Um pacote de dependência especificou uma restrição de versão em uma versão superior de um pacote de restauração finalmente resolvida. Ou seja, devido a "mais próximo de wins" regra durante a resolução de pacotes, um pacote mais próximo no gráfico pode ter substituído um pacote distante. |
| **Exemplo de mensagem** | *Detectado o downgrade do pacote: NuGet.Versioning de 4.0.0 para 3.5.0. Referenciar o pacote diretamente do projeto para selecionar uma versão diferente.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0* |
| **Solução** | Adicione uma referência direta ao projeto para a versão posterior do pacote que você deseja usar. |

## <a name="resolver-conflict-warnings"></a>Avisos de conflito de resolução

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **Problema** | Um pacote resolvido é maior do que permite que uma restrição de dependência. Isso significa que um pacote referenciado diretamente por um projeto substitui as restrições de dependência de outros pacotes.|
| **Exemplo de mensagem** | *Versão do pacote detectado fora da restrição de dependência: x 1.0.0 requer y (= 1.0.0), mas a versão y 2.0.0 foi resolvido.* |
| **Solução** | Em alguns casos, isso é intencional e o aviso pode ser suprimido. Caso contrário, altere a referência do projeto para o pacote para ampliar suas restrições de versão. |

## <a name="package-fallback-warnings"></a>Avisos de fallback do pacote

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **Problema** | `PackageTargetFallback` / `AssetTargetFallback` foi usado para selecionar os ativos de um pacote. O aviso de permitir que os usuários saibam que os ativos podem não ser 100% compatível. |
| **Exemplo de mensagem** | *Pacote 'NuGet.Versioning' foi restaurado usando 'portátil net45 + win8' em vez disso, a estrutura de destino do projeto 'netstandard1.5'. Esse pacote pode não ser totalmente compatível com o seu projeto.* |
| **Solução** | Altere a estrutura de destino do projeto para um com suporte no pacote. |

## <a name="feed-warnings"></a>Avisos de feeds

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **Problema** | Ocorreu um erro ao ler o feed quando `IgnoreFailedSources` está definido como true, convertendo-o para um aviso não fatal. Isso pode conter qualquer mensagem e é genérico. |
| **Exemplo de mensagem** | N/D |
| **Solução** | Edite sua configuração para especificar fontes válidos. |

## <a name="nuget-internal-errors-and-warnings"></a>Avisos e erros internos do NuGet

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **Problema** | Um erro interno não específico do NuGet. |
| **Solução** | Verifique os logs para obter mais informações |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **Problema** | Um aviso interno não específico do NuGet. |
| **Solução** | Verifique os logs para obter mais informações |

## <a name="signed-packages-creation-and-verification"></a>Pacotes assinados (criação e verificação)

*NuGet 4.6.0+*

[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)

### <a name="nu3000"></a>NU3000

| | |
| --- | --- |
| **Problema** | Um erro não específico relacionado à assinatura do pacote e assinado verificação do pacote. |
| **Solução** | Verifique os logs para obter mais informações. |

### <a name="nu3001"></a>NU3001

| | |
| --- | --- |
| **Problema** | Argumentos inválidos para o o [sign comando](../tools/cli-ref-sign.md) ou [Verifique se o comando](../tools/cli-ref-verify.md). |
| **Solução** | Verifique e corrija os argumentos fornecidos. |

### <a name="nu3002"></a>NU3002

| | |
| --- | --- |
| **Problema** | O `-Timestamper` opção não foi especificada com o [comando de entrada do nuget](../tools/cli-ref-sign.md). |
| **Exemplo de mensagem** | *O '-Timestamper' opção não foi fornecida. O pacote assinado não poderá ser a marca.* |
| **Solução** | Especifique o `-Timestamper` com a opção `nuget sign`. |

### <a name="nu3004"></a>NU3004

| | |
| --- | --- |
| **Problema** | Um pacote não assinado foi fornecido para o [nuget Verifique se o comando](../tools/cli-ref-verify.md). |
| **Solução** | Executar `nuget verify` com um pacote assinado. Consulte [assinar um pacote](../create-packages/Sign-a-Package.md). |

### <a name="nu3008"></a>NU3008

| | |
| --- | --- |
| **Problema** | Falha na verificação de integridade do pacote, que significa que um pacote assinado foi violado desde que está sendo assinado. |
| **Solução** | Examine o computador com um software antivírus. Remova o pacote do computador, reinstale-o e tente a operação novamente. Se o problema persistir, contate o proprietário da origem do pacote e o pacote. |

### <a name="nu3018"></a>NU3018

| | |
| --- | --- |
| **Problema** | Falha na criação da cadeia de certificados para a assinatura principal. O certificado de autenticação primário é confiável, revogado, ou informações de revogação do certificado não estão disponíveis. |
| **Exemplo de mensagem** | *Aviso: NU3018: A função de revogação não pôde verificar a revogação do certificado.* |
| **Solução** | Use um certificado válido e não confiáveis. Verifique a conectividade com a internet. |

### <a name="nu3028"></a>NU3028

| | |
| --- | --- |
| **Problema** | Falha na criação da cadeia de certificados para a assinatura de carimbo de hora. O certificado de assinatura de carimbo de hora é confiável, revogado, ou informações de revogação do certificado não estão disponíveis. |
| **Exemplo de mensagem** | *Aviso: NU3028: A função de revogação não pôde verificar a revogação do certificado.* |
| **Solução** | Use um certificado válido e não confiáveis. Verifique a conectividade com a internet. |
