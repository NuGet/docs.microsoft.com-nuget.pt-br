---
title: Formas de instalar pacotes NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Descreve o processo de instalação de pacotes NuGet em um projeto, incluindo o que acontece no disco e com os arquivos de projeto aplicáveis."
keywords: "instalar o NuGet, consumo de pacote NuGet, instalação de pacotes NuGet, referências de pacote NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3bae03e148a366388c10d08e83c89dac6ff56d06
ms.sourcegitcommit: 33436d122873249dbb20616556cd8c6783f38909
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Maneiras diferentes de instalar um pacote NuGet

Os pacotes NuGet são baixados e instalados usando qualquer um dos métodos a seguir (veja [Instalar ferramentas de cliente NuGet](../install-nuget-client-tools.md) se eles ainda não estiverem instalados):

| Método | Descrição |
| --- | --- |
| CLI do dotnet.exe<br/>`dotnet install <package_name>` | (Todas as plataformas) Baixa o pacote identificado por \<package_name\>, expande seu conteúdo para uma pasta no diretório atual e adiciona uma referência ao arquivo do projeto. Além disso, baixa e instala as dependências.<ul><li>[Instalar e usar um pacote (CLI do dotnet)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[Comandos dotnet](../tools/dotnet-commands.md)</li></ul> |
| Interface do Usuário do Gerenciador de Pacotes (Visual Studio) | (Windows e Mac) Fornece uma interface do usuário por meio da qual você pode procurar, selecionar e instalar pacotes e suas dependências em um projeto. Adicione referências a pacotes instalados ao arquivo de projeto.<ul><li>[Instalar e usar um pacote (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Referência da interface do usuário do Gerenciador de Pacotes (Windows)](../tools/package-manager-ui.md)</li><li>[Incluir um pacote NuGet ao seu projeto (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Console do Gerenciador de Pacotes (Visual Studio)<br/>`Install-Package <package_name>` | (Somente Windows) Baixa e instala o pacote identificado por \<package_name\> em um projeto especificado na solução, depois adiciona uma referência ao arquivo do projeto. Além disso, baixa e instala as dependências.<ul><li>[Instalar e usar um pacote (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Guia do Console do Gerenciador de Pacotes](../tools/package-manager-console.md)</li></ul> |
| CLI do nuget.exe<br/>`nuget install <package_name>` | (Todas as plataformas) Baixa o pacote identificado por \<package_name\> e expande seu conteúdo em uma pasta no diretório atual; também pode baixar todos os pacotes listados em um arquivo do `packages.config`. Também baixa e instala as dependências, mas não altera os arquivos do projeto.<ul><li>[comando install](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a>Processo de instalação geral

Em geral, o NuGet faz o seguinte ao receber uma solicitação de instalação de um pacote:

1. Adquira o pacote:
    - Verifique se o pacote solicitado já existe em um cache (veja [Gerenciar o cache do NuGet](managing-the-nuget-cache.md)).
    - Se o pacote não estiver armazenado no cache, tente baixá-lo das fontes listadas nos [arquivos de configuração](Configuring-NuGet-Behavior.md).
      - No caso dos projetos que usam o formato de referência `packages.config`, o NuGet usa a ordem das fontes na configuração.
      - No caso dos projetos que usam o formato PackageReference, o NuGet verifica primeiro as fontes que estão em pastas locais, em seguida, verifica as fontes de compartilhamentos de rede e depois as fontes HTTP (Internet).
      - De modo geral, a ordem em que o NuGet verifica as fontes não é especialmente significativa, porque todos os pacotes fornecidos com um identificador e número de versão específicos são exatamente os mesmos em todas as fontes encontradas.
    - Se o pacote for adquirido com êxito de uma das fontes, o NuGet o adicionará ao cache. Caso contrário, a instalação falhará.

1. Expanda o pacote no projeto.
    - Expandir significa descompactar o conteúdo do pacote em uma subpasta apropriada. Uma cópia do próprio `.nupkg` também é colocada na subpasta.
    - Se o pacote estiver sendo instalado em um projeto do Visual Studio ou do .NET Core, somente os arquivos relevantes à estrutura de destino do projeto serão expandidos. Quando é instalado usando a linha de comando do nuget.exe, ocorre a expansão de todos os assemblies.

1. Se o pacote for instalado no Visual Studio ou na CLI do dotnet, uma referência será adicionada ao arquivo de projeto apropriado (ou `packages.config` para alguns tipos de projeto no Visual Studio).

## <a name="related-topics"></a>Tópicos relacionados

- [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/overview-and-workflow.md)
- [Localizando e escolhendo pacotes](../consume-packages/finding-and-choosing-packages.md)
- [Configuração do comportamento de NuGet](../consume-packages/configuring-nuget-behavior.md)
- [Gerenciamento do cache do NuGet](managing-the-nuget-cache.md)
