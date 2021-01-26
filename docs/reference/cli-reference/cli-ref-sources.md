---
title: Comando de fontes da CLI do NuGet
description: Referência para o comando nuget.exe sources
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e9cbdd089c5c0f66d25e7588ece504feae63f2f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780007"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="f1034-103">comando Sources (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f1034-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="f1034-104">**Aplica-se a:** consumo de pacote, &bullet; **versões com suporte para publicação:** todos</span><span class="sxs-lookup"><span data-stu-id="f1034-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f1034-105">Gerencia a lista de fontes localizadas no arquivo de configuração de escopo do usuário ou um arquivo de configuração especificado.</span><span class="sxs-lookup"><span data-stu-id="f1034-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="f1034-106">O arquivo de configuração de escopo do usuário está localizado em `%appdata%\NuGet\NuGet.Config` (Windows) e `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="f1034-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="f1034-107">Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="f1034-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="f1034-108">Uso</span><span class="sxs-lookup"><span data-stu-id="f1034-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="f1034-109">em que `<operation>` é uma *lista, adicionar, remover, habilitar, desabilitar* ou *Atualizar*, `<name>` é o nome da origem e `<source>` é a URL da origem.</span><span class="sxs-lookup"><span data-stu-id="f1034-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="f1034-110">Você pode operar em apenas uma fonte de cada vez.</span><span class="sxs-lookup"><span data-stu-id="f1034-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="f1034-111">Opções</span><span class="sxs-lookup"><span data-stu-id="f1034-111">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="f1034-112">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="f1034-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f1034-113">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="f1034-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="f1034-114">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="f1034-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Format`**

  <span data-ttu-id="f1034-115">Aplica-se à `list` ação e pode ser `Detailed` (o padrão) ou `Short` .</span><span class="sxs-lookup"><span data-stu-id="f1034-115">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span>

- **`-?|-help`**

  <span data-ttu-id="f1034-116">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="f1034-116">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="f1034-117">Nome da origem.</span><span class="sxs-lookup"><span data-stu-id="f1034-117">Name of the source.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="f1034-118">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="f1034-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Password`**

  <span data-ttu-id="f1034-119">Especifica a senha para autenticação com a origem.</span><span class="sxs-lookup"><span data-stu-id="f1034-119">Specifies the password for authenticating with the source.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="f1034-120">Caminho para a origem de pacote (s).</span><span class="sxs-lookup"><span data-stu-id="f1034-120">Path to the package(s) source.</span></span>

- **`-StorePasswordInClearText`**

  <span data-ttu-id="f1034-121">Indica armazenar a senha em texto não criptografado em vez do comportamento padrão de armazenamento de um formulário criptografado.</span><span class="sxs-lookup"><span data-stu-id="f1034-121">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span>

- **`-UserName`**

  <span data-ttu-id="f1034-122">Especifica o nome de usuário para autenticação com a origem.</span><span class="sxs-lookup"><span data-stu-id="f1034-122">Specifies the user name for authenticating with the source.</span></span>

- **`-ValidAuthenticationTypes`**

  <span data-ttu-id="f1034-123">Lista separada por vírgulas de tipos de autenticação válidos para esta fonte.</span><span class="sxs-lookup"><span data-stu-id="f1034-123">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="f1034-124">Por padrão, todos os tipos de autenticação são válidos.</span><span class="sxs-lookup"><span data-stu-id="f1034-124">By default, all authentication types are valid.</span></span> <span data-ttu-id="f1034-125">Exemplo: `basic,negotiate`.</span><span class="sxs-lookup"><span data-stu-id="f1034-125">Example: `basic,negotiate`.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="f1034-126">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="f1034-126">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

> [!Note]
> <span data-ttu-id="f1034-127">Certifique-se de adicionar a senha de origem no mesmo contexto de usuário que o nuget.exe é usado posteriormente para acessar a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="f1034-127">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="f1034-128">A senha será armazenada criptografada no arquivo de configuração e só poderá ser descriptografada no mesmo contexto de usuário que foi criptografada.</span><span class="sxs-lookup"><span data-stu-id="f1034-128">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="f1034-129">Por exemplo, quando você usa um servidor de compilação para restaurar os pacotes NuGet, a senha deve ser criptografada com o mesmo usuário do Windows no qual a tarefa do servidor de compilação será executada.</span><span class="sxs-lookup"><span data-stu-id="f1034-129">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="f1034-130">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f1034-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f1034-131">Exemplos</span><span class="sxs-lookup"><span data-stu-id="f1034-131">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
