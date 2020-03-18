---
title: Plug-ins de plataforma cruzada do NuGet
description: Plug-ins de plataforma cruzada do NuGet para NuGet. exe, dotnet. exe, MSBuild. exe e Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429104"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="1aa03-103">Plug-ins de plataforma cruzada do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="1aa03-104">No NuGet 4.8 + suporte para plug-ins de plataforma cruzada foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="1aa03-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="1aa03-105">Isso foi conseguido com a criação de um novo modelo de extensibilidade de plug-in, que precisa estar em conformidade com um conjunto estrito de regras de operação.</span><span class="sxs-lookup"><span data-stu-id="1aa03-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="1aa03-106">Os plug-ins são executáveis independentes (executáveis no mundo do .NET Core), que os clientes NuGet iniciam em um processo separado.</span><span class="sxs-lookup"><span data-stu-id="1aa03-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="1aa03-107">Essa é uma verdadeira gravação única, execute o plug-in de todos os lugares.</span><span class="sxs-lookup"><span data-stu-id="1aa03-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="1aa03-108">Ele funcionará com todas as ferramentas de cliente do NuGet.</span><span class="sxs-lookup"><span data-stu-id="1aa03-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="1aa03-109">Os plug-ins podem ser .NET Framework (NuGet. exe, MSBuild. exe e Visual Studio) ou .NET Core (dotNet. exe).</span><span class="sxs-lookup"><span data-stu-id="1aa03-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="1aa03-110">Um protocolo de comunicação com versão entre o cliente NuGet e o plug-in é definido.</span><span class="sxs-lookup"><span data-stu-id="1aa03-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="1aa03-111">Durante o handshake de inicialização, os 2 processos negociam a versão do protocolo.</span><span class="sxs-lookup"><span data-stu-id="1aa03-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="1aa03-112">Para abranger todos os cenários de ferramentas de cliente do NuGet, é necessário um plug-in de .NET Framework e do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="1aa03-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="1aa03-113">A seguir, a descrição das combinações de cliente/estrutura dos plug-ins.</span><span class="sxs-lookup"><span data-stu-id="1aa03-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="1aa03-114">Ferramenta de cliente</span><span class="sxs-lookup"><span data-stu-id="1aa03-114">Client tool</span></span>  | <span data-ttu-id="1aa03-115">Framework</span><span class="sxs-lookup"><span data-stu-id="1aa03-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="1aa03-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1aa03-116">Visual Studio</span></span> | <span data-ttu-id="1aa03-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1aa03-117">.NET Framework</span></span> |
| <span data-ttu-id="1aa03-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="1aa03-118">dotnet.exe</span></span> | <span data-ttu-id="1aa03-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="1aa03-119">.NET Core</span></span> |
| <span data-ttu-id="1aa03-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="1aa03-120">NuGet.exe</span></span> | <span data-ttu-id="1aa03-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1aa03-121">.NET Framework</span></span> |
| <span data-ttu-id="1aa03-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="1aa03-122">MSBuild.exe</span></span> | <span data-ttu-id="1aa03-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1aa03-123">.NET Framework</span></span> |
| <span data-ttu-id="1aa03-124">NuGet. exe no mono</span><span class="sxs-lookup"><span data-stu-id="1aa03-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="1aa03-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1aa03-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="1aa03-126">Como funciona</span><span class="sxs-lookup"><span data-stu-id="1aa03-126">How does it work</span></span>

<span data-ttu-id="1aa03-127">O fluxo de trabalho de alto nível pode ser descrito da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1aa03-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="1aa03-128">O NuGet descobre plugins disponíveis.</span><span class="sxs-lookup"><span data-stu-id="1aa03-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="1aa03-129">Quando aplicável, o NuGet irá iterar sobre os plug-ins em ordem de prioridade e os iniciará um a um.</span><span class="sxs-lookup"><span data-stu-id="1aa03-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="1aa03-130">O NuGet usará o primeiro plug-in que pode atender à solicitação.</span><span class="sxs-lookup"><span data-stu-id="1aa03-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="1aa03-131">Os plug-ins serão desligados quando não forem mais necessários.</span><span class="sxs-lookup"><span data-stu-id="1aa03-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="1aa03-132">Requisitos gerais de plug-in</span><span class="sxs-lookup"><span data-stu-id="1aa03-132">General plugin requirements</span></span>

<span data-ttu-id="1aa03-133">A versão atual do protocolo é *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="1aa03-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="1aa03-134">Nesta versão, os requisitos são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="1aa03-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="1aa03-135">Ter um assembly de assinatura de Authenticode confiável válido que será executado no Windows e no mono.</span><span class="sxs-lookup"><span data-stu-id="1aa03-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="1aa03-136">Ainda não há nenhum requisito de confiança especial para assemblies executados no Linux e Mac.</span><span class="sxs-lookup"><span data-stu-id="1aa03-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="1aa03-137">Problema relevante</span><span class="sxs-lookup"><span data-stu-id="1aa03-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="1aa03-138">Suporte à inicialização sem monitoração de estado no contexto de segurança atual das ferramentas de cliente do NuGet.</span><span class="sxs-lookup"><span data-stu-id="1aa03-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="1aa03-139">Por exemplo, as ferramentas de cliente do NuGet não executarão a elevação ou inicialização adicional fora do protocolo de plug-in descrito posteriormente.</span><span class="sxs-lookup"><span data-stu-id="1aa03-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="1aa03-140">Ser não interativo, a menos que especificado explicitamente.</span><span class="sxs-lookup"><span data-stu-id="1aa03-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="1aa03-141">Siga a versão do protocolo de plug-in negociado.</span><span class="sxs-lookup"><span data-stu-id="1aa03-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="1aa03-142">Responder a todas as solicitações em um período de tempo razoável.</span><span class="sxs-lookup"><span data-stu-id="1aa03-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="1aa03-143">Honra as solicitações de cancelamento para qualquer operação em andamento.</span><span class="sxs-lookup"><span data-stu-id="1aa03-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="1aa03-144">A especificação técnica é descrita mais detalhadamente nas especificações a seguir:</span><span class="sxs-lookup"><span data-stu-id="1aa03-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="1aa03-145">Plug-in de download do pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="1aa03-146">Plug-in de autenticação entre Plat do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="1aa03-147">Interação do plug-in do cliente</span><span class="sxs-lookup"><span data-stu-id="1aa03-147">Client - Plugin interaction</span></span>

<span data-ttu-id="1aa03-148">As ferramentas de cliente do NuGet e os plug-ins se comunicam com JSON sobre fluxos padrão (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="1aa03-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="1aa03-149">Todos os dados devem ser codificados em UTF-8.</span><span class="sxs-lookup"><span data-stu-id="1aa03-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="1aa03-150">Os plug-ins são iniciados com o argumento "-plugin".</span><span class="sxs-lookup"><span data-stu-id="1aa03-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="1aa03-151">No caso de um usuário iniciar diretamente um executável de plug-in sem esse argumento, o plug-in pode fornecer uma mensagem informativa em vez de aguardar um handshake de protocolo.</span><span class="sxs-lookup"><span data-stu-id="1aa03-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="1aa03-152">O tempo limite de handshake de protocolo é de 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="1aa03-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="1aa03-153">O plug-in deve concluir a configuração no menor valor possível.</span><span class="sxs-lookup"><span data-stu-id="1aa03-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="1aa03-154">As ferramentas de cliente do NuGet consultarão as operações com suporte de um plug-in passando o índice de serviço para uma origem do NuGet.</span><span class="sxs-lookup"><span data-stu-id="1aa03-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="1aa03-155">Um plug-in pode usar o índice de serviço para verificar a presença de tipos de serviço com suporte.</span><span class="sxs-lookup"><span data-stu-id="1aa03-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="1aa03-156">A comunicação entre as ferramentas de cliente do NuGet e o plug-in é bidirecional.</span><span class="sxs-lookup"><span data-stu-id="1aa03-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="1aa03-157">Cada solicitação tem um tempo limite de 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="1aa03-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="1aa03-158">Se as operações devem levar mais tempo, o respectivo processo deve enviar uma mensagem de progresso para impedir que a solicitação atinja o tempo limite. Após 1 minuto de inatividade, um plug-in é considerado ocioso e é desligado.</span><span class="sxs-lookup"><span data-stu-id="1aa03-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="1aa03-159">Instalação e descoberta do plug-in</span><span class="sxs-lookup"><span data-stu-id="1aa03-159">Plugin installation and discovery</span></span>

<span data-ttu-id="1aa03-160">Os plug-ins serão descobertos por meio de uma estrutura de diretório baseada em convenção.</span><span class="sxs-lookup"><span data-stu-id="1aa03-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="1aa03-161">Cenários de CI/CD e usuários avançados podem usar variáveis de ambiente para substituir o comportamento.</span><span class="sxs-lookup"><span data-stu-id="1aa03-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="1aa03-162">Ao usar variáveis de ambiente, somente caminhos absolutos são permitidos.</span><span class="sxs-lookup"><span data-stu-id="1aa03-162">When using environment variables, only absolute paths are allowed.</span></span> <span data-ttu-id="1aa03-163">Observe que `NUGET_NETFX_PLUGIN_PATHS` e `NUGET_NETCORE_PLUGIN_PATHS` estão disponíveis apenas com a versão 5.3 + das ferramentas do NuGet e posterior.</span><span class="sxs-lookup"><span data-stu-id="1aa03-163">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="1aa03-164">`NUGET_NETFX_PLUGIN_PATHS`-define os plug-ins que serão usados pelas ferramentas baseadas em .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="1aa03-164">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="1aa03-165">Tem precedência sobre `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="1aa03-165">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="1aa03-166">(Somente NuGet versão 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="1aa03-166">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="1aa03-167">`NUGET_NETCORE_PLUGIN_PATHS`-define os plug-ins que serão usados pelas ferramentas baseadas no .NET Core (dotNet. exe).</span><span class="sxs-lookup"><span data-stu-id="1aa03-167">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="1aa03-168">Tem precedência sobre `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="1aa03-168">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="1aa03-169">(Somente NuGet versão 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="1aa03-169">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="1aa03-170">`NUGET_PLUGIN_PATHS`-define os plug-ins que serão usados para esse processo NuGet, prioridade preservada.</span><span class="sxs-lookup"><span data-stu-id="1aa03-170">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority preserved.</span></span> <span data-ttu-id="1aa03-171">Se essa variável de ambiente for definida, ela substituirá a descoberta baseada em convenção.</span><span class="sxs-lookup"><span data-stu-id="1aa03-171">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="1aa03-172">Ignorado se uma das variáveis específicas do Framework for especificada.</span><span class="sxs-lookup"><span data-stu-id="1aa03-172">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="1aa03-173">Local do usuário, o local inicial do NuGet em `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="1aa03-173">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="1aa03-174">Esse local não pode ser substituído.</span><span class="sxs-lookup"><span data-stu-id="1aa03-174">This location cannot be overriden.</span></span> <span data-ttu-id="1aa03-175">Um diretório raiz diferente será usado para os plug-ins .NET Core e .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="1aa03-175">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="1aa03-176">Framework</span><span class="sxs-lookup"><span data-stu-id="1aa03-176">Framework</span></span> | <span data-ttu-id="1aa03-177">Local de descoberta raiz</span><span class="sxs-lookup"><span data-stu-id="1aa03-177">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="1aa03-178">.NET Core</span><span class="sxs-lookup"><span data-stu-id="1aa03-178">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="1aa03-179">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1aa03-179">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="1aa03-180">Cada plug-in deve ser instalado em sua própria pasta.</span><span class="sxs-lookup"><span data-stu-id="1aa03-180">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="1aa03-181">O ponto de entrada do plug-in será o nome da pasta instalada, com as extensões. dll para .NET Core e a extensão. exe para .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="1aa03-181">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="1aa03-182">No momento, não há nenhuma história de usuário para a instalação dos plug-ins.</span><span class="sxs-lookup"><span data-stu-id="1aa03-182">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="1aa03-183">É tão simples quanto mover os arquivos necessários para o local predeterminado.</span><span class="sxs-lookup"><span data-stu-id="1aa03-183">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="1aa03-184">Operações com suporte</span><span class="sxs-lookup"><span data-stu-id="1aa03-184">Supported operations</span></span>

<span data-ttu-id="1aa03-185">Há suporte para duas operações no novo protocolo de plugin.</span><span class="sxs-lookup"><span data-stu-id="1aa03-185">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="1aa03-186">Nome da operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-186">Operation name</span></span> | <span data-ttu-id="1aa03-187">Versão mínima do protocolo</span><span class="sxs-lookup"><span data-stu-id="1aa03-187">Minimum protocol version</span></span> | <span data-ttu-id="1aa03-188">Versão mínima do cliente NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-188">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="1aa03-189">Baixar pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-189">Download Package</span></span> | <span data-ttu-id="1aa03-190">1.0.0</span><span class="sxs-lookup"><span data-stu-id="1aa03-190">1.0.0</span></span> | <span data-ttu-id="1aa03-191">4.3.0</span><span class="sxs-lookup"><span data-stu-id="1aa03-191">4.3.0</span></span> |
| [<span data-ttu-id="1aa03-192">Autenticação</span><span class="sxs-lookup"><span data-stu-id="1aa03-192">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="1aa03-193">2.0.0</span><span class="sxs-lookup"><span data-stu-id="1aa03-193">2.0.0</span></span> | <span data-ttu-id="1aa03-194">4.8.0</span><span class="sxs-lookup"><span data-stu-id="1aa03-194">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="1aa03-195">Executando plug-ins no tempo de execução correto</span><span class="sxs-lookup"><span data-stu-id="1aa03-195">Running plugins under the correct runtime</span></span>

<span data-ttu-id="1aa03-196">Para o NuGet em cenários dotnet. exe, os plug-ins precisam ser capazes de executar sob esse tempo de execução específico do dotnet. exe.</span><span class="sxs-lookup"><span data-stu-id="1aa03-196">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="1aa03-197">Ele está no provedor de plug-in e no consumidor para garantir que uma combinação de dotnet. exe/plugin compatível seja usada.</span><span class="sxs-lookup"><span data-stu-id="1aa03-197">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="1aa03-198">Um problema potencial pode surgir com os plug-ins de localização do usuário quando, por exemplo, um dotnet. exe no tempo de execução 2,0 tentar usar um plug-in gravado para o tempo de execução 2,1.</span><span class="sxs-lookup"><span data-stu-id="1aa03-198">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="1aa03-199">Recursos de cache</span><span class="sxs-lookup"><span data-stu-id="1aa03-199">Capabilities caching</span></span>

<span data-ttu-id="1aa03-200">A verificação de segurança e a instanciação dos plug-ins são dispendiosas.</span><span class="sxs-lookup"><span data-stu-id="1aa03-200">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="1aa03-201">A operação de download ocorre de maneira mais frequente do que a operação de autenticação, no entanto, o usuário NuGet médio provavelmente terá um plug-in de autenticação.</span><span class="sxs-lookup"><span data-stu-id="1aa03-201">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="1aa03-202">Para melhorar a experiência, o NuGet armazenará em cache as declarações de operação para a solicitação especificada.</span><span class="sxs-lookup"><span data-stu-id="1aa03-202">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="1aa03-203">Esse cache é por plug-in com a chave do plug-in sendo o caminho do plug-in e a expiração desse cache de recursos é de 30 dias.</span><span class="sxs-lookup"><span data-stu-id="1aa03-203">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="1aa03-204">O cache está localizado em `%LocalAppData%/NuGet/plugins-cache` e substituído pela variável de ambiente `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="1aa03-204">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="1aa03-205">Para limpar esse [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), é possível executar o comando locals com a opção `plugins-cache`.</span><span class="sxs-lookup"><span data-stu-id="1aa03-205">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="1aa03-206">A opção `all` locais agora também excluirá o cache de plug-ins.</span><span class="sxs-lookup"><span data-stu-id="1aa03-206">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="1aa03-207">Índice de mensagens de protocolo</span><span class="sxs-lookup"><span data-stu-id="1aa03-207">Protocol messages index</span></span>

<span data-ttu-id="1aa03-208">Mensagens da versão *1.0.0* do protocolo:</span><span class="sxs-lookup"><span data-stu-id="1aa03-208">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="1aa03-209">Feche</span><span class="sxs-lookup"><span data-stu-id="1aa03-209">Close</span></span>
    * <span data-ttu-id="1aa03-210">Direção da solicitação: plugin > do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-210">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1aa03-211">A solicitação não conterá nenhuma carga</span><span class="sxs-lookup"><span data-stu-id="1aa03-211">The request will contain no payload</span></span>
    * <span data-ttu-id="1aa03-212">Nenhuma resposta é esperada.</span><span class="sxs-lookup"><span data-stu-id="1aa03-212">No response is expected.</span></span>  <span data-ttu-id="1aa03-213">A resposta correta é para que o processo do plug-in seja fechado imediatamente.</span><span class="sxs-lookup"><span data-stu-id="1aa03-213">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="1aa03-214">Copiar arquivos no pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-214">Copy files in package</span></span>
    * <span data-ttu-id="1aa03-215">Direção da solicitação: plugin > do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-215">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1aa03-216">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-216">The request will contain:</span></span>
        * <span data-ttu-id="1aa03-217">a ID e a versão do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-217">the package ID and version</span></span>
        * <span data-ttu-id="1aa03-218">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-218">the package source repository location</span></span>
        * <span data-ttu-id="1aa03-219">caminho do diretório de destino</span><span class="sxs-lookup"><span data-stu-id="1aa03-219">destination directory path</span></span>
        * <span data-ttu-id="1aa03-220">um enumerável de arquivos no pacote a ser copiado para o caminho do diretório de destino</span><span class="sxs-lookup"><span data-stu-id="1aa03-220">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="1aa03-221">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-221">A response will contain:</span></span>
        * <span data-ttu-id="1aa03-222">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-222">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1aa03-223">um enumerável de caminhos completos para arquivos copiados no diretório de destino se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="1aa03-223">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="1aa03-224">Copiar arquivo de pacote (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="1aa03-224">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="1aa03-225">Direção da solicitação: plugin > do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-225">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1aa03-226">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-226">The request will contain:</span></span>
        * <span data-ttu-id="1aa03-227">a ID e a versão do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-227">the package ID and version</span></span>
        * <span data-ttu-id="1aa03-228">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-228">the package source repository location</span></span>
        * <span data-ttu-id="1aa03-229">o caminho do arquivo de destino</span><span class="sxs-lookup"><span data-stu-id="1aa03-229">the destination file path</span></span>
    * <span data-ttu-id="1aa03-230">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-230">A response will contain:</span></span>
        * <span data-ttu-id="1aa03-231">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-231">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="1aa03-232">Obter credenciais</span><span class="sxs-lookup"><span data-stu-id="1aa03-232">Get credentials</span></span>
    * <span data-ttu-id="1aa03-233">Direção da solicitação: > do plugin-NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-233">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="1aa03-234">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-234">The request will contain:</span></span>
        * <span data-ttu-id="1aa03-235">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-235">the package source repository location</span></span>
        * <span data-ttu-id="1aa03-236">o código de status HTTP obtido do repositório de origem do pacote usando as credenciais atuais</span><span class="sxs-lookup"><span data-stu-id="1aa03-236">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="1aa03-237">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-237">A response will contain:</span></span>
        * <span data-ttu-id="1aa03-238">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1aa03-239">um nome de usuário, se disponível</span><span class="sxs-lookup"><span data-stu-id="1aa03-239">a username, if available</span></span>
        * <span data-ttu-id="1aa03-240">uma senha, se disponível</span><span class="sxs-lookup"><span data-stu-id="1aa03-240">a password, if available</span></span>

5.  <span data-ttu-id="1aa03-241">Obter arquivos no pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-241">Get files in package</span></span>
    * <span data-ttu-id="1aa03-242">Direção da solicitação: plugin > do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-242">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1aa03-243">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-243">The request will contain:</span></span>
        * <span data-ttu-id="1aa03-244">a ID e a versão do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-244">the package ID and version</span></span>
        * <span data-ttu-id="1aa03-245">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-245">the package source repository location</span></span>
    * <span data-ttu-id="1aa03-246">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-246">A response will contain:</span></span>
        * <span data-ttu-id="1aa03-247">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-247">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1aa03-248">um enumerável de caminhos de arquivo no pacote se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="1aa03-248">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="1aa03-249">Obter declarações de operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-249">Get operation claims</span></span> 
    * <span data-ttu-id="1aa03-250">Direção da solicitação: plugin > do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-250">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1aa03-251">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-251">The request will contain:</span></span>
        * <span data-ttu-id="1aa03-252">o Service index. JSON para uma origem de pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-252">the service index.json for a package source</span></span>
        * <span data-ttu-id="1aa03-253">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-253">the package source repository location</span></span>
    * <span data-ttu-id="1aa03-254">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-254">A response will contain:</span></span>
        * <span data-ttu-id="1aa03-255">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-255">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1aa03-256">um enumerável de operações com suporte (por exemplo: download de pacote) se a operação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="1aa03-256">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="1aa03-257">Se um plug-in não oferecer suporte à origem do pacote, o plug-in deverá retornar um conjunto vazio de operações com suporte.</span><span class="sxs-lookup"><span data-stu-id="1aa03-257">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="1aa03-258">Esta mensagem foi atualizada na versão *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="1aa03-258">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="1aa03-259">Ele está no cliente para preservar a compatibilidade com versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="1aa03-259">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="1aa03-260">Obter hash do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-260">Get package hash</span></span>
    * <span data-ttu-id="1aa03-261">Direção da solicitação: plugin > do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1aa03-262">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-262">The request will contain:</span></span>
        * <span data-ttu-id="1aa03-263">a ID e a versão do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-263">the package ID and version</span></span>
        * <span data-ttu-id="1aa03-264">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-264">the package source repository location</span></span>
        * <span data-ttu-id="1aa03-265">o algoritmo de hash</span><span class="sxs-lookup"><span data-stu-id="1aa03-265">the hash algorithm</span></span>
    * <span data-ttu-id="1aa03-266">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-266">A response will contain:</span></span>
        * <span data-ttu-id="1aa03-267">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-267">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1aa03-268">um hash de arquivo de pacote usando o algoritmo de hash solicitado se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="1aa03-268">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="1aa03-269">Obter versões de pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-269">Get package versions</span></span>
    * <span data-ttu-id="1aa03-270">Direção da solicitação: plugin > do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-270">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1aa03-271">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-271">The request will contain:</span></span>
        * <span data-ttu-id="1aa03-272">a ID do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-272">the package ID</span></span>
        * <span data-ttu-id="1aa03-273">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-273">the package source repository location</span></span>
    * <span data-ttu-id="1aa03-274">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-274">A response will contain:</span></span>
        * <span data-ttu-id="1aa03-275">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-275">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1aa03-276">um enumerável de versões de pacote se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="1aa03-276">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="1aa03-277">Obter índice de serviço</span><span class="sxs-lookup"><span data-stu-id="1aa03-277">Get service index</span></span>
    * <span data-ttu-id="1aa03-278">Direção da solicitação: > do plugin-NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-278">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="1aa03-279">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-279">The request will contain:</span></span>
        * <span data-ttu-id="1aa03-280">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-280">the package source repository location</span></span>
    * <span data-ttu-id="1aa03-281">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-281">A response will contain:</span></span>
        * <span data-ttu-id="1aa03-282">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-282">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1aa03-283">o índice de serviço se a operação foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="1aa03-283">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="1aa03-284">Handshake</span><span class="sxs-lookup"><span data-stu-id="1aa03-284">Handshake</span></span>
     * <span data-ttu-id="1aa03-285">Direção da solicitação: plug-in < > do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-285">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="1aa03-286">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-286">The request will contain:</span></span>
         * <span data-ttu-id="1aa03-287">a versão do protocolo do plugin atual</span><span class="sxs-lookup"><span data-stu-id="1aa03-287">the current plugin protocol version</span></span>
         * <span data-ttu-id="1aa03-288">a versão mínima do protocolo de plug-in com suporte</span><span class="sxs-lookup"><span data-stu-id="1aa03-288">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="1aa03-289">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-289">A response will contain:</span></span>
         * <span data-ttu-id="1aa03-290">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-290">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="1aa03-291">a versão do protocolo negociado se a operação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="1aa03-291">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="1aa03-292">Uma falha resultará no encerramento do plug-in.</span><span class="sxs-lookup"><span data-stu-id="1aa03-292">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="1aa03-293">Inicializar</span><span class="sxs-lookup"><span data-stu-id="1aa03-293">Initialize</span></span>
     * <span data-ttu-id="1aa03-294">Direção da solicitação: plugin > do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-294">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="1aa03-295">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-295">The request will contain:</span></span>
         * <span data-ttu-id="1aa03-296">a versão da ferramenta do cliente NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-296">the NuGet client tool version</span></span>
         * <span data-ttu-id="1aa03-297">o idioma efetivo da ferramenta de cliente NuGet.</span><span class="sxs-lookup"><span data-stu-id="1aa03-297">the NuGet client tool effective language.</span></span>  <span data-ttu-id="1aa03-298">Isso leva em consideração a configuração ForceEnglishOutput, se usada.</span><span class="sxs-lookup"><span data-stu-id="1aa03-298">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="1aa03-299">o tempo limite de solicitação padrão, que substitui o padrão de protocolo.</span><span class="sxs-lookup"><span data-stu-id="1aa03-299">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="1aa03-300">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-300">A response will contain:</span></span>
         * <span data-ttu-id="1aa03-301">um código de resposta que indica o resultado da operação.</span><span class="sxs-lookup"><span data-stu-id="1aa03-301">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="1aa03-302">Uma falha resultará no encerramento do plug-in.</span><span class="sxs-lookup"><span data-stu-id="1aa03-302">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="1aa03-303">Log</span><span class="sxs-lookup"><span data-stu-id="1aa03-303">Log</span></span>
     * <span data-ttu-id="1aa03-304">Direção da solicitação: > do plugin-NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-304">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="1aa03-305">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-305">The request will contain:</span></span>
         * <span data-ttu-id="1aa03-306">o nível de log para a solicitação</span><span class="sxs-lookup"><span data-stu-id="1aa03-306">the log level for the request</span></span>
         * <span data-ttu-id="1aa03-307">uma mensagem a ser registrada</span><span class="sxs-lookup"><span data-stu-id="1aa03-307">a message to log</span></span>
     * <span data-ttu-id="1aa03-308">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-308">A response will contain:</span></span>
         * <span data-ttu-id="1aa03-309">um código de resposta que indica o resultado da operação.</span><span class="sxs-lookup"><span data-stu-id="1aa03-309">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="1aa03-310">Monitorar a saída do processo NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-310">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="1aa03-311">Direção da solicitação: plugin > do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-311">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="1aa03-312">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-312">The request will contain:</span></span>
         * <span data-ttu-id="1aa03-313">a ID do processo NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-313">the NuGet process ID</span></span>
     * <span data-ttu-id="1aa03-314">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-314">A response will contain:</span></span>
         * <span data-ttu-id="1aa03-315">um código de resposta que indica o resultado da operação.</span><span class="sxs-lookup"><span data-stu-id="1aa03-315">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="1aa03-316">Pacote de pré-busca</span><span class="sxs-lookup"><span data-stu-id="1aa03-316">Prefetch package</span></span>
     * <span data-ttu-id="1aa03-317">Direção da solicitação: plugin > do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-317">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="1aa03-318">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-318">The request will contain:</span></span>
         * <span data-ttu-id="1aa03-319">a ID e a versão do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-319">the package ID and version</span></span>
         * <span data-ttu-id="1aa03-320">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-320">the package source repository location</span></span>
     * <span data-ttu-id="1aa03-321">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-321">A response will contain:</span></span>
         * <span data-ttu-id="1aa03-322">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-322">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="1aa03-323">Definir as credenciais</span><span class="sxs-lookup"><span data-stu-id="1aa03-323">Set credentials</span></span>
     * <span data-ttu-id="1aa03-324">Direção da solicitação: plugin > do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-324">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="1aa03-325">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-325">The request will contain:</span></span>
         * <span data-ttu-id="1aa03-326">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-326">the package source repository location</span></span>
         * <span data-ttu-id="1aa03-327">o último nome de usuário de origem do pacote conhecido, se disponível</span><span class="sxs-lookup"><span data-stu-id="1aa03-327">the last known package source username, if available</span></span>
         * <span data-ttu-id="1aa03-328">a última senha de origem do pacote conhecida, se disponível</span><span class="sxs-lookup"><span data-stu-id="1aa03-328">the last known package source password, if available</span></span>
         * <span data-ttu-id="1aa03-329">o último nome de usuário de proxy conhecido, se disponível</span><span class="sxs-lookup"><span data-stu-id="1aa03-329">the last known proxy username, if available</span></span>
         * <span data-ttu-id="1aa03-330">a última senha de proxy conhecida, se disponível</span><span class="sxs-lookup"><span data-stu-id="1aa03-330">the last known proxy password, if available</span></span>
     * <span data-ttu-id="1aa03-331">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-331">A response will contain:</span></span>
         * <span data-ttu-id="1aa03-332">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-332">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="1aa03-333">Definir nível de log</span><span class="sxs-lookup"><span data-stu-id="1aa03-333">Set log level</span></span>
     * <span data-ttu-id="1aa03-334">Direção da solicitação: plugin > do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-334">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="1aa03-335">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-335">The request will contain:</span></span>
         * <span data-ttu-id="1aa03-336">o nível de log padrão</span><span class="sxs-lookup"><span data-stu-id="1aa03-336">the default log level</span></span>
     * <span data-ttu-id="1aa03-337">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-337">A response will contain:</span></span>
         * <span data-ttu-id="1aa03-338">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-338">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="1aa03-339">Mensagens de *2.0.0* de versão de protocolo</span><span class="sxs-lookup"><span data-stu-id="1aa03-339">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="1aa03-340">Obter declarações de operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-340">Get Operation Claims</span></span>

* <span data-ttu-id="1aa03-341">Direção da solicitação: plugin > do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-341">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1aa03-342">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-342">The request will contain:</span></span>
        * <span data-ttu-id="1aa03-343">o Service index. JSON para uma origem de pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-343">the service index.json for a package source</span></span>
        * <span data-ttu-id="1aa03-344">o local do repositório de origem do pacote</span><span class="sxs-lookup"><span data-stu-id="1aa03-344">the package source repository location</span></span>
    * <span data-ttu-id="1aa03-345">Uma resposta conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-345">A response will contain:</span></span>
        * <span data-ttu-id="1aa03-346">um código de resposta que indica o resultado da operação</span><span class="sxs-lookup"><span data-stu-id="1aa03-346">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1aa03-347">um enumerável de operações com suporte se a operação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="1aa03-347">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="1aa03-348">Se um plug-in não oferecer suporte à origem do pacote, o plug-in deverá retornar um conjunto vazio de operações com suporte.</span><span class="sxs-lookup"><span data-stu-id="1aa03-348">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="1aa03-349">Se o índice de serviço e a origem do pacote forem nulos, o plug-in poderá responder com a autenticação.</span><span class="sxs-lookup"><span data-stu-id="1aa03-349">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="1aa03-350">Obter credenciais de autenticação</span><span class="sxs-lookup"><span data-stu-id="1aa03-350">Get Authentication Credentials</span></span>

* <span data-ttu-id="1aa03-351">Direção da solicitação: plugin > do NuGet</span><span class="sxs-lookup"><span data-stu-id="1aa03-351">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="1aa03-352">A solicitação conterá:</span><span class="sxs-lookup"><span data-stu-id="1aa03-352">The request will contain:</span></span>
    * <span data-ttu-id="1aa03-353">Uri</span><span class="sxs-lookup"><span data-stu-id="1aa03-353">Uri</span></span>
    * <span data-ttu-id="1aa03-354">Isrepetir</span><span class="sxs-lookup"><span data-stu-id="1aa03-354">isRetry</span></span>
    * <span data-ttu-id="1aa03-355">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1aa03-355">NonInteractive</span></span>
    * <span data-ttu-id="1aa03-356">Canshowdialog</span><span class="sxs-lookup"><span data-stu-id="1aa03-356">CanShowDialog</span></span>
* <span data-ttu-id="1aa03-357">Uma resposta conterá</span><span class="sxs-lookup"><span data-stu-id="1aa03-357">A response will contain</span></span>
    * <span data-ttu-id="1aa03-358">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="1aa03-358">Username</span></span>
    * <span data-ttu-id="1aa03-359">Senha</span><span class="sxs-lookup"><span data-stu-id="1aa03-359">Password</span></span>
    * <span data-ttu-id="1aa03-360">Mensagem</span><span class="sxs-lookup"><span data-stu-id="1aa03-360">Message</span></span>
    * <span data-ttu-id="1aa03-361">Lista de tipos de autenticação</span><span class="sxs-lookup"><span data-stu-id="1aa03-361">List of Auth Types</span></span>
    * <span data-ttu-id="1aa03-362">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="1aa03-362">MessageResponseCode</span></span>
