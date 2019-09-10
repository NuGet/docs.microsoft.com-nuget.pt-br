---
title: Plug-ins de plataforma cruzada do NuGet
description: Plug-ins de plataforma cruzada do NuGet para NuGet. exe, dotnet. exe, MSBuild. exe e Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 74b80b1791dcb403c90bb3032c009717c11ffe57
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815309"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="fd54a-103">Plug-ins de plataforma cruzada do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="fd54a-104">No NuGet 4.8 + suporte para plug-ins de plataforma cruzada foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="fd54a-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="fd54a-105">Isso foi conseguido com a criação de um novo modelo de extensibilidade de plug-in, que precisa estar em conformidade com um conjunto estrito de regras de operação.</span><span class="sxs-lookup"><span data-stu-id="fd54a-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="fd54a-106">Os plug-ins são executáveis independentes (executáveis no mundo do .NET Core), que os clientes NuGet iniciam em um processo separado.</span><span class="sxs-lookup"><span data-stu-id="fd54a-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="fd54a-107">Essa é uma verdadeira gravação única, execute o plug-in de todos os lugares.</span><span class="sxs-lookup"><span data-stu-id="fd54a-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="fd54a-108">Ele funcionará com todas as ferramentas de cliente do NuGet.</span><span class="sxs-lookup"><span data-stu-id="fd54a-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="fd54a-109">Os plug-ins podem ser .NET Framework (NuGet. exe, MSBuild. exe e Visual Studio) ou .NET Core (dotNet. exe).</span><span class="sxs-lookup"><span data-stu-id="fd54a-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="fd54a-110">Um protocolo de comunicação com versão entre o cliente NuGet e o plug-in é definido.</span><span class="sxs-lookup"><span data-stu-id="fd54a-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="fd54a-111">Durante o handshake de inicialização, os 2 processos negociam a versão do protocolo.</span><span class="sxs-lookup"><span data-stu-id="fd54a-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="fd54a-112">Para abranger todos os cenários de ferramentas de cliente do NuGet, é necessário um plug-in de .NET Framework e do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="fd54a-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="fd54a-113">A seguir, a descrição das combinações de cliente/estrutura dos plug-ins.</span><span class="sxs-lookup"><span data-stu-id="fd54a-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="fd54a-114">Ferramenta de cliente</span><span class="sxs-lookup"><span data-stu-id="fd54a-114">Client tool</span></span>  | <span data-ttu-id="fd54a-115">Framework</span><span class="sxs-lookup"><span data-stu-id="fd54a-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="fd54a-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fd54a-116">Visual Studio</span></span> | <span data-ttu-id="fd54a-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="fd54a-117">.NET Framework</span></span> |
| <span data-ttu-id="fd54a-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="fd54a-118">dotnet.exe</span></span> | <span data-ttu-id="fd54a-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="fd54a-119">.NET Core</span></span> |
| <span data-ttu-id="fd54a-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="fd54a-120">NuGet.exe</span></span> | <span data-ttu-id="fd54a-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="fd54a-121">.NET Framework</span></span> |
| <span data-ttu-id="fd54a-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="fd54a-122">MSBuild.exe</span></span> | <span data-ttu-id="fd54a-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="fd54a-123">.NET Framework</span></span> |
| <span data-ttu-id="fd54a-124">NuGet. exe no mono</span><span class="sxs-lookup"><span data-stu-id="fd54a-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="fd54a-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="fd54a-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="fd54a-126">Como funciona</span><span class="sxs-lookup"><span data-stu-id="fd54a-126">How does it work</span></span>

<span data-ttu-id="fd54a-127">O fluxo de trabalho de alto nível pode ser descrito da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="fd54a-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="fd54a-128">O NuGet descobre plugins disponíveis.</span><span class="sxs-lookup"><span data-stu-id="fd54a-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="fd54a-129">Quando aplicável, o NuGet irá iterar sobre os plug-ins em ordem de prioridade e os iniciará um a um.</span><span class="sxs-lookup"><span data-stu-id="fd54a-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="fd54a-130">O NuGet usará o primeiro plug-in que pode atender à solicitação.</span><span class="sxs-lookup"><span data-stu-id="fd54a-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="fd54a-131">Os plug-ins serão desligados quando não forem mais necessários.</span><span class="sxs-lookup"><span data-stu-id="fd54a-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="fd54a-132">Requisitos gerais de plug-in</span><span class="sxs-lookup"><span data-stu-id="fd54a-132">General plugin requirements</span></span>

<span data-ttu-id="fd54a-133">A versão atual do protocolo é *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="fd54a-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="fd54a-134">Nesta versão, os requisitos são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="fd54a-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="fd54a-135">Ter um assembly de assinatura de Authenticode confiável válido que será executado no Windows e no mono.</span><span class="sxs-lookup"><span data-stu-id="fd54a-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="fd54a-136">Ainda não há nenhum requisito de confiança especial para assemblies executados no Linux e Mac.</span><span class="sxs-lookup"><span data-stu-id="fd54a-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="fd54a-137">Problema relevante</span><span class="sxs-lookup"><span data-stu-id="fd54a-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="fd54a-138">Suporte à inicialização sem monitoração de estado no contexto de segurança atual das ferramentas de cliente do NuGet.</span><span class="sxs-lookup"><span data-stu-id="fd54a-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="fd54a-139">Por exemplo, as ferramentas de cliente do NuGet não executarão a elevação ou inicialização adicional fora do protocolo de plug-in descrito posteriormente.</span><span class="sxs-lookup"><span data-stu-id="fd54a-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="fd54a-140">Ser não interativo, a menos que especificado explicitamente.</span><span class="sxs-lookup"><span data-stu-id="fd54a-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="fd54a-141">Siga a versão do protocolo de plug-in negociado.</span><span class="sxs-lookup"><span data-stu-id="fd54a-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="fd54a-142">Responder a todas as solicitações em um período de tempo razoável.</span><span class="sxs-lookup"><span data-stu-id="fd54a-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="fd54a-143">Honra as solicitações de cancelamento para qualquer operação em andamento.</span><span class="sxs-lookup"><span data-stu-id="fd54a-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="fd54a-144">A especificação técnica é descrita mais detalhadamente nas especificações a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd54a-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="fd54a-145">Plug-in de download do pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="fd54a-146">Plug-in de autenticação entre Plat do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="fd54a-147">Interação do plug-in do cliente</span><span class="sxs-lookup"><span data-stu-id="fd54a-147">Client - Plugin interaction</span></span>

<span data-ttu-id="fd54a-148">As ferramentas de cliente do NuGet e os plug-ins se comunicam com JSON sobre fluxos padrão (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="fd54a-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="fd54a-149">Todos os dados devem ser codificados em UTF-8.</span><span class="sxs-lookup"><span data-stu-id="fd54a-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="fd54a-150">Os plug-ins são iniciados com o argumento "-plugin".</span><span class="sxs-lookup"><span data-stu-id="fd54a-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="fd54a-151">No caso de um usuário iniciar diretamente um executável de plug-in sem esse argumento, o plug-in pode fornecer uma mensagem informativa em vez de aguardar um handshake de protocolo.</span><span class="sxs-lookup"><span data-stu-id="fd54a-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="fd54a-152">O tempo limite de handshake de protocolo é de 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="fd54a-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="fd54a-153">O plug-in deve concluir a configuração no menor valor possível.</span><span class="sxs-lookup"><span data-stu-id="fd54a-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="fd54a-154">As ferramentas de cliente do NuGet consultarão as operações com suporte de um plug-in passando o índice de serviço para uma origem do NuGet.</span><span class="sxs-lookup"><span data-stu-id="fd54a-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="fd54a-155">Um plug-in pode usar o índice de serviço para verificar a presença de tipos de serviço com suporte.</span><span class="sxs-lookup"><span data-stu-id="fd54a-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="fd54a-156">A comunicação entre as ferramentas de cliente do NuGet e o plug-in é bidirecional.</span><span class="sxs-lookup"><span data-stu-id="fd54a-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="fd54a-157">Cada solicitação tem um tempo limite de 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="fd54a-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="fd54a-158">Se as operações devem levar mais tempo, o respectivo processo deve enviar uma mensagem de progresso para impedir que a solicitação atinja o tempo limite. Após 1 minuto de inatividade, um plug-in é considerado ocioso e é desligado.</span><span class="sxs-lookup"><span data-stu-id="fd54a-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="fd54a-159">Instalação e descoberta do plug-in</span><span class="sxs-lookup"><span data-stu-id="fd54a-159">Plugin installation and discovery</span></span>

<span data-ttu-id="fd54a-160">Os plug-ins serão descobertos por meio de uma estrutura de diretório baseada em convenção.</span><span class="sxs-lookup"><span data-stu-id="fd54a-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="fd54a-161">Cenários de CI/CD e usuários avançados podem usar variáveis de ambiente para substituir o comportamento.</span><span class="sxs-lookup"><span data-stu-id="fd54a-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="fd54a-162">Observe que `NUGET_NETFX_PLUGIN_PATHS` o `NUGET_NETCORE_PLUGIN_PATHS` e o estão disponíveis apenas com a versão 5.3 + das ferramentas do NuGet e posterior.</span><span class="sxs-lookup"><span data-stu-id="fd54a-162">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="fd54a-163">`NUGET_NETFX_PLUGIN_PATHS`-define os plug-ins que serão usados pelas ferramentas baseadas em .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="fd54a-163">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="fd54a-164">Tem precedência `NUGET_PLUGIN_PATHS`sobre.</span><span class="sxs-lookup"><span data-stu-id="fd54a-164">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="fd54a-165">(Somente NuGet versão 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="fd54a-165">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="fd54a-166">`NUGET_NETCORE_PLUGIN_PATHS`-define os plug-ins que serão usados pelas ferramentas baseadas no .NET Core (dotNet. exe).</span><span class="sxs-lookup"><span data-stu-id="fd54a-166">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="fd54a-167">Tem precedência `NUGET_PLUGIN_PATHS`sobre.</span><span class="sxs-lookup"><span data-stu-id="fd54a-167">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="fd54a-168">(Somente NuGet versão 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="fd54a-168">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="fd54a-169">`NUGET_PLUGIN_PATHS`-define os plug-ins que serão usados para o processo NuGet, prioridade reservada.</span><span class="sxs-lookup"><span data-stu-id="fd54a-169">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="fd54a-170">Se essa variável de ambiente for definida, ela substituirá a descoberta baseada em convenção.</span><span class="sxs-lookup"><span data-stu-id="fd54a-170">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="fd54a-171">Ignorado se uma das variáveis específicas do Framework for especificada.</span><span class="sxs-lookup"><span data-stu-id="fd54a-171">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="fd54a-172">Local do usuário, o local inicial do NuGet `%UserProfile%/.nuget/plugins`em.</span><span class="sxs-lookup"><span data-stu-id="fd54a-172">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="fd54a-173">Esse local não pode ser substituído.</span><span class="sxs-lookup"><span data-stu-id="fd54a-173">This location cannot be overriden.</span></span> <span data-ttu-id="fd54a-174">Um diretório raiz diferente será usado para os plug-ins .NET Core e .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="fd54a-174">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="fd54a-175">Framework</span><span class="sxs-lookup"><span data-stu-id="fd54a-175">Framework</span></span> | <span data-ttu-id="fd54a-176">Local de descoberta raiz</span><span class="sxs-lookup"><span data-stu-id="fd54a-176">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="fd54a-177">.NET Core</span><span class="sxs-lookup"><span data-stu-id="fd54a-177">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="fd54a-178">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="fd54a-178">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="fd54a-179">Cada plug-in deve ser instalado em sua própria pasta.</span><span class="sxs-lookup"><span data-stu-id="fd54a-179">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="fd54a-180">O ponto de entrada do plug-in será o nome da pasta instalada, com as extensões. dll para .NET Core e a extensão. exe para .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="fd54a-180">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="fd54a-181">No momento, não há nenhuma história de usuário para a instalação dos plug-ins.</span><span class="sxs-lookup"><span data-stu-id="fd54a-181">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="fd54a-182">É tão simples quanto mover os arquivos necessários para o local predeterminado.</span><span class="sxs-lookup"><span data-stu-id="fd54a-182">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="fd54a-183">Operações com suporte</span><span class="sxs-lookup"><span data-stu-id="fd54a-183">Supported operations</span></span>

<span data-ttu-id="fd54a-184">Há suporte para duas operações no novo protocolo de plugin.</span><span class="sxs-lookup"><span data-stu-id="fd54a-184">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="fd54a-185">Nome da operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-185">Operation name</span></span> | <span data-ttu-id="fd54a-186">Versão mínima do protocolo</span><span class="sxs-lookup"><span data-stu-id="fd54a-186">Minimum protocol version</span></span> | <span data-ttu-id="fd54a-187">Versão mínima do cliente NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-187">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="fd54a-188">Baixar pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-188">Download Package</span></span> | <span data-ttu-id="fd54a-189">1.0.0</span><span class="sxs-lookup"><span data-stu-id="fd54a-189">1.0.0</span></span> | <span data-ttu-id="fd54a-190">4.3.0</span><span class="sxs-lookup"><span data-stu-id="fd54a-190">4.3.0</span></span> |
| [<span data-ttu-id="fd54a-191">Autenticação</span><span class="sxs-lookup"><span data-stu-id="fd54a-191">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="fd54a-192">2.0.0</span><span class="sxs-lookup"><span data-stu-id="fd54a-192">2.0.0</span></span> | <span data-ttu-id="fd54a-193">4.8.0</span><span class="sxs-lookup"><span data-stu-id="fd54a-193">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="fd54a-194">Executando plug-ins no tempo de execução correto</span><span class="sxs-lookup"><span data-stu-id="fd54a-194">Running plugins under the correct runtime</span></span>

<span data-ttu-id="fd54a-195">Para o NuGet em cenários dotnet. exe, os plug-ins precisam ser capazes de executar sob esse tempo de execução específico do dotnet. exe.</span><span class="sxs-lookup"><span data-stu-id="fd54a-195">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="fd54a-196">Ele está no provedor de plug-in e no consumidor para garantir que uma combinação de dotnet. exe/plugin compatível seja usada.</span><span class="sxs-lookup"><span data-stu-id="fd54a-196">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="fd54a-197">Um problema potencial pode surgir com os plug-ins de localização do usuário quando, por exemplo, um dotnet. exe no tempo de execução 2,0 tentar usar um plug-in gravado para o tempo de execução 2,1.</span><span class="sxs-lookup"><span data-stu-id="fd54a-197">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="fd54a-198">Recursos de cache</span><span class="sxs-lookup"><span data-stu-id="fd54a-198">Capabilities caching</span></span>

<span data-ttu-id="fd54a-199">A verificação de segurança e a instanciação dos plug-ins são dispendiosas.</span><span class="sxs-lookup"><span data-stu-id="fd54a-199">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="fd54a-200">A operação de download ocorre de maneira mais frequente do que a operação de autenticação, no entanto, o usuário NuGet médio provavelmente terá um plug-in de autenticação.</span><span class="sxs-lookup"><span data-stu-id="fd54a-200">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="fd54a-201">Para melhorar a experiência, o NuGet armazenará em cache as declarações de operação para a solicitação especificada.</span><span class="sxs-lookup"><span data-stu-id="fd54a-201">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="fd54a-202">Esse cache é por plug-in com a chave do plug-in sendo o caminho do plug-in e a expiração desse cache de recursos é de 30 dias.</span><span class="sxs-lookup"><span data-stu-id="fd54a-202">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="fd54a-203">O cache está localizado em `%LocalAppData%/NuGet/plugins-cache` e é substituído pela variável `NUGET_PLUGINS_CACHE_PATH`de ambiente.</span><span class="sxs-lookup"><span data-stu-id="fd54a-203">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="fd54a-204">Para limpar esse [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), é possível executar o comando local com a `plugins-cache` opção.</span><span class="sxs-lookup"><span data-stu-id="fd54a-204">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="fd54a-205">A `all` opção locais agora também excluirá o cache de plug-ins.</span><span class="sxs-lookup"><span data-stu-id="fd54a-205">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="fd54a-206">Índice de mensagens de protocolo</span><span class="sxs-lookup"><span data-stu-id="fd54a-206">Protocol messages index</span></span>

<span data-ttu-id="fd54a-207">Mensagens da versão *1.0.0* do protocolo:</span><span class="sxs-lookup"><span data-stu-id="fd54a-207">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="fd54a-208">Fechar</span><span class="sxs-lookup"><span data-stu-id="fd54a-208">Close</span></span>
    * <span data-ttu-id="fd54a-209">Direção da solicitação:  Plug-in > do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-209">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="fd54a-210">A solicitação não conterá nenhuma carga</span><span class="sxs-lookup"><span data-stu-id="fd54a-210">The request will contain no payload</span></span>
    * <span data-ttu-id="fd54a-211">Nenhuma resposta é esperada.</span><span class="sxs-lookup"><span data-stu-id="fd54a-211">No response is expected.</span></span>  <span data-ttu-id="fd54a-212">A resposta correta é para que o processo do plug-in seja fechado imediatamente.</span><span class="sxs-lookup"><span data-stu-id="fd54a-212">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="fd54a-213">Copiar arquivos no pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-213">Copy files in package</span></span>
    * <span data-ttu-id="fd54a-214">Direção da solicitação:  Plug-in > do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-214">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="fd54a-215">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-215">The request will contain:</span></span>
        * <span data-ttu-id="fd54a-216">a ID e a versão do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-216">the package ID and version</span></span>
        * <span data-ttu-id="fd54a-217">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-217">the package source repository location</span></span>
        * <span data-ttu-id="fd54a-218">caminho do diretório de destino</span><span class="sxs-lookup"><span data-stu-id="fd54a-218">destination directory path</span></span>
        * <span data-ttu-id="fd54a-219">um enumerável de arquivos no pacote a ser copiado para o caminho do diretório de destino</span><span class="sxs-lookup"><span data-stu-id="fd54a-219">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="fd54a-220">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-220">A response will contain:</span></span>
        * <span data-ttu-id="fd54a-221">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-221">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="fd54a-222">um enumerável de caminhos completos para arquivos copiados no diretório de destino se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="fd54a-222">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="fd54a-223">Copiar arquivo de pacote (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="fd54a-223">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="fd54a-224">Direção da solicitação:  Plug-in > do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-224">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="fd54a-225">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-225">The request will contain:</span></span>
        * <span data-ttu-id="fd54a-226">a ID e a versão do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-226">the package ID and version</span></span>
        * <span data-ttu-id="fd54a-227">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-227">the package source repository location</span></span>
        * <span data-ttu-id="fd54a-228">o caminho do arquivo de destino</span><span class="sxs-lookup"><span data-stu-id="fd54a-228">the destination file path</span></span>
    * <span data-ttu-id="fd54a-229">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-229">A response will contain:</span></span>
        * <span data-ttu-id="fd54a-230">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-230">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="fd54a-231">Obter credenciais</span><span class="sxs-lookup"><span data-stu-id="fd54a-231">Get credentials</span></span>
    * <span data-ttu-id="fd54a-232">Direção da solicitação: > do plugin-NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-232">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="fd54a-233">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-233">The request will contain:</span></span>
        * <span data-ttu-id="fd54a-234">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-234">the package source repository location</span></span>
        * <span data-ttu-id="fd54a-235">o código de status HTTP obtido do repositório de origem do pacote usando as credenciais atuais</span><span class="sxs-lookup"><span data-stu-id="fd54a-235">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="fd54a-236">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-236">A response will contain:</span></span>
        * <span data-ttu-id="fd54a-237">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-237">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="fd54a-238">um nome de usuário, se disponível</span><span class="sxs-lookup"><span data-stu-id="fd54a-238">a username, if available</span></span>
        * <span data-ttu-id="fd54a-239">uma senha, se disponível</span><span class="sxs-lookup"><span data-stu-id="fd54a-239">a password, if available</span></span>

5.  <span data-ttu-id="fd54a-240">Obter arquivos no pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-240">Get files in package</span></span>
    * <span data-ttu-id="fd54a-241">Direção da solicitação:  Plug-in > do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="fd54a-242">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-242">The request will contain:</span></span>
        * <span data-ttu-id="fd54a-243">a ID e a versão do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-243">the package ID and version</span></span>
        * <span data-ttu-id="fd54a-244">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-244">the package source repository location</span></span>
    * <span data-ttu-id="fd54a-245">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-245">A response will contain:</span></span>
        * <span data-ttu-id="fd54a-246">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="fd54a-247">um enumerável de caminhos de arquivo no pacote se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="fd54a-247">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="fd54a-248">Obter declarações de operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-248">Get operation claims</span></span> 
    * <span data-ttu-id="fd54a-249">Direção da solicitação:  Plug-in > do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-249">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="fd54a-250">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-250">The request will contain:</span></span>
        * <span data-ttu-id="fd54a-251">o Service index. JSON para uma origem de pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-251">the service index.json for a package source</span></span>
        * <span data-ttu-id="fd54a-252">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-252">the package source repository location</span></span>
    * <span data-ttu-id="fd54a-253">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-253">A response will contain:</span></span>
        * <span data-ttu-id="fd54a-254">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-254">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="fd54a-255">um enumerável de operações com suporte (por exemplo: download de pacote) se a operação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="fd54a-255">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="fd54a-256">Se um plug-in não oferecer suporte à origem do pacote, o plug-in deverá retornar um conjunto vazio de operações com suporte.</span><span class="sxs-lookup"><span data-stu-id="fd54a-256">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="fd54a-257">Esta mensagem foi atualizada na versão *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="fd54a-257">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="fd54a-258">Ele está no cliente para preservar a compatibilidade com versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="fd54a-258">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="fd54a-259">Obter hash do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-259">Get package hash</span></span>
    * <span data-ttu-id="fd54a-260">Direção da solicitação:  Plug-in > do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-260">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="fd54a-261">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-261">The request will contain:</span></span>
        * <span data-ttu-id="fd54a-262">a ID e a versão do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-262">the package ID and version</span></span>
        * <span data-ttu-id="fd54a-263">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-263">the package source repository location</span></span>
        * <span data-ttu-id="fd54a-264">o algoritmo de hash</span><span class="sxs-lookup"><span data-stu-id="fd54a-264">the hash algorithm</span></span>
    * <span data-ttu-id="fd54a-265">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-265">A response will contain:</span></span>
        * <span data-ttu-id="fd54a-266">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="fd54a-267">um hash de arquivo de pacote usando o algoritmo de hash solicitado se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="fd54a-267">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="fd54a-268">Obter versões do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-268">Get package versions</span></span>
    * <span data-ttu-id="fd54a-269">Direção da solicitação:  Plug-in > do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-269">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="fd54a-270">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-270">The request will contain:</span></span>
        * <span data-ttu-id="fd54a-271">a ID do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-271">the package ID</span></span>
        * <span data-ttu-id="fd54a-272">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-272">the package source repository location</span></span>
    * <span data-ttu-id="fd54a-273">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-273">A response will contain:</span></span>
        * <span data-ttu-id="fd54a-274">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-274">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="fd54a-275">um enumerável de versões de pacote se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="fd54a-275">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="fd54a-276">Obter índice de serviço</span><span class="sxs-lookup"><span data-stu-id="fd54a-276">Get service index</span></span>
    * <span data-ttu-id="fd54a-277">Direção da solicitação: > do plugin-NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-277">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="fd54a-278">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-278">The request will contain:</span></span>
        * <span data-ttu-id="fd54a-279">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-279">the package source repository location</span></span>
    * <span data-ttu-id="fd54a-280">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-280">A response will contain:</span></span>
        * <span data-ttu-id="fd54a-281">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-281">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="fd54a-282">o índice de serviço se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="fd54a-282">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="fd54a-283">Handshake</span><span class="sxs-lookup"><span data-stu-id="fd54a-283">Handshake</span></span>
     * <span data-ttu-id="fd54a-284">Direção da solicitação:  Plug-in < > do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-284">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="fd54a-285">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-285">The request will contain:</span></span>
         * <span data-ttu-id="fd54a-286">a versão do protocolo do plugin atual</span><span class="sxs-lookup"><span data-stu-id="fd54a-286">the current plugin protocol version</span></span>
         * <span data-ttu-id="fd54a-287">a versão mínima do protocolo de plug-in com suporte</span><span class="sxs-lookup"><span data-stu-id="fd54a-287">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="fd54a-288">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-288">A response will contain:</span></span>
         * <span data-ttu-id="fd54a-289">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-289">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="fd54a-290">a versão do protocolo negociado se a operação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="fd54a-290">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="fd54a-291">Uma falha resultará no encerramento do plug-in.</span><span class="sxs-lookup"><span data-stu-id="fd54a-291">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="fd54a-292">Initialize</span><span class="sxs-lookup"><span data-stu-id="fd54a-292">Initialize</span></span>
     * <span data-ttu-id="fd54a-293">Direção da solicitação:  Plug-in > do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-293">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="fd54a-294">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-294">The request will contain:</span></span>
         * <span data-ttu-id="fd54a-295">a versão da ferramenta do cliente NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-295">the NuGet client tool version</span></span>
         * <span data-ttu-id="fd54a-296">o idioma efetivo da ferramenta de cliente NuGet.</span><span class="sxs-lookup"><span data-stu-id="fd54a-296">the NuGet client tool effective language.</span></span>  <span data-ttu-id="fd54a-297">Isso leva em consideração a configuração ForceEnglishOutput, se usada.</span><span class="sxs-lookup"><span data-stu-id="fd54a-297">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="fd54a-298">o tempo limite de solicitação padrão, que substitui o padrão de protocolo.</span><span class="sxs-lookup"><span data-stu-id="fd54a-298">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="fd54a-299">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-299">A response will contain:</span></span>
         * <span data-ttu-id="fd54a-300">um código de resposta que indica o resultado da operação.</span><span class="sxs-lookup"><span data-stu-id="fd54a-300">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="fd54a-301">Uma falha resultará no encerramento do plug-in.</span><span class="sxs-lookup"><span data-stu-id="fd54a-301">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="fd54a-302">Log</span><span class="sxs-lookup"><span data-stu-id="fd54a-302">Log</span></span>
     * <span data-ttu-id="fd54a-303">Direção da solicitação: > do plugin-NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-303">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="fd54a-304">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-304">The request will contain:</span></span>
         * <span data-ttu-id="fd54a-305">o nível de log para a solicitação</span><span class="sxs-lookup"><span data-stu-id="fd54a-305">the log level for the request</span></span>
         * <span data-ttu-id="fd54a-306">uma mensagem a ser registrada</span><span class="sxs-lookup"><span data-stu-id="fd54a-306">a message to log</span></span>
     * <span data-ttu-id="fd54a-307">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-307">A response will contain:</span></span>
         * <span data-ttu-id="fd54a-308">um código de resposta que indica o resultado da operação.</span><span class="sxs-lookup"><span data-stu-id="fd54a-308">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="fd54a-309">Monitorar a saída do processo NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-309">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="fd54a-310">Direção da solicitação:  Plug-in > do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-310">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="fd54a-311">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-311">The request will contain:</span></span>
         * <span data-ttu-id="fd54a-312">a ID do processo NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-312">the NuGet process ID</span></span>
     * <span data-ttu-id="fd54a-313">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-313">A response will contain:</span></span>
         * <span data-ttu-id="fd54a-314">um código de resposta que indica o resultado da operação.</span><span class="sxs-lookup"><span data-stu-id="fd54a-314">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="fd54a-315">Pacote de pré-busca</span><span class="sxs-lookup"><span data-stu-id="fd54a-315">Prefetch package</span></span>
     * <span data-ttu-id="fd54a-316">Direção da solicitação:  Plug-in > do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-316">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="fd54a-317">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-317">The request will contain:</span></span>
         * <span data-ttu-id="fd54a-318">a ID e a versão do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-318">the package ID and version</span></span>
         * <span data-ttu-id="fd54a-319">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-319">the package source repository location</span></span>
     * <span data-ttu-id="fd54a-320">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-320">A response will contain:</span></span>
         * <span data-ttu-id="fd54a-321">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-321">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="fd54a-322">Definir credenciais</span><span class="sxs-lookup"><span data-stu-id="fd54a-322">Set credentials</span></span>
     * <span data-ttu-id="fd54a-323">Direção da solicitação:  Plug-in > do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-323">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="fd54a-324">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-324">The request will contain:</span></span>
         * <span data-ttu-id="fd54a-325">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-325">the package source repository location</span></span>
         * <span data-ttu-id="fd54a-326">o último nome de usuário de origem do pacote conhecido, se disponível</span><span class="sxs-lookup"><span data-stu-id="fd54a-326">the last known package source username, if available</span></span>
         * <span data-ttu-id="fd54a-327">a última senha de origem do pacote conhecida, se disponível</span><span class="sxs-lookup"><span data-stu-id="fd54a-327">the last known package source password, if available</span></span>
         * <span data-ttu-id="fd54a-328">o último nome de usuário de proxy conhecido, se disponível</span><span class="sxs-lookup"><span data-stu-id="fd54a-328">the last known proxy username, if available</span></span>
         * <span data-ttu-id="fd54a-329">a última senha de proxy conhecida, se disponível</span><span class="sxs-lookup"><span data-stu-id="fd54a-329">the last known proxy password, if available</span></span>
     * <span data-ttu-id="fd54a-330">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-330">A response will contain:</span></span>
         * <span data-ttu-id="fd54a-331">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-331">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="fd54a-332">Definir nível de log</span><span class="sxs-lookup"><span data-stu-id="fd54a-332">Set log level</span></span>
     * <span data-ttu-id="fd54a-333">Direção da solicitação:  Plug-in > do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-333">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="fd54a-334">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-334">The request will contain:</span></span>
         * <span data-ttu-id="fd54a-335">o nível de log padrão</span><span class="sxs-lookup"><span data-stu-id="fd54a-335">the default log level</span></span>
     * <span data-ttu-id="fd54a-336">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-336">A response will contain:</span></span>
         * <span data-ttu-id="fd54a-337">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-337">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="fd54a-338">Mensagens de *2.0.0* de versão de protocolo</span><span class="sxs-lookup"><span data-stu-id="fd54a-338">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="fd54a-339">Obter declarações de operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-339">Get Operation Claims</span></span>

* <span data-ttu-id="fd54a-340">Direção da solicitação:  Plug-in > do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-340">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="fd54a-341">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-341">The request will contain:</span></span>
        * <span data-ttu-id="fd54a-342">o Service index. JSON para uma origem de pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-342">the service index.json for a package source</span></span>
        * <span data-ttu-id="fd54a-343">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="fd54a-343">the package source repository location</span></span>
    * <span data-ttu-id="fd54a-344">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-344">A response will contain:</span></span>
        * <span data-ttu-id="fd54a-345">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="fd54a-345">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="fd54a-346">um enumerável de operações com suporte se a operação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="fd54a-346">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="fd54a-347">Se um plug-in não oferecer suporte à origem do pacote, o plug-in deverá retornar um conjunto vazio de operações com suporte.</span><span class="sxs-lookup"><span data-stu-id="fd54a-347">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="fd54a-348">Se o índice de serviço e a origem do pacote forem nulos, o plug-in poderá responder com a autenticação.</span><span class="sxs-lookup"><span data-stu-id="fd54a-348">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="fd54a-349">Obter credenciais de autenticação</span><span class="sxs-lookup"><span data-stu-id="fd54a-349">Get Authentication Credentials</span></span>

* <span data-ttu-id="fd54a-350">Direção da solicitação: Plug-in > do NuGet</span><span class="sxs-lookup"><span data-stu-id="fd54a-350">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="fd54a-351">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="fd54a-351">The request will contain:</span></span>
    * <span data-ttu-id="fd54a-352">URI</span><span class="sxs-lookup"><span data-stu-id="fd54a-352">Uri</span></span>
    * <span data-ttu-id="fd54a-353">isrepetir</span><span class="sxs-lookup"><span data-stu-id="fd54a-353">isRetry</span></span>
    * <span data-ttu-id="fd54a-354">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="fd54a-354">NonInteractive</span></span>
    * <span data-ttu-id="fd54a-355">Canshowdialog</span><span class="sxs-lookup"><span data-stu-id="fd54a-355">CanShowDialog</span></span>
* <span data-ttu-id="fd54a-356">Uma resposta conterá</span><span class="sxs-lookup"><span data-stu-id="fd54a-356">A response will contain</span></span>
    * <span data-ttu-id="fd54a-357">Nome de usuário</span><span class="sxs-lookup"><span data-stu-id="fd54a-357">Username</span></span>
    * <span data-ttu-id="fd54a-358">Senha</span><span class="sxs-lookup"><span data-stu-id="fd54a-358">Password</span></span>
    * <span data-ttu-id="fd54a-359">Mensagem</span><span class="sxs-lookup"><span data-stu-id="fd54a-359">Message</span></span>
    * <span data-ttu-id="fd54a-360">Lista de tipos de autenticação</span><span class="sxs-lookup"><span data-stu-id="fd54a-360">List of Auth Types</span></span>
    * <span data-ttu-id="fd54a-361">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="fd54a-361">MessageResponseCode</span></span>
