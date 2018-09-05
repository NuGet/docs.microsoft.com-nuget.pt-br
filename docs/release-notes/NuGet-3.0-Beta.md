---
title: Notas de versão do NuGet 3.0 Beta
description: Notas de versão do NuGet 3.0 Beta, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f9fec6a1af8dfbcfdcfa05a301ff52409521228
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550907"
---
# <a name="nuget-30-beta-release-notes"></a>Notas de versão do NuGet 3.0 Beta

[Notas de versão de visualização do NuGet 3.0](../release-notes/nuget-3.0-preview.md) | [notas de versão do NuGet 3.0 RC](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 Beta foi lançado em 23 de fevereiro de 2015 para a versão do Visual Studio 2015 CTP 6. Esta versão significa muito à nossa equipe, pois temos uma série de aprimoramentos de desempenho e de arquitetura para compartilhar e estamos ansiosos para iniciar o ajuste as configurações de desempenho do nosso serviço nuget.org.

É altamente recomendável que você desinstale qualquer versão anterior da extensão do NuGet Visual Studio 2015 antes de instalar essa nova versão.  Se você tiver problemas com esta versão da extensão, é recomendável que você reverter para o [versão prévia](http://nuget.codeplex.com/downloads/get/909582) para uso com o Visual Studio 2015 preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Este Beta do NuGet 3.0 está disponível para instalação no Visual Studio 2015 CTP 6 extensão de galeria. Estamos trabalhando para obter os descartes de visualização-out para Visual Studio 2012 e Visual Studio 2013 muito em breve. Compartilhamos anteriormente nossa intenção [descontinuar atualizações para o Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), podemos tomar essa decisão difícil.

## <a name="new-clientserver-api"></a>Novo cliente/servidor de API

Estamos trabalhando em alguns detalhes de implementação para o protocolo de cliente/servidor do NuGet. O trabalho que fizemos é criar "V3 da API" para o NuGet, que é desenvolvido em torno de alta disponibilidade para cenários críticos como restauração de pacote e instalar pacotes. A nova API é baseada em REST e selecionou hipermídia e podemos [JSON-LD](http://json-ld.org) como nosso formato de recurso.

Os bits de NuGet 3.0 Beta, você verá uma nova origem de pacote chamada "api.nuget.org" no menu suspenso de origem do pacote.   Se você selecionar essa origem do pacote, vamos usar nossa nova API em vez disso, para se conectar ao nuget.org. No NuGet 3.0 RC, essa nova fonte de pacote com base em v3 da API substituirá a origem do pacote com base em v2 "nuget.org".  Recomendamos desabilitar todas as outras fontes de pacote público e deixe apenas api.nuget.org como seu repositório de pacote somente público.

Nós agrupamos muito tempo na criação de nossa API v3 e continuará a manter a API v2 standard para clientes antigos que buscam acessar o repositório público.

## <a name="updated-ui"></a>Interface do usuário atualizada

Nós aprimoramos a interface do usuário nesta versão para incluir uma caixa de combinação que permitirá que você escolha uma ação a ser tomada com o pacote e feito a transição de botão de visualização para uma caixa de seleção na área de opções da tela.  A área de opções não é mais flexível e agora fornece um link de Ajuda que descreve as opções disponíveis.

![O novo UI NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Log de operações

Removemos a janela modal com informações de registro em log que rapidamente aparecem e ocultar durante a instalação ou desinstalação.  Essa janela não adicionou nenhum valor quando você realmente gostaria de ver as informações ou ser capaz de copiar e colar a partir dele.  Em vez disso, podemos agora está redirecionando toda a saída de registro em log para o painel do Gerenciador de pacotes da janela de saída.  Acreditamos que isso é mais confortável e semelhante a um relatório de compilação típico que você deseja inspecionar.


### <a name="focus-on-performance"></a>O foco no desempenho

Fizemos muitas alterações no nome de melhorar o desempenho de pesquisas do NuGet e buscas.  Isso era nossa preocupação número uma de nossos clientes, e queríamos ter certeza de que resolvemos nesta versão.  Criamos ajustado nossos servidores, desenvolveu um novo CDN e melhor a consulta lógica para espera-se fornecer a você mais relevantes de correspondência e resultados da pesquisa mais rápida do pacote.

Conforme avançamos durante essa fase do desenvolvimento do NuGet 3.0, estamos será de ajuste e o serviço de nuget.org para garantir que podemos entregar uma experiência aprimorada de monitoramento.  Podemos não pretende participar de qualquer tempo de inatividade, mas seja adicionando e alterando os recursos no serviço.  Fique de olho nossas [feed do twitter](http://twitter.com/nuget) para obter detalhes sobre quando alteramos a configuração do serviço.

## <a name="building-nuget-with-nuget"></a>Construção NuGet com o NuGet

Agora podemos ter reprojetada nossos clientes do NuGet em vários componentes que estão sendo compilados em pacotes do NuGet. Essa reutilização das nossas próprias bibliotecas força nos criar componentes que são reutilizáveis e que pode ser empacotado corretamente.  Foi possível eliminar código duplicado e aprendeu como configurar melhor o nosso processo de desenvolvimento para dar suporte a necessidade de compilar pacotes durante nossas soluções.  Procure uma postagem de blog em breve em que vamos falar sobre como os projetos de código são estruturados e como funciona o nosso processo de compilação.

## <a name="stay-tuned"></a>Fique ligado

Por favor, fique atento [nosso blog](http://blog.nuget.org) para obter mais progresso e anúncios para NuGet 3.0!
