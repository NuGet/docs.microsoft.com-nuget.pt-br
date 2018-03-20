---
title: "Visão geral e fluxo de trabalho da criação de pacotes do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Uma visão geral do processo de criar e publicar um pacote do NuGet, com links para outras partes específicas do processo."
keywords: "Criação de pacotes do NuGet, visão geral de criação do NuGet, fluxo de trabalho de criação do NuGet, fluxo de trabalho de criação de pacote, visão geral de criação de pacote."
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 84587ad1f511416cc03b6fee153d1df44d0e7aa7
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="package-creation-workflow"></a>Fluxo de trabalho de criação de pacote

Criar um pacote começa com o código compilado (normalmente assemblies .NET) que você deseja empacotar e compartilhar com outras pessoas, seja por meio da galeria nuget.org pública ou de uma galeria privada dentro de sua organização. O pacote também pode incluir arquivos adicionais, como um arquivo Leiame que é exibido quando o pacote for instalado e pode incluir as transformações para alguns arquivos de projeto.

Um pacote também pode servir somente para efetuar pull em qualquer número de outras dependências, sem conter qualquer código próprio. Esse tipo de pacote é uma maneira conveniente de entregar um SDK que é composto por vários pacotes independentes. Em outros casos, um pacote pode conter apenas arquivos de símbolos (`.pdb`) para auxiliar na depuração.

> [!Note]
> Quando você cria um pacote para ser usado por outros desenvolvedores, é importante entender que eles estão adotando uma dependência do seu trabalho. Dessa forma, criar e publicar um pacote também implica em um compromisso em corrigir os bugs e fazer outras atualizações ou, pelo menos, disponibilizar o pacote como software livre para que outras pessoas possam ajudar a mantê-lo.

Seja qual for o caso, criar um pacote começa com a decisão de quais assemblies e outros arquivos são empacotados. Crie um arquivo de manifesto, conhecido como um arquivo `.nuspec`, para descrever o conteúdo do pacote juntamente com o identificador, o número de versão, as informações de direitos autorais, os arquivos de propriedades e de destinos do MSBuild e muito mais.

Quando você tiver preparado todos os arquivos necessários nas pastas apropriadas e tiver criado o arquivo `.nuspec` apropriado, use o comando `nuget pack` (ou o [pack target do MSBuild](../reference/msbuild-targets.md)) para juntar tudo em um arquivo `.nupkg`. Agora, você está pronto para implantar o pacote em qualquer host e torná-lo disponível para outros desenvolvedores.

> [!Tip]
> Um pacote do NuGet com a extensão `.nupkg` é simplesmente um arquivo ZIP. Para examinar facilmente qualquer conteúdo de pacote, altere a extensão para `.zip` e expanda seu conteúdo normalmente. Verifique apenas se a extensão foi alterada de volta para `.nupkg` antes de tentar carregá-la para um host.

Para aprender e compreender o processo de criação, inicie com [Criando um pacote](../create-packages/creating-a-package.md) que orienta você por meio dos principais processos comuns a todos os pacotes.

A partir daí, você pode considerar diversas outras opções para seu pacote:

- [Suporte a várias estruturas de destino](../create-packages/supporting-multiple-target-frameworks.md) descreve como criar um pacote com diversas variantes para diferentes versões do .NET Framework.
- [Criando pacotes localizados](../create-packages/creating-localized-packages.md) descreve como estruturar um pacote com vários recursos de linguagem e como usar pacotes satélite localizados separados.
- [Pacotes de pré-lançamento](../create-packages/prerelease-packages.md) demonstra como lançar pacotes de versão alfa, beta e rc para os clientes que estejam interessados.
- [Origem e transformações do arquivo de configuração](../create-packages/source-and-config-file-transformations.md) descreve como você pode fazer as duas substituições de token unidirecionais em arquivos que são adicionados a um projeto e modificam `web.config` e `app.config` com configurações que também são recuperadas quando o pacote é desinstalado.
- [Pacotes de símbolos](../create-packages/symbol-packages.md) oferece diretrizes para o fornecimento de símbolos para a biblioteca que permite aos consumidores intervir no seu código durante a depuração.
- [Controle de versão do pacote](../reference/package-versioning.md) aborda como identificar as versões exatas que você permite para as suas dependências (outros pacotes que você consume do seu pacote).
- [Pacotes nativos](../create-packages/native-packages.md) descrevem o processo para criar um pacote para os consumidores do C++.
- [Assinando pacotes](../create-packages/sign-a-package.md) descreve o processo para adicionar uma assinatura digital a um pacote.

Quando você estiver pronto para publicar um pacote no nuget.org, siga o processo simples em [Publicar um pacote](../create-packages/publish-a-package.md).

Se você quiser usar um feed privado em vez do nuget.org, consulte a [Visão geral da hospedagem de pacotes](../hosting-packages/overview.md)
