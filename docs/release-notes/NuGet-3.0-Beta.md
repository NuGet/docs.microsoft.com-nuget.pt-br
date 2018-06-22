---
title: Notas de versão do NuGet 3.0 Beta
description: Notas de versão do NuGet 3.0 Beta, incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4608b196d19f95410f9fe20f6a22e31c15955b89
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819621"
---
# <a name="nuget-30-beta-release-notes"></a>Notas de versão do NuGet 3.0 Beta

[Notas de versão de visualização do NuGet 3.0](../release-notes/nuget-3.0-preview.md) | [notas de versão do NuGet 3.0 RC](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 Beta foi lançado em 23 de fevereiro de 2015 para a versão do Visual Studio 2015 CTP 6. Esta versão significa muito para nossa equipe, como temos inúmeras melhorias de desempenho e de arquitetura para compartilhar e estamos empolgados em para iniciar o ajuste as configurações de desempenho em nosso serviço nuget.org.

É altamente recomendável que você desinstale qualquer versão anterior da extensão do NuGet Visual Studio 2015 antes de instalar esta nova versão.  Se você tiver problemas com esta versão da extensão, recomendamos que você reverter para a [versão anterior](http://nuget.codeplex.com/downloads/get/909582) para uso com o Visual Studio 2015 preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Este NuGet 3.0 Beta está disponível para instalação no Visual Studio 2015 CTP 6 extensão de galeria. Estamos trabalhando para sair descartes de preview para Visual Studio 2012 e o Visual Studio 2013 muito em breve. Anteriormente, compartilhamos nossa intenção [interromper as atualizações para o Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), e fez essa decisão difícil.

## <a name="new-clientserver-api"></a>Novo cliente/servidor de API

Estamos trabalhando alguns detalhes de implementação para o protocolo de cliente/servidor do NuGet. O trabalho que já fizemos é criar "API v3" NuGet, que foi projetado para alta disponibilidade de cenários críticos como a restauração do pacote e instalação de pacotes. A nova API é baseada em REST e hipermídia e selecionou [JSON LD](http://json-ld.org) como nosso formato de recurso.

Os bits do NuGet 3.0 Beta, você verá uma nova origem do pacote chamada "api.nuget.org" no menu suspenso de origem do pacote.   Se você selecionar essa fonte de pacote, vamos usar nossa nova API em vez disso, para se conectar ao nuget.org. No NuGet 3.0 RC, essa nova fonte de pacote com base em v3 API substituirá a origem do pacote com base em v2 "nuget.org".  Recomendamos desabilitar todas as outras fontes de pacote público e deixe apenas api.nuget.org como o repositório de pacotes somente públicos.

Nós agrupamos muito tempo na criação de nossa API v3 e continuará a manter a API v2 padrão para clientes antigos que desejam acessar o repositório público.

## <a name="updated-ui"></a>Interface de usuário atualizada

Aprimoramos a interface do usuário nesta versão para incluir uma caixa de combinação que permitirá que você escolha uma ação a ser executada com o pacote e o botão de visualização por transição para uma caixa de seleção na área de opções da tela.  A área de opções não é mais flexível e agora fornece um link de Ajuda que descreve as opções disponíveis.

![O novo UI NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Log de operações

Removemos janela modal com informações de log que rapidamente aparecem e ocultar durante a instalação ou desinstalação.  Esta janela não adicionar nenhum valor quando seria realmente deseja ver as informações ou ser capaz de copiar e colar.  Em vez disso, podemos agora está redirecionando toda a saída de log para o painel do Gerenciador de pacotes da janela de saída.  Acreditamos que isso é mais confortável e semelhante a um relatório típico de compilação que você deseja inspecionar.


### <a name="focus-on-performance"></a>Foque no desempenho

Fizemos muitas alterações no nome de melhorar o desempenho de pesquisas do NuGet e buscas.  Essa era nossa preocupação número uma de nossos clientes e, em seguida, queremos ter certeza de que é o abordado nesta versão.  Nós ajustados nossos servidores, criados um novo CDN e melhor a consulta lógica para Esperamos que oferecer a mais relevante de correspondência e resultados de pesquisa mais rápida do pacote.

Resto nesta fase de desenvolvimento do NuGet 3.0, vamos ser ajuste e monitorar o serviço nuget.org para garantir que fornecemos uma experiência aprimorada.  Não planeja participar a qualquer tempo de inatividade, mas será ser adicionando e alterando os recursos no serviço.  Fique atento nosso [feed do twitter](http://twitter.com/nuget) para obter detalhes sobre quando podemos alterar a configuração do serviço.

## <a name="building-nuget-with-nuget"></a>Criando NuGet com o NuGet

Agora podemos ter reprojetado nossos clientes do NuGet em vários componentes que são sendo compilado em pacotes do NuGet. Essa reutilização das nossas próprias bibliotecas força nos criar componentes que são reutilizáveis e que podem ser empacotados corretamente.  Conseguimos eliminar código duplicado e aprendeu a melhor configurar nosso processo de desenvolvimento para oferecer suporte a necessidade de criar pacotes em nossas soluções.  Procure uma postagem de blog em breve onde falaremos sobre como os projetos de código são estruturados e como funciona o nosso processo de compilação.

## <a name="stay-tuned"></a>Fique atento

Fique atento [nosso blog](http://blog.nuget.org) para mais de progresso e avisos do NuGet 3.0!
