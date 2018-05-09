---
title: Maneiras de instalar os pacotes do NuGet
description: Descreve o processo de instalação de pacotes NuGet em um projeto, incluindo o que acontece no disco e com os arquivos de projeto aplicáveis.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 02/12/2018
ms.topic: overview
ms.openlocfilehash: 028fb9710e808974348d9cca3c56103c087d5390
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Maneiras diferentes de instalar um pacote NuGet

Os pacotes do NuGet serão baixados e instalados usando qualquer um dos métodos da tabela a seguir (veja [Instalar ferramentas de cliente do NuGet](../install-nuget-client-tools.md) se eles ainda não estiverem instalados). É possível recuperar o pacote de um cache, em vez de baixá-lo.

| Método | Descrição |
| --- | --- |
| CLI do dotnet.exe<br/>`dotnet add package <package_name>` | (Todas as plataformas) Recupera o pacote identificado por \<package_name\>, expande seu conteúdo para uma pasta no diretório atual e adiciona uma referência ao arquivo de projeto. Além disso, recupera e instala as dependências.<ul><li>[Instalar e usar um pacote (CLI do dotnet)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[comando dotnet add package](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| Interface do Usuário do Gerenciador de Pacotes (Visual Studio) | (Windows e Mac) Fornece uma interface do usuário por meio da qual você pode procurar, selecionar e instalar pacotes e suas dependências em um projeto a partir de uma fonte do pacote especificado. Adicione referências a pacotes instalados ao arquivo de projeto.<ul><li>[Instalar e usar um pacote (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Referência da interface do usuário do Gerenciador de Pacotes (Windows)](../tools/package-manager-ui.md)</li><li>[Incluir um pacote NuGet ao seu projeto (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Console do Gerenciador de Pacotes (Visual Studio)<br/>`Install-Package <package_name>` | (Somente Windows) Recupera e instala o pacote identificado por \<package_name\> de uma fonte selecionada em um projeto especificado na solução, depois adiciona uma referência ao arquivo de projeto. Além disso, recupera e instala as dependências.<ul><li>[Instalar e usar um pacote (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Guia do Console do Gerenciador de Pacotes](../tools/package-manager-console.md)</li></ul> |
| CLI do nuget.exe<br/>`nuget install <package_name>` | (Todas as plataformas) Recupera o pacote identificado por \<package_name\> e expande seu conteúdo em uma pasta no diretório atual; também pode recuperar todos os pacotes listados em um arquivo do `packages.config`. Também recupera e instala dependências, mas não altera arquivos de projeto ou `packages.config`.<ul><li>[comando install](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>O que acontece quando um pacote é instalado

Em poucas palavras, as diferentes ferramentas NuGet normalmente criam uma referência a um pacote no arquivo de projeto ou em `packages.config`, depois executam uma restauração de pacote, o que efetivamente instala o pacote. A exceção é `nuget install`, que apenas expande o pacote em uma pasta `packages` e não modifica nenhum outro arquivo.

O processo geral é o seguinte:

1. (Todas as ferramentas, exceto `nuget.exe`) Registre a versão e o identificador de pacote no arquivo de projeto ou em `packages.config`.

2. Adquira o pacote:
   - Verifique se o pacote (pelo identificador exato ou pelo número da versão) já está instalado na pasta *global-packages* conforme descrito em [Como gerenciar as pastas de pacotes globais e de cache](managing-the-global-packages-and-cache-folders.md).

   - Se o pacote não estiver armazenado na pasta *global-packages*, tente recuperá-lo das fontes listadas nos [arquivos de configuração](Configuring-NuGet-Behavior.md). Para fontes online, primeiro tente recuperar o pacote do cache, a menos que `-NoCache` esteja especificado com comandos `nuget.exe` ou `--no-cache` esteja especificado com `dotnet restore`. (O Visual Studio e o `dotnet add package` sempre usam o cache). Se for usado um pacote do cache, "CACHE" será exibido na saída. O cache tem um tempo de expiração de 30 minutos.

   - Se o pacote não estiver armazenado no cache, tente baixá-lo das fontes listadas na configuração. Se um pacote for baixado, "GET" e "OK" serão exibidos na saída.

   - Se o pacote não puder ser adquirido com êxito de nenhuma fonte, a instalação falhará neste ponto com um erro como [NU1103](../reference/errors-and-warnings.md#nu1103). Os erros de comandos `nuget.exe` mostram apenas a última fonte selecionada, mas implicam que o pacote não estava disponível de nenhuma fonte.

   Na aquisição do pacote, a ordem das fontes na configuração do NuGet pode ser aplicável:

   - No caso dos projetos que usam o formato PackageReference, o NuGet verifica primeiro a pasta local de fontes e os compartilhamentos de rede antes de verificar as fontes HTTP.

   - No caso dos projetos que usam o formato de gerenciamento `packages.config`, o NuGet usa a ordem das fontes na configuração. Uma exceção são as operações de restauração, caso em que a ordenação das fontes é ignorada e o NuGet usa o pacote da fonte que responder primeiro.

   - De modo geral, a ordem em que o NuGet verifica as fontes não é especialmente significativa, porque todos os pacotes fornecidos com um identificador e número de versão específicos são exatamente os mesmos em todas as fontes encontradas.

3. (Todas as ferramentas, exceto `nuget.exe`) salvam uma cópia do pacote e outras informações na pasta *http-cache*, conforme descrito em [Como gerenciar as pastas de pacotes globais e de cache](managing-the-global-packages-and-cache-folders.md).

4. Se o pacote for baixado, instale-o na pasta *global-packages* por usuário. O NuGet cria uma subpasta para cada identificador de pacote e, em seguida, cria subpastas para cada versão instalada do pacote.

5. Atualize outros arquivos de projeto e pastas:

    - Em caso de projetos que usam PackageReference, atualize o grafo de dependência do pacote armazenado em `obj/project.assets.json`. O conteúdo do pacote em si não é copiado para nenhuma pasta de projeto.
    - Em projetos que usam `packages.config`, copie as partes do pacote expandido que correspondem à estrutura de destino do projeto na pasta `packages` do projeto. (Quando `nuget install` é usado, todo o pacote expandido é copiado, pois `nuget.exe` não examina arquivos de projeto para identificar a estrutura de destino).
    - Atualize `app.config` e/ou `web.config` se o pacote usar [transformações de origem e arquivo de configuração](../create-packages/source-and-config-file-transformations.md).

6. Instale todas as dependências de nível inferior se não estiverem presentes no projeto. Esse processo pode atualizar versões do pacote, conforme descrito em [Resolução de dependências](../consume-packages/dependency-resolution.md).

7. (Somente no Visual Studio) Exiba o arquivo Leiame do pacote, se disponível, em uma janela do Visual Studio.

## <a name="related-articles"></a>Artigos relacionados

- [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/overview-and-workflow.md)
- [Localizando e escolhendo pacotes](../consume-packages/finding-and-choosing-packages.md)
- [Como gerenciar as pastas global-packages e de cache do NuGet](managing-the-global-packages-and-cache-folders.md)
- [Configuração do comportamento de NuGet](../consume-packages/configuring-nuget-behavior.md)
