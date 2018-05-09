---
title: Criar pacotes nativos do NuGet
description: Detalhes sobre a criação de pacotes do NuGet nativos que contém código C++ em vez do código gerenciado, para uso em projetos C++.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 1fa8bf23a3fbed686b99f1c783b0ce55b373e548
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="creating-native-packages"></a>Criando pacotes nativos

Um pacote nativo contém o código C++ nativo em vez do código gerenciado, permitindo que ele seja usado dentro de projetos C++. (Consulte [Pacotes C++ nativos](../consume-packages/finding-and-choosing-packages.md#native-c-packages) na seção Consumir.)

Para ser consumido em um projeto C++, um pacote precisa ter como destino a estrutura `native`. No momento não há nenhum número de versão associado a essa estrutura, visto que o NuGet trata todos os projetos do C++ da mesma forma.

> [!Note]
> Lembre-se de incluir *nativo* na seção `<tags>` do seu `.nuspec` para ajudar outros desenvolvedores a encontrarem seu pacote pesquisando essa marca.

Pacotes do NuGet nativos voltados para `native` fornecerão arquivos nas pastas `\build`, `\content` e `\tools`. `\lib` não é usado neste caso (o NuGet não pode adicionar referências a um projeto C++ diretamente). Um pacote também pode incluir arquivos de destino e objetos no `\build` que o NuGet importará automaticamente para os projetos que consomem o pacote. Esses arquivos precisam ter o mesmo nome que a ID do pacote com as extensões `.targets` e/ou `.props`. Por exemplo, o pacote [cpprestsdk](https://nuget.org/packages/cpprestsdk/) inclui um arquivo `cpprestsdk.targets` em sua pasta `\build`.

A pasta `\build` pode ser usada para todos os pacotes do NuGet e não apenas pacotes nativos. A pasta `\build` respeita a estrutura de destino como as pastas `\content`, `\lib` e `\tools`. Isso significa que você pode criar as pastas `\build\net40` e `\build\net45`, e o NuGet importará os objetos e arquivos de destino para o projeto. (Não é necessário usar scripts do PowerShell para importar destinos do MSBuild.)
