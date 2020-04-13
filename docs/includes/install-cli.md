---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610525"
---
#### <a name="windows"></a><span data-ttu-id="f97e5-101">Windows</span><span class="sxs-lookup"><span data-stu-id="f97e5-101">Windows</span></span>

> [!Note]
> <span data-ttu-id="f97e5-102">O NuGet.exe 5.0 e posteriores exigem o .NET Framework 4.7.2 ou posterior para executar.</span><span class="sxs-lookup"><span data-stu-id="f97e5-102">NuGet.exe 5.0 and later require .NET Framework 4.7.2 or later to execute.</span></span>

1. <span data-ttu-id="f97e5-103">Visite [nuget.org/downloads](https://nuget.org/downloads) e selecione NuGet 3.3 ou posterior (2.8.6 não é compatível com Mono).</span><span class="sxs-lookup"><span data-stu-id="f97e5-103">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="f97e5-104">Sempre é recomendada a versão mais recente, e a 4.1.0+ é necessária para publicar pacotes em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f97e5-104">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="f97e5-105">Cada download baixa diretamente o arquivo `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="f97e5-105">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="f97e5-106">Programe o browser para salvar o arquivo na pasta de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="f97e5-106">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="f97e5-107">O arquivo *não* é um instalador; nada ocorrerá se você executá-lo diretamente no browser.</span><span class="sxs-lookup"><span data-stu-id="f97e5-107">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="f97e5-108">Adicione a pasta onde você colocou o `nuget.exe` à variável de ambiente PATH para usar a ferramenta CLI de qualquer local.</span><span class="sxs-lookup"><span data-stu-id="f97e5-108">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="f97e5-109">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="f97e5-109">macOS/Linux</span></span>

<span data-ttu-id="f97e5-110">Os comportamentos podem variar levemente de acordo com a distribuição do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="f97e5-110">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="f97e5-111">Instale o [Mono 4.4.2 ou posterior](https://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="f97e5-111">Install [Mono 4.4.2 or later](https://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="f97e5-112">Execute o seguinte comando em um prompt do shell:</span><span class="sxs-lookup"><span data-stu-id="f97e5-112">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="f97e5-113">Crie um alias adicionando o script a seguir ao arquivo apropriado ou ao seu sistema operacional (normalmente `~/.bash_aliases` ou `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="f97e5-113">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="f97e5-114">Recarregue o shell.</span><span class="sxs-lookup"><span data-stu-id="f97e5-114">Reload the shell.</span></span>  <span data-ttu-id="f97e5-115">Teste a instalação inserindo `nuget` sem parâmetros.</span><span class="sxs-lookup"><span data-stu-id="f97e5-115">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="f97e5-116">A ajuda da CLI do NuGet deve ser exibida.</span><span class="sxs-lookup"><span data-stu-id="f97e5-116">NuGet CLI help should display.</span></span>
