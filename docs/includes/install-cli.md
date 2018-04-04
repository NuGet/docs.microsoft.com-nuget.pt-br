#### <a name="windows"></a>Windows
1. Visite [nuget.org/downloads](https://nuget.org/downloads) e selecione NuGet 3.3 ou superior (2.8.6 não é compatível com Mono). A versão mais recente é sempre recomendável e 4.1.0+ é necessário para publicar pacotes em nuget.org.
2. Cada download o `nuget.exe` arquivo diretamente. Instrua o seu navegador para salvar o arquivo em uma pasta de sua escolha. O arquivo é *não* um instalador; você não verá nada se você executá-lo diretamente do navegador.
3. Adicione a pasta onde você colocou `nuget.exe` à sua variável de ambiente PATH para usar a ferramenta CLI de qualquer lugar.

#### <a name="macoslinux"></a>macOS/Linux
Comportamentos podem variar um pouco pela distribuição de sistema operacional.

1. Instalar [Mono 4.4.2 ou posterior](http://www.mono-project.com/docs/getting-started/install/).
2. Execute os seguintes comandos em um prompt de shell:
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. Criar um alias, adicionando o script a seguir para o arquivo apropriado para seu sistema operacional (geralmente `~/.bash_aliases` ou `~/.bash_profile`):
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. Recarregue o shell.  Testar a instalação digitando `nuget` sem parâmetros. Ajuda do NuGet CLI deve exibir.