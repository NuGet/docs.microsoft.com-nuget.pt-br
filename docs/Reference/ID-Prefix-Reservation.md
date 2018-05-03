---
title: Prefixo de ID de referência de reserva
description: Descrição do recurso de reserva de prefixo de ID de pacote e guia do autor.
author: diverdan92
ms.author: diverdan92
manager: unnir
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 63f442ae25b92aacbbf5af7d9b3ea1a5dafe5fc9
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2018
---
# <a name="package-id-prefix-reservation"></a>Reserva de prefixo de ID de pacote

Os proprietários do pacote podem reservar e proteger sua identidade ao reservar prefixos de ID. Os consumidores de pacote são fornecidas com informações adicionais quando o consumo de pacotes que o pacote que estão consumindo não são enganosos em suas propriedades de identifica. 

[NuGet.org](https://www.nuget.org/) e Visual Studio 2017 versão 15.4 ou posterior para mostrar um indicador visual para pacotes que são enviados pelos proprietários com um prefixo de ID de pacote reservado, desde que o pacote coincide com o ID reservado do prefixo padrão de nomenclatura. A seguir referência explica o que implica a reserva de prefixo de ID e como aplicar um proprietário de um prefixo de ID.

## <a name="id-prefix-reservation-details"></a>Detalhes de reserva de prefixo de ID

Quando um prefixo de ID do pacote é reservado, várias coisas acontecem no [nuget.org](https://www.nuget.org/) galeria, bem como no Visual Studio. Além disso, são avançadas cenários que são suportados pelo reservas de prefixo de ID, como definir um prefixo como 'public', delegando subconjuntos de prefixo para vários proprietários.

### <a name="id-prefix-reservation-on-nugetorg"></a>Reserva de prefixo de ID em nuget.org

Quando um prefixo é reservado no [nuget.org](https://www.nuget.org/), acontecerá o seguinte:

1. Uma reserva de prefixo é associada com um proprietário ou o conjunto de proprietários em [nuget.org](https://www.nuget.org/).

1. Sempre que um pacote é enviado para o [nuget.org](https://www.nuget.org/) com uma ID que corresponde ao prefixo de ID reservado, o pacote é rejeitado, a menos que originou o proprietário que reservou o prefixo de ID.

1. Qualquer pacote que coincide com o prefixo reservado da ID e origina-se de que o proprietário que reservou o prefixo de ID terá um indicador visual na versão do Visual Studio de 2017 15.4 ou posterior e em [nuget.org](https://www.nuget.org/) indicando que o pacote está em um prefixo de ID reservado. Isso é verdadeiro para envios de novo pacote, bem como os pacotes existentes sob o proprietário. **Observação:** o indicador no Visual Studio aparece somente se um único feed é selecionado como a origem do pacote.

1. Todos os pacotes existentes que correspondem ao prefixo de ID reservado, mas são *não* pertencem ao proprietário do reservado prefixo permanece inalterado (não será removido da lista, mas ele também não terá o indicador visual). Além disso, os proprietários desses pacotes ainda poderão enviar novas versões para o pacote.

Essas alterações são baseadas nas seguintes condições e impõem várias restrições adicionais:

- Somente um proprietário de um pacote deve ter o prefixo reservado para o indicador visual apareça (para pacotes com vários proprietários).

- Se houver mais de um proprietário de um pacote em que um ou mais proprietários tem o prefixo reservado e um ou mais proprietários não tem o prefixo reservado, somente o proprietário com o prefixo reservado pode remover outros proprietários com um prefixo reservado. Os proprietários que não têm o prefixo reservado não é possível remover os proprietários com o prefixo reservado. Eles ainda podem remover outros proprietários que também não têm o prefixo reservado.

- Depois que um pacote tem o indicador visual, deveria *sempre* tem o indicador visual (garantir que pelo menos um proprietário com o prefixo reservado sempre permanecerá um proprietário)

### <a name="advanced-prefix-reservation-scenarios"></a>Cenários de reserva de prefixo avançadas

Há vários cenários mais avançados de reserva prefixo descritos abaixo, incluindo delegação subprefix e prefixos de marcação como público. Abaixo estão as reservas de prefixo mais avançadas que podem ser feitas. 

- Durante a reserva de prefixo, o proprietário pode solicitar a delegação de subconjuntos de prefixo (ou o prefixo) para outros proprietários. Por exemplo, se '[Microsoft](https://www.nuget.org/profiles/microsoft)' possui ' Microsoft.\*', mas '[aspnet](https://www.nuget.org/profiles/aspnet)' deseja reservar ' Microsoft.AspNet.\*','[Microsoft](https://www.nuget.org/profiles/microsoft)' pode optar por delegar ' Microsoft.AspNet. \*' para o [aspnet](https://www.nuget.org/profiles/aspnet) conta.

- Durante a reserva de prefixo, o proprietário pode optar por publicar um prefixo. Isso ainda fornecerá a eles o indicador visual mostrando que o pacote se origina de um prefixo reservado, mas ele será **não** bloquear envios de pacote futuras no prefixo para qualquer proprietário. Isso é útil para projetos de código aberto com muitos colaboradores - os colaboradores superior ou principal podem ter o prefixo reservado, mas ainda pode ser aberta para todos os colaboradores. 

### <a name="prefix-reservation-visual-indicator"></a>Indicador visual de reserva de prefixo

Quando um pacote é proveniente de um prefixo reservado, você verá o abaixo indicadores visuais no [nuget.org](https://www.nuget.org/) galeria e no Visual Studio 2017 versão 15.4 ou posterior:

**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)

**O Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Processo de aplicativo de reserva de prefixo de ID

1. Examine a aceitação [critérios de reserva de ID de prefixo](#id-prefix-reservation-criteria).

2. Determinar os namespaces que você deseja reservar, além de qualquer [prefixo reserva cenários avançados](#advanced-prefix-reservation-scenarios) talvez seja necessária.

3. Enviar um email para [ account@nuget.org ](mailto:account@nuget.org) com o proprietário do nome para exibição em [nuget.org](https://www.nuget.org/), bem como os prefixos reservados que você está solicitando. Se você estiver delegando subconjuntos de prefixo para proprietários de várias, certifique-se de mencionar todos os nomes de exibição proprietário e subconjuntos de prefixo.

Depois que o aplicativo for enviado, você será notificado de aceitação ou rejeição (com os critérios que causou a rejeição). Pode, precisamos fazer mais perguntas de identifica para confirmar a identidade do proprietário.

### <a name="id-prefix-reservation-criteria"></a>Critérios de reserva de prefixo de ID

Ao revisar qualquer aplicativo de reserva de prefixo de ID, o [nuget.org](https://www.nuget.org/) equipe avaliará o aplicativo em relação a abaixo critérios. Nem todos os critérios precisam ser atendidas para que um prefixo a ser reservado, mas o aplicativo pode ser negado se não houver evidências substancial dos critérios sejam atendidos (com uma explicação fornecida):

1. O prefixo de ID de pacote corretamente e claramente Identifique o proprietário do pacote?

1. Tem um número significativo de pacotes que já tenham sido enviadas pelo proprietário sob o prefixo de ID do pacote?

1. O prefixo de ID do pacote é algo comum que não deve pertencer a nenhum proprietário individual ou organização?

1. Seria *não* reservar o prefixo de ID de pacote causar ambiguidade e confusão para a comunidade?

1. São as propriedades de identifica dos pacotes que correspondem ao pacote ID prefixo claro e consistente (especialmente o autor do pacote)?

## <a name="third-party-feed-provider-scenarios"></a>Cenários de provedor de feed de terceiros

Se um provedor de feed de terceiros está interessado em implementar seu próprio serviço para fornecer reservas de prefixo, poderá fazê-lo ao modificar o serviço de pesquisa no NuGet V3 feed provedores. A adição no serviço de pesquisa de feed é adicionar a *verificado* propriedade, com exemplos para os feeds V3 abaixo. O cliente do NuGet não dará suporte a propriedade adicionada no feed V2.

Para obter mais informações, consulte o [documentação sobre o serviço de pesquisa da API](../api/search-query-service-resource.md).
