---
title: Preterindo pacotes no nuget.org
description: Descrição detalhada sobre o processo de substituição de pacotes e como os clientes mostram essas informações
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096877"
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
> A mensagem personalizada só é mostrada em nuget.org, mas não nos clientes. Atualmente, clientes como `dotnet.exe` e o Gerenciador de pacotes NuGet não mostram a mensagem personalizada.

## <a name="client-experience-for-deprecated-packages"></a>Experiência do cliente para pacotes preteridos
Depois que um pacote tiver sido preterido, seus consumidores serão notificados sobre ele das seguintes maneiras (dependendo do cliente usado).

### <a name="visual-studio"></a>Visual Studio 
*Disponível a partir do Visual Studio 2019 versão 16,3*

O Visual Studio avisa sobre o uso de um pacote preterido na guia `Installed`. Ele mostrará um aviso para o pacote e suas informações de substituição (incluindo o motivo pelo qual ele foi preterido e o pacote alternativo a ser usado, se presente).

   ![Pacotes preteridos na guia Visual Studio instalada do Gerenciador de pacotes](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet. exe
*Disponível a partir do SDK do .NET 3,0*

Se você usar dotnet. exe, poderá executar o comando `dotnet list package --deprecated` na pasta da solução ou do projeto para obter uma lista de pacotes preteridos junto com as informações de substituição:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
