---
title: Preterindo pacotes no nuget.org
description: Descrição detalhada sobre o processo de substituição de pacotes e como os clientes mostram essas informações
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 4a6dbd645cb72b0085fd0347def58ade134fc5ee
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726958"
---
# <a name="deprecating-packages"></a>Substituição de pacotes

Você poderá substituir um pacote se não mantiver mais um pacote ou se desejar incentivar os consumidores do pacote a migrar para outro pacote. 

A substituição do pacote é diferente de **deslistar** o pacote, conforme explicado abaixo:
* A **deslistação** de um pacote impede sua descoberta porque está oculta nos resultados da pesquisa. 
* A **substituição** de um pacote permite que os consumidores existentes do pacote descubram se eles o têm instalado ou usados em seus projetos. Ele também permite que eles saibam o motivo da substituição e um pacote recomendado alternativo, conforme especificado por você (o fornecedor do pacote). A substituição de um pacote não lista o pacote. 

Como Publicador, você pode optar por deslistar, bem como substituir pacotes.

## <a name="deprecation-workflow"></a>Fluxo de trabalho de substituição
1. Para substituir um pacote, vá para **gerenciar pacotes** e selecione **reprovação**:

    ![Ir para a opção de pacote obsoleto](media/deprecation-select-option.png)

2. Selecione a versão que deseja substituir. Se você quiser substituir toda a versão, escolha a opção **selecionar todas as versões** .

    ![Selecionar versões de pacote para preterir](media/deprecation-select-version.png)

3. Escolha um motivo para a reprovação. Se o pacote não for mais mantido, escolha a opção **herdada** . Se a versão específica tiver um bug crítico, escolha a opção **tem bugs críticos** . Por qualquer outro motivo, selecione **outro**. Você sempre pode especificar um pacote recomendado alternativo (e versão) e uma mensagem personalizada para os proprietários. 

    ![Selecionar motivos da recomendação do pacote alternativo e da mensagem personalizada](media/deprecation-save.png)

> [!Note]
> A mensagem personalizada só é mostrada em nuget.org, mas não nos clientes. atualmente, clientes como `dotnet.exe` o e o NuGet Gerenciador de Pacotes não mostram a mensagem personalizada.

## <a name="client-experience-for-deprecated-packages"></a>Experiência do cliente para pacotes preteridos
Depois que um pacote tiver sido preterido, seus consumidores serão notificados sobre ele das seguintes maneiras (dependendo do cliente usado).

### <a name="visual-studio"></a>Visual Studio 
*disponível a partir do Visual Studio 2019 versão 16,3*

Visual Studio avisa sobre o uso de um pacote preterido na `Installed` guia. Ele mostrará um aviso para o pacote e suas informações de substituição (incluindo o motivo pelo qual ele foi preterido e o pacote alternativo a ser usado, se presente).

   ![pacotes preteridos na guia Visual Studio instalados do gerenciador de pacotes](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*Disponível a partir do SDK do .NET 3,0*

Se você usar dotnet.exe, poderá executar o comando `dotnet list package --deprecated` na pasta da solução ou do projeto para obter uma lista de pacotes preteridos junto com as informações de substituição:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```

## <a name="transfer-popularity-to-a-newer-package"></a>Transferir a popularidade para um pacote mais recente

Os autores de pacotes que Preteriram um pacote herdado podem optar por transferir sua "popularidade" para um pacote mais recente para aumentar a classificação de pesquisa do pacote mais recente. Isso ajuda os clientes a descobrir o pacote mais recente em vez do pacote preterido.

Por exemplo, digamos que eu tenha dois pacotes:

* Meu pacote herdado preterido, `Contoso.Legacy` com downloads 3 milhões
* Meu pacote mais recente, `Contoso.Latest` com 5 downloads

NuGet. org prefere resultados de pesquisa com downloads/popularidade mais altos. Dada a consulta de pesquisa "contoso", meu pacote preterido `Contoso.Legacy` provavelmente será classificado acima do meu pacote mais recente `Contoso.Latest` nos resultados da pesquisa.

Para resolver esse problema, posso aplicar para transferir a popularidade do meu pacote herdado preterido para meu pacote mais recente. Isso faria com que `Contoso.Latest` a classificação seja mais alta nos resultados da pesquisa, enquanto a `Contoso.Legacy` classificação era menor. Somente as pontuações de popularidade interna para os pacotes são impactadas, a contagem de download real para cada pacote não será afetada.

> [!Note]
> As transferências de popularidade podem tornar significativamente mais difícil para os consumidores encontrarem o pacote herdado.

Consulte a tabela abaixo para obter uma ideia concreta de como uma transferência de popularidade pode afetar as classificações de pesquisa para a consulta "contoso":

| Pesquisar classificação    | Antes da transferência de popularidade        | Após a transferência da popularidade         |
|----------------   |--------------------------------   |--------------------------------   |
| 1                 | *Contoso. Legacy, downloads do 3M*    | *Contoso. mais recente, 5 downloads*     |
| 2                 | Contoso. scanner, downloads de 2M     | Contoso. scanner, downloads de 2M     |
| 3                 | Downloads de contoso. Core, 1.5 M     | Downloads de contoso. Core, 1.5 M     |
| 4                 | Contoso. UI, 1 milhão de downloads          | Contoso. UI, 1 milhão de downloads          |
| ...               | ...                               | ...                               |
| 20                | *Contoso. mais recente, 5 downloads*     | *Contoso. Legacy, downloads do 3M*    |

### <a name="popularity-transfer-application-process"></a>Processo de aplicativo de transferência de popularidade

1. Examine os [requisitos de transferência de popularidade](#popularity-transfer-requirements).
2. Email [account@nuget.org](mailto:account@nuget.org) com o pacote preterido cuja popularidade deve ser transferida e a lista de pacotes estáveis que devem receber a transferência de popularidade.

Depois que o aplicativo for enviado, você será notificado sobre a aceitação ou rejeição do seu aplicativo (com os critérios que causaram a rejeição). Talvez seja necessário fazer outras perguntas de identificação para confirmar a identidade do proprietário.

#### <a name="popularity-transfer-requirements"></a>Requisitos de transferência de popularidade

* Os pacotes herdados e os novos pacotes devem compartilhar todos os proprietários.
* Os novos pacotes devem estar claramente relacionados aos pacotes herdados na nomenclatura e na função (ou seja, uma evolução ou uma próxima geração).
* Todas as versões dos pacotes herdados devem ser preteridas e apontar para os novos pacotes que recebem a transferência.
* a transferência de popularidade não deve causar confusão para NuGet usuários ou worsen a experiência de pesquisa NuGet.
* Os novos pacotes devem ter uma versão estável.
* O pacote herdado não deve receber transferências de popularidade de outro pacote preterido.

### <a name="advanced-popularity-transfer-scenarios"></a>Cenários de transferência de popularidade avançada

#### <a name="package-consolidations"></a>Consolidações de pacote

Posso transferir a popularidade de vários pacotes preteridos em favor de um único pacote novo. Por exemplo, digamos que tenha três pacotes:

* Meu primeiro pacote herdado preterido, `Contoso.Legacy1`
* Meu segundo pacote herdado preterido, `Contoso.Legacy2`
* Meu novo pacote consolidado, `Contoso.Latest`

Depois de preterir `Contoso.Legacy1` e `Contoso.Legacy2` , posso aplicar para transferir sua popularidade para o `Contoso.Latest` .

#### <a name="package-splits"></a>Divisões de pacote

Uma popularidade de pacote preterida pode ser transferida para e dividida entre até 5 pacotes mais recentes. Isso será útil se a funcionalidade de um pacote preterido tiver sido dividida entre vários novos pacotes. Por exemplo, digamos que tenha três pacotes:

* Meu pacote herdado preterido, `Contoso.Legacy`
* Meu primeiro pacote novo, `Contoso.Web`
* Meu segundo pacote novo, `Contoso.Cloud`

`Contoso.Legacy` inclui a funcionalidade da Web e da nuvem, mas decidi separar essa funcionalidade em diferentes pacotes para a próxima geração. Depois de preterir `Contoso.Legacy` , posso aplicar para transferir sua popularidade para o `Contoso.Web` e o `Contoso.Cloud` .

> [!Warning]
> A popularidade transferida será dividida uniformemente entre todos os novos pacotes. Como resultado, é recomendável transferir a popularidade do pacote preterido para o mínimo de pacotes possível.

#### <a name="popularity-transfer-chains"></a>Cadeias de transferência de popularidade

Um pacote preterido não poderá transferir sua popularidade se ele já estiver recebendo popularidade de outro pacote preterido. Por exemplo, digamos que tenho 3 pacotes:

* Meu pacote herdado preterido, `Contoso.First`
* Meu pacote herdado preterido, `Contoso.Second`
* Meu novo pacote, `Contoso.Latest`

Se `Contoso.First` transferir sua popularidade `Contoso.Second,` para, então, `Contoso.Second` não poderá transferir sua popularidade para `Contoso.Latest` . Em vez disso, recomendamos transferir a popularidade de e para , de acordo `Contoso.First` com o cenário de `Contoso.Second` `Contoso.Latest` [consolidações de](#package-consolidations) pacotes.
