---
title: Referência de reserva de prefixo de ID
description: Descrição do recurso de reserva de prefixo de ID de pacote e guia do autor.
author: diverdan92
ms.author: diverdan92
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 32f83bede42f7643a9a4fed593643eefea0453c1
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2018
ms.locfileid: "50980996"
---
# <a name="package-id-prefix-reservation"></a>Reserva de prefixo de ID de pacote

Os proprietários de pacote podem reservar e proteger sua identidade ao reservar prefixos de ID. Os consumidores de pacote são fornecidos com informações adicionais quando o consumo de pacotes que o pacote que estão sendo consumidos não são enganosos em suas propriedades de identifica. 

[NuGet.org](https://www.nuget.org/) e Visual Studio 2017 versão 15.4 ou posterior para mostrar um indicador visual para o padrão de nomenclatura de prefixo de pacotes que são enviados por proprietários com um prefixo de ID de pacote reservado, desde que o pacote corresponde à ID reservado. O abaixo fazem referência explica o que envolve a reserva de prefixo de ID, e como um proprietário pode aplicar para um prefixo de ID.

## <a name="id-prefix-reservation-details"></a>Detalhes de reserva de prefixo de ID

Quando um prefixo de ID do pacote é reservado, várias coisas acontecem na [nuget.org](https://www.nuget.org/) galeria, bem como no Visual Studio. Além disso, existem avançados cenários que são compatíveis com as reservas de prefixo de ID, como a configuração de um prefixo como 'public', delegando subconjuntos de prefixo para vários proprietários.

### <a name="id-prefix-reservation-on-nugetorg"></a>Reserva de prefixo de ID em nuget.org

Quando um prefixo é reservado [nuget.org](https://www.nuget.org/), acontecerá o seguinte:

1. Uma reserva de prefixo é associada com um proprietário ou o conjunto de proprietários na [nuget.org](https://www.nuget.org/).

1. Sempre que um pacote é enviado para o [nuget.org](https://www.nuget.org/) com uma ID que corresponde ao prefixo de ID reservado, o pacote é rejeitado, a menos que originou o proprietário que reservou o prefixo de ID.

1. Qualquer pacote que corresponde ao prefixo de ID reservado e o proprietário que o prefixo de ID de reservado é proveniente terá um indicador visual no Visual Studio 2017 versão 15.4 ou posterior e no [nuget.org](https://www.nuget.org/) indicando que o pacote está em um prefixo de ID reservado. Isso é verdadeiro para novos envios de pacote, bem como os pacotes existentes sob o proprietário. **Observação:** o indicador no Visual Studio é exibida somente se um único feed é selecionado como a origem do pacote.

1. Todos os pacotes existentes anteriormente que corresponde ao prefixo de ID reservado, mas são *não* pertencem ao proprietário do reservado prefixo permanecerá inalterado (não será removido da lista, mas eles também terão o indicador visual não). Além disso, os proprietários desses pacotes ainda poderão enviar novas versões para o pacote.

Essas alterações se baseiam nas seguintes condições e impõem várias restrições adicionais:

- Somente um proprietário de um pacote precisa ter o prefixo reservado para o indicador visual aparecerá (para pacotes com vários proprietários).

- Se houver mais de um proprietário de um pacote em que um ou mais proprietários tem o prefixo reservado e um ou mais proprietários não tem o prefixo reservado, somente o proprietário com o prefixo reservado pode remover outros proprietários com um prefixo reservado. Os proprietários que não têm o prefixo reservado não é possível remover os proprietários com o prefixo reservado. Eles ainda podem remover outros proprietários que também não têm o prefixo reservado.

- Depois que um pacote tiver o indicador visual, deveria *sempre* têm o indicador visual (garantir que pelo menos um proprietário com o prefixo reservado sempre permanecerá um proprietário)

### <a name="advanced-prefix-reservation-scenarios"></a>Cenários de reserva de prefixo avançada

Há vários cenários de reserva de prefixo mais avançados descritos abaixo, incluindo delegação subprefix e prefixos de marcação como público. Abaixo estão as reservas de prefixo mais avançadas que podem ser feitas. 

- Durante a reserva de prefixo, o proprietário pode solicitar a delegação de subconjuntos de prefixo (ou o prefixo) para outros proprietários. Por exemplo, se '[Microsoft](https://www.nuget.org/profiles/microsoft)' possui ' Microsoft.\*', mas '[aspnet](https://www.nuget.org/profiles/aspnet)' deseja reservar ' Microsoft.AspNet.\*','[Microsoft](https://www.nuget.org/profiles/microsoft)' can optar por delegar ' Microsoft.AspNet. \*' para o [aspnet](https://www.nuget.org/profiles/aspnet) conta.

- Durante a reserva de prefixo, o proprietário pode optar por tornar um prefixo público. Isso ainda fornecerá a eles o indicador visual que mostra que o pacote é proveniente de um prefixo reservado, mas ele será **não** bloquear envios de futuras do pacote no prefixo para qualquer proprietário. Isso é útil para projetos de software livre com muitos colaboradores – os colaboradores da parte superior ou core podem ter o prefixo reservado, mas ainda pode ser aberto para todos os colaboradores. 

### <a name="prefix-reservation-visual-indicator"></a>Indicador visual de reserva de prefixo

Quando um pacote é proveniente de um prefixo reservado, você verá o abaixo de indicadores visuais sobre o [nuget.org](https://www.nuget.org/) galeria e no Visual Studio 2017 versão 15.4 ou posterior:

**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Processo de aplicativo de reserva de prefixo de ID

1. Examine a aceitação [critérios para a reserva de ID de prefixo](#id-prefix-reservation-criteria).

2. Determinar os prefixos que você deseja reservar, além de quaisquer [cenários de reserva de prefixo avançados](#advanced-prefix-reservation-scenarios) talvez seja necessária.

3. Enviar um email para [ account@nuget.org ](mailto:account@nuget.org) com o proprietário do nome de exibição no [nuget.org](https://www.nuget.org/), bem como os prefixos reservados que você está solicitando. Se você estiver delegando subconjuntos de prefixo para vários proprietários, verifique se você menciona todos os nomes de exibição do proprietário e subconjuntos de prefixo.

Depois que o aplicativo é enviado, você será notificado de aceitação ou a rejeição (com os critérios que causou a rejeição). Talvez seja necessário fazer perguntas adicionais de identifica para confirmar a identidade do proprietário.

### <a name="id-prefix-reservation-criteria"></a>Critérios de reserva de prefixo de ID

Ao revisar qualquer aplicativo de reserva de prefixo de ID, o [nuget.org](https://www.nuget.org/) equipe avaliará o aplicativo contra os critérios abaixo. Nem todos os critérios precisam ser atendidas para que um prefixo a ser reservado, mas o aplicativo pode ser negado se não houver evidências substancial dos critérios que estão sendo atendidos (com uma explicação dada):

1. O prefixo de ID de pacote corretamente e claramente identifica o proprietário do pacote?

1. Tem um número significativo de pacotes que já foram enviados pelo proprietário sob o prefixo de ID do pacote?

1. O prefixo de ID do pacote é algo comum que não deve pertencer a nenhum proprietário individual ou organização?

1. Seria *não* reservar o prefixo de ID de pacote causar ambiguidade e confusão para a comunidade?

1. São as propriedades de identifica dos pacotes que correspondem ao pacote ID prefixo claro e consistente (especialmente o autor do pacote)?

## <a name="third-party-feed-provider-scenarios"></a>Cenários do provedor de feed de terceiros

Se um provedor de feed de terceiros está interessado em implementar seus próprios serviços para fornecer as reservas de prefixo, poderá fazê-lo, modificando o serviço de pesquisa no NuGet V3 feed provedores. A adição no serviço de pesquisa de feed é adicionar o *verificado* propriedade, com exemplos para os feeds V3 abaixo. O cliente do NuGet não dará suporte a propriedade adicionada no feed V2.

Para obter mais informações, consulte o [documentação sobre o serviço de pesquisa da API](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Política de controvérsia de reserva de prefixo de ID de pacote
Se você acredita que um proprietário na [NuGet.org](https://www.nuget.org) foi atribuído a uma reserva de prefixo de ID de pacote que vai contra os critérios listados acima, ou infringe em marcas comerciais ou de direitos autorais, por favor, email [ support@nuget.org ](mailto:support@nuget.org)com o prefixo de ID em questão, o proprietário do prefixo de ID e o motivo para discutir a reserva de prefixo atribuído.

