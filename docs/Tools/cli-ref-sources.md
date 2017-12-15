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
ms.openlocfilehash: 52c46dba168e7395d50cb8d8f9775839389e614c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="8a5dd-104">comando de fontes (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8a5dd-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="8a5dd-105">**Aplica-se a:** consumo de pacote, a publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="8a5dd-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8a5dd-106">Gerencia a lista de fontes localizadas na `%AppData%\NuGet\NuGet.Config` ou arquivo de configuração especificado.</span><span class="sxs-lookup"><span data-stu-id="8a5dd-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

## <a name="usage"></a><span data-ttu-id="8a5dd-107">Uso</span><span class="sxs-lookup"><span data-stu-id="8a5dd-107">Usage</span></span>

```
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="8a5dd-108">onde `<operation>` é um dos *lista, adicionar, remover, habilitar, desabilitar,* ou *atualização*, `<name>` é o nome da fonte, e `<source>` é a URL da fonte.</span><span class="sxs-lookup"><span data-stu-id="8a5dd-108">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>


## <a name="options"></a><span data-ttu-id="8a5dd-109">Opções</span><span class="sxs-lookup"><span data-stu-id="8a5dd-109">Options</span></span>

| <span data-ttu-id="8a5dd-110">Opção</span><span class="sxs-lookup"><span data-stu-id="8a5dd-110">Option</span></span> | <span data-ttu-id="8a5dd-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="8a5dd-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8a5dd-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8a5dd-112">ConfigFile</span></span> | <span data-ttu-id="8a5dd-113">*(2.5 +)*  NuGet o arquivo de configuração para aplicar.</span><span class="sxs-lookup"><span data-stu-id="8a5dd-113">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="8a5dd-114">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="8a5dd-114">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="8a5dd-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8a5dd-115">ForceEnglishOutput</span></span> | <span data-ttu-id="8a5dd-116">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="8a5dd-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8a5dd-117">Formatar</span><span class="sxs-lookup"><span data-stu-id="8a5dd-117">Format</span></span> | <span data-ttu-id="8a5dd-118">Aplica-se para o `list` ação e pode ser `Detailed` (o padrão) ou `Short`.</span><span class="sxs-lookup"><span data-stu-id="8a5dd-118">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="8a5dd-119">Ajuda</span><span class="sxs-lookup"><span data-stu-id="8a5dd-119">Help</span></span> | <span data-ttu-id="8a5dd-120">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="8a5dd-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="8a5dd-121">Não interativo</span><span class="sxs-lookup"><span data-stu-id="8a5dd-121">NonInteractive</span></span> | <span data-ttu-id="8a5dd-122">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="8a5dd-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8a5dd-123">Senha</span><span class="sxs-lookup"><span data-stu-id="8a5dd-123">Password</span></span> | <span data-ttu-id="8a5dd-124">Especifica a senha para autenticar com o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="8a5dd-124">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="8a5dd-125">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="8a5dd-125">StorePasswordInClearText</span></span> | <span data-ttu-id="8a5dd-126">Indica para armazenar a senha em texto não criptografado em vez do comportamento padrão de armazenar um formato criptografado.</span><span class="sxs-lookup"><span data-stu-id="8a5dd-126">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="8a5dd-127">UserName</span><span class="sxs-lookup"><span data-stu-id="8a5dd-127">UserName</span></span> | <span data-ttu-id="8a5dd-128">Especifica o nome de usuário para autenticar com o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="8a5dd-128">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="8a5dd-129">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="8a5dd-129">Verbosity</span></span> | <span data-ttu-id="8a5dd-130">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="8a5dd-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

> [!Note]
> <span data-ttu-id="8a5dd-131">Certifique-se de Adicionar senha as fontes no mesmo contexto de usuário, como o nuget.exe mais tarde é usada para acessar a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="8a5dd-131">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="8a5dd-132">A senha será armazenada criptografado no arquivo de configuração e só pode ser descriptografada no mesmo contexto de usuário, como ele foi criptografado.</span><span class="sxs-lookup"><span data-stu-id="8a5dd-132">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="8a5dd-133">Assim, por exemplo quando você usar um servidor de compilação para restaurar os pacotes do NuGet que a senha deve ser criptografada com o mesmo usuário do Windows sob a qual a tarefa do servidor de compilação será executado.</span><span class="sxs-lookup"><span data-stu-id="8a5dd-133">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="8a5dd-134">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8a5dd-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8a5dd-135">Exemplos</span><span class="sxs-lookup"><span data-stu-id="8a5dd-135">Examples</span></span>

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
