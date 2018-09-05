---
title: NuGet cruzada plugins de plataforma
description: NuGet cross plugins de plataforma para NuGet.exe, dotnet.exe, msbuild.exe e Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: fdefc5b6189051fd83b2de644080284c09dd85f4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548200"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="f3546-103">NuGet cruzada plugins de plataforma</span><span class="sxs-lookup"><span data-stu-id="f3546-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="f3546-104">No NuGet 4.8 + foi adicionado suporte para várias plugins de plataforma.</span><span class="sxs-lookup"><span data-stu-id="f3546-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="f3546-105">Isso foi obtido com, criando um novo modelo de extensibilidade de plug-in, que deve estar de acordo com um conjunto restrito de regras de operação.</span><span class="sxs-lookup"><span data-stu-id="f3546-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="f3546-106">Os plug-ins são executáveis independentes (executáveis no mundo do .NET Core), que os clientes do NuGet Iniciar em um processo separado.</span><span class="sxs-lookup"><span data-stu-id="f3546-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="f3546-107">Trata-se de uma gravação true uma vez, execute em qualquer lugar de plug-in.</span><span class="sxs-lookup"><span data-stu-id="f3546-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="f3546-108">Ele funcionará com todas as ferramentas de cliente do NuGet.</span><span class="sxs-lookup"><span data-stu-id="f3546-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="f3546-109">Os plug-ins podem ser (NuGet.exe, MSBuild.exe e Visual Studio) do .NET Framework ou .NET Core (dotnet.exe).</span><span class="sxs-lookup"><span data-stu-id="f3546-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="f3546-110">Um protocolo de comunicação com controle de versão entre o cliente do NuGet e o plug-in é definido.</span><span class="sxs-lookup"><span data-stu-id="f3546-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="f3546-111">Durante o handshake de inicialização, os 2 processos negociam a versão do protocolo.</span><span class="sxs-lookup"><span data-stu-id="f3546-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="f3546-112">Para cobrir todos os cenários de ferramentas de cliente NuGet, é necessário um .NET Framework e um plug-in do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f3546-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="f3546-113">A seguir descreve as combinações de estrutura do cliente dos plug-ins.</span><span class="sxs-lookup"><span data-stu-id="f3546-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="f3546-114">Ferramenta de cliente</span><span class="sxs-lookup"><span data-stu-id="f3546-114">Client tool</span></span>  | <span data-ttu-id="f3546-115">Framework</span><span class="sxs-lookup"><span data-stu-id="f3546-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="f3546-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f3546-116">Visual Studio</span></span> | <span data-ttu-id="f3546-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f3546-117">.NET Framework</span></span> |
| <span data-ttu-id="f3546-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="f3546-118">dotnet.exe</span></span> | <span data-ttu-id="f3546-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f3546-119">.NET Core</span></span> |
| <span data-ttu-id="f3546-120">NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="f3546-120">NuGet.exe</span></span> | <span data-ttu-id="f3546-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f3546-121">.NET Framework</span></span> |
| <span data-ttu-id="f3546-122">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="f3546-122">MSBuild.exe</span></span> | <span data-ttu-id="f3546-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f3546-123">.NET Framework</span></span> |
| <span data-ttu-id="f3546-124">NuGet.exe no Mono</span><span class="sxs-lookup"><span data-stu-id="f3546-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="f3546-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f3546-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="f3546-126">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="f3546-126">How does it work</span></span>

<span data-ttu-id="f3546-127">O fluxo de trabalho de alto nível pode ser descrito da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f3546-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="f3546-128">NuGet descobre plug-ins disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f3546-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="f3546-129">Quando aplicável, o NuGet irá iterar sobre os plug-ins na ordem de prioridade e inicia um um.</span><span class="sxs-lookup"><span data-stu-id="f3546-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="f3546-130">O NuGet usará o primeiro plug-in que pode atender à solicitação.</span><span class="sxs-lookup"><span data-stu-id="f3546-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="f3546-131">Os plug-ins serão desligados quando eles não são mais necessários.</span><span class="sxs-lookup"><span data-stu-id="f3546-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="f3546-132">Requisitos de plug-in de geral</span><span class="sxs-lookup"><span data-stu-id="f3546-132">General plugin requirements</span></span>

<span data-ttu-id="f3546-133">É a versão atual do protocolo *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="f3546-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="f3546-134">Nesta versão, os requisitos são:</span><span class="sxs-lookup"><span data-stu-id="f3546-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="f3546-135">Ter um assemblies de assinatura Authenticode válida e confiável que serão executado no Windows e Mono.</span><span class="sxs-lookup"><span data-stu-id="f3546-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="f3546-136">Não há nenhum requisito de confiança especiais para assemblies executados no Linux e Mac ainda.</span><span class="sxs-lookup"><span data-stu-id="f3546-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="f3546-137">Problema relevante</span><span class="sxs-lookup"><span data-stu-id="f3546-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="f3546-138">Suporte a iniciar sem monitoração de estado no contexto de segurança atual das ferramentas de cliente do NuGet.</span><span class="sxs-lookup"><span data-stu-id="f3546-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="f3546-139">Por exemplo, as ferramentas de cliente do NuGet não executará elevação ou inicialização adicional fora o protocolo de plug-in descrito posteriormente.</span><span class="sxs-lookup"><span data-stu-id="f3546-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="f3546-140">Ser não interativo, a menos que explicitamente especificado.</span><span class="sxs-lookup"><span data-stu-id="f3546-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="f3546-141">Seguir a versão do protocolo negociado plug-in.</span><span class="sxs-lookup"><span data-stu-id="f3546-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="f3546-142">Responda a todas as solicitações em um período de tempo razoável.</span><span class="sxs-lookup"><span data-stu-id="f3546-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="f3546-143">Cumpram as solicitações de cancelamento para qualquer operação em andamento.</span><span class="sxs-lookup"><span data-stu-id="f3546-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="f3546-144">A especificação técnica é descrita mais detalhadamente nas seguintes especificações:</span><span class="sxs-lookup"><span data-stu-id="f3546-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="f3546-145">Plug-in de Download de pacote do NuGet</span><span class="sxs-lookup"><span data-stu-id="f3546-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="f3546-146">NuGet cruzada plug-in de autenticação de várias plataformas</span><span class="sxs-lookup"><span data-stu-id="f3546-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="f3546-147">Cliente - interação de plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-147">Client - Plugin interaction</span></span>

<span data-ttu-id="f3546-148">Os plug-ins e ferramentas de cliente do NuGet se comunicar com JSON em fluxos padrão (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="f3546-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="f3546-149">Todos os dados devem ser codificados em UTF-8.</span><span class="sxs-lookup"><span data-stu-id="f3546-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="f3546-150">Os plug-ins são iniciados com o argumento "-plug-in".</span><span class="sxs-lookup"><span data-stu-id="f3546-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="f3546-151">No caso de um usuário inicia diretamente um plug-in do arquivo executável sem esse argumento, o plug-in pode fornecer uma mensagem informativa em vez de esperar um handshake de protocolo.</span><span class="sxs-lookup"><span data-stu-id="f3546-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="f3546-152">Tempo limite de handshake do protocolo é 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="f3546-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="f3546-153">O plug-in deve concluir a configuração no como sem que seja necessário um valor possível.</span><span class="sxs-lookup"><span data-stu-id="f3546-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="f3546-154">Ferramentas de cliente do NuGet consultará operações com suporte do plug-in, passando o índice de serviço para uma fonte do NuGet.</span><span class="sxs-lookup"><span data-stu-id="f3546-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="f3546-155">Um plug-in pode usar o índice de serviço para verificar a presença de tipos de serviço com suporte.</span><span class="sxs-lookup"><span data-stu-id="f3546-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="f3546-156">A comunicação entre as ferramentas de cliente do NuGet e o plug-in é bidirecional.</span><span class="sxs-lookup"><span data-stu-id="f3546-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="f3546-157">Cada solicitação tem um tempo limite de 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="f3546-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="f3546-158">Se as operações devem para levar mais tempo o processo respectivo deve enviar uma mensagem de progresso para impedir que a solicitação atingir o tempo limite. Após um minuto de inatividade um plug-in é considerado ocioso e é desligado.</span><span class="sxs-lookup"><span data-stu-id="f3546-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="f3546-159">Descoberta e instalação do plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-159">Plugin installation and discovery</span></span>

<span data-ttu-id="f3546-160">Os plug-ins serão descobertos por meio de uma estrutura de diretório baseado na convenção.</span><span class="sxs-lookup"><span data-stu-id="f3546-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="f3546-161">Cenários de CI/CD e usuários avançados podem usar uma variável de ambiente para substituir o comportamento.</span><span class="sxs-lookup"><span data-stu-id="f3546-161">CI/CD scenarios and power users can use an environment variable to override the behavior.</span></span>

- <span data-ttu-id="f3546-162">`NUGET_PLUGIN_PATHS` -Define os plug-ins que serão usados para esse processo do NuGet, prioridade reservado.</span><span class="sxs-lookup"><span data-stu-id="f3546-162">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="f3546-163">Se essa variável de ambiente for definida, ela substitui a descoberta baseado na convenção.</span><span class="sxs-lookup"><span data-stu-id="f3546-163">If this environment variable is set, it overrides the convention based discovery.</span></span>
-  <span data-ttu-id="f3546-164">Local do usuário, o local da página inicial do NuGet em `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="f3546-164">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="f3546-165">Esse local não pode ser substituído.</span><span class="sxs-lookup"><span data-stu-id="f3546-165">This location cannot be overriden.</span></span> <span data-ttu-id="f3546-166">Um diretório raiz diferente será usado para o plug-ins do .NET Core e .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f3546-166">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="f3546-167">Framework</span><span class="sxs-lookup"><span data-stu-id="f3546-167">Framework</span></span> | <span data-ttu-id="f3546-168">Local de detecção de raiz</span><span class="sxs-lookup"><span data-stu-id="f3546-168">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="f3546-169">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f3546-169">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="f3546-170">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f3546-170">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="f3546-171">Cada plug-in deve ser instalado em sua própria pasta.</span><span class="sxs-lookup"><span data-stu-id="f3546-171">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="f3546-172">O ponto de entrada do plug-in será o nome da pasta instalado, com as extensões. dll para o .NET Core e a extensão .exe para o .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f3546-172">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="f3546-173">Atualmente, não há nenhuma história de usuário para a instalação dos plug-ins.</span><span class="sxs-lookup"><span data-stu-id="f3546-173">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="f3546-174">Ele é tão simple quanto mover os arquivos necessários para o local predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f3546-174">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="f3546-175">Operações com suporte</span><span class="sxs-lookup"><span data-stu-id="f3546-175">Supported operations</span></span>

<span data-ttu-id="f3546-176">Duas operações têm suporte com o novo protocolo de plug-in.</span><span class="sxs-lookup"><span data-stu-id="f3546-176">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="f3546-177">Nome da operação</span><span class="sxs-lookup"><span data-stu-id="f3546-177">Operation name</span></span> | <span data-ttu-id="f3546-178">Versão mínima do protocolo</span><span class="sxs-lookup"><span data-stu-id="f3546-178">Minimum protocol version</span></span> | <span data-ttu-id="f3546-179">Versão mínima do cliente do NuGet</span><span class="sxs-lookup"><span data-stu-id="f3546-179">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="f3546-180">Baixe o pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-180">Download Package</span></span> | <span data-ttu-id="f3546-181">1.0.0</span><span class="sxs-lookup"><span data-stu-id="f3546-181">1.0.0</span></span> | <span data-ttu-id="f3546-182">4.3.0</span><span class="sxs-lookup"><span data-stu-id="f3546-182">4.3.0</span></span> |
| [<span data-ttu-id="f3546-183">Autenticação</span><span class="sxs-lookup"><span data-stu-id="f3546-183">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="f3546-184">2.0.0</span><span class="sxs-lookup"><span data-stu-id="f3546-184">2.0.0</span></span> | <span data-ttu-id="f3546-185">4.8.0</span><span class="sxs-lookup"><span data-stu-id="f3546-185">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="f3546-186">Executando plug-ins no tempo de execução correto</span><span class="sxs-lookup"><span data-stu-id="f3546-186">Running plugins under the correct runtime</span></span>

<span data-ttu-id="f3546-187">Para o NuGet em cenários de dotnet.exe, plug-ins precisam poder ser executado sob esse tempo de execução específico do dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="f3546-187">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="f3546-188">É o provedor de plug-in e o consumidor para certificar-se de que uma combinação de dotnet.exe/plugin compatível é usada.</span><span class="sxs-lookup"><span data-stu-id="f3546-188">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="f3546-189">Um problema em potencial que poderia surgir com o local do usuário plug-ins quando, por exemplo, um dotnet.exe no tempo de execução 2.0 tenta usar um plug-in escrito para o tempo de execução 2.1.</span><span class="sxs-lookup"><span data-stu-id="f3546-189">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="f3546-190">Recursos de armazenamento em cache</span><span class="sxs-lookup"><span data-stu-id="f3546-190">Capabilities caching</span></span>

<span data-ttu-id="f3546-191">A verificação de segurança e a instanciação dos plug-ins é caro.</span><span class="sxs-lookup"><span data-stu-id="f3546-191">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="f3546-192">A operação de download acontece com muito mais frequência do que a operação de autenticação, no entanto, o usuário médio do NuGet só é provavelmente terá um plug-in de autenticação.</span><span class="sxs-lookup"><span data-stu-id="f3546-192">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="f3546-193">Para melhorar a experiência, o NuGet armazenará em cache as declarações de operação para a solicitação em questão.</span><span class="sxs-lookup"><span data-stu-id="f3546-193">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="f3546-194">Esse cache é por plug-in com a chave de plug-in que está sendo o caminho de plug-in e a expiração para esse cache de recursos é de 30 dias.</span><span class="sxs-lookup"><span data-stu-id="f3546-194">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="f3546-195">O cache está localizado em `%LocalAppData%/NuGet/plugins-cache` e ser substituída com a variável de ambiente `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="f3546-195">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="f3546-196">Para limpar esse [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), os locais pode ser executada com o `plugins-cache` opção.</span><span class="sxs-lookup"><span data-stu-id="f3546-196">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="f3546-197">O `all` opção locais agora também excluirá o cache de plug-ins.</span><span class="sxs-lookup"><span data-stu-id="f3546-197">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="f3546-198">Índice de mensagens de protocolo</span><span class="sxs-lookup"><span data-stu-id="f3546-198">Protocol messages index</span></span>

<span data-ttu-id="f3546-199">Versão do protocolo *1.0.0* mensagens:</span><span class="sxs-lookup"><span data-stu-id="f3546-199">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="f3546-200">Fechar</span><span class="sxs-lookup"><span data-stu-id="f3546-200">Close</span></span>
    * <span data-ttu-id="f3546-201">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-201">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f3546-202">A solicitação não irá conter nenhuma carga útil</span><span class="sxs-lookup"><span data-stu-id="f3546-202">The request will contain no payload</span></span>
    * <span data-ttu-id="f3546-203">Nenhuma resposta é esperada.</span><span class="sxs-lookup"><span data-stu-id="f3546-203">No response is expected.</span></span>  <span data-ttu-id="f3546-204">A resposta correta é para o processo de plug-in seja encerrado imediatamente.</span><span class="sxs-lookup"><span data-stu-id="f3546-204">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="f3546-205">Copiar arquivos de pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-205">Copy files in package</span></span>
    * <span data-ttu-id="f3546-206">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-206">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f3546-207">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-207">The request will contain:</span></span>
        * <span data-ttu-id="f3546-208">a ID do pacote e versão</span><span class="sxs-lookup"><span data-stu-id="f3546-208">the package ID and version</span></span>
        * <span data-ttu-id="f3546-209">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-209">the package source repository location</span></span>
        * <span data-ttu-id="f3546-210">caminho do diretório de destino</span><span class="sxs-lookup"><span data-stu-id="f3546-210">destination directory path</span></span>
        * <span data-ttu-id="f3546-211">um enumerável de arquivos no pacote a ser copiado para o caminho do diretório de destino</span><span class="sxs-lookup"><span data-stu-id="f3546-211">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="f3546-212">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-212">A response will contain:</span></span>
        * <span data-ttu-id="f3546-213">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="f3546-213">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f3546-214">um enumerável de caminhos completos para arquivos copiados no diretório de destino, se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="f3546-214">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="f3546-215">Copie o arquivo de pacote (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="f3546-215">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="f3546-216">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-216">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f3546-217">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-217">The request will contain:</span></span>
        * <span data-ttu-id="f3546-218">a ID do pacote e versão</span><span class="sxs-lookup"><span data-stu-id="f3546-218">the package ID and version</span></span>
        * <span data-ttu-id="f3546-219">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-219">the package source repository location</span></span>
        * <span data-ttu-id="f3546-220">o caminho do arquivo de destino</span><span class="sxs-lookup"><span data-stu-id="f3546-220">the destination file path</span></span>
    * <span data-ttu-id="f3546-221">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-221">A response will contain:</span></span>
        * <span data-ttu-id="f3546-222">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="f3546-222">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="f3546-223">Obter credenciais</span><span class="sxs-lookup"><span data-stu-id="f3546-223">Get credentials</span></span>
    * <span data-ttu-id="f3546-224">Direção de solicitação: plug-in -> NuGet</span><span class="sxs-lookup"><span data-stu-id="f3546-224">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="f3546-225">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-225">The request will contain:</span></span>
        * <span data-ttu-id="f3546-226">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-226">the package source repository location</span></span>
        * <span data-ttu-id="f3546-227">o código de status HTTP obtido no repositório de origem do pacote usando as credenciais atuais</span><span class="sxs-lookup"><span data-stu-id="f3546-227">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="f3546-228">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-228">A response will contain:</span></span>
        * <span data-ttu-id="f3546-229">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="f3546-229">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f3546-230">um nome de usuário, se disponível</span><span class="sxs-lookup"><span data-stu-id="f3546-230">a username, if available</span></span>
        * <span data-ttu-id="f3546-231">uma senha, se disponível</span><span class="sxs-lookup"><span data-stu-id="f3546-231">a password, if available</span></span>

5.  <span data-ttu-id="f3546-232">Obter os arquivos no pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-232">Get files in package</span></span>
    * <span data-ttu-id="f3546-233">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-233">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f3546-234">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-234">The request will contain:</span></span>
        * <span data-ttu-id="f3546-235">a ID do pacote e versão</span><span class="sxs-lookup"><span data-stu-id="f3546-235">the package ID and version</span></span>
        * <span data-ttu-id="f3546-236">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-236">the package source repository location</span></span>
    * <span data-ttu-id="f3546-237">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-237">A response will contain:</span></span>
        * <span data-ttu-id="f3546-238">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="f3546-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f3546-239">um enumerável de caminhos de arquivo no pacote se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="f3546-239">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="f3546-240">Obter declarações de operação</span><span class="sxs-lookup"><span data-stu-id="f3546-240">Get operation claims</span></span> 
    * <span data-ttu-id="f3546-241">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f3546-242">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-242">The request will contain:</span></span>
        * <span data-ttu-id="f3546-243">o serviço index.json para uma origem de pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-243">the service index.json for a package source</span></span>
        * <span data-ttu-id="f3546-244">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-244">the package source repository location</span></span>
    * <span data-ttu-id="f3546-245">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-245">A response will contain:</span></span>
        * <span data-ttu-id="f3546-246">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="f3546-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f3546-247">um enumerável de operações com suporte (por exemplo: download do pacote) se a operação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="f3546-247">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="f3546-248">Se um plug-in não oferece suporte a origem do pacote, o plug-in deve retornar um conjunto vazio de operações com suporte.</span><span class="sxs-lookup"><span data-stu-id="f3546-248">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="f3546-249">Esta mensagem foi atualizada na versão *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="f3546-249">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="f3546-250">É no cliente para preservar a compatibilidade com versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="f3546-250">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="f3546-251">Obter o hash do pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-251">Get package hash</span></span>
    * <span data-ttu-id="f3546-252">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-252">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f3546-253">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-253">The request will contain:</span></span>
        * <span data-ttu-id="f3546-254">a ID do pacote e versão</span><span class="sxs-lookup"><span data-stu-id="f3546-254">the package ID and version</span></span>
        * <span data-ttu-id="f3546-255">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-255">the package source repository location</span></span>
        * <span data-ttu-id="f3546-256">o algoritmo de hash</span><span class="sxs-lookup"><span data-stu-id="f3546-256">the hash algorithm</span></span>
    * <span data-ttu-id="f3546-257">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-257">A response will contain:</span></span>
        * <span data-ttu-id="f3546-258">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="f3546-258">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f3546-259">um hash do arquivo de pacote usando o algoritmo de hash solicitado, se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="f3546-259">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="f3546-260">Obter versões de pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-260">Get package versions</span></span>
    * <span data-ttu-id="f3546-261">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f3546-262">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-262">The request will contain:</span></span>
        * <span data-ttu-id="f3546-263">a ID do pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-263">the package ID</span></span>
        * <span data-ttu-id="f3546-264">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-264">the package source repository location</span></span>
    * <span data-ttu-id="f3546-265">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-265">A response will contain:</span></span>
        * <span data-ttu-id="f3546-266">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="f3546-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f3546-267">um enumerável de versões do pacote se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="f3546-267">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="f3546-268">Obter índice de serviço</span><span class="sxs-lookup"><span data-stu-id="f3546-268">Get service index</span></span>
    * <span data-ttu-id="f3546-269">Direção de solicitação: plug-in -> NuGet</span><span class="sxs-lookup"><span data-stu-id="f3546-269">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="f3546-270">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-270">The request will contain:</span></span>
        * <span data-ttu-id="f3546-271">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-271">the package source repository location</span></span>
    * <span data-ttu-id="f3546-272">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-272">A response will contain:</span></span>
        * <span data-ttu-id="f3546-273">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="f3546-273">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f3546-274">o índice de serviço se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="f3546-274">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="f3546-275">Handshake</span><span class="sxs-lookup"><span data-stu-id="f3546-275">Handshake</span></span>
     * <span data-ttu-id="f3546-276">Direção de solicitação: plug-in do NuGet <> –</span><span class="sxs-lookup"><span data-stu-id="f3546-276">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="f3546-277">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-277">The request will contain:</span></span>
         * <span data-ttu-id="f3546-278">a versão atual do protocolo de plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-278">the current plugin protocol version</span></span>
         * <span data-ttu-id="f3546-279">a versão do protocolo de plug-in com suporte mínimo</span><span class="sxs-lookup"><span data-stu-id="f3546-279">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="f3546-280">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-280">A response will contain:</span></span>
         * <span data-ttu-id="f3546-281">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="f3546-281">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="f3546-282">a versão do protocolo negociado se a operação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="f3546-282">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="f3546-283">Uma falha resultará no encerramento do plug-in.</span><span class="sxs-lookup"><span data-stu-id="f3546-283">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="f3546-284">inicializar</span><span class="sxs-lookup"><span data-stu-id="f3546-284">Initialize</span></span>
     * <span data-ttu-id="f3546-285">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-285">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f3546-286">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-286">The request will contain:</span></span>
         * <span data-ttu-id="f3546-287">a versão da ferramenta cliente NuGet</span><span class="sxs-lookup"><span data-stu-id="f3546-287">the NuGet client tool version</span></span>
         * <span data-ttu-id="f3546-288">o NuGet ferramenta efetivação idioma do cliente.</span><span class="sxs-lookup"><span data-stu-id="f3546-288">the NuGet client tool effective language.</span></span>  <span data-ttu-id="f3546-289">Isso leva em consideração a configuração de ForceEnglishOutput, se usado.</span><span class="sxs-lookup"><span data-stu-id="f3546-289">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="f3546-290">o padrão tempo limite da solicitação, que substitui o padrão de protocolo.</span><span class="sxs-lookup"><span data-stu-id="f3546-290">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="f3546-291">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-291">A response will contain:</span></span>
         * <span data-ttu-id="f3546-292">um código de resposta que indica o resultado da operação.</span><span class="sxs-lookup"><span data-stu-id="f3546-292">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="f3546-293">Uma falha resultará no encerramento do plug-in.</span><span class="sxs-lookup"><span data-stu-id="f3546-293">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="f3546-294">Log</span><span class="sxs-lookup"><span data-stu-id="f3546-294">Log</span></span>
     * <span data-ttu-id="f3546-295">Direção de solicitação: plug-in -> NuGet</span><span class="sxs-lookup"><span data-stu-id="f3546-295">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="f3546-296">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-296">The request will contain:</span></span>
         * <span data-ttu-id="f3546-297">o nível de log para a solicitação</span><span class="sxs-lookup"><span data-stu-id="f3546-297">the log level for the request</span></span>
         * <span data-ttu-id="f3546-298">uma mensagem de log</span><span class="sxs-lookup"><span data-stu-id="f3546-298">a message to log</span></span>
     * <span data-ttu-id="f3546-299">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-299">A response will contain:</span></span>
         * <span data-ttu-id="f3546-300">um código de resposta que indica o resultado da operação.</span><span class="sxs-lookup"><span data-stu-id="f3546-300">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="f3546-301">Monitorar a saída do processo de NuGet</span><span class="sxs-lookup"><span data-stu-id="f3546-301">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="f3546-302">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-302">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f3546-303">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-303">The request will contain:</span></span>
         * <span data-ttu-id="f3546-304">a ID de processo do NuGet</span><span class="sxs-lookup"><span data-stu-id="f3546-304">the NuGet process ID</span></span>
     * <span data-ttu-id="f3546-305">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-305">A response will contain:</span></span>
         * <span data-ttu-id="f3546-306">um código de resposta que indica o resultado da operação.</span><span class="sxs-lookup"><span data-stu-id="f3546-306">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="f3546-307">Pacote de pré-busca</span><span class="sxs-lookup"><span data-stu-id="f3546-307">Prefetch package</span></span>
     * <span data-ttu-id="f3546-308">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-308">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f3546-309">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-309">The request will contain:</span></span>
         * <span data-ttu-id="f3546-310">a ID do pacote e versão</span><span class="sxs-lookup"><span data-stu-id="f3546-310">the package ID and version</span></span>
         * <span data-ttu-id="f3546-311">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-311">the package source repository location</span></span>
     * <span data-ttu-id="f3546-312">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-312">A response will contain:</span></span>
         * <span data-ttu-id="f3546-313">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="f3546-313">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="f3546-314">Definir credenciais</span><span class="sxs-lookup"><span data-stu-id="f3546-314">Set credentials</span></span>
     * <span data-ttu-id="f3546-315">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-315">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f3546-316">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-316">The request will contain:</span></span>
         * <span data-ttu-id="f3546-317">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-317">the package source repository location</span></span>
         * <span data-ttu-id="f3546-318">último pacote conhecidos origem nome de usuário, se disponível</span><span class="sxs-lookup"><span data-stu-id="f3546-318">the last known package source username, if available</span></span>
         * <span data-ttu-id="f3546-319">a última senha de origem de pacotes conhecidas, se disponível</span><span class="sxs-lookup"><span data-stu-id="f3546-319">the last known package source password, if available</span></span>
         * <span data-ttu-id="f3546-320">o último proxy conhecidos nome de usuário, se disponível</span><span class="sxs-lookup"><span data-stu-id="f3546-320">the last known proxy username, if available</span></span>
         * <span data-ttu-id="f3546-321">a última senha proxy conhecidos, se disponível</span><span class="sxs-lookup"><span data-stu-id="f3546-321">the last known proxy password, if available</span></span>
     * <span data-ttu-id="f3546-322">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-322">A response will contain:</span></span>
         * <span data-ttu-id="f3546-323">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="f3546-323">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="f3546-324">Definir o nível de log</span><span class="sxs-lookup"><span data-stu-id="f3546-324">Set log level</span></span>
     * <span data-ttu-id="f3546-325">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-325">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f3546-326">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-326">The request will contain:</span></span>
         * <span data-ttu-id="f3546-327">o nível de log padrão</span><span class="sxs-lookup"><span data-stu-id="f3546-327">the default log level</span></span>
     * <span data-ttu-id="f3546-328">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-328">A response will contain:</span></span>
         * <span data-ttu-id="f3546-329">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="f3546-329">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="f3546-330">Versão do protocolo *2.0.0* mensagens</span><span class="sxs-lookup"><span data-stu-id="f3546-330">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="f3546-331">Obter declarações de operação</span><span class="sxs-lookup"><span data-stu-id="f3546-331">Get Operation Claims</span></span>

* <span data-ttu-id="f3546-332">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-332">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f3546-333">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-333">The request will contain:</span></span>
        * <span data-ttu-id="f3546-334">o serviço index.json para uma origem de pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-334">the service index.json for a package source</span></span>
        * <span data-ttu-id="f3546-335">o local de repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="f3546-335">the package source repository location</span></span>
    * <span data-ttu-id="f3546-336">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-336">A response will contain:</span></span>
        * <span data-ttu-id="f3546-337">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="f3546-337">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f3546-338">um enumerável de operações com suporte se a operação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="f3546-338">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="f3546-339">Se um plug-in não oferece suporte a origem do pacote, o plug-in deve retornar um conjunto vazio de operações com suporte.</span><span class="sxs-lookup"><span data-stu-id="f3546-339">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="f3546-340">Se a origem de índice e o pacote de serviço forem nula, o plug-in pode responder com a autenticação.</span><span class="sxs-lookup"><span data-stu-id="f3546-340">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="f3546-341">Obter credenciais de autenticação</span><span class="sxs-lookup"><span data-stu-id="f3546-341">Get Authentication Credentials</span></span>

* <span data-ttu-id="f3546-342">Direção de solicitação: NuGet -> Plug-in</span><span class="sxs-lookup"><span data-stu-id="f3546-342">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="f3546-343">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="f3546-343">The request will contain:</span></span>
    * <span data-ttu-id="f3546-344">URI</span><span class="sxs-lookup"><span data-stu-id="f3546-344">Uri</span></span>
    * <span data-ttu-id="f3546-345">isRetry</span><span class="sxs-lookup"><span data-stu-id="f3546-345">isRetry</span></span>
    * <span data-ttu-id="f3546-346">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f3546-346">NonInteractive</span></span>
    * <span data-ttu-id="f3546-347">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="f3546-347">CanShowDialog</span></span>
* <span data-ttu-id="f3546-348">Uma resposta irá conter</span><span class="sxs-lookup"><span data-stu-id="f3546-348">A response will contain</span></span>
    * <span data-ttu-id="f3546-349">Nome de usuário</span><span class="sxs-lookup"><span data-stu-id="f3546-349">Username</span></span>
    * <span data-ttu-id="f3546-350">Senha</span><span class="sxs-lookup"><span data-stu-id="f3546-350">Password</span></span>
    * <span data-ttu-id="f3546-351">Mensagem</span><span class="sxs-lookup"><span data-stu-id="f3546-351">Message</span></span>
    * <span data-ttu-id="f3546-352">Lista de tipos de autenticação</span><span class="sxs-lookup"><span data-stu-id="f3546-352">List of Auth Types</span></span>
    * <span data-ttu-id="f3546-353">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="f3546-353">MessageResponseCode</span></span>