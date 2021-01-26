---
title: Notas de versão do NuGet 3,0 beta
description: Notas de versão do NuGet 3,0 beta, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7970c3d81c724edc743d7b2d38c4c157237a0271
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776624"
---
# <a name="nuget-30-beta-release-notes"></a>Notas de versão do NuGet 3,0 beta

Notas de versão de [visualização do NuGet 3,0](../release-notes/nuget-3.0-preview.md)  |  [Notas de versão do NuGet 3,0 RC](../release-notes/nuget-3.0-rc.md)

O NuGet 3,0 beta foi lançado em 23 de fevereiro de 2015 para a versão do Visual Studio 2015 CTP 6. Esta versão significa muito para nossa equipe, pois temos uma série de aprimoramentos de arquitetura e desempenho para compartilhar, e estamos empolgados em começar a ajustar as configurações de desempenho em nosso serviço nuget.org.

É altamente recomendável que você desinstale qualquer versão anterior da extensão NuGet do Visual Studio 2015 antes de instalar essa nova versão.  Se você tiver problemas com esta versão da extensão, recomendamos que você reverta para a [versão anterior](http://nuget.codeplex.com/downloads/get/909582) para uso com o Visual Studio 2015 Preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Este NuGet 3,0 beta está disponível para instalação na Galeria de extensões do Visual Studio 2015 CTP 6. Estamos trabalhando para obter uma visualização descartada para o Visual Studio 2012 e Visual Studio 2013 muito em breve. Anteriormente, compartilhamos nossa intenção de [descontinuar as atualizações para o Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), e fizemos essa decisão difícil.

## <a name="new-clientserver-api"></a>Nova API de cliente/servidor

Estamos trabalhando em alguns detalhes de implementação para o protocolo cliente/servidor do NuGet. O trabalho que fizemos é criar a "API v3" para o NuGet, que foi projetado em relação à alta disponibilidade para cenários críticos, como a restauração de pacotes e a instalação de pacotes. A nova API é baseada em REST e hipermídia e selecionamos [JSON-LD](http://json-ld.org) como nosso formato de recurso.

Nos bits do NuGet 3,0 beta, você verá uma nova origem do pacote chamada "api.nuget.org" na lista suspensa origem do pacote.   Se você selecionar essa origem do pacote, usaremos nossa nova API em vez de conectar-se ao nuget.org. No NuGet 3,0 RC, essa nova fonte de pacote baseada na API v3 substituirá a origem do pacote "nuget.org" baseado em v2.  É recomendável desabilitar todas as outras fontes de pacote público e deixar apenas api.nuget.org como seu único repositório de pacotes público.

Nós colocamos muito tempo na criação da API v3 e continuaremos mantendo a API v2 padrão para clientes antigos que buscam acessar o repositório público.

## <a name="updated-ui"></a>IU atualizada

Aprimoramos a interface do usuário nesta versão para incluir uma caixa de combinação que permitirá que você escolha uma ação a ser tomada com o pacote e a transição do botão de visualização para uma CheckBox na área de opções da tela.  A área de opções não é mais recolhível e agora fornece um link de ajuda que descreve as opções disponíveis.

![A nova interface do usuário do NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Log de operação

Removemos a janela modal com informações de log que seriam exibidas rapidamente e se ocultam durante a instalação ou desinstalação do.  Essa janela não adicionou nenhum valor quando você realmente deseja ver as informações ou poder copiá-las e colá-las.  Em vez disso, agora estamos redirecionando todo o log de saída para o painel do Gerenciador de pacotes da janela de saída.  Achamos que isso é mais confortável e semelhante a um relatório de compilação típico que você desejará inspecionar.


### <a name="focus-on-performance"></a>Foco no desempenho

Fizemos muitas alterações no nome do aprimoramento do desempenho de pesquisas do NuGet e buscas.  Esse foi o nosso número uma preocupação de nossos clientes e queríamos ter certeza de que nós o abordamos nesta versão.  Ajustamos nossos servidores, criamos uma nova CDN e melhoramos a lógica de correspondência de consulta para que você, espero, fornecer resultados de pesquisa de pacote mais rápidos e relevantes.

Conforme avançamos nesta fase do desenvolvimento do NuGet 3,0, iremos ajustar e monitorar o serviço nuget.org para garantir que oferecemos uma experiência aprimorada.  Não planejamos se envolver em nenhum tempo de inatividade, mas adicionaremos e alteraremos os recursos no serviço.  Fique atento ao nosso [feed do Twitter](http://twitter.com/nuget) para obter detalhes sobre quando alteramos a configuração do serviço.

## <a name="building-nuget-with-nuget"></a>Compilando NuGet com NuGet

Agora, rearquitetamos nossos clientes NuGet em vários componentes que estão sendo criados em pacotes NuGet. Essa reutilização de nossas próprias bibliotecas nos obriga a criar componentes que são reutilizáveis e que podem ser empacotados corretamente.  Conseguimos eliminar o código duplicado e aprender como configurar melhor nosso processo de desenvolvimento para dar suporte à necessidade de criar pacotes em todas as nossas soluções.  Procure uma postagem no blog em breve, onde falaremos sobre como os projetos de código são estruturados e como o processo de compilação funciona.

## <a name="stay-tuned"></a>Fique atento

Fique atento ao [nosso blog](http://blog.nuget.org) para obter mais progresso e anúncios para o NuGet 3,0!
