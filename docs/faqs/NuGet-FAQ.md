---
title: Perguntas frequentes do NuGet
description: Perguntas e respostas comuns sobre como usar o NuGet na linha de comando e no Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 8bc6af90638408847af6e97cebcbf428f1d5d886
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467759"
---
# <a name="nuget-frequently-asked-questions"></a>Perguntas frequentes do NuGet

**O que é necessário para executar o NuGet?**

Todas as informações sobre a interface do usuário e as ferramentas de linha de comando estão disponíveis na [Guia de instalação](../install-nuget-client-tools.md).

**O NuGet é compatível com o Mono?**

A ferramenta de linha de comando, `nuget.exe`, compila e executa em Mono 3.2 e superior, e pode criar pacotes em Mono.

Embora `nuget.exe` funcione completamente no Windows, existem alguns problemas conhecidos no Linux e no OS X. Consulte [Problemas do Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) no GitHub.

Um [cliente gráfico](https://github.com/mrward/monodevelop-nuget-addin) está disponível como um suplemento para MonoDevelop.

**Como fazer para determinar o que um pacote contém e se ele é estável e útil para meu aplicativo?**

A origem primária para aprender sobre um pacote é a página de listagem em nuget.org (ou outro feed privado). Cada página do pacote em nuget.org inclui uma descrição do pacote, seu histórico de versão e as estatísticas de uso. A seção **Informações** na página do pacote também contém um link para o site da Web do projeto em que você normalmente encontrar muitos exemplos e documentação para ajudá-lo a aprender como o pacote é usado.

Para obter mais informações, consulte [Localizando e escolhendo pacotes](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet no Visual Studio

**Como é a compatibilidade do NuGet com os diferentes produtos do Visual Studio?**

- O Visual Studio no Windows é compatível com a [Interface do usuário do Gerenciador de Pacotes](../tools/package-manager-ui.md) e o [Console do Gerenciador de Pacotes](../tools/package-manager-console.md).
- O Visual Studio para Mac tem recursos internos do NuGet, conforme descrito em [Incluindo um pacote do NuGet em seu projeto](/visualstudio/mac/nuget-walkthrough).
- O Visual Studio Code (todas as plataformas) não tem nenhuma integração direta do NuGet. Usar a [CLI do NuGet](../tools/nuget-exe-cli-reference.md) ou a [CLI do dotnet](../tools/dotnet-commands.md).
- O Azure DevOps fornece [uma etapa de build para restaurar os pacotes do NuGet](/vsts/build-release/tasks/package/nuget). Você também pode [hospedar feeds privados de pacote do NuGet no Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).

**Como fazer para verificar a versão exata das ferramentas do NuGet que estão instaladas?**

No Visual Studio, use o comando **Ajuda > Sobre o Microsoft Visual Studio** e examine a versão exibida ao lado de **Gerenciador de Pacotes do NuGet**.

Como alternativa, inicie o Console do Gerenciador de Pacotes (**Ferramentas > Gerenciador de Pacotes do NuGet > Console do Gerenciador de Pacotes**) e digite `$host` para ver informações sobre o NuGet, incluindo a versão.

**Quais linguagens de programação são compatíveis com o NuGet?**

O NuGet geralmente funciona para linguagens .NET e foi projetado para trazer bibliotecas .NET em um projeto. Como também há suporte para a automação do MSBuild e do Visual Studio em alguns tipos de projeto, também há suporte para outros projetos e idiomas em diversos níveis.

A versão mais recente do NuGet é compatível com C#, Visual Basic, F#, WiX e C++.

**Quais modelos de projeto são compatíveis com o NuGet?**

O NuGet tem suporte completo para uma variedade de modelos de projeto como Windows, Web, Cloud, SharePoint, Wix e assim por diante.

**Como fazer para atualizar pacotes que fazem parte dos modelos do Visual Studio?**

Acesse a guia **Atualizações** na interface do usuário do Gerenciador de Pacotes e selecione **Atualizar tudo** [ou use o comando `Update-Package`](../tools/ps-ref-update-package.md) do Console do Gerenciador de Pacotes.

Para atualizar o próprio modelo, você precisa atualizar manualmente o repositório de modelos. Consulte o [blog de Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) sobre este assunto. Observe que isso é feito por seu próprio risco, pois atualizações manuais podem corromper o modelo se a versão mais recente de todas as dependências não forem compatível entre si.

**Posso usar o NuGet fora do Visual Studio?**

Sim, o NuGet funciona diretamente da linha de comando. Consulte o [Guia de instalação](../install-nuget-client-tools.md) e a [CLI de referência](../tools/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>Linha de comando do NuGet

**Como fazer para obter a versão mais recente da ferramenta de linha de comando do NuGet?**

Consulte o [Guia de instalação](../install-nuget-client-tools.md).

**O que é a licença para nuget.exe?**

Você pode redistribuir o nuget.exe sob os termos da licença do MIT. Você é responsável pela atualização e manutenção das cópias do nuget.exe que você escolhe redistribuir.

**É possível estender a ferramenta de linha de comando do NuGet?**

Sim, é possível adicionar comandos personalizados para `nuget.exe`, conforme descrito na [postagem de Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Console do Gerenciador de Pacotes do NuGet (Visual Studio no Windows)

**Como fazer para obter acesso ao objeto DTE no console do Gerenciador de Pacotes?**

O objeto de nível superior no modelo de objeto de automação do Visual Studio é chamado o objeto DTE (Ambiente de Ferramentas de Desenvolvimento). O console fornece isso por meio de uma variável chamada `$DTE`. Para obter mais informações, consulte [Visão geral do modelo de automação](/visualstudio/extensibility/internals/automation-model-overview) na documentação de Extensibilidade do Visual Studio.

**Tento converter a variável $DTE para o tipo DTE2, mas eu recebo um erro: Não é possível converter o valor de "EnvDTE.DTEClass" do tipo "EnvDTE.DTEClass" para o tipo "EnvDTE80.DTE2". Qual é o problema?**

Este é um problema conhecido em como o PowerShell interage com um objeto COM. Experimente o seguinte:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` é uma função auxiliar adicionada pelo host do NuGet PowerShell.

## <a name="creating-and-publishing-packages"></a>Criar e publicar pacotes

**Como fazer para listar meu pacote em um feed?**

Consulte [Criar e publicar um pacote](../quickstart/create-and-publish-a-package.md).

**Tenho várias versões da minha biblioteca que usam versões diferentes do .NET Framework. Como fazer para compilar um único pacote compatível com isso?**

Consulte [Suporte a várias versões e perfis do .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).

**Como fazer para configurar meu próprio repositório ou feed?**

Consulte a [Visão geral de hospedagem de pacotes](../hosting-packages/overview.md).

**Como posso carregar pacotes para meu feed do NuGet em massa?**

Consulte [Publicação de pacotes do NuGet em massa](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Trabalhando com pacotes

**Qual é a diferença entre um pacote de nível de projeto e um pacote de nível de solução?**

Um pacote de nível de solução (NuGet 3.x ou superior) é instalado apenas uma vez em uma solução e fica disponível para todos os projetos na solução. Um pacote de nível de projeto está instalado em cada projeto que o utiliza. Um pacote de nível de solução também pode instalar novos comandos que podem ser chamados de dentro do Console do Gerenciador de Pacotes.

**É possível instalar os pacotes do NuGet sem conectividade com a Internet?**

Sim, consulte a postagem no blog de Scott Hanselman [How to access NuGet when nuget.org is down (or you're on a plane) [Como acessar o NuGet quando o nuget.org estiver inativo (ou você estiver a bordo de um avião)]](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).

**Como fazer para instalar pacotes em um local diferente da pasta de pacotes padrão?**

Defina a configuração [`repositoryPath`](../reference/nuget-config-file.md#config-section) em `Nuget.Config` usando `nuget config -set repositoryPath=<path>`.

**Como evitar adicionar a pasta de pacotes do NuGet ao controle do código-fonte?**

Defina o [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) em `Nuget.Config` para `true`. Essa chave funciona no nível da solução e, portanto, precisa ser adicionada ao arquivo `$(Solutiondir)\.nuget\Nuget.Config`. Habilitando a restauração do pacote do Visual Studio cria esse arquivo automaticamente.

**Como fazer para desligar a restauração do pacote?**

Consulte [Habilitar e desabilitar a restauração de pacote](../consume-packages/package-restore.md#enable-and-disable-package-restore).

**Por que recebo um “Não é possível resolver o erro de dependência” ao instalar um pacote local com dependências remotas?**

Você precisa selecionar a origem **Todos** ao instalar um pacote local para o projeto. Isso agrega todos os feeds em vez de usar apenas um. O motivo pelo qual este erro ocorre é que os usuários de um repositório local geralmente desejam evitar instalar acidentalmente um pacote remoto devido a políticas corporativa.

**Tenho vários projetos na mesma pasta, como posso usar arquivos packages.config separados para cada projeto?**

Na maioria dos projetos em que projetos separados residem em pastas separadas, isso não é um problema, pois o NuGet identifica os arquivos `packages.config` em cada projeto. Com o NuGet 3.3 e superior, e com vários projetos na mesma pasta, você pode inserir o nome do projeto nos nomes de arquivo `packages.config` que usam o padrão `packages.{project-name}.config` e o NuGet usará esse arquivo.

Isso não é um problema ao usar PackageReference, pois cada arquivo de projeto contém sua própria lista de dependências.

**Não vejo o nuget.org na minha lista de repositórios, como faço para obtê-lo novamente?**

- Adicione `https://api.nuget.org/v3/index.json` à lista de fontes ou
- Exclua `%appdata%\.nuget\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) e deixe o NuGet recriá-lo.
