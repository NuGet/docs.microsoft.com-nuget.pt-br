---
title: Criando pacotes do NuGet nativos | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 7a70d748-efe2-4f8f-a3fd-67ddb0f6214e
description: "Detalhes sobre a criação de pacotes do NuGet nativos que contém código C++ em vez do código gerenciado, para uso em projetos C++."
keywords: "Pacotes do NuGet nativos, pacotes do NuGet C++, pacotes de código nativo, voltado para projetos C++"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fa5baaa6ecbad0f5f6dd85d657679ffbbbc8a47a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="creating-native-packages"></a>Criando pacotes nativos

Um pacote nativo contém o código C++ nativo em vez do código gerenciado, permitindo que ele seja usado dentro de projetos C++. (Consulte [Pacotes C++ nativos](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages) na seção Consumir.)

Para ser consumido em um projeto C++, um pacote precisa ter como destino a estrutura `native`. No momento não há nenhum número de versão associado a essa estrutura, visto que o NuGet trata todos os projetos do C++ da mesma forma.

> [!Note]
> Lembre-se de incluir *nativo* na seção `<tags>` do seu `.nuspec` para ajudar outros desenvolvedores a encontrarem seu pacote pesquisando essa marca.

Pacotes do NuGet nativos voltados para `native` fornecerão arquivos nas pastas `\build`, `\content` e `\tools`. `\lib` não é usado neste caso (o NuGet não pode adicionar referências a um projeto C++ diretamente). Um pacote também pode incluir arquivos de destino e objetos no `\build` que o NuGet importará automaticamente para os projetos que consomem o pacote. Esses arquivos precisam ter o mesmo nome que a ID do pacote com as extensões `.targets` e/ou `.props`. Por exemplo, o pacote [cpprestsdk](https://nuget.org/packages/cpprestsdk/) inclui um arquivo `cpprestsdk.targets` em sua pasta `\build`.

A pasta `\build` pode ser usada para todos os pacotes do NuGet e não apenas pacotes nativos. A pasta `\build` respeita a estrutura de destino como as pastas `\content`, `\lib` e `\tools`. Isso significa que você pode criar as pastas `\build\net40` e `\build\net45`, e o NuGet importará os objetos e arquivos de destino para o projeto. (Não é necessário usar scripts do PowerShell para importar destinos do MSBuild.)
