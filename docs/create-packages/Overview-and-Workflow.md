---
title: Visão geral e fluxo de trabalho da criação de pacotes do NuGet
description: Uma visão geral do processo de criar e publicar um pacote do NuGet, com links para outras partes específicas do processo.
author: JonDouglas
ms.author: jodou
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: d34f8e73dce64a58393433637067651fced08173
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774674"
---
# <a name="package-creation-workflow"></a>Fluxo de trabalho de criação de pacote

Criar um pacote começa com o código compilado (normalmente assemblies .NET) que você deseja empacotar e compartilhar com outras pessoas, seja por meio da galeria nuget.org pública ou de uma galeria privada dentro de sua organização. O pacote também pode incluir arquivos adicionais, como um arquivo Leiame que é exibido quando o pacote for instalado e pode incluir as transformações para alguns arquivos de projeto.

Um pacote também pode servir somente para efetuar pull em qualquer número de outras dependências, sem conter qualquer código próprio. Esse tipo de pacote é uma maneira conveniente de entregar um SDK que é composto por vários pacotes independentes. Em outros casos, um pacote pode conter apenas arquivos de símbolos (`.pdb`) para auxiliar na depuração.

> [!Note]
> Quando você cria um pacote para ser usado por outros desenvolvedores, é importante entender que eles estão adotando uma dependência do seu trabalho. Dessa forma, criar e publicar um pacote também implica em um compromisso em corrigir os bugs e fazer outras atualizações ou, pelo menos, disponibilizar o pacote como software livre para que outras pessoas possam ajudar a mantê-lo.

Seja qual for o caso, a criação de um pacote começa com a decisão de seu identificador, número de versão, licença, informações de direitos autorais e qualquer outro conteúdo necessário. Depois de concluído, você pode usar o comando "pack" para colocar tudo em um arquivo `.nupkg`. Esse arquivo pode ser publicado em um feed do NuGet, como nuget.org.

> [!Tip]
> Um pacote do NuGet com a extensão `.nupkg` é simplesmente um arquivo ZIP. Para examinar facilmente qualquer conteúdo de pacote, altere a extensão para `.zip` e expanda seu conteúdo normalmente. Verifique apenas se a extensão foi alterada de volta para `.nupkg` antes de tentar carregá-la para um host.

Para aprender e compreender o processo de criação, inicie com [Criando um pacote](../create-packages/creating-a-package.md) que orienta você por meio dos principais processos comuns a todos os pacotes.

A partir daí, você pode considerar diversas outras opções para seu pacote:

- [Suporte a várias estruturas de destino](../create-packages/supporting-multiple-target-frameworks.md) descreve como criar um pacote com diversas variantes para diferentes versões do .NET Framework.
- [Criando pacotes localizados](../create-packages/creating-localized-packages.md) descreve como estruturar um pacote com vários recursos de linguagem e como usar pacotes satélite localizados separados.
- [Pacotes de pré-lançamento](../create-packages/prerelease-packages.md) demonstra como lançar pacotes de versão alfa, beta e rc para os clientes que estejam interessados.
- [Origem e transformações do arquivo de configuração](../create-packages/source-and-config-file-transformations.md) descreve como você pode fazer as duas substituições de token unidirecionais em arquivos que são adicionados a um projeto e modificam `web.config` e `app.config` com configurações que também são recuperadas quando o pacote é desinstalado.
- [Pacotes de símbolos](../create-packages/symbol-packages-snupkg.md) oferece diretrizes para o fornecimento de símbolos para a biblioteca que permite aos consumidores intervir no seu código durante a depuração.
- [Controle de versão do pacote](../concepts/package-versioning.md) aborda como identificar as versões exatas que você permite para as suas dependências (outros pacotes que você consume do seu pacote).
- [Pacotes nativos](../guides/native-packages.md) descrevem o processo para criar um pacote para os consumidores do C++.
- [Assinando pacotes](../create-packages/sign-a-package.md) descreve o processo para adicionar uma assinatura digital a um pacote.

Quando você estiver pronto para publicar um pacote no nuget.org, siga o processo simples em [Publicar um pacote](../nuget-org/publish-a-package.md).

Se você quiser usar um feed privado em vez do nuget.org, consulte a [Visão geral da hospedagem de pacotes](../hosting-packages/overview.md)
