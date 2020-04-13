---
title: Instale e use um pacote NuGet no Visual Studio para Mac
description: Um tutorial passo a passo sobre o processo de instalação e uso de um pacote NuGet em um projeto do Visual Studio for Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238472"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>Quickstart: Instale e use um pacote no Visual Studio para Mac

Os pacotes NuGet contém código reutilizável que outros desenvolvedores disponibilizam para uso em seus projetos. Consulte [O que há de novo no NuGet](../What-is-NuGet.md) para obter mais informações. Os pacotes são instalados em um projeto do Visual Studio for Mac usando o NuGet Package Manager. Este artigo demonstra o processo usando o popular pacote [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) e um projeto de console .NET Core. O mesmo processo se aplica a qualquer outro projeto Xamarin ou .NET Core.

Depois de instalado, consulte o pacote no código com `using <namespace>` em que \<namespace\> é específico para o pacote que você está usando. Depois que a referência é feita, você pode chamar o pacote por meio de sua API.

> [!Tip]
> **Comece com nuget.org**: Navegar *nuget.org* é como os desenvolvedores do .NET normalmente encontram componentes que podem reutilizar em seus próprios aplicativos. Você pode pesquisar no *nuget.org* diretamente ou localizar e instalar pacotes de dentro do Visual Studio, conforme mostrado neste artigo. Para saber mais, confira [Localizar e avaliar pacotes do NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Pré-requisitos

- Visual Studio 2019 para Mac.

É possível instalar a edição Community 2019 gratuitamente em [visualstudio.com](https://www.visualstudio.com/) ou usar as edições Professional ou Enterprise.

Se você estiver usando o Visual Studio no Windows, consulte [Instalar e usar um pacote no Visual Studio (Somente windows)](install-and-use-a-package-in-visual-studio.md).

## <a name="create-a-project"></a>Criar um projeto

É possível instalar pacotes do NuGet em qualquer projeto .NET, desde que o pacote ofereça suporte à mesma estrutura de destino do projeto.

Para este passo a passo, use um aplicativo simples .NET Core Console. Crie um projeto no Visual Studio para Mac usando **file > New Solution...**, selecione o modelo **de aplicativo > de > console do .NET Core.** Clique em **Próximo**. Aceite os valores padrão para **O Quadro de destino** quando solicitado.

O Visual Studio criará o projeto, que será aberto no Gerenciador de Soluções.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Adicionar o pacote do NuGet Newtonsoft.Json

Para instalar o pacote, use o NuGet Package Manager. Quando você instala um pacote, o NuGet registra a `packages.config` dependência no arquivo do projeto ou em um arquivo (dependendo do formato do projeto). Para obter mais informações, veja [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Gerenciador de Pacotes NuGet

1. No Solution Explorer, clique com o botão direito do mouse **em Dependências** e escolha **Adicionar pacotes...**.

    ![Gerenciar o comando de pacotes do NuGet para referências de projeto](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. Escolha "nuget.org" como a **fonte do Pacote** no canto superior esquerdo da caixa de diálogo e procure por **Newtonsoft.Json**, selecione esse pacote na lista e selecione **Adicionar pacotes...**:

    ![Localizando o pacote Newtonsoft.Json](media/QS_Use_Mac-03-NewtonsoftJson.png)

    Se você quiser mais informações sobre o NuGet Package Manager, consulte [Instalar e gerenciar pacotes usando o Visual Studio para Mac](../consume-packages/install-use-packages-visual-studio.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Use a API Newtonsoft.Json no aplicativo

Com o pacote Newtonsoft.Json no projeto, você pode chamar seu método `JsonConvert.SerializeObject` para converter um objeto em uma cadeia de caracteres legível.

1. Abra `Program.cs` o arquivo (localizado no Bloco de solução) e substitua o conteúdo do arquivo pelo seguinte código:

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. Construa e execute o aplicativo selecionando **Executar > Iniciar depuração**:

1. Uma vez que o aplicativo seja executado, você verá a saída JSON serializada aparecer no console:

  ![Saída do aplicativo Console](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>Próximas etapas
Parabéns por instalar e usar seu primeiro pacote do NuGet!

> [!div class="nextstepaction"]
> [Instale e gerencie pacotes usando o Visual Studio para Mac](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

Para ver o que mais o NuGet tem a oferecer, selecione os links abaixo.

- [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/overview-and-workflow.md)
- [Referências de pacotes em arquivos de projeto](../consume-packages/package-references-in-project-files.md)
