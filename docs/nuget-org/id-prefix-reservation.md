---
title: Reserva de prefixo da ID
description: Guia do autor e descrição do recurso Reserva de prefixo da ID do pacote.
author: JonDouglas
ms.author: jodou
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: 428fd3d7b324f6eb825b17e4a87a662fbd84a2f0
ms.sourcegitcommit: af059dc776cfdcbad20baab2919b5d6dc1e9022d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2021
ms.locfileid: "99990104"
---
# <a name="package-id-prefix-reservation"></a>Reserva de prefixo da ID do pacote

Os proprietários de pacotes podem reservar e proteger suas identidades reservando prefixos da ID. Os consumidores de pacote são fornecidos com informações adicionais quando os pacotes que estão consumindo não são enganosos em suas propriedades de identificação. 

O [nuget.org](https://www.nuget.org/) e o Visual Studio 2017 versão 15.4 ou posterior mostram um indicador visual para os pacotes que são enviados por proprietários com um prefixo reservado da ID do pacote, desde que o pacote corresponda ao padrão de nomenclatura de prefixo reservado da ID. A referência abaixo explica o que envolve a reserva de prefixo da ID e como um proprietário pode solicitar um prefixo da ID.

## <a name="id-prefix-reservation-details"></a>Detalhes sobre a reserva de prefixo da ID

Quando um prefixo da ID do pacote é reservado, várias coisas acontecem na galeria do [nuget.org](https://www.nuget.org/), bem como no Visual Studio. Além disso, existem cenários avançados que são compatíveis com as reservas de prefixo da ID, como a configuração de um prefixo como 'público' e a delegação de subconjuntos de prefixos a vários proprietários.

### <a name="id-prefix-reservation-on-nugetorg"></a>Reserva de prefixo da ID no nuget.org

Quando um prefixo for reservado no [nuget.org](https://www.nuget.org/), acontecerá o seguinte:

1. Uma reserva de prefixo será associada a um proprietário ou um conjunto de proprietários no [nuget.org](https://www.nuget.org/).

1. Sempre que um pacote for enviado ao [nuget.org](https://www.nuget.org/) com uma ID que corresponda ao prefixo reservado da ID, o pacote será rejeitado, a menos que seja proveniente dos proprietários que reservaram o prefixo da ID.

1. Qualquer pacote que corresponda ao prefixo reservado da ID e que seja proveniente dos proprietários que reservaram o prefixo da ID terá um indicador visual no Visual Studio 2017 versão 15.4 ou posterior e no [nuget.org](https://www.nuget.org/), indicando que o pacote contém um prefixo reservado da ID. Esse é o caso de envios de novos pacotes, bem como os pacotes existentes dos proprietários. **Observação:** O indicador no Visual Studio será exibido somente se um único feed for selecionado como a origem do pacote.

1. Todos os pacotes anteriormente existentes que correspondem ao prefixo reservado da ID, mas que *não* pertencem ao proprietário do prefixo reservado, permanecerão inalterados (eles não serão removidos da lista, mas também não terão o indicador visual). Além disso, os proprietários desses pacotes ainda poderão enviar novas versões ao pacote.

Essas alterações se baseiam nas seguintes condições e impõem várias restrições adicionais:

- Somente um proprietário de um pacote precisa ter o prefixo reservado para que o indicador visual seja exibido (para pacotes com vários proprietários).

- Se houver mais de um proprietário de um pacote, em que um ou mais proprietários tenham o prefixo reservado e um ou mais proprietários não tenham o prefixo reservado, somente os proprietários com o prefixo reservado poderão remover outros proprietários com um prefixo reservado. Os proprietários que não têm o prefixo reservado não podem remover proprietários com o prefixo reservado. Eles ainda podem remover outros proprietários que também não têm o prefixo reservado.

- Depois que um pacote tiver o indicador visual, ele *sempre* deverá ter o indicador visual (garantindo que, pelo menos, um proprietário com o prefixo reservado sempre permaneça um proprietário)

### <a name="advanced-prefix-reservation-scenarios"></a>Cenários avançados de reserva de prefixo

Há vários cenários mais avançados de reserva de prefixo descritos abaixo, incluindo delegação de subprefixo e marcação de prefixos como públicos. Veja abaixo as reservas de prefixo mais avançadas que podem ser feitas. 

- Durante a reserva de prefixo, o proprietário pode solicitar a delegação de subconjuntos de prefixos (ou do prefixo) a outros proprietários. Por exemplo, se '[Microsoft](https://www.nuget.org/profiles/microsoft)' é o proprietário de 'Microsoft.\*', mas '[aspnet](https://www.nuget.org/profiles/aspnet)' deseja reservar 'Microsoft.AspNet.\*', '[Microsoft](https://www.nuget.org/profiles/microsoft)' pode optar por delegar 'Microsoft.AspNet.\*' à conta de [aspnet](https://www.nuget.org/profiles/aspnet).

- Durante a reserva de prefixo, o proprietário pode optar por tornar um prefixo público. Isso ainda fornecerá a ele o indicador visual, mostrando que o pacote é proveniente de um prefixo reservado, mas **não** bloqueará envios de pacotes futuros no prefixo para qualquer proprietário. Isso é útil para projetos de software livre com muitos colaboradores – os principais colaboradores podem ter o prefixo reservado, mas ele ainda poderá estar aberto para todos os colaboradores. 

### <a name="prefix-reservation-visual-indicator"></a>Indicador visual de reserva de prefixo

Quando um pacote for proveniente de um prefixo reservado, você verá os indicadores visuais abaixo na galeria do [nuget.org](https://www.nuget.org/) e no Visual Studio 2017 versão 15.4 ou posterior:

 
 Galeria ![ de NuGet.org Galeria de nuget.org](media/nuget-gallery-reserved-prefix.png)

**Visual Studio** 
 ![ Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Processo de solicitação de reserva de prefixo da ID

1. Examine os [critérios de aceitação para a reserva de prefixo da ID](#id-prefix-reservation-criteria).

2. Determine os prefixos que deseja reservar, além dos [cenários avançados de reserva de prefixo](#advanced-prefix-reservation-scenarios) que possam ser necessários.

3. Envie um email para [account@nuget.org](mailto:account@nuget.org) com o nome de exibição do proprietário em [NuGet.org](https://www.nuget.org/), bem como quaisquer prefixos reservados que você esteja solicitando. Se estiver delegando subconjuntos de prefixos a vários proprietários, mencione todos os nomes de exibição dos proprietários e os subconjuntos de prefixos.

Após o envio da solicitação, você será notificado da aceitação ou da rejeição (com os critérios que causaram a rejeição). Talvez seja necessário fazer outras perguntas de identificação para confirmar a identidade do proprietário.

### <a name="id-prefix-reservation-criteria"></a>Critérios para a reserva de prefixo da ID

Ao examinar qualquer aplicativo para a reserva de prefixo de ID, a equipe [NuGet.org](https://www.nuget.org) avaliará o aplicativo em relação aos critérios abaixo. Observe que nem todos os critérios precisam ser atendidos para que um prefixo seja reservado, mas o aplicativo poderá ser negado se não houver evidências substanciais sobre os critérios que estão sendo atendidos (com uma explicação fornecida):

1. O prefixo da ID do pacote é apropriado e identifica claramente o proprietário da reserva?

1. O proprietário [habilitou o 2FA para sua conta do NuGet.org](individual-accounts.md#enable-two-factor-authentication-2fa)?

1. O prefixo da ID do pacote é algo comum que não deve pertencer a nenhum proprietário individual ou nenhuma organização?

1. *Não* reservaria o prefixo da ID do pacote causa ambigüidade, confusão ou outros danos à Comunidade?

Ao publicar pacotes para NuGet.org em sua reserva de prefixo de ID, as seguintes práticas recomendadas devem ser consideradas:

1. As propriedades de identificação dos pacotes que correspondem ao prefixo da ID do pacote são claras e consistentes (especialmente o autor do pacote)?

1. Os pacotes têm uma licença (que usa o elemento de metadados [license](../reference/nuspec.md#license) e NÃO licenseUrl, que está sendo preterido)?

1. Se os pacotes tiverem um ícone (usando o elemento de metadados iconUrl), eles também estão usando o elemento de metadados [Icon](../reference/nuspec.md#icon) ? Não é necessário remover os iconUrl, mas os ícones inseridos devem ser usados.
 
Considere a análise do [Guia de práticas recomendadas de criação de pacote](../create-packages/package-authoring-best-practices.md) completo, além dos pontos acima.

## <a name="third-party-feed-provider-scenarios"></a>Cenários de provedor de feed de terceiros

Se um provedor de feed de terceiros estiver interessado em implementar seu próprio serviço para fornecer reservas de prefixo, ele poderá fazer isso modificando o serviço de pesquisa nos provedores de feeds do NuGet v3. A alteração no serviço de pesquisa de feed é adicionar a `verified` propriedade. O cliente do NuGet não dará suporte à propriedade adicionada no feed da V2.

Para obter mais informações, confira a [documentação sobre o serviço de pesquisa da API](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Política de controvérsias referentes à reserva de prefixo da ID do pacote
Se você acredita que um proprietário no [NuGet.org](https://www.nuget.org) recebeu uma reserva de prefixo da ID do pacote que vá contra os critérios listados acima ou que viole marcas ou direitos autorais, envie um email para [support@nuget.org](mailto:support@nuget.org) com o prefixo da ID em questão, o proprietário do prefixo da ID e o motivo da controvérsia referente à reserva de prefixo atribuída.

