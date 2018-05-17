---
title: NuGet CLI fontes de comando
description: Referência para o nuget.exe fontes de comando
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d588ff09075ad75b76b7dd3645f3cdff29f6f093
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="c34b8-103">Commando sources (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c34b8-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="c34b8-104">**Aplica-se a:** consumo de pacote, a publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="c34b8-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c34b8-105">Gerencia a lista de fontes localizado no arquivo de configuração de escopo de usuário ou um arquivo de configuração especificado.</span><span class="sxs-lookup"><span data-stu-id="c34b8-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="c34b8-106">O arquivo de configuração de escopo do usuário está localizado em `%appdata%\NuGet\NuGet.Config` (Windows) e `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c34b8-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="c34b8-107">Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="c34b8-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="c34b8-108">Uso</span><span class="sxs-lookup"><span data-stu-id="c34b8-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="c34b8-109">onde `<operation>` é um dos *lista, adicionar, remover, habilitar, desabilitar,* ou *atualização*, `<name>` é o nome da fonte, e `<source>` é a URL da fonte.</span><span class="sxs-lookup"><span data-stu-id="c34b8-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="c34b8-110">Opções</span><span class="sxs-lookup"><span data-stu-id="c34b8-110">Options</span></span>

| <span data-ttu-id="c34b8-111">Opção</span><span class="sxs-lookup"><span data-stu-id="c34b8-111">Option</span></span> | <span data-ttu-id="c34b8-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="c34b8-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c34b8-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c34b8-113">ConfigFile</span></span> | <span data-ttu-id="c34b8-114">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="c34b8-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c34b8-115">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="c34b8-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c34b8-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c34b8-116">ForceEnglishOutput</span></span> | <span data-ttu-id="c34b8-117">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="c34b8-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c34b8-118">Formatar</span><span class="sxs-lookup"><span data-stu-id="c34b8-118">Format</span></span> | <span data-ttu-id="c34b8-119">Aplica-se para o `list` ação e pode ser `Detailed` (o padrão) ou `Short`.</span><span class="sxs-lookup"><span data-stu-id="c34b8-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="c34b8-120">Ajuda</span><span class="sxs-lookup"><span data-stu-id="c34b8-120">Help</span></span> | <span data-ttu-id="c34b8-121">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="c34b8-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="c34b8-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c34b8-122">NonInteractive</span></span> | <span data-ttu-id="c34b8-123">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="c34b8-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c34b8-124">Senha</span><span class="sxs-lookup"><span data-stu-id="c34b8-124">Password</span></span> | <span data-ttu-id="c34b8-125">Especifica a senha para autenticar com o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="c34b8-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="c34b8-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="c34b8-126">StorePasswordInClearText</span></span> | <span data-ttu-id="c34b8-127">Indica para armazenar a senha em texto não criptografado em vez do comportamento padrão de armazenar um formato criptografado.</span><span class="sxs-lookup"><span data-stu-id="c34b8-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="c34b8-128">UserName</span><span class="sxs-lookup"><span data-stu-id="c34b8-128">UserName</span></span> | <span data-ttu-id="c34b8-129">Especifica o nome de usuário para autenticar com o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="c34b8-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="c34b8-130">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="c34b8-130">Verbosity</span></span> | <span data-ttu-id="c34b8-131">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="c34b8-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="c34b8-132">Certifique-se de Adicionar senha as fontes no mesmo contexto de usuário, como o nuget.exe mais tarde é usada para acessar a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="c34b8-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="c34b8-133">A senha será armazenada criptografado no arquivo de configuração e só pode ser descriptografada no mesmo contexto de usuário, como ele foi criptografado.</span><span class="sxs-lookup"><span data-stu-id="c34b8-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="c34b8-134">Assim, por exemplo quando você usar um servidor de compilação para restaurar os pacotes do NuGet que a senha deve ser criptografada com o mesmo usuário do Windows sob a qual a tarefa do servidor de compilação será executado.</span><span class="sxs-lookup"><span data-stu-id="c34b8-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="c34b8-135">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c34b8-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c34b8-136">Exemplos</span><span class="sxs-lookup"><span data-stu-id="c34b8-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
