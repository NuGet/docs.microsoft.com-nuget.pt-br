#### <a name="windows"></a>Windows

1. Visite [nuget.org/downloads](https://nuget.org/downloads) e selecione NuGet 3.3 ou posterior (2.8.6 não é compatível com Mono). Sempre é recomendada a versão mais recente, e a 4.1.0+ é necessária para publicar pacotes em nuget.org.
1. Cada download baixa diretamente o arquivo `nuget.exe`. Programe o browser para salvar o arquivo na pasta de sua escolha. O arquivo *não* é um instalador; nada ocorrerá se você executá-lo diretamente no browser.
1. Adicione a pasta onde você colocou o `nuget.exe` à variável de ambiente PATH para usar a ferramenta CLI de qualquer local.

#### <a name="macoslinux"></a>macOS/Linux

Os comportamentos podem variar levemente de acordo com a distribuição do sistema operacional.

1. Instale o [Mono 4.4.2 ou posterior](http://www.mono-project.com/docs/getting-started/install/).

1. Execute os seguintes comandos no prompt do shell:

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```

1. Crie um alias adicionando o script a seguir ao arquivo apropriado ou ao seu sistema operacional (normalmente `~/.bash_aliases` ou `~/.bash_profile`):

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Recarregue o shell.  Teste a instalação inserindo `nuget` sem parâmetros. A ajuda da CLI do NuGet deve ser exibida.