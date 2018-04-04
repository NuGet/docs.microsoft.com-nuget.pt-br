---
title: NuGet CLI fontes comando | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referência para o nuget.exe fontes de comando
keywords: NuGet fontes de referência, fontes de comando
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5fb34654dc294de34cf0e15f784240884dc1e3d1
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="66c32-104">comando de fontes (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="66c32-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="66c32-105">**Aplica-se a:** consumo de pacote, a publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="66c32-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="66c32-106">Gerencia a lista de fontes localizado no arquivo de configuração de escopo de usuário ou um arquivo de configuração especificado.</span><span class="sxs-lookup"><span data-stu-id="66c32-106">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="66c32-107">O arquivo de configuração de escopo do usuário está localizado em `%appdata%\NuGet\NuGet.Config` (Windows) e `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="66c32-107">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="66c32-108">Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="66c32-108">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="66c32-109">Uso</span><span class="sxs-lookup"><span data-stu-id="66c32-109">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="66c32-110">onde `<operation>` é um dos *lista, adicionar, remover, habilitar, desabilitar,* ou *atualização*, `<name>` é o nome da fonte, e `<source>` é a URL da fonte.</span><span class="sxs-lookup"><span data-stu-id="66c32-110">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="66c32-111">Opções</span><span class="sxs-lookup"><span data-stu-id="66c32-111">Options</span></span>

| <span data-ttu-id="66c32-112">Opção</span><span class="sxs-lookup"><span data-stu-id="66c32-112">Option</span></span> | <span data-ttu-id="66c32-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="66c32-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66c32-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="66c32-114">ConfigFile</span></span> | <span data-ttu-id="66c32-115">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="66c32-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="66c32-116">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="66c32-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="66c32-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="66c32-117">ForceEnglishOutput</span></span> | <span data-ttu-id="66c32-118">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="66c32-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="66c32-119">Formatar</span><span class="sxs-lookup"><span data-stu-id="66c32-119">Format</span></span> | <span data-ttu-id="66c32-120">Aplica-se para o `list` ação e pode ser `Detailed` (o padrão) ou `Short`.</span><span class="sxs-lookup"><span data-stu-id="66c32-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="66c32-121">Ajuda</span><span class="sxs-lookup"><span data-stu-id="66c32-121">Help</span></span> | <span data-ttu-id="66c32-122">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="66c32-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="66c32-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="66c32-123">NonInteractive</span></span> | <span data-ttu-id="66c32-124">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="66c32-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="66c32-125">Senha</span><span class="sxs-lookup"><span data-stu-id="66c32-125">Password</span></span> | <span data-ttu-id="66c32-126">Especifica a senha para autenticar com o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="66c32-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="66c32-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="66c32-127">StorePasswordInClearText</span></span> | <span data-ttu-id="66c32-128">Indica para armazenar a senha em texto não criptografado em vez do comportamento padrão de armazenar um formato criptografado.</span><span class="sxs-lookup"><span data-stu-id="66c32-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="66c32-129">UserName</span><span class="sxs-lookup"><span data-stu-id="66c32-129">UserName</span></span> | <span data-ttu-id="66c32-130">Especifica o nome de usuário para autenticar com o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="66c32-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="66c32-131">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="66c32-131">Verbosity</span></span> | <span data-ttu-id="66c32-132">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="66c32-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="66c32-133">Certifique-se de Adicionar senha as fontes no mesmo contexto de usuário, como o nuget.exe mais tarde é usada para acessar a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="66c32-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="66c32-134">A senha será armazenada criptografado no arquivo de configuração e só pode ser descriptografada no mesmo contexto de usuário, como ele foi criptografado.</span><span class="sxs-lookup"><span data-stu-id="66c32-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="66c32-135">Assim, por exemplo quando você usar um servidor de compilação para restaurar os pacotes do NuGet que a senha deve ser criptografada com o mesmo usuário do Windows sob a qual a tarefa do servidor de compilação será executado.</span><span class="sxs-lookup"><span data-stu-id="66c32-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="66c32-136">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="66c32-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="66c32-137">Exemplos</span><span class="sxs-lookup"><span data-stu-id="66c32-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
