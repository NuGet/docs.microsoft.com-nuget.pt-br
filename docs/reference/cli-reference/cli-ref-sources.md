---
title: Comando de fontes da CLI do NuGet
description: Referência para o comando de origens do NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327593"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="7b2bf-103">Commando sources (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7b2bf-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="7b2bf-104">**Aplica-se a:** consumo de &bullet; pacote, **versões com suporte para publicação:** todos</span><span class="sxs-lookup"><span data-stu-id="7b2bf-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7b2bf-105">Gerencia a lista de fontes localizadas no arquivo de configuração de escopo do usuário ou um arquivo de configuração especificado.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="7b2bf-106">O arquivo de configuração de escopo do usuário `%appdata%\NuGet\NuGet.Config` está localizado em ( `~/.nuget/NuGet/NuGet.Config` Windows) e (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="7b2bf-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="7b2bf-107">Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="7b2bf-108">Uso</span><span class="sxs-lookup"><span data-stu-id="7b2bf-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="7b2bf-109">em `<operation>` que é uma *lista, adicionar, remover, habilitar, desabilitar* ou *Atualizar*, `<name>` é o nome da origem e `<source>` é a URL da origem.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="7b2bf-110">Você pode operar em apenas uma fonte de cada vez.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="7b2bf-111">Opções</span><span class="sxs-lookup"><span data-stu-id="7b2bf-111">Options</span></span>

| <span data-ttu-id="7b2bf-112">Opção</span><span class="sxs-lookup"><span data-stu-id="7b2bf-112">Option</span></span> | <span data-ttu-id="7b2bf-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="7b2bf-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7b2bf-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7b2bf-114">ConfigFile</span></span> | <span data-ttu-id="7b2bf-115">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7b2bf-116">Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7b2bf-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7b2bf-117">ForceEnglishOutput</span></span> | <span data-ttu-id="7b2bf-118">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7b2bf-119">Formatar</span><span class="sxs-lookup"><span data-stu-id="7b2bf-119">Format</span></span> | <span data-ttu-id="7b2bf-120">Aplica-se `list` à ação e pode `Detailed` ser (o padrão) `Short`ou.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="7b2bf-121">Ajuda</span><span class="sxs-lookup"><span data-stu-id="7b2bf-121">Help</span></span> | <span data-ttu-id="7b2bf-122">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="7b2bf-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="7b2bf-123">NonInteractive</span></span> | <span data-ttu-id="7b2bf-124">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7b2bf-125">Senha</span><span class="sxs-lookup"><span data-stu-id="7b2bf-125">Password</span></span> | <span data-ttu-id="7b2bf-126">Especifica a senha para autenticação com a origem.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="7b2bf-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="7b2bf-127">StorePasswordInClearText</span></span> | <span data-ttu-id="7b2bf-128">Indica armazenar a senha em texto não criptografado em vez do comportamento padrão de armazenamento de um formulário criptografado.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="7b2bf-129">UserName</span><span class="sxs-lookup"><span data-stu-id="7b2bf-129">UserName</span></span> | <span data-ttu-id="7b2bf-130">Especifica o nome de usuário para autenticação com a origem.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="7b2bf-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="7b2bf-131">Verbosity</span></span> | <span data-ttu-id="7b2bf-132">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="7b2bf-133">Certifique-se de adicionar a senha de origem no mesmo contexto de usuário que o NuGet. exe é usado posteriormente para acessar a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="7b2bf-134">A senha será armazenada criptografada no arquivo de configuração e só poderá ser descriptografada no mesmo contexto de usuário que foi criptografada.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="7b2bf-135">Por exemplo, quando você usa um servidor de compilação para restaurar os pacotes NuGet, a senha deve ser criptografada com o mesmo usuário do Windows no qual a tarefa do servidor de compilação será executada.</span><span class="sxs-lookup"><span data-stu-id="7b2bf-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="7b2bf-136">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7b2bf-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7b2bf-137">Exemplos</span><span class="sxs-lookup"><span data-stu-id="7b2bf-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
