---
title: Notas de versão do NuGet 1,4
description: Notas de versão do NuGet 1,4 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e51083be308d97110be9fd67b68f6ba68ccd3df5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777149"
---
# <a name="nuget-14-release-notes"></a>Notas de versão do NuGet 1,4

Notas de versão do [NuGet 1,3](../release-notes/nuget-1.3.md)  |  [Notas de versão do NuGet 1,5](../release-notes/nuget-1.5.md)

O NuGet 1,4 foi lançado em 17 de junho de 2011.

## <a name="features"></a>Recursos

### <a name="update-package-improvements"></a>Aprimoramentos de Update-Package
O NuGet 1,4 apresenta muitos aprimoramentos no comando Update-Package, facilitando a manutenção de pacotes na mesma versão em vários projetos em uma solução. Por exemplo, ao atualizar um pacote para a versão mais recente, é muito comum que você queira que todos os projetos com o pacote instalado sejam atualizados para o mesmo verision.

O `Update-Package` comando agora torna mais fácil:

#### <a name="update-all-packages-in-a-single-project"></a>Atualizar todos os pacotes em um único projeto

```
Update-Package -Project MvcApplication1
```

#### <a name="update-a-package-in-all-projects"></a>Atualizar um pacote em todos os projetos

```
Update-Package PackageId
```

#### <a name="update-all-packages-in-all-projects"></a>Atualizar todos os pacotes em todos os projetos

```
Update-Package
```

#### <a name="perform-a-safe-update-on-all-packages"></a>Executar uma atualização "segura" em todos os pacotes
O `-Safe` sinalizador restringe atualizações para apenas versões com o mesmo componente de versão principal e secundária. Por exemplo, se a versão 1.0.0 de um pacote estiver instalada e as versões 1.0.1, 1.0.2 e 1,1 estiverem disponíveis no feed, o `-Safe` sinalizador atualizará o pacote para 1.0.2. Atualizar sem o `-Safe` sinalizador atualizaria o pacote para a versão mais recente, 1,1.

```
Update-Package -Safe
```

### <a name="managing-packages-at-the-solution-level"></a>Gerenciando pacotes no nível da solução
Antes do NuGet 1,4, a instalação de um pacote em vários projetos era complicada usando a caixa de diálogo. Ele exigiu a inicialização da caixa de diálogo uma vez por projeto.

O NuGet 1,4 adiciona suporte para instalação/desinstalação/atualização de pacotes em vários projetos ao mesmo tempo. Basta iniciar o clicando com o botão direito do mouse na solução e selecionando a opção de menu **gerenciar pacotes NuGet** .

![Caixa de diálogo gerenciar pacotes NuGet no nível da solução](./media/manage-nuget-packages-solution-dialog.png)

Observe que na barra de título da caixa de diálogo, o nome da solução é exibido, não o nome de um projeto.
As operações de pacote agora fornecem uma lista de caixas de seleção com a lista de projetos aos quais a operação deve ser aplicada.

![Gerenciar a seleção de projeto de pacotes NuGet](./media/manage-nuget-packages-project-selection.png)

Para obter mais detalhes, consulte o tópico sobre como [gerenciar pacotes para a solução](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Restringindo atualizações para versões permitidas
Por padrão, ao executar o `Update-Package` comando em um pacote (ou atualizar o pacote usando a caixa de diálogo), ele será atualizado para a versão mais recente no feed. Com o novo suporte para atualizar todos os pacotes, pode haver casos em que você deseja bloquear um pacote para um intervalo de versão específico. Por exemplo, você pode saber com antecedência que seu aplicativo só funcionará com a versão 2. * de um pacote, mas não 3,0 e acima. Para evitar a atualização acidental do pacote para 3, o NuGet 1,4 adiciona suporte para restringir o intervalo de versões para as quais os pacotes podem ser atualizados manualmente editando o `packages.config` arquivo usando o novo `allowedVersions` atributo.

Por exemplo, o exemplo a seguir mostra como bloquear o `SomePackage` pacote do intervalo de versão 2,0-3,0 (exclusivo).
O `allowedVersions` atributo aceita valores usando o [formato de intervalo de versão](../concepts/package-versioning.md#version-ranges).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Observe que, em 1,4, o bloqueio de um pacote para um intervalo de versão específico deve ser editado manualmente. No NuGet 1,5, planejamos adicionar suporte para colocar esse intervalo por meio do `Install-Package` comando.

### <a name="package-visualizer"></a>Visualizador de pacote
O novo Visualizador de pacote, iniciado por meio da biblioteca de **ferramentas**  ->  **Gerenciador** de pacotes opção de menu do  ->  **Visualizador de pacotes** , permite que você visualize facilmente todos os projetos e suas dependências de pacote em uma solução.

_**Observação importante:** Esse recurso aproveita o suporte do DGML no Visual Studio. Só há suporte para a criação da visualização no Visual Studio Ultimate. Só há suporte para a exibição de um diagrama DGML no Visual Studio Premium ou superior._

![Visualizador de pacote](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Verificação de atualização automática para a caixa de diálogo do NuGet
Algumas versões do NuGet introduzem novos recursos expressos por meio do `.nuspec` arquivo que não são compreendidos por versões mais antigas da caixa de diálogo do NuGet.
Um exemplo é a introdução no NuGet 1,4 para [especificar assemblies de estrutura](../release-notes/nuget-1.2.md#framework-assembly-refs).
Por isso, é importante usar a versão mais recente do NuGet para garantir que você possa usar pacotes que aproveitam os recursos mais recentes.
Para tornar as atualizações do NuGet mais visíveis, a caixa de diálogo NuGet contém a lógica para realçar quando uma versão mais recente está disponível.

_**Observação**: a verificação só será feita se a guia **online** tiver sido selecionada na sessão atual._

![Caixa de diálogo gerenciar pacotes NuGet com a nova versão disponível](./media/manage-nuget-packages-update-notification.png)

Para desativar a verificação automática de atualizações, vá para a caixa de diálogo Configurações do NuGet e desmarque **verificar automaticamente se há atualizações**.

![Configurações do NuGet](./media/nuget-settings.png)

Esse recurso foi realmente adicionado no NuGet 1,3, mas não estaria visível, é claro, até que uma atualização para 1,3, como o NuGet 1,4, fosse disponibilizada.

### <a name="package-manager-dialog-improvements"></a>Melhorias da caixa de diálogo do Gerenciador de pacotes
* **Nomes de menu aprimorados**: as opções de menu para iniciar a caixa de diálogo foram renomeadas para fins de clareza. A opção de menu agora é **gerenciar pacotes NuGet**.
* O **painel de detalhes mostra a data de atualização mais recente**: a caixa de diálogo NuGet exibe a data da última atualização no painel de detalhes de um pacote quando a guia **online** ou **atualizações** está selecionada.
* **Lista de marcas exibidas**: a caixa de diálogo NuGet exibe marcas.

### <a name="powershell-improvements"></a>Aprimoramentos do PowerShell
* **Scripts do PowerShell assinados**: o NuGet inclui scripts do PowerShell assinados que habilitam o uso em ambientes mais restritivos.
* **Solicitando suporte**: o console do Gerenciador de pacotes agora dá suporte à solicitação por meio dos `$host.ui.Prompt` `$host.ui.PromptForChoice` comandos e.
* **Nomes de origem de pacote**: o fornecimento do nome de uma origem de pacote tem suporte ao especificar uma origem de pacote usando o `-Source` sinalizador.

### <a name="nugetexe-command-line-improvements"></a>Aprimoramentos na linha de comando do nuget.exe
* **Comandos personalizados do NuGet**: nuget.exe é extensível por meio de comandos personalizados usando o MEF.
* **Mais simples o fluxo de trabalho para a criação de pacotes de símbolo**: o `-Symbols` sinalizador pode ser aplicado a uma estrutura de pasta baseada em Convenção normal, criando um pacote de símbolos apenas incluindo a origem e os `.pdb` arquivos dentro da pasta.
* **Especificando várias fontes**: o `NuGet install` comando dá suporte à especificação de várias fontes usando ponto e vírgula como um delimitador ou especificando `-Source` várias vezes.
* **Suporte à autenticação de proxy**: o NuGet 1,4 adiciona suporte para solicitar credenciais de usuário ao usar o NuGet por trás de um proxy que requer autenticação.
* **nuget.exe atualizar alteração significativa**: o `-Self` sinalizador agora é necessário para que nuget.exe se atualize. `nuget.exe Update` Agora leva um caminho para o `packages.config` arquivo e tentará atualizar os pacotes. Observe que essa atualização é limitada, pois não irá: * * atualizar, adicionar, remover conteúdo no arquivo de projeto.
* * Executar scripts do PowerShell dentro do pacote.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Suporte do servidor NuGet para envio por push de pacotes usando nuget.exe
O NuGet inclui uma maneira simples de hospedar um [repositório NuGet baseado na Web leve](../hosting-packages/nuget-server.md) por meio do `NuGet.Server` pacote NuGet. Com o NuGet 1,4, o servidor leve dá suporte ao envio e exclusão de pacotes usando nuget.exe.
A versão mais recente do `NuGet.Server` adiciona um novo `appSetting` , chamado `apiKey` . Quando a chave é omitida ou deixada em branco, o envio de pacotes para o feed é desabilitado. Definir o apiKey como um valor (idealmente uma senha forte) permite enviar pacotes por push usando nuget.exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Suporte para ferramentas do Windows Phone Mango Edition
Agora, o NuGet tem suporte na versão Release Candidate do Windows Phone Tools para Mango.
Atualmente, as ferramentas de Windows Phone não têm suporte para o Gerenciador de extensões do Visual Studio, portanto, para instalar o NuGet para ferramentas de Windows Phone, talvez seja necessário baixar e executar o VSIX manualmente.

Para desinstalar o NuGet para ferramentas de Windows Phone, execute o comando a seguir.

```
vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5
```

## <a name="bug-fixes"></a>Correções de bugs
O NuGet 1,4 tinha um total de 88 itens de trabalho corrigidos. 71 deles foram marcados como bugs.

Para obter uma lista completa de itens de trabalho corrigidos no NuGet 1,4, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correções de bugs vale a pena observar:

* [Problema 603](http://nuget.codeplex.com/workitem/603): as dependências de pacote em diferentes repositórios são resolvidas corretamente ao especificar uma origem de pacote específica.
* [Problema 1036](http://nuget.codeplex.com/workitem/1036): `NuGet Pack SomeProject.csproj` a adição ao evento de pós-compilação não causa mais um loop infinito.
* [Problema 961](http://nuget.codeplex.com/workitem/961): o `-Source` sinalizador dá suporte a caminhos relativos.

## <a name="nuget-14-update"></a>Atualização do NuGet 1,4
Logo após o lançamento do NuGet 1,4, encontramos alguns problemas que eram importantes para corrigir.
O número de versão específico desta atualização para 1,4 é 1.4.20615.9020.

### <a name="bug-fixes"></a>Correções de bugs
* [Problema 1220](http://nuget.codeplex.com/workitem/1220): Update-Package não é executado `install.ps1` / `uninstall.ps1` em todos os projetos quando há mais de um projeto
* [Problema 1156](http://nuget.codeplex.com/workitem/1156): o Gerenciador de pacotes console paralisado no W2K3/XP (quando o PowerShell 2 não está instalado)
