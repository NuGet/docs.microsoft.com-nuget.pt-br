---
title: Notas de versão 1.8 do NuGet
description: Notas de versão para versão 1.8 do NuGet incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ff6d12606b1bed479e63eebccd978ff9cd4a7faf
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546615"
---
# <a name="nuget-18-release-notes"></a>Notas de versão 1.8 do NuGet

[Notas de versão do NuGet 1.7](../release-notes/nuget-1.7.md) | [notas de versão do NuGet 2.0](../release-notes/nuget-2.0.md)

NuGet 1.8 foi lançado em 23 de maio de 2012.

## <a name="known-installation-issue"></a>Problema de instalação conhecidos
Se você estiver executando o VS 2010 SP1, você pode executar em um erro de instalação quando tentar atualizar o NuGet se você tiver uma versão mais antiga instalada.

A solução alternativa é simplesmente desinstalar o NuGet e, em seguida, instalá-lo da Galeria de extensão do VS.  Ver [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) para obter mais informações, ou [vá diretamente para o hotfix VS](http://bit.ly/vsixcertfix).

Observação: Se o Visual Studio não permitirão que você desinstale a extensão (o botão Desinstalar está desabilitado), em seguida, é provável que você precisa reiniciar o Visual Studio usando "Executar como administrador".

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 incompatível com o Windows XP, hotfix publicado

Logo após o lançamento do NuGet 1.8, aprendemos que uma alteração de criptografia no 1.8 rompeu usuários no Windows XP.

Já lançamos um hotfix que resolve esse problema.  Ao atualizar o NuGet por meio da Galeria de extensão do Visual Studio, você recebe esse hotfix.

## <a name="features"></a>Recursos

### <a name="satellite-packages-for-localized-resources"></a>Pacotes satélite para recursos localizados
NuGet 1.8 agora dá suporte a capacidade de criar pacotes separados para recursos localizados, semelhantes aos recursos do .NET Framework assembly satélite.  Um pacote satélite é criado da mesma forma como qualquer outro pacote do NuGet com a adição de algumas convenções:

* O nome de arquivo e de ID de pacote satélite deve incluir um sufixo que corresponde a um dos padrão [cultura de cadeias de caracteres usadas pelo .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* No seu `.nuspec` arquivo, o pacote satélite deve definir um elemento de linguagem com a mesma cadeia de caracteres de cultura usada na ID
* O pacote satélite deve definir uma dependência em seu `.nuspec` arquivo para seu pacote principal, que é simplesmente o pacote com a mesma ID menos o sufixo do idioma.  O pacote principal precisa estar disponível no repositório para uma instalação bem-sucedida.

Para instalar um pacote com recursos localizados, o desenvolvedor seleciona explicitamente o pacote localizado do repositório. No momento, a Galeria do NuGet não dá qualquer tipo de tratamento especial para pacotes satélite.

![Caixa de diálogo de Gerenciador de pacote com pacakges localizada](./media/dlg-w-loc-packs.png)

Porque o pacote satélite lista uma dependência ao seu pacote de núcleo, pacotes satélite e de núcleo são extraídos para a pasta de pacotes do NuGet e instalados.

![Pasta de pacotes com pacotes localizados](./media/fldr-loc-packs.png)

Além disso, ao instalar o pacote satélite, o NuGet também reconhece a convenção de nomenclatura de cadeia de caracteres de cultura e, em seguida, copia o assembly de recurso localizado para a subpasta correta dentro do pacote principal para que ele pode ser escolhido pelo .NET Framework.

![Pasta do pacote principal com a pasta de recurso copiado](./media/fldr-copied-loc.png)

Um bug existente observar com pacotes satélite é que o NuGet não copiar recursos localizados para o `bin` pasta projetos de site.  Esse problema será corrigido na próxima versão do NuGet.

Para obter um exemplo completo que demonstra como criar e usar pacotes satélite, consulte [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Consentimento de restauração de pacote
No NuGet 1.8, estamos apresentadas as bases para dar suporte a uma restrição importante na restauração do pacote para proteger a privacidade do usuário. Essa restrição requer que os desenvolvedores que criam projetos e soluções que estão usando a restauração de pacote consentir explicitamente para restauração de pacote vai online para baixar pacotes de fontes de pacote configurado.

Existem 2 maneiras de fornecer esse consentimento. O primeiro pode ser encontrado no diálogo de configuração do Gerenciador de pacote conforme mostrado abaixo.  Este método destina-se principalmente a computadores de desenvolvedor.

![Diálogo de configuração do Gerenciador de pacote](./media/pr-consent-configdlg.png)

O segundo método é definir o ambiente variável "EnableNuGetPackageRestore" como o valor "true".  Este método destina-se a máquinas autônomas, como servidores de CI ou compilação.

Agora, como mencionado acima, estamos apenas formaram a base para esse recurso no NuGet 1.8.  Na prática, isso significa que enquanto adicionamos toda a lógica para habilitar o recurso, ele é atualmente não imposto nesta versão. Ele será habilitado, no entanto, na próxima versão do NuGet, portanto, queremos que você fique ciente-lo assim que possível para que você pode configurar seus ambientes de forma adequada e, portanto, não ser afetado quando começarmos a impor a restrição de consentimento.

Para obter mais detalhes, consulte o [postagem no blog da equipe](http://blog.nuget.org/20120518/package-restore-and-consent.html) sobre esse recurso.

### <a name="nugetexe-performance-improvements"></a>Melhorias de desempenho NuGet.exe
Modificando o comando de instalação para baixar e instalar pacotes em paralelo, o NuGet 1.8 traz melhorias expressivas de desempenho para nuget.exe – e pela restauração de pacote de extensão.  Testes de nível alto mostram o que melhora o desempenho para instalar os 6 pacotes em um projeto em cerca de 35% no NuGet 1.8.  Aumentar o número de pacotes para 25 mostra um ganho de desempenho de cerca de 60%.

## <a name="bug-fixes"></a>Correções de Bug
NuGet 1.8 inclui algumas correções de bugs com ênfase no console do Gerenciador de pacotes e fluxo de trabalho de restauração de pacote, especialmente no que diz respeito ao consentimento de restauração de pacote e a integração do Windows 8 Express.
Para obter uma lista completa de trabalho itens corrigidos no NuGet 1.8, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
