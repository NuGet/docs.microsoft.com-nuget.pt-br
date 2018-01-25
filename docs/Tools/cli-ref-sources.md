---
title: NuGet CLI fontes comando | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o nuget.exe fontes de comando"
keywords: "NuGet fontes de referência, fontes de comando"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c1cd909c0c35d52f0269d267367669df46f9db55
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="f6384-104">comando de fontes (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f6384-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="f6384-105">**Aplica-se a:** consumo de pacote, a publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="f6384-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f6384-106">Gerencia a lista de fontes localizadas na `%AppData%\NuGet\NuGet.Config` ou arquivo de configuração especificado.</span><span class="sxs-lookup"><span data-stu-id="f6384-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

<span data-ttu-id="f6384-107">Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="f6384-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="f6384-108">Uso</span><span class="sxs-lookup"><span data-stu-id="f6384-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="f6384-109">onde `<operation>` é um dos *lista, adicionar, remover, habilitar, desabilitar,* ou *atualização*, `<name>` é o nome da fonte, e `<source>` é a URL da fonte.</span><span class="sxs-lookup"><span data-stu-id="f6384-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="f6384-110">Opções</span><span class="sxs-lookup"><span data-stu-id="f6384-110">Options</span></span>

| <span data-ttu-id="f6384-111">Opção</span><span class="sxs-lookup"><span data-stu-id="f6384-111">Option</span></span> | <span data-ttu-id="f6384-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="f6384-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f6384-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f6384-113">ConfigFile</span></span> | <span data-ttu-id="f6384-114">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="f6384-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f6384-115">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="f6384-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="f6384-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f6384-116">ForceEnglishOutput</span></span> | <span data-ttu-id="f6384-117">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="f6384-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f6384-118">Formatar</span><span class="sxs-lookup"><span data-stu-id="f6384-118">Format</span></span> | <span data-ttu-id="f6384-119">Aplica-se para o `list` ação e pode ser `Detailed` (o padrão) ou `Short`.</span><span class="sxs-lookup"><span data-stu-id="f6384-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="f6384-120">Ajuda</span><span class="sxs-lookup"><span data-stu-id="f6384-120">Help</span></span> | <span data-ttu-id="f6384-121">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="f6384-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="f6384-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f6384-122">NonInteractive</span></span> | <span data-ttu-id="f6384-123">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="f6384-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f6384-124">Senha</span><span class="sxs-lookup"><span data-stu-id="f6384-124">Password</span></span> | <span data-ttu-id="f6384-125">Especifica a senha para autenticar com o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="f6384-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="f6384-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="f6384-126">StorePasswordInClearText</span></span> | <span data-ttu-id="f6384-127">Indica para armazenar a senha em texto não criptografado em vez do comportamento padrão de armazenar um formato criptografado.</span><span class="sxs-lookup"><span data-stu-id="f6384-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="f6384-128">UserName</span><span class="sxs-lookup"><span data-stu-id="f6384-128">UserName</span></span> | <span data-ttu-id="f6384-129">Especifica o nome de usuário para autenticar com o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="f6384-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="f6384-130">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="f6384-130">Verbosity</span></span> | <span data-ttu-id="f6384-131">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="f6384-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="f6384-132">Certifique-se de Adicionar senha as fontes no mesmo contexto de usuário, como o nuget.exe mais tarde é usada para acessar a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="f6384-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="f6384-133">A senha será armazenada criptografado no arquivo de configuração e só pode ser descriptografada no mesmo contexto de usuário, como ele foi criptografado.</span><span class="sxs-lookup"><span data-stu-id="f6384-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="f6384-134">Assim, por exemplo quando você usar um servidor de compilação para restaurar os pacotes do NuGet que a senha deve ser criptografada com o mesmo usuário do Windows sob a qual a tarefa do servidor de compilação será executado.</span><span class="sxs-lookup"><span data-stu-id="f6384-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="f6384-135">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f6384-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f6384-136">Exemplos</span><span class="sxs-lookup"><span data-stu-id="f6384-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
