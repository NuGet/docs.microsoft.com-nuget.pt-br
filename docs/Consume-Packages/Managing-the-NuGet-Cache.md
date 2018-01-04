---
title: Como gerenciar o cache de pacotes no NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3932217d-780d-4bd1-ad15-767acd3e8870
description: "Como gerenciar os diferentes caches de pacote do NuGet que existem em um computador, os quais são usados durante a instalação ou restauração de pacotes."
keywords: Cache de pacote do NuGet, cache de pacote, caches do NuGet, gerenciar caches, cache local do NuGet, cache global do NuGet, comando locals do NuGet, limpar um cache
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6e76c219ba420eb285af20e67b26dcdceebb6bab
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="managing-the-nuget-cache"></a>Gerenciando o cache do NuGet

O NuGet gerencia vários caches locais para evitar o download de pacotes que já estão no computador e para fornecer suporte offline. O NuGet 2.8 ou superior reverterá automaticamente para o cache ao instalar ou reinstalar pacotes sem uma conexão de rede.

Locais de cache estão disponíveis usando o [comando locals](../tools/cli-ref-locals.md):

```
nuget locals all -list
```

A saída é a seguinte:

    http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
    packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
    global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
    temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder

Se você encontrar problemas de instalação do pacote ou se desejar garantir que você está instalando pacotes de uma galeria remota, use a opção `locals -clear`:

```
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

Observe que o gerenciamento de cache é compatível atualmente somente com a linha de comando do NuGet e não com o Visual Studio, nem por meio do Console do Gerenciador de Pacotes. Além disso, o gerenciamento de cache do 2.x não é compatível com o NuGet 3.6 e posterior.

Os seguintes erros podem ocorrer ao usar `nuget locals`:

* **Falha ao limpar os recursos locais: não é possível excluir um ou mais arquivos**
* **O diretório não está vazio**

Eles indicam que você não tem permissão para excluir arquivos no cache ou que um ou mais arquivos no cache estão sendo usados por outro processo, o qual precisa ser fechado para que tais arquivos possam ser removidos.
