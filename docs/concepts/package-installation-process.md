---
title: O que acontece quando um pacote é instalado?
description: Informações detalhadas sobre o processo de instalação do pacote
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 5676239bedb7f8fbe9f74725864afd297405d5c1
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842327"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>O que acontece quando um pacote NuGet é instalado?

Em poucas palavras, as diferentes ferramentas NuGet normalmente criam uma referência a um pacote no arquivo de projeto ou em `packages.config`, depois executam uma restauração de pacote, o que efetivamente instala o pacote. A exceção é `nuget install`, que apenas expande o pacote em uma pasta `packages` e não modifica nenhum outro arquivo.

O processo geral é o seguinte:

1. (Todas as ferramentas, exceto `nuget.exe`) Registre a versão e o identificador de pacote no arquivo de projeto ou em `packages.config`.

   Se a ferramenta de instalação for o Visual Studio ou a CLI do dotnet, primeiro a ferramenta tentará instalar o pacote. Se ele for incompatível, o pacote não será adicionado ao arquivo de projeto nem a `packages.config`.

2. Adquira o pacote:
   - Verifique se o pacote (pelo identificador exato ou pelo número da versão) já está instalado na pasta *global-packages* conforme descrito em [Como gerenciar as pastas de pacotes globais e de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

   - Se o pacote não estiver armazenado na pasta *global-packages*, tente recuperá-lo das fontes listadas nos [arquivos de configuração](../consume-packages/Configuring-NuGet-Behavior.md). Para fontes online, primeiro tente recuperar o pacote do cache HTTP, a menos que `-NoCache` seja especificado com comandos `nuget.exe` ou que `--no-cache` seja especificado com `dotnet restore`. (O Visual Studio e o `dotnet add package` sempre usam o cache). Se for usado um pacote do cache, "CACHE" será exibido na saída. O cache tem um tempo de expiração de 30 minutos.

   - Se o pacote não estiver no cache HTTP, tente baixá-lo nas fontes listadas na configuração. Se um pacote for baixado, "GET" e "OK" serão exibidos na saída. O NuGet registra o tráfego HTTP em log no nível de detalhes normal.

   - Se o pacote não puder ser adquirido com êxito de nenhuma fonte, a instalação falhará neste ponto com um erro como [NU1103](../reference/errors-and-warnings/NU1103.md). Os erros de comandos `nuget.exe` mostram apenas a última fonte selecionada, mas implicam que o pacote não estava disponível de nenhuma fonte.

   Na aquisição do pacote, a ordem das fontes na configuração do NuGet pode ser aplicável:

   - O NuGet verifica a pasta local de fontes e os compartilhamentos de rede antes de verificar as fontes HTTP.

3. Salve uma cópia do pacote e outras informações na pasta *http-cache*, conforme descrito em [Como gerenciar os pacotes globais e as pastas de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

4. Se o pacote for baixado, instale-o na pasta *global-packages* por usuário. O NuGet cria uma subpasta para cada identificador de pacote e, em seguida, cria subpastas para cada versão instalada do pacote.

5. O NuGet instala as dependências do pacote conforme necessário. Esse processo pode atualizar versões do pacote, conforme descrito em [Resolução de dependências](../consume-packages/dependency-resolution.md).

6. Atualize outros arquivos de projeto e pastas:

    - Em caso de projetos que usam PackageReference, atualize o grafo de dependência do pacote armazenado em `obj/project.assets.json`. O conteúdo do pacote em si não é copiado para nenhuma pasta de projeto.
    - Atualize `app.config` e/ou `web.config` se o pacote usar [transformações de origem e arquivo de configuração](../create-packages/source-and-config-file-transformations.md).

7. (Somente no Visual Studio) Exiba o arquivo Leiame do pacote, se disponível, em uma janela do Visual Studio.

Aproveite sua programação produtiva com pacotes do NuGet.
