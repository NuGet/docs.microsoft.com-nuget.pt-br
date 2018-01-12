---
title: NuGet CLI fontes comando | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "Referência para o nuget.exe fontes de comando"
keywords: "NuGet fontes de referência, fontes de comando"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2eca8557840c467a60f5f708efe242cd83609164
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="b14e3-104">comando de fontes (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b14e3-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="b14e3-105">**Aplica-se a:** consumo de pacote, a publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="b14e3-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b14e3-106">Gerencia a lista de fontes localizadas na `%AppData%\NuGet\NuGet.Config` ou arquivo de configuração especificado.</span><span class="sxs-lookup"><span data-stu-id="b14e3-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

<span data-ttu-id="b14e3-107">Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="b14e3-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="b14e3-108">Uso</span><span class="sxs-lookup"><span data-stu-id="b14e3-108">Usage</span></span>

```
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="b14e3-109">onde `<operation>` é um dos *lista, adicionar, remover, habilitar, desabilitar,* ou *atualização*, `<name>` é o nome da fonte, e `<source>` é a URL da fonte.</span><span class="sxs-lookup"><span data-stu-id="b14e3-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="b14e3-110">Opções</span><span class="sxs-lookup"><span data-stu-id="b14e3-110">Options</span></span>

| <span data-ttu-id="b14e3-111">Opção</span><span class="sxs-lookup"><span data-stu-id="b14e3-111">Option</span></span> | <span data-ttu-id="b14e3-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="b14e3-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b14e3-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b14e3-113">ConfigFile</span></span> | <span data-ttu-id="b14e3-114">*(2.5 +)*  NuGet o arquivo de configuração para aplicar.</span><span class="sxs-lookup"><span data-stu-id="b14e3-114">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="b14e3-115">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="b14e3-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="b14e3-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b14e3-116">ForceEnglishOutput</span></span> | <span data-ttu-id="b14e3-117">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="b14e3-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b14e3-118">Formatar</span><span class="sxs-lookup"><span data-stu-id="b14e3-118">Format</span></span> | <span data-ttu-id="b14e3-119">Aplica-se para o `list` ação e pode ser `Detailed` (o padrão) ou `Short`.</span><span class="sxs-lookup"><span data-stu-id="b14e3-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="b14e3-120">Ajuda</span><span class="sxs-lookup"><span data-stu-id="b14e3-120">Help</span></span> | <span data-ttu-id="b14e3-121">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="b14e3-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="b14e3-122">Não interativo</span><span class="sxs-lookup"><span data-stu-id="b14e3-122">NonInteractive</span></span> | <span data-ttu-id="b14e3-123">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="b14e3-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b14e3-124">Senha</span><span class="sxs-lookup"><span data-stu-id="b14e3-124">Password</span></span> | <span data-ttu-id="b14e3-125">Especifica a senha para autenticar com o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="b14e3-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="b14e3-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="b14e3-126">StorePasswordInClearText</span></span> | <span data-ttu-id="b14e3-127">Indica para armazenar a senha em texto não criptografado em vez do comportamento padrão de armazenar um formato criptografado.</span><span class="sxs-lookup"><span data-stu-id="b14e3-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="b14e3-128">UserName</span><span class="sxs-lookup"><span data-stu-id="b14e3-128">UserName</span></span> | <span data-ttu-id="b14e3-129">Especifica o nome de usuário para autenticar com o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="b14e3-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="b14e3-130">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="b14e3-130">Verbosity</span></span> | <span data-ttu-id="b14e3-131">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="b14e3-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

> [!Note]
> <span data-ttu-id="b14e3-132">Certifique-se de Adicionar senha as fontes no mesmo contexto de usuário, como o nuget.exe mais tarde é usada para acessar a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="b14e3-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="b14e3-133">A senha será armazenada criptografado no arquivo de configuração e só pode ser descriptografada no mesmo contexto de usuário, como ele foi criptografado.</span><span class="sxs-lookup"><span data-stu-id="b14e3-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="b14e3-134">Assim, por exemplo quando você usar um servidor de compilação para restaurar os pacotes do NuGet que a senha deve ser criptografada com o mesmo usuário do Windows sob a qual a tarefa do servidor de compilação será executado.</span><span class="sxs-lookup"><span data-stu-id="b14e3-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="b14e3-135">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b14e3-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b14e3-136">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b14e3-136">Examples</span></span>

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
