---
title: Notas de versão do NuGet 1,8
description: Notas de versão do NuGet 1,8 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 973a2d010cb75eeeb383be94baf2fb17a999dd7c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383455"
---
# <a name="nuget-18-release-notes"></a>Notas de versão do NuGet 1,8

[Notas de versão do nuget 1,7](../release-notes/nuget-1.7.md) | [notas de versão do NuGet 2,0](../release-notes/nuget-2.0.md)

O NuGet 1,8 foi lançado em 23 de maio de 2012.

## <a name="known-installation-issue"></a>Problema de instalação conhecido
Se você estiver executando o VS 2010 SP1, poderá encontrar um erro de instalação ao tentar atualizar o NuGet se tiver uma versão mais antiga instalada.

A solução alternativa é simplesmente desinstalar o NuGet e, em seguida, instalá-lo a partir da Galeria de extensões do VS.  Consulte <https://support.microsoft.com/kb/2581019> para obter mais informações ou [vá diretamente para o hotfix do vs](http://bit.ly/vsixcertfix).

Observação: se o Visual Studio não permitir que você desinstale a extensão (o botão desinstalar está desabilitado), provavelmente, você precisará reiniciar o Visual Studio usando "executar como administrador".

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1,8 incompatível com o Windows XP, hotfix publicado

Logo após o lançamento do NuGet 1,8, aprendemos que uma alteração de criptografia em 1,8 usuários quebrados no Windows XP.

Já lançamos um hotfix que resolve esse problema.  Ao atualizar o NuGet por meio da Galeria de extensões do Visual Studio, você receberá esse hotfix.

## <a name="features"></a>Recursos

### <a name="satellite-packages-for-localized-resources"></a>Pacotes satélite para recursos localizados
O NuGet 1,8 agora dá suporte à capacidade de criar pacotes separados para recursos localizados, semelhante aos recursos de assembly satélite do .NET Framework.  Um pacote satélite é criado da mesma maneira que qualquer outro pacote NuGet com a adição de algumas convenções:

* A ID do pacote satélite e o nome do arquivo devem incluir um sufixo que corresponda a uma das [cadeias de caracteres de cultura padrão usadas pelo .NET Framework](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).
* Em seu arquivo de `.nuspec`, o pacote satélite deve definir um elemento de linguagem com a mesma cadeia de caracteres de cultura usada na ID
* O pacote satélite deve definir uma dependência em seu arquivo de `.nuspec` para seu pacote principal, que é simplesmente o pacote com a mesma ID menos o sufixo de idioma.  O pacote principal precisa estar disponível no repositório para uma instalação bem-sucedida.

Para instalar um pacote com recursos localizados, um desenvolvedor seleciona explicitamente o pacote localizado do repositório. No momento, a galeria do NuGet não fornece nenhum tipo de tratamento especial para pacotes satélite.

![Caixa de diálogo Gerenciador de pacotes com pacakges localizada](./media/dlg-w-loc-packs.png)

Como o pacote satélite lista uma dependência de seu pacote principal, os pacotes satélite e núcleo são puxados para a pasta pacotes NuGet e instalados.

![Pasta de pacotes com pacotes localizados](./media/fldr-loc-packs.png)

Além disso, ao instalar o pacote satélite, o NuGet também reconhece a Convenção de nomenclatura de cadeia de caracteres de cultura e, em seguida, copia o assembly de recursos localizado na subpasta correta dentro do pacote principal para que ele possa ser escolhido pelo .NET Framework.

![Pasta do pacote principal com a pasta de recursos copiada](./media/fldr-copied-loc.png)

Um bug existente a ser observado com pacotes satélite é que o NuGet não copia recursos localizados para a pasta `bin` para projetos de site.  Esse problema será corrigido na próxima versão do NuGet.

Para obter um exemplo completo demonstrando como criar e usar pacotes satélite, consulte [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Consentimento de restauração de pacote
No NuGet 1,8, nós criamos a base para dar suporte a uma restrição importante na restauração do pacote para proteger a privacidade do usuário. Essa restrição exige que os desenvolvedores criando projetos e soluções que estão usando a restauração de pacote para consentir explicitamente a restauração de pacote ficarão online para baixar pacotes de fontes de pacote configuradas.

Há duas maneiras de fornecer esse consentimento. O primeiro pode ser encontrado na caixa de diálogo de configuração do Gerenciador de pacotes, conforme mostrado abaixo.  Esse método destina-se principalmente a computadores de desenvolvedor.

![Caixa de diálogo de configuração do Gerenciador de pacotes](./media/pr-consent-configdlg.png)

O segundo método é definir a variável de ambiente "EnableNuGetPackageRestore" com o valor "true".  Esse método destina-se a computadores autônomos, como servidores de CI ou de Build.

Agora, como mencionado acima, apresentamos apenas as bases para esse recurso no NuGet 1,8.  Praticamente, isso significa que, embora tenhamos adicionado toda a lógica para habilitar o recurso, ele não é aplicado atualmente nesta versão. Ele será habilitado, no entanto, na próxima versão do NuGet, portanto, queríamos fazer com que você saiba disso assim que possível para configurar seus ambientes adequadamente e, portanto, não serem afetados quando começarmos a impor a restrição de consentimento.

Para obter mais detalhes, consulte a [postagem no blog da equipe](http://blog.nuget.org/20120518/package-restore-and-consent.html) sobre esse recurso.

### <a name="nugetexe-performance-improvements"></a>Melhorias de desempenho do NuGet. exe
Ao modificar o comando install para baixar e instalar pacotes em paralelo, o NuGet 1,8 traz melhorias consideráveis de desempenho para NuGet. exe – e por restauração do pacote de extensão.  O teste de alto nível mostra que o desempenho para a instalação de 6 pacotes em um projeto melhora em cerca de 35% no NuGet 1,8.  Aumentar o número de pacotes para 25 mostra um lucro de desempenho de cerca de 60%.

## <a name="bug-fixes"></a>Correções de Bug
O NuGet 1,8 inclui algumas correções de bugs com ênfase no console do Gerenciador de pacotes e no fluxo de trabalho de restauração do pacote, particularmente, pois ele está relacionado ao consentimento da restauração do pacote e à integração do Windows 8 Express.
Para obter uma lista completa de itens de trabalho corrigidos no NuGet 1,8, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
