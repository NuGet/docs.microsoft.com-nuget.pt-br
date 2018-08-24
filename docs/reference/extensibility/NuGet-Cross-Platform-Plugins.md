---
title: NuGet cruzada plugins de plataforma
description: NuGet cross plugins de plataforma para NuGet.exe, dotnet.exe, msbuild.exe e Visual Studio
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: cf2c4fb484703b034a8569d053f2417fe58e41ff
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794187"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="929b6-103">NuGet cruzada plugins de plataforma</span><span class="sxs-lookup"><span data-stu-id="929b6-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="929b6-104">No NuGet 4.8 + foi adicionado suporte para várias plugins de plataforma.</span><span class="sxs-lookup"><span data-stu-id="929b6-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="929b6-105">Isso foi obtido com, criando um novo modelo de extensibilidade de plug-in, que deve estar de acordo com um conjunto restrito de regras de operação.</span><span class="sxs-lookup"><span data-stu-id="929b6-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="929b6-106">Os plug-ins são executáveis independentes (executáveis no mundo do .NET Core), que os clientes do NuGet Iniciar em um processo separado.</span><span class="sxs-lookup"><span data-stu-id="929b6-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="929b6-107">Trata-se de uma gravação true uma vez, execute em qualquer lugar de plug-in.</span><span class="sxs-lookup"><span data-stu-id="929b6-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="929b6-108">Ele funcionará com todas as ferramentas de cliente do NuGet.</span><span class="sxs-lookup"><span data-stu-id="929b6-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="929b6-109">Os plug-ins podem ser (NuGet.exe, MSBuild.exe e Visual Studio) do .NET Framework ou .NET Core (dotnet.exe).</span><span class="sxs-lookup"><span data-stu-id="929b6-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="929b6-110">Um protocolo de comunicação com controle de versão entre o cliente do NuGet e o plug-in é definido.</span><span class="sxs-lookup"><span data-stu-id="929b6-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="929b6-111">Durante o handshake de inicialização, os 2 processos negociam a versão do protocolo.</span><span class="sxs-lookup"><span data-stu-id="929b6-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="929b6-112">Para cobrir todos os cenários de ferramentas de cliente NuGet, é necessário um .NET Framework e um plug-in do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="929b6-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="929b6-113">A seguir descreve as combinações de estrutura do cliente dos plug-ins.</span><span class="sxs-lookup"><span data-stu-id="929b6-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="929b6-114">Ferramenta de cliente</span><span class="sxs-lookup"><span data-stu-id="929b6-114">Client tool</span></span>  | <span data-ttu-id="929b6-115">Framework</span><span class="sxs-lookup"><span data-stu-id="929b6-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="929b6-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="929b6-116">Visual Studio</span></span> | <span data-ttu-id="929b6-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="929b6-117">.NET Framework</span></span> |
| <span data-ttu-id="929b6-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="929b6-118">dotnet.exe</span></span> | <span data-ttu-id="929b6-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="929b6-119">.NET Core</span></span> |
| <span data-ttu-id="929b6-120">NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="929b6-120">NuGet.exe</span></span> | <span data-ttu-id="929b6-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="929b6-121">.NET Framework</span></span> |
| <span data-ttu-id="929b6-122">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="929b6-122">MSBuild.exe</span></span> | <span data-ttu-id="929b6-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="929b6-123">.NET Framework</span></span> |
| <span data-ttu-id="929b6-124">NuGet.exe no Mono</span><span class="sxs-lookup"><span data-stu-id="929b6-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="929b6-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="929b6-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="929b6-126">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="929b6-126">How does it work</span></span>

<span data-ttu-id="929b6-127">O fluxo de trabalho de alto nível pode ser descrito da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="929b6-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="929b6-128">NuGet descobre plug-ins disponíveis.</span><span class="sxs-lookup"><span data-stu-id="929b6-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="929b6-129">Quando aplicável, o NuGet irá iterar sobre os plug-ins na ordem de prioridade e inicia um um.</span><span class="sxs-lookup"><span data-stu-id="929b6-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="929b6-130">O NuGet usará o primeiro plug-in que pode atender à solicitação.</span><span class="sxs-lookup"><span data-stu-id="929b6-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="929b6-131">Os plug-ins serão desligados quando eles não são mais necessários.</span><span class="sxs-lookup"><span data-stu-id="929b6-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="929b6-132">Requisitos de plug-in de geral</span><span class="sxs-lookup"><span data-stu-id="929b6-132">General plugin requirements</span></span>

<span data-ttu-id="929b6-133">É a versão atual do protocolo *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="929b6-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="929b6-134">Nesta versão, os requisitos são:</span><span class="sxs-lookup"><span data-stu-id="929b6-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="929b6-135">Ter um assemblies de assinatura Authenticode válida e confiável que serão executado no Windows e Mono.</span><span class="sxs-lookup"><span data-stu-id="929b6-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="929b6-136">Não há nenhum requisito de confiança especiais para assemblies executados no Linux e Mac ainda.</span><span class="sxs-lookup"><span data-stu-id="929b6-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="929b6-137">Problema relevante</span><span class="sxs-lookup"><span data-stu-id="929b6-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="929b6-138">Suporte a iniciar sem monitoração de estado no contexto de segurança atual das ferramentas de cliente do NuGet.</span><span class="sxs-lookup"><span data-stu-id="929b6-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="929b6-139">Por exemplo, as ferramentas de cliente do NuGet não executará elevação ou inicialização adicional fora o protocolo de plug-in descrito posteriormente.</span><span class="sxs-lookup"><span data-stu-id="929b6-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="929b6-140">Ser não interativo, a menos que explicitamente especificado.</span><span class="sxs-lookup"><span data-stu-id="929b6-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="929b6-141">Seguir a versão do protocolo negociado plug-in.</span><span class="sxs-lookup"><span data-stu-id="929b6-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="929b6-142">Responda a todas as solicitações em um período de tempo razoável.</span><span class="sxs-lookup"><span data-stu-id="929b6-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="929b6-143">Cumpram as solicitações de cancelamento para qualquer operação em andamento.</span><span class="sxs-lookup"><span data-stu-id="929b6-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="929b6-144">A especificação técnica é descrita mais detalhadamente nas seguintes especificações:</span><span class="sxs-lookup"><span data-stu-id="929b6-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="929b6-145">Plug-in de Download de pacote do NuGet</span><span class="sxs-lookup"><span data-stu-id="929b6-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="929b6-146">NuGet cruzada plug-in de autenticação de várias plataformas</span><span class="sxs-lookup"><span data-stu-id="929b6-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="929b6-147">Cliente - interação de plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-147">Client - Plugin interaction</span></span>

<span data-ttu-id="929b6-148">Os plug-ins e ferramentas de cliente do NuGet se comunicar com JSON em fluxos padrão (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="929b6-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="929b6-149">Todos os dados devem ser codificados em UTF-8.</span><span class="sxs-lookup"><span data-stu-id="929b6-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="929b6-150">Os plug-ins são iniciados com o argumento "-plug-in".</span><span class="sxs-lookup"><span data-stu-id="929b6-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="929b6-151">No caso de um usuário inicia diretamente um plug-in do arquivo executável sem esse argumento, o plug-in pode fornecer uma mensagem informativa em vez de esperar um handshake de protocolo.</span><span class="sxs-lookup"><span data-stu-id="929b6-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="929b6-152">Tempo limite de handshake do protocolo é 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="929b6-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="929b6-153">O plug-in deve concluir a configuração no como sem que seja necessário um valor possível.</span><span class="sxs-lookup"><span data-stu-id="929b6-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="929b6-154">Ferramentas de cliente do NuGet consultará operações com suporte do plug-in, passando o índice de serviço para uma fonte do NuGet.</span><span class="sxs-lookup"><span data-stu-id="929b6-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="929b6-155">Um plug-in pode usar o índice de serviço para verificar a presença de tipos de serviço com suporte.</span><span class="sxs-lookup"><span data-stu-id="929b6-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="929b6-156">A comunicação entre as ferramentas de cliente do NuGet e o plug-in é bidirecional.</span><span class="sxs-lookup"><span data-stu-id="929b6-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="929b6-157">Cada solicitação tem um tempo limite de 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="929b6-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="929b6-158">Se as operações devem para levar mais tempo o processo respectivo deve enviar uma mensagem de progresso para impedir que a solicitação atingir o tempo limite. Após um minuto de inatividade um plug-in é considerado ocioso e é desligado.</span><span class="sxs-lookup"><span data-stu-id="929b6-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="929b6-159">Descoberta e instalação do plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-159">Plugin installation and discovery</span></span>

<span data-ttu-id="929b6-160">Os plug-ins serão descobertos por meio de uma estrutura de diretório baseado na convenção.</span><span class="sxs-lookup"><span data-stu-id="929b6-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="929b6-161">Cenários de CI/CD e usuários avançados podem usar uma variável de ambiente para substituir o comportamento.</span><span class="sxs-lookup"><span data-stu-id="929b6-161">CI/CD scenarios and power users can use an environment variable to override the behavior.</span></span>

- <span data-ttu-id="929b6-162">`NUGET_PLUGIN_PATHS` -Define os plug-ins que serão usados para esse processo do NuGet, prioridade reservado.</span><span class="sxs-lookup"><span data-stu-id="929b6-162">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="929b6-163">Se essa variável de ambiente for definida, ela substitui a descoberta baseado na convenção.</span><span class="sxs-lookup"><span data-stu-id="929b6-163">If this environment variable is set, it overrides the convention based discovery.</span></span>
-  <span data-ttu-id="929b6-164">Local do usuário, o local da página inicial do NuGet em `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="929b6-164">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="929b6-165">Esse local não pode ser substituído.</span><span class="sxs-lookup"><span data-stu-id="929b6-165">This location cannot be overriden.</span></span> <span data-ttu-id="929b6-166">Um diretório raiz diferente será usado para o plug-ins do .NET Core e .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="929b6-166">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="929b6-167">Framework</span><span class="sxs-lookup"><span data-stu-id="929b6-167">Framework</span></span> | <span data-ttu-id="929b6-168">Local de detecção de raiz</span><span class="sxs-lookup"><span data-stu-id="929b6-168">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="929b6-169">.NET Core</span><span class="sxs-lookup"><span data-stu-id="929b6-169">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="929b6-170">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="929b6-170">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="929b6-171">Cada plug-in deve ser instalado em sua própria pasta.</span><span class="sxs-lookup"><span data-stu-id="929b6-171">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="929b6-172">O ponto de entrada do plug-in será o nome da pasta instalado, com as extensões. dll para o .NET Core e a extensão .exe para o .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="929b6-172">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> <span data-ttu-id="929b6-173">Atualmente, não há nenhuma história de usuário para a instalação dos plug-ins.</span><span class="sxs-lookup"><span data-stu-id="929b6-173">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="929b6-174">Ele é tão simple quanto mover os arquivos necessários para o local predeterminado.</span><span class="sxs-lookup"><span data-stu-id="929b6-174">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="929b6-175">Operações com suporte</span><span class="sxs-lookup"><span data-stu-id="929b6-175">Supported operations</span></span>

<span data-ttu-id="929b6-176">Duas operações têm suporte com o novo protocolo de plug-in.</span><span class="sxs-lookup"><span data-stu-id="929b6-176">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="929b6-177">Nome da operação</span><span class="sxs-lookup"><span data-stu-id="929b6-177">Operation name</span></span> | <span data-ttu-id="929b6-178">Versão mínima do protocolo</span><span class="sxs-lookup"><span data-stu-id="929b6-178">Minimum protocol version</span></span> | <span data-ttu-id="929b6-179">Versão mínima do cliente do NuGet</span><span class="sxs-lookup"><span data-stu-id="929b6-179">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="929b6-180">Baixe o pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-180">Download Package</span></span> | <span data-ttu-id="929b6-181">1.0.0</span><span class="sxs-lookup"><span data-stu-id="929b6-181">1.0.0</span></span> | <span data-ttu-id="929b6-182">4.3.0</span><span class="sxs-lookup"><span data-stu-id="929b6-182">4.3.0</span></span> |
| [<span data-ttu-id="929b6-183">Autenticação</span><span class="sxs-lookup"><span data-stu-id="929b6-183">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="929b6-184">2.0.0</span><span class="sxs-lookup"><span data-stu-id="929b6-184">2.0.0</span></span> | <span data-ttu-id="929b6-185">4.8.0</span><span class="sxs-lookup"><span data-stu-id="929b6-185">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="929b6-186">Executando plug-ins no tempo de execução correto</span><span class="sxs-lookup"><span data-stu-id="929b6-186">Running plugins under the correct runtime</span></span>

<span data-ttu-id="929b6-187">Para o NuGet em cenários de dotnet.exe, plug-ins precisam poder ser executado sob esse tempo de execução específico do dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="929b6-187">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="929b6-188">É o provedor de plug-in e o consumidor para certificar-se de que uma combinação de dotnet.exe/plugin compatível é usada.</span><span class="sxs-lookup"><span data-stu-id="929b6-188">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="929b6-189">Um problema em potencial que poderia surgir com o local do usuário plug-ins quando, por exemplo, um dotnet.exe no tempo de execução 2.0 tenta usar um plug-in escrito para o tempo de execução 2.1.</span><span class="sxs-lookup"><span data-stu-id="929b6-189">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="929b6-190">Recursos de armazenamento em cache</span><span class="sxs-lookup"><span data-stu-id="929b6-190">Capabilities caching</span></span>

<span data-ttu-id="929b6-191">A verificação de segurança e a instanciação dos plug-ins é caro.</span><span class="sxs-lookup"><span data-stu-id="929b6-191">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="929b6-192">A operação de download acontece com muito mais frequência do que a operação de autenticação, no entanto, o usuário médio do NuGet só é provavelmente terá um plug-in de autenticação.</span><span class="sxs-lookup"><span data-stu-id="929b6-192">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="929b6-193">Para melhorar a experiência, o NuGet armazenará em cache as declarações de operação para a solicitação em questão.</span><span class="sxs-lookup"><span data-stu-id="929b6-193">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="929b6-194">Esse cache é por plug-in com a chave de plug-in que está sendo o caminho de plug-in e a expiração para esse cache de recursos é de 30 dias.</span><span class="sxs-lookup"><span data-stu-id="929b6-194">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="929b6-195">O cache está localizado em `%LocalAppData%/NuGet/plugins-cache` e ser substituída com a variável de ambiente `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="929b6-195">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="929b6-196">Para limpar esse [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), os locais pode ser executada com o `plugins-cache` opção.</span><span class="sxs-lookup"><span data-stu-id="929b6-196">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="929b6-197">O `all` opção locais agora também excluirá o cache de plug-ins.</span><span class="sxs-lookup"><span data-stu-id="929b6-197">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="929b6-198">Índice de mensagens de protocolo</span><span class="sxs-lookup"><span data-stu-id="929b6-198">Protocol messages index</span></span>

<span data-ttu-id="929b6-199">Versão do protocolo *1.0.0* mensagens:</span><span class="sxs-lookup"><span data-stu-id="929b6-199">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="929b6-200">Fechar</span><span class="sxs-lookup"><span data-stu-id="929b6-200">Close</span></span>
    * <span data-ttu-id="929b6-201">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-201">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="929b6-202">A solicitação não irá conter nenhuma carga útil</span><span class="sxs-lookup"><span data-stu-id="929b6-202">The request will contain no payload</span></span>
    * <span data-ttu-id="929b6-203">Nenhuma resposta é esperada.</span><span class="sxs-lookup"><span data-stu-id="929b6-203">No response is expected.</span></span>  <span data-ttu-id="929b6-204">A resposta correta é para o processo de plug-in seja encerrado imediatamente.</span><span class="sxs-lookup"><span data-stu-id="929b6-204">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="929b6-205">Copiar arquivos de pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-205">Copy files in package</span></span>
    * <span data-ttu-id="929b6-206">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-206">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="929b6-207">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-207">The request will contain:</span></span>
        * <span data-ttu-id="929b6-208">a ID do pacote e versão</span><span class="sxs-lookup"><span data-stu-id="929b6-208">the package ID and version</span></span>
        * <span data-ttu-id="929b6-209">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-209">the package source repository location</span></span>
        * <span data-ttu-id="929b6-210">caminho do diretório de destino</span><span class="sxs-lookup"><span data-stu-id="929b6-210">destination directory path</span></span>
        * <span data-ttu-id="929b6-211">um enumerável de arquivos no pacote a ser copiado para o caminho do diretório de destino</span><span class="sxs-lookup"><span data-stu-id="929b6-211">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="929b6-212">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-212">A response will contain:</span></span>
        * <span data-ttu-id="929b6-213">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="929b6-213">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="929b6-214">um enumerável de caminhos completos para arquivos copiados no diretório de destino, se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="929b6-214">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="929b6-215">Copie o arquivo de pacote (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="929b6-215">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="929b6-216">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-216">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="929b6-217">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-217">The request will contain:</span></span>
        * <span data-ttu-id="929b6-218">a ID do pacote e versão</span><span class="sxs-lookup"><span data-stu-id="929b6-218">the package ID and version</span></span>
        * <span data-ttu-id="929b6-219">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-219">the package source repository location</span></span>
        * <span data-ttu-id="929b6-220">o caminho do arquivo de destino</span><span class="sxs-lookup"><span data-stu-id="929b6-220">the destination file path</span></span>
    * <span data-ttu-id="929b6-221">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-221">A response will contain:</span></span>
        * <span data-ttu-id="929b6-222">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="929b6-222">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="929b6-223">Obter credenciais</span><span class="sxs-lookup"><span data-stu-id="929b6-223">Get credentials</span></span>
    * <span data-ttu-id="929b6-224">Direção de solicitação: plug-in -> NuGet</span><span class="sxs-lookup"><span data-stu-id="929b6-224">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="929b6-225">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-225">The request will contain:</span></span>
        * <span data-ttu-id="929b6-226">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-226">the package source repository location</span></span>
        * <span data-ttu-id="929b6-227">o código de status HTTP obtido no repositório de origem do pacote usando as credenciais atuais</span><span class="sxs-lookup"><span data-stu-id="929b6-227">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="929b6-228">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-228">A response will contain:</span></span>
        * <span data-ttu-id="929b6-229">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="929b6-229">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="929b6-230">um nome de usuário, se disponível</span><span class="sxs-lookup"><span data-stu-id="929b6-230">a username, if available</span></span>
        * <span data-ttu-id="929b6-231">uma senha, se disponível</span><span class="sxs-lookup"><span data-stu-id="929b6-231">a password, if available</span></span>

5.  <span data-ttu-id="929b6-232">Obter os arquivos no pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-232">Get files in package</span></span>
    * <span data-ttu-id="929b6-233">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-233">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="929b6-234">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-234">The request will contain:</span></span>
        * <span data-ttu-id="929b6-235">a ID do pacote e versão</span><span class="sxs-lookup"><span data-stu-id="929b6-235">the package ID and version</span></span>
        * <span data-ttu-id="929b6-236">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-236">the package source repository location</span></span>
    * <span data-ttu-id="929b6-237">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-237">A response will contain:</span></span>
        * <span data-ttu-id="929b6-238">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="929b6-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="929b6-239">um enumerável de caminhos de arquivo no pacote se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="929b6-239">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="929b6-240">Obter declarações de operação</span><span class="sxs-lookup"><span data-stu-id="929b6-240">Get operation claims</span></span> 
    * <span data-ttu-id="929b6-241">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="929b6-242">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-242">The request will contain:</span></span>
        * <span data-ttu-id="929b6-243">o serviço index.json para uma origem de pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-243">the service index.json for a package source</span></span>
        * <span data-ttu-id="929b6-244">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-244">the package source repository location</span></span>
    * <span data-ttu-id="929b6-245">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-245">A response will contain:</span></span>
        * <span data-ttu-id="929b6-246">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="929b6-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="929b6-247">um enumerável de operações com suporte (por exemplo: download do pacote) se a operação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="929b6-247">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="929b6-248">Se um plug-in não oferece suporte a origem do pacote, o plug-in deve retornar um conjunto vazio de operações com suporte.</span><span class="sxs-lookup"><span data-stu-id="929b6-248">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="929b6-249">Esta mensagem foi atualizada na versão *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="929b6-249">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="929b6-250">É no cliente para preservar a compatibilidade com versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="929b6-250">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="929b6-251">Obter o hash do pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-251">Get package hash</span></span>
    * <span data-ttu-id="929b6-252">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-252">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="929b6-253">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-253">The request will contain:</span></span>
        * <span data-ttu-id="929b6-254">a ID do pacote e versão</span><span class="sxs-lookup"><span data-stu-id="929b6-254">the package ID and version</span></span>
        * <span data-ttu-id="929b6-255">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-255">the package source repository location</span></span>
        * <span data-ttu-id="929b6-256">o algoritmo de hash</span><span class="sxs-lookup"><span data-stu-id="929b6-256">the hash algorithm</span></span>
    * <span data-ttu-id="929b6-257">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-257">A response will contain:</span></span>
        * <span data-ttu-id="929b6-258">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="929b6-258">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="929b6-259">um hash do arquivo de pacote usando o algoritmo de hash solicitado, se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="929b6-259">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="929b6-260">Obter versões de pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-260">Get package versions</span></span>
    * <span data-ttu-id="929b6-261">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="929b6-262">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-262">The request will contain:</span></span>
        * <span data-ttu-id="929b6-263">a ID do pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-263">the package ID</span></span>
        * <span data-ttu-id="929b6-264">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-264">the package source repository location</span></span>
    * <span data-ttu-id="929b6-265">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-265">A response will contain:</span></span>
        * <span data-ttu-id="929b6-266">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="929b6-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="929b6-267">um enumerável de versões do pacote se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="929b6-267">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="929b6-268">Obter índice de serviço</span><span class="sxs-lookup"><span data-stu-id="929b6-268">Get service index</span></span>
    * <span data-ttu-id="929b6-269">Direção de solicitação: plug-in -> NuGet</span><span class="sxs-lookup"><span data-stu-id="929b6-269">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="929b6-270">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-270">The request will contain:</span></span>
        * <span data-ttu-id="929b6-271">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-271">the package source repository location</span></span>
    * <span data-ttu-id="929b6-272">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-272">A response will contain:</span></span>
        * <span data-ttu-id="929b6-273">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="929b6-273">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="929b6-274">o índice de serviço se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="929b6-274">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="929b6-275">Handshake</span><span class="sxs-lookup"><span data-stu-id="929b6-275">Handshake</span></span>
     * <span data-ttu-id="929b6-276">Direção de solicitação: plug-in do NuGet <> –</span><span class="sxs-lookup"><span data-stu-id="929b6-276">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="929b6-277">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-277">The request will contain:</span></span>
         * <span data-ttu-id="929b6-278">a versão atual do protocolo de plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-278">the current plugin protocol version</span></span>
         * <span data-ttu-id="929b6-279">a versão do protocolo de plug-in com suporte mínimo</span><span class="sxs-lookup"><span data-stu-id="929b6-279">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="929b6-280">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-280">A response will contain:</span></span>
         * <span data-ttu-id="929b6-281">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="929b6-281">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="929b6-282">a versão do protocolo negociado se a operação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="929b6-282">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="929b6-283">Uma falha resultará no encerramento do plug-in.</span><span class="sxs-lookup"><span data-stu-id="929b6-283">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="929b6-284">inicializar</span><span class="sxs-lookup"><span data-stu-id="929b6-284">Initialize</span></span>
     * <span data-ttu-id="929b6-285">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-285">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="929b6-286">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-286">The request will contain:</span></span>
         * <span data-ttu-id="929b6-287">a versão da ferramenta cliente NuGet</span><span class="sxs-lookup"><span data-stu-id="929b6-287">the NuGet client tool version</span></span>
         * <span data-ttu-id="929b6-288">o NuGet ferramenta efetivação idioma do cliente.</span><span class="sxs-lookup"><span data-stu-id="929b6-288">the NuGet client tool effective language.</span></span>  <span data-ttu-id="929b6-289">Isso leva em consideração a configuração de ForceEnglishOutput, se usado.</span><span class="sxs-lookup"><span data-stu-id="929b6-289">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="929b6-290">o padrão tempo limite da solicitação, que substitui o padrão de protocolo.</span><span class="sxs-lookup"><span data-stu-id="929b6-290">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="929b6-291">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-291">A response will contain:</span></span>
         * <span data-ttu-id="929b6-292">um código de resposta que indica o resultado da operação.</span><span class="sxs-lookup"><span data-stu-id="929b6-292">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="929b6-293">Uma falha resultará no encerramento do plug-in.</span><span class="sxs-lookup"><span data-stu-id="929b6-293">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="929b6-294">Log</span><span class="sxs-lookup"><span data-stu-id="929b6-294">Log</span></span>
     * <span data-ttu-id="929b6-295">Direção de solicitação: plug-in -> NuGet</span><span class="sxs-lookup"><span data-stu-id="929b6-295">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="929b6-296">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-296">The request will contain:</span></span>
         * <span data-ttu-id="929b6-297">o nível de log para a solicitação</span><span class="sxs-lookup"><span data-stu-id="929b6-297">the log level for the request</span></span>
         * <span data-ttu-id="929b6-298">uma mensagem de log</span><span class="sxs-lookup"><span data-stu-id="929b6-298">a message to log</span></span>
     * <span data-ttu-id="929b6-299">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-299">A response will contain:</span></span>
         * <span data-ttu-id="929b6-300">um código de resposta que indica o resultado da operação.</span><span class="sxs-lookup"><span data-stu-id="929b6-300">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="929b6-301">Monitorar a saída do processo de NuGet</span><span class="sxs-lookup"><span data-stu-id="929b6-301">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="929b6-302">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-302">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="929b6-303">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-303">The request will contain:</span></span>
         * <span data-ttu-id="929b6-304">a ID de processo do NuGet</span><span class="sxs-lookup"><span data-stu-id="929b6-304">the NuGet process ID</span></span>
     * <span data-ttu-id="929b6-305">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-305">A response will contain:</span></span>
         * <span data-ttu-id="929b6-306">um código de resposta que indica o resultado da operação.</span><span class="sxs-lookup"><span data-stu-id="929b6-306">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="929b6-307">Pacote de pré-busca</span><span class="sxs-lookup"><span data-stu-id="929b6-307">Prefetch package</span></span>
     * <span data-ttu-id="929b6-308">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-308">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="929b6-309">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-309">The request will contain:</span></span>
         * <span data-ttu-id="929b6-310">a ID do pacote e versão</span><span class="sxs-lookup"><span data-stu-id="929b6-310">the package ID and version</span></span>
         * <span data-ttu-id="929b6-311">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-311">the package source repository location</span></span>
     * <span data-ttu-id="929b6-312">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-312">A response will contain:</span></span>
         * <span data-ttu-id="929b6-313">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="929b6-313">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="929b6-314">Definir credenciais</span><span class="sxs-lookup"><span data-stu-id="929b6-314">Set credentials</span></span>
     * <span data-ttu-id="929b6-315">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-315">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="929b6-316">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-316">The request will contain:</span></span>
         * <span data-ttu-id="929b6-317">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-317">the package source repository location</span></span>
         * <span data-ttu-id="929b6-318">último pacote conhecidos origem nome de usuário, se disponível</span><span class="sxs-lookup"><span data-stu-id="929b6-318">the last known package source username, if available</span></span>
         * <span data-ttu-id="929b6-319">a última senha de origem de pacotes conhecidas, se disponível</span><span class="sxs-lookup"><span data-stu-id="929b6-319">the last known package source password, if available</span></span>
         * <span data-ttu-id="929b6-320">o último proxy conhecidos nome de usuário, se disponível</span><span class="sxs-lookup"><span data-stu-id="929b6-320">the last known proxy username, if available</span></span>
         * <span data-ttu-id="929b6-321">a última senha proxy conhecidos, se disponível</span><span class="sxs-lookup"><span data-stu-id="929b6-321">the last known proxy password, if available</span></span>
     * <span data-ttu-id="929b6-322">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-322">A response will contain:</span></span>
         * <span data-ttu-id="929b6-323">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="929b6-323">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="929b6-324">Definir o nível de log</span><span class="sxs-lookup"><span data-stu-id="929b6-324">Set log level</span></span>
     * <span data-ttu-id="929b6-325">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-325">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="929b6-326">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-326">The request will contain:</span></span>
         * <span data-ttu-id="929b6-327">o nível de log padrão</span><span class="sxs-lookup"><span data-stu-id="929b6-327">the default log level</span></span>
     * <span data-ttu-id="929b6-328">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-328">A response will contain:</span></span>
         * <span data-ttu-id="929b6-329">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="929b6-329">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="929b6-330">Versão do protocolo *2.0.0* mensagens</span><span class="sxs-lookup"><span data-stu-id="929b6-330">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="929b6-331">Obter declarações de operação</span><span class="sxs-lookup"><span data-stu-id="929b6-331">Get Operation Claims</span></span>

* <span data-ttu-id="929b6-332">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-332">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="929b6-333">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-333">The request will contain:</span></span>
        * <span data-ttu-id="929b6-334">o serviço index.json para uma origem de pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-334">the service index.json for a package source</span></span>
        * <span data-ttu-id="929b6-335">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="929b6-335">the package source repository location</span></span>
    * <span data-ttu-id="929b6-336">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-336">A response will contain:</span></span>
        * <span data-ttu-id="929b6-337">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="929b6-337">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="929b6-338">um enumerável de operações com suporte se a operação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="929b6-338">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="929b6-339">Se um plug-in não oferece suporte a origem do pacote, o plug-in deve retornar um conjunto vazio de operações com suporte.</span><span class="sxs-lookup"><span data-stu-id="929b6-339">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="929b6-340">Se a origem de índice e o pacote de serviço forem nula, o plug-in pode responder com a autenticação.</span><span class="sxs-lookup"><span data-stu-id="929b6-340">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="929b6-341">Obter credenciais de autenticação</span><span class="sxs-lookup"><span data-stu-id="929b6-341">Get Authentication Credentials</span></span>

* <span data-ttu-id="929b6-342">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="929b6-342">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="929b6-343">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="929b6-343">The request will contain:</span></span>
    * <span data-ttu-id="929b6-344">URI</span><span class="sxs-lookup"><span data-stu-id="929b6-344">Uri</span></span>
    * <span data-ttu-id="929b6-345">isRetry</span><span class="sxs-lookup"><span data-stu-id="929b6-345">isRetry</span></span>
    * <span data-ttu-id="929b6-346">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="929b6-346">NonInteractive</span></span>
    * <span data-ttu-id="929b6-347">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="929b6-347">CanShowDialog</span></span>
* <span data-ttu-id="929b6-348">Uma resposta irá conter</span><span class="sxs-lookup"><span data-stu-id="929b6-348">A response will contain</span></span>
    * <span data-ttu-id="929b6-349">Nome de usuário</span><span class="sxs-lookup"><span data-stu-id="929b6-349">Username</span></span>
    * <span data-ttu-id="929b6-350">Senha</span><span class="sxs-lookup"><span data-stu-id="929b6-350">Password</span></span>
    * <span data-ttu-id="929b6-351">Mensagem</span><span class="sxs-lookup"><span data-stu-id="929b6-351">Message</span></span>
    * <span data-ttu-id="929b6-352">Lista de tipos de autenticação</span><span class="sxs-lookup"><span data-stu-id="929b6-352">List of Auth Types</span></span>
    * <span data-ttu-id="929b6-353">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="929b6-353">MessageResponseCode</span></span>