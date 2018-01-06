---
title: "Notas de versão do NuGet 1.8 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: e694ee1a-fe4c-4397-8d0a-7336be4dfebe
description: "Notas de versão do NuGet 1.8 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 1.8 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 350f0d9590c1e0ef1a843fd783203b158059efa7
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-18-release-notes"></a>Notas de versão 1.8 do NuGet

[Notas de versão 1.7 do NuGet](../release-notes/nuget-1.7.md) | [notas de versão do NuGet 2.0](../release-notes/nuget-2.0.md)

1.8 NuGet foi lançado em 23 de maio de 2012.

## <a name="known-installation-issue"></a>Problema de instalação conhecidos
Se você estiver executando o VS 2010 SP1, você pode executar em um erro de instalação durante a tentativa de atualizar o NuGet se você tiver uma versão mais antiga.

A solução alternativa é simplesmente desinstalar NuGet e, em seguida, instalá-lo a partir da Galeria de extensão do VS.  Consulte [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) para obter mais informações, ou [vá diretamente para o hotfix VS](http://bit.ly/vsixcertfix).

Observação: Se o Visual Studio não permitirão que você desinstalar a extensão (o botão de desinstalação estiver desabilitado), em seguida, provavelmente você precisa reiniciar o Visual Studio usando "Executar como administrador".

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 incompatível com o Windows XP, hotfix publicado

Logo após o lançamento do NuGet 1.8, aprendemos que uma alteração de criptografia no 1.8 rompeu usuários no Windows XP.

Já lançamos um hotfix que resolve esse problema.  Atualizando NuGet por meio da Galeria de extensão do Visual Studio, você receberá esse hotfix.

## <a name="features"></a>Recursos

### <a name="satellite-packages-for-localized-resources"></a>Pacotes de satélite para recursos localizados
1.8 NuGet agora dá suporte a capacidade de criar pacotes separados para recursos localizados, semelhantes aos recursos de assembly satélite do .NET Framework.  Um pacote de satélite é criado da mesma maneira como qualquer outro pacote do NuGet com a adição de alguns convenções:

* O nome de arquivo e ID de pacote do satélite deve incluir um sufixo que corresponde a um padrão [cultura cadeias de caracteres usadas pelo .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* No seu `.nuspec` arquivo, o pacote de satélite deve definir um elemento de linguagem com a mesma cadeia de caracteres de cultura usada na ID
* O pacote de satélite deve definir uma dependência em seu `.nuspec` arquivo para seu pacote de núcleo, que é simplesmente o pacote com a mesma ID menos o sufixo do idioma.  O pacote básico precisa estar disponível no repositório para uma instalação bem-sucedida.

Para instalar um pacote com os recursos localizados, um desenvolvedor explicitamente seleciona o pacote localizado do repositório. No momento, a Galeria do NuGet não dá nenhum tipo de tratamento especial para pacotes de satélite.

![Caixa de diálogo de Gerenciador de pacote com pacakges localizada](./media/dlg-w-loc-packs.png)

Porque o pacote de satélite lista uma dependência ao seu pacote de núcleos, o principal e satélite pacotes extraídos para a pasta de pacotes do NuGet e instalados.

![Pasta de pacotes com pacotes localizadas](./media/fldr-loc-packs.png)

Além disso, ao instalar o pacote de satélite, NuGet também reconhece a convenção de nomenclatura de cadeia de caracteres de cultura e, em seguida, copia o assembly de recurso localizado na subpasta correta dentro do pacote principal para que ele pode ser separado pelo .NET Framework.

![Pasta do pacote principal com a pasta de recurso copiado](./media/fldr-copied-loc.png)

Um bug existente observar com pacotes de satélite é que o NuGet não copiar recursos localizados para o `bin` pasta para projetos de site.  Esse problema será corrigido na próxima versão do NuGet.

Para um exemplo completo que demonstra como criar e usar pacotes de satélite, consulte [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Consentimento de restauração do pacote
Na versão 1.8 do NuGet, é apresentada a base para dar suporte a uma restrição importante na restauração do pacote para proteger a privacidade do usuário. Essa restrição requer que os desenvolvedores que criam projetos e soluções que estão usando a restauração do pacote para autorização explicitamente a restauração do pacote vai online para baixar os pacotes de fontes de pacote configurado.

Há 2 modos para fornecer esse consentimento. O primeiro pode ser encontrado no diálogo de configuração do Gerenciador de pacote conforme mostrado abaixo.  Esse método é usado principalmente para computadores de desenvolvedor.

![Diálogo de configuração do Gerenciador de pacote](./media/pr-consent-configdlg.png)

O segundo método é definir o ambiente de variável "EnableNuGetPackageRestore" como o valor "true".  Este método destina-se a máquinas autônomas como servidores de CI ou compilação.

Agora, conforme mencionado acima, vamos apenas estabelecido a base para esse recurso no NuGet 1.8.  Praticamente, isso significa que enquanto adicionamos toda a lógica para habilitar o recurso, ele é não aplicado no momento nesta versão. Ele será habilitado, no entanto, na próxima versão do NuGet, para que nós desejamos que você conheça-lo assim que possível para que você pode configurar seus ambientes adequadamente e, portanto, não ser afetado quando começarmos a impor a restrição de autorização.

Para obter mais detalhes, consulte o [postagem no blog da equipe](http://blog.nuget.org/20120518/package-restore-and-consent.html) sobre esse recurso.

### <a name="nugetexe-performance-improvements"></a>Melhorias de desempenho de NuGet.exe
Modificando o comando de instalação para baixar e instalar pacotes em paralelo, o NuGet 1.8 traz muitas melhorias no desempenho nuget.exe – e restauração do pacote de extensão.  Teste de nível alto mostra o que melhora o desempenho para instalar 6 pacotes em um projeto em cerca de 35% no NuGet 1.8.  Aumentar o número de pacotes para 25 mostra um ganho de desempenho de aproximadamente 60%.

## <a name="bug-fixes"></a>Correções de Bug
NuGet 1.8 inclui algumas correções de bugs com ênfase em como o console do Gerenciador de pacote e o fluxo de trabalho de restauração do pacote, particularmente quando se trata de consentimento de restauração do pacote e integração do Windows 8 Express.
Para obter uma lista completa de trabalho itens corrigidos na versão 1.8 do NuGet,. exibição o [NuGet Issue Tracker para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
