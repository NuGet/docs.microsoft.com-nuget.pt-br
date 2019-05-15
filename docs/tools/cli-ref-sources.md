---
title: CLI do NuGet fontes de comando
description: Referência para o nuget.exe fontes de comando
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610626"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="89cae-103">Commando sources (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="89cae-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="89cae-104">**Aplica-se a:** consumo de pacote, publicando &bullet; **versões com suporte:** todos os</span><span class="sxs-lookup"><span data-stu-id="89cae-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="89cae-105">Gerencia a lista de fontes, localizado no arquivo de configuração de escopo de usuário ou um arquivo de configuração especificado.</span><span class="sxs-lookup"><span data-stu-id="89cae-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="89cae-106">O arquivo de configuração de escopo do usuário está localizado em `%appdata%\NuGet\NuGet.Config` (Windows) e `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="89cae-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="89cae-107">Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="89cae-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="89cae-108">Uso</span><span class="sxs-lookup"><span data-stu-id="89cae-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="89cae-109">em que `<operation>` é uma das *listar, adicionar, remover, habilitar, desabilitar* ou *Update*, `<name>` é o nome da fonte, e `<source>` é a URL da fonte.</span><span class="sxs-lookup"><span data-stu-id="89cae-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="89cae-110">Você pode operar em apenas uma fonte de cada vez.</span><span class="sxs-lookup"><span data-stu-id="89cae-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="89cae-111">Opções</span><span class="sxs-lookup"><span data-stu-id="89cae-111">Options</span></span>

| <span data-ttu-id="89cae-112">Opção</span><span class="sxs-lookup"><span data-stu-id="89cae-112">Option</span></span> | <span data-ttu-id="89cae-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="89cae-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="89cae-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="89cae-114">ConfigFile</span></span> | <span data-ttu-id="89cae-115">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="89cae-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="89cae-116">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="89cae-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="89cae-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="89cae-117">ForceEnglishOutput</span></span> | <span data-ttu-id="89cae-118">*(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="89cae-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="89cae-119">Formatar</span><span class="sxs-lookup"><span data-stu-id="89cae-119">Format</span></span> | <span data-ttu-id="89cae-120">Aplica-se para o `list` ação e pode ser `Detailed` (o padrão) ou `Short`.</span><span class="sxs-lookup"><span data-stu-id="89cae-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="89cae-121">Ajuda</span><span class="sxs-lookup"><span data-stu-id="89cae-121">Help</span></span> | <span data-ttu-id="89cae-122">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="89cae-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="89cae-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="89cae-123">NonInteractive</span></span> | <span data-ttu-id="89cae-124">Suprime a solicitações de entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="89cae-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="89cae-125">Senha</span><span class="sxs-lookup"><span data-stu-id="89cae-125">Password</span></span> | <span data-ttu-id="89cae-126">Especifica a senha para autenticação com o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="89cae-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="89cae-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="89cae-127">StorePasswordInClearText</span></span> | <span data-ttu-id="89cae-128">Indica para armazenar a senha em texto não criptografado em vez do comportamento padrão de armazenar um formato criptografado.</span><span class="sxs-lookup"><span data-stu-id="89cae-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="89cae-129">UserName</span><span class="sxs-lookup"><span data-stu-id="89cae-129">UserName</span></span> | <span data-ttu-id="89cae-130">Especifica o nome de usuário para autenticar com o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="89cae-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="89cae-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="89cae-131">Verbosity</span></span> | <span data-ttu-id="89cae-132">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="89cae-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="89cae-133">Certifique-se de adicionar a senha dos fontes no mesmo contexto de usuário como o nuget.exe é usado posteriormente para acessar a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="89cae-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="89cae-134">A senha será armazenada criptografado no arquivo de configuração e só pode ser descriptografada no mesmo contexto de usuário porque ele foi criptografado.</span><span class="sxs-lookup"><span data-stu-id="89cae-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="89cae-135">Por exemplo, quando você usar um servidor de compilação para restaurar pacotes do NuGet que a senha deve ser criptografada com o mesmo usuário do Windows sob a qual a tarefa do servidor de compilação será executado.</span><span class="sxs-lookup"><span data-stu-id="89cae-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="89cae-136">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="89cae-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="89cae-137">Exemplos</span><span class="sxs-lookup"><span data-stu-id="89cae-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
