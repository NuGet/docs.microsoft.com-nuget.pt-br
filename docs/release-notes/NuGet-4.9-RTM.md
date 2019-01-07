---
title: Notas sobre a versão do NuGet 4.9 RTM
description: Notas sobre a versão do NuGet 4.9, incluindo problemas conhecidos, correções de bugs, novas funcionalidades e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 7dcb2e430ad80815f716f5567b511ff08acfe31b
ms.sourcegitcommit: a9babe261f67da0f714d168d04ea54a66628974b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2018
ms.locfileid: "53735130"
---
# <a name="nuget-49-release-notes"></a>Notas sobre a versão do NuGet 4.9

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio| Disponível em SDKs do .NET|
|:---|:---|:---|
| **4.9.0** | Versão 15.9.0 do Visual Studio 2017 | 2.1.500, 2.2.100 |
| **4.9.1** | N/D | N/D |
| [**4.9.2**](https://nuget.org/downloads) |[Versão 15.9.4 do Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) | [2.1.502, 2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |

## <a name="summary-whats-new-in-490"></a>Resumo: Novidades no 4.9.0

* Assinatura: Habilite ClientPolicies para exigir o uso de um conjunto de Repositórios e Autores Confiáveis listados em NuGet.Config – [#6961](https://github.com/NuGet/Home/issues/6961), [postagem no blog](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)

* Crie arquivos ".snupkg" para conter símbolos no pacote – aprimore o envio por push para reconhecer o protocolo nuget para aceitar arquivos snupkg para o servidor de símbolos – [#6878](https://github.com/NuGet/Home/issues/6878), [postagem no blog](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)

* Plug-in de credencial do NuGet V2 – [#6642](https://github.com/NuGet/Home/issues/6642)

* Pacotes NuGet autossuficientes – Licença – [#4628](https://github.com/NuGet/Home/issues/4628), [comunicado](https://github.com/NuGet/Announcements/issues/32)

* Habilitar a aceitação de metadados "GeneratePathProperty" em um PackageReference para gerar uma propriedade MSBuild por pacote para "Foo.Bar\1.0\" diretório – [#6949](https://github.com/NuGet/Home/issues/6949)

* Ampliar o sucesso do cliente com operações NuGet – [#7108](https://github.com/NuGet/Home/issues/7108)

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

* Avisos elevados a erros (por meio de WarnAsErrors) acionados por PackageExtraction não devem deixar para trás pacotes extraídos – [#7445](https://github.com/NuGet/Home/issues/7445)

* Pacotes assinados de forma inadequada não devem acabar na pasta de pacotes globais – [#7423](https://github.com/NuGet/Home/issues/7423)

* a associação da geração de redirecionamento não deve ignorar assemblies de fachada – [#7393](https://github.com/NuGet/Home/issues/7393)

* É igual a VersionRange não compara intervalos flutuantes – [#7324](https://github.com/NuGet/Home/issues/7324)

* Restaurar: regressão de desempenho usando a nova pilha HTTP .NET Core 2.1 – [#7314](https://github.com/NuGet/Home/issues/7314)

* A atualização de um Pacote não deve modificar os PrivateAssets de uma PackageReference – [#7285](https://github.com/NuGet/Home/issues/7285)

* Assinatura: a entrada deverá falhar se um pacote tiver muitas entradas de pacote (>65534) – [#7248](https://github.com/NuGet/Home/issues/7248)

* O caminho de código "dotnet nuget push" deve ser compatível com novas credenciais de provedor – [#7233](https://github.com/NuGet/Home/issues/7233)

* Suporte a plug-ins em execução com cultura invariável (como ocorre no docker) – [#7223](https://github.com/NuGet/Home/issues/7223)

* a adição das fontes de nuget não devem excluir credenciais de NuGet.config – [#7200](https://github.com/NuGet/Home/issues/7200)

* a instalação de um devDependency PackageReference deve ter como padrão excludeassets=compile – [#7084](https://github.com/NuGet/Home/issues/7084)

* corrigir a opção de migrador a ser exibida para todos os projetos e exibir uma mensagem de erro se o projeto for incompatível – [#6958](https://github.com/NuGet/Home/issues/6958)

* o "dotnet add package" deve confirmar a restauração que ele realiza para o arquivo de ativos – [#6928](https://github.com/NuGet/Home/issues/6928)

* Assinatura: melhorar as mensagens de erro relacionadas a assinaturas – [#6906](https://github.com/NuGet/Home/issues/6906)

* [Test Failure][zh-TW]A cadeia de caracteres "Package Manager Console" não é localizada no Console do Gerenciador de Pacotes – [#6381](https://github.com/NuGet/Home/issues/6381)

* Mensagem de erro em torno de "Não é possível encontrar informações sobre o projeto" deve ser um pouco mais específica no VS – [#5350](https://github.com/NuGet/Home/issues/5350)

* Mensagem de erro inútil ao usar incorretamente a marca de versão de nuspec do pacote nuget – [#2714](https://github.com/NuGet/Home/issues/2714)

* DCR – Assinatura; oferece suporte ao protocolo NuGet: recurso RepositorySignatures/4.9.0 – [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR – O arquivo .nupkg.metadata será criado durante a extração do pacote – contém "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR – Ignorar a verificação do código de autenticação de plug-ins durante a execução no Mono – [#7222](https://github.com/NuGet/Home/issues/7222)

[Lista de todos os problemas corrigidos na versão 4.9.0](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Resumo: Novidades no 4.9.1

* Adição de suporte para leitura e gravação para o nuget.config por meio de um novo comando signatários-confiáveis – [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

* Correção da geração de links de licença – [#7515](https://github.com/NuGet/Home/issues/7515)

* Regressão de códigos de erro para validação de assinaturas – [#7492](https://github.com/NuGet/Home/issues/7492)

* O pacote NuGet.Build.Tasks.Pack não contém informações de licença – [#7379](https://github.com/NuGet/Home/issues/7379)

[Lista de todas as correções da versão 4.9.1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>Resumo: Novidades no 4.9.2

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

* O recurso VS/dotnet.exe/nuget.exe/msbuild.exe não usa as credenciais quando o nome de origem contém um espaço em branco – [#7517](https://github.com/NuGet/Home/issues/7517)

* Problemas de acessibilidade LicenseAcceptanceWindow e LicenseFileWindow – [#7452](https://github.com/NuGet/Home/issues/7452)

* Correção de FormatException em DateTime.Parse do DateTimeConverter – [#7539](https://github.com/NuGet/Home/issues/7539)

[Lista de todas as correções da versão 4.9.2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="known-issues"></a>Problemas conhecidos

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>dotnet nuget push –-a interatividade gera um erro no Mac. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Problema
O argumento `--interactive` não está sendo encaminhado pela cli do dotnet, resultando no erro `error: Missing value for option 'interactive'`

#### <a name="workaround"></a>Solução alternativa
Execute qualquer outro comando dotnet com a opção interativa, como `dotnet restore --interactive`, e autentique. A autenticação deve ser armazenada em cache pelo provedor das credenciais. Em seguida, execute `dotnet nuget push`.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Os pacotes em FallbackFolders instalados pelo SDK .NET Core são instalados de forma personalizada e falham ao validar a assinatura. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Problema
Ao usar o dotnet.exe 2.x para restaurar um projeto que fará o direcionamento múltiplo para netcoreapp 1.x e netcoreapp 2.x, a pasta de fallback será tratada como um feed de arquivos. Isso significa que, ao restaurar, o NuGet escolherá o pacote da pasta de fallback e tentará instalá-lo na pasta de pacotes globais e fazer a validação de assinatura usual que falha.

#### <a name="workaround"></a>Solução alternativa
Desabilite a pasta de fallback configurando `RestoreAdditionalProjectSources` como nada. `<RestoreAdditionalProjectSources/>` Use essa opção com cuidado porque ela pode fazer com que muitos dos pacotes sejam baixados do NuGet.org, os quais, normalmente, seriam restaurados da pasta de fallback.
