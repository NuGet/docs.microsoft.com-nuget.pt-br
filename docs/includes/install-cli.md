#### <a name="windows"></a><span data-ttu-id="abe1c-101">Windows</span><span class="sxs-lookup"><span data-stu-id="abe1c-101">Windows</span></span>
1. <span data-ttu-id="abe1c-102">Visite [nuget.org/downloads](https://nuget.org/downloads) e selecione NuGet 3.3 ou superior (2.8.6 não é compatível com Mono).</span><span class="sxs-lookup"><span data-stu-id="abe1c-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="abe1c-103">A versão mais recente é sempre recomendável e 4.1.0+ é necessário para publicar pacotes em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="abe1c-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
2. <span data-ttu-id="abe1c-104">Cada download o `nuget.exe` arquivo diretamente.</span><span class="sxs-lookup"><span data-stu-id="abe1c-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="abe1c-105">Instrua o seu navegador para salvar o arquivo em uma pasta de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="abe1c-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="abe1c-106">O arquivo é *não* um instalador; você não verá nada se você executá-lo diretamente do navegador.</span><span class="sxs-lookup"><span data-stu-id="abe1c-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
3. <span data-ttu-id="abe1c-107">Adicione a pasta onde você colocou `nuget.exe` à sua variável de ambiente PATH para usar a ferramenta CLI de qualquer lugar.</span><span class="sxs-lookup"><span data-stu-id="abe1c-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="abe1c-108">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="abe1c-108">macOS/Linux</span></span>
<span data-ttu-id="abe1c-109">Comportamentos podem variar um pouco pela distribuição de sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="abe1c-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="abe1c-110">Instalar [Mono 4.4.2 ou posterior](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="abe1c-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>
2. <span data-ttu-id="abe1c-111">Execute os seguintes comandos em um prompt de shell:</span><span class="sxs-lookup"><span data-stu-id="abe1c-111">Execute the following commands at a shell prompt:</span></span>
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. <span data-ttu-id="abe1c-112">Criar um alias, adicionando o script a seguir para o arquivo apropriado para seu sistema operacional (geralmente `~/.bash_aliases` ou `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="abe1c-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. <span data-ttu-id="abe1c-113">Recarregue o shell.</span><span class="sxs-lookup"><span data-stu-id="abe1c-113">Reload the shell.</span></span>  <span data-ttu-id="abe1c-114">Testar a instalação digitando `nuget` sem parâmetros.</span><span class="sxs-lookup"><span data-stu-id="abe1c-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="abe1c-115">Ajuda do NuGet CLI deve exibir.</span><span class="sxs-lookup"><span data-stu-id="abe1c-115">NuGet CLI help should display.</span></span>