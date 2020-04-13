---
title: Depreciando pacotes em nuget.org
description: Descrição detalhada sobre o processo de depreciação de pacotes e como os clientes mostram essas informações
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "74096877"
---
# <a name="deprecating-packages"></a>Depreciação de pacotes

Você pode depreciar um pacote se você não mantiver mais um pacote ou se quiser encorajar os consumidores do seu pacote a se mudarem para outro pacote. 

A depreciação do pacote é diferente da **deslistagem** do seu pacote, conforme explicado abaixo:
* **A deslistagem de** um pacote impede sua descoberta porque está escondida nos resultados de pesquisa. 
* **Depreciar** um pacote permite que os consumidores existentes do seu pacote descubram se eles o instalaram ou foram usados em seus projetos. Ele também permite que eles saibam o motivo da depreciação e um pacote recomendado alternativo, conforme especificado por você (o editor do pacote). Depreciar um pacote não deslista o pacote. 

Como editor, você pode optar por deslistar, bem como depredar pacotes.

## <a name="deprecation-workflow"></a>Fluxo de trabalho de depreciação
1. Para depreciar um pacote, vá para **Gerenciar pacotes** e **selecione Depreciação**:

    ![Vá para depreciar a opção de pacote](media/deprecation-select-option.png)

2. Selecione a versão que deseja depreciar. Se você quiser depreciar todas as versões, escolha Selecionar a opção **Selecionar todas as versões.**

    ![Selecione versões do pacote para depreciar](media/deprecation-select-version.png)

3. Escolha uma razão para depreciação. Se o pacote não for mais mantido, escolha a opção **Legado.** Se a versão específica tiver um bug crítico, escolha a opção **tem bugs críticos.** Por qualquer outra razão, selecione **Outros**. Você sempre pode especificar um pacote recomendado alternativo (e uma versão) e uma mensagem personalizada para os proprietários. 

    ![Selecione razões para recomendação de pacote alternativo e mensagem personalizada](media/deprecation-save.png)

> [!Note]
> A mensagem personalizada só é mostrada em nuget.org mas não dos clientes. Atualmente, clientes `dotnet.exe` como e o NuGet Package Manager não mostram a mensagem personalizada.

## <a name="client-experience-for-deprecated-packages"></a>Experiência do cliente para pacotes preteridos
Uma vez que um pacote tenha sido preterido, seus consumidores são notificados sobre ele das seguintes maneiras (dependendo do cliente utilizado).

### <a name="visual-studio"></a>Visual Studio 
*Disponível a partir do Visual Studio 2019 versão 16.3*

Visual Studio avisa sobre o uso de um `Installed` pacote preterido na guia. Ele mostrará um aviso para o pacote e suas informações de depreciação (incluindo a razão pela qual foi preterido e o pacote alternativo para usar em seu lugar, se presente).

   ![Pacotes depreciados no Visual Studio instalado guia do gerenciador de pacotes](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*Disponível a partir de .NET SDK 3.0*

Se você usar dotnet.exe, você `dotnet list package --deprecated` pode executar o comando na solução ou pasta do projeto para obter uma lista de pacotes depreciados, juntamente com as informações de depreciação:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
