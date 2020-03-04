---
title: Instalar e usar um pacote NuGet no Visual Studio para Mac
description: Um tutorial explicativo sobre o processo de instalação e uso de um pacote NuGet em um projeto Visual Studio para Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70238472"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>Início Rápido: Instalar e usar um pacote no Visual Studio para Mac

Os pacotes NuGet contém código reutilizável que outros desenvolvedores disponibilizam para uso em seus projetos. Consulte [O que há de novo no NuGet](../What-is-NuGet.md) para obter mais informações. Os pacotes são instalados em um projeto Visual Studio para Mac usando o Gerenciador de pacotes NuGet. Este artigo demonstra o processo usando o popular pacote [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) e um projeto de console do .NET Core. O mesmo processo se aplica a qualquer outro projeto do Xamarin ou do .NET Core.

Depois de instalado, consulte o pacote no código com `using <namespace>` em que \<namespace\> é específico para o pacote que você está usando. Depois que a referência é feita, você pode chamar o pacote por meio de sua API.

> [!Tip]
> **Começar no nuget.org**: normalmente, os desenvolvedores em .NET encontram componentes que podem reutilizar em seus próprios aplicativos procurando no *nuget.org*. Você pode pesquisar no *nuget.org* diretamente ou localizar e instalar pacotes de dentro do Visual Studio, conforme mostrado neste artigo. Para saber mais, confira [Localizar e avaliar pacotes do NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Prerequisites

- Visual Studio 2019 para Mac.

É possível instalar a edição Community 2019 gratuitamente em [visualstudio.com](https://www.visualstudio.com/) ou usar as edições Professional ou Enterprise.

Se você estiver usando o Visual Studio no Windows, consulte [instalar e usar um pacote no Visual Studio (somente Windows)](install-and-use-a-package-in-visual-studio.md).

## <a name="create-a-project"></a>Criar um projeto

É possível instalar pacotes do NuGet em qualquer projeto .NET, desde que o pacote ofereça suporte à mesma estrutura de destino do projeto.

Para esta explicação, use um aplicativo de console simples do .NET Core. Crie um projeto no Visual Studio para Mac usando **arquivo > nova solução...** , selecione o modelo **aplicativo de > do .NET Core > de aplicativos do console** . Clique em **Avançar**. Aceite os valores padrão para a **estrutura de destino** quando solicitado.

O Visual Studio criará o projeto, que será aberto no Gerenciador de Soluções.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Adicionar o pacote do NuGet Newtonsoft.Json

Para instalar o pacote, use o Gerenciador de pacotes NuGet. Quando você instala um pacote, o NuGet registra a dependência no arquivo de projeto ou em `packages.config` um arquivo (dependendo do formato do projeto). Para obter mais informações, veja [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Gerenciador de pacotes do NuGet

1. Em Gerenciador de Soluções, clique com o botão direito do mouse em **dependências** e escolha **adicionar pacotes...** .

    ![Gerenciar o comando de pacotes do NuGet para referências de projeto](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. Escolha "nuget.org" como a **origem do pacote** no canto superior esquerdo da caixa de diálogo e procure **Newtonsoft. JSON**, selecione esse pacote na lista e selecione **adicionar pacotes...** :

    ![Localizando o pacote Newtonsoft.Json](media/QS_Use_Mac-03-NewtonsoftJson.png)

    Se você quiser obter mais informações sobre o Gerenciador de pacotes NuGet, consulte [instalar e gerenciar pacotes usando o Visual Studio para Mac](../consume-packages/install-use-packages-visual-studio.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Use a API Newtonsoft.Json no aplicativo

Com o pacote Newtonsoft.Json no projeto, você pode chamar seu método `JsonConvert.SerializeObject` para converter um objeto em uma cadeia de caracteres legível.

1. Abra o `Program.cs` arquivo (localizado no painel de soluções) e substitua o conteúdo do arquivo pelo código a seguir:

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

1. Compile e execute o aplicativo selecionando **executar > iniciar a depuração**:

1. Depois que o aplicativo for executado, você verá a saída JSON serializada aparecer no console:

  ![Saída do aplicativo de console](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>Próximas etapas
Parabéns por instalar e usar seu primeiro pacote do NuGet!

> [!div class="nextstepaction"]
> [Instalar e gerenciar pacotes usando o Visual Studio para Mac](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

Para ver o que mais o NuGet tem a oferecer, selecione os links abaixo.

- [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/overview-and-workflow.md)
- [Referências de pacotes em arquivos de projeto](../consume-packages/package-references-in-project-files.md)
