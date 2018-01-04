A instalação de um pacote acontece de três maneiras:

| Método | Descrição | Referência |
| --- | --- | --- |
| CLI do nuget.exe: `nuget install <package_name>` | Baixa o pacote identificado por \<package_name\> e expande seu conteúdo para uma pasta no diretório atual. Se nenhum pacote for especificado, instala todos os pacotes listados no arquivo `packages.config` do projeto. Nenhuma alteração foi feita nos arquivos de projeto. As dependências também são baixadas e expandidas. | [Referência da CLI](../tools/nuget-exe-CLI-Reference.md) |
| Console do Gerenciador de Pacotes (Visual Studio): `Install-Package <package_name>` | Baixa e instala o pacote no projeto atual e depois atualiza o arquivo de projeto para listar o pacote como uma dependência. | [Guia do Console do Gerenciador de Pacotes](../tools/Package-Manager-Console.md) |
| Interface do Usuário do Gerenciador de Pacotes (Visual Studio) | Fornece uma interface do usuário por meio da qual você pode procurar, selecionar e instalar pacotes em um projeto. Atualiza o arquivo de projeto para listar o pacote como uma dependência. | [Referência da interface do usuário do Gerenciador de Pacotes](../tools/Package-Manager-UI.md) |