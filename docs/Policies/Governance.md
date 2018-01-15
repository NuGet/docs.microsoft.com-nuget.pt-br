---
title: "Governança de Projeto NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 94c088ce-ec96-4876-a210-fbdae743942c
description: "O modelo de governança para o NuGet, inclusive funções e responsabilidades de confirmadores, colaboradores e usuários."
keywords: "Governança do NuGet, ditador benevolente do NuGet, responsabilidades de confirmador, responsabilidades de colaborador, responsabilidades de usuário"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0437b7d41f965da6a7ad44a7d0675916ed655fe1
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-governance"></a>Governança do NuGet

> Este documento baseia-se no [Modelo de Governança de Ditador Benevolente](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) da Universidade de Oxford. Ele é licenciado pela [Creative Commons Attribution-ShareAlike 2.0 UK: licença da Inglaterra e País de Gales](http://creativecommons.org/licenses/by-sa/2.0/uk/).

O projeto NuGet é administrado por um Ditador Benevolente e gerenciado pela comunidade. Ou seja, a comunidade contribui ativamente para a manutenção diária do projeto, mas a linha estratégica geral é comandada pelo ditador benevolente. Em caso de divergência, o ditador benevolente tem a palavra final.

A função do ditador benevolente é solucionar controvérsias na comunidade e verificar se o projeto é capaz de prosseguir de maneira coordenada. Por sua vez, a função da comunidade é guiar as decisões do ditador benevolente por meio de envolvimento e contribuição ativas.

## <a name="roles-and-responsibilities"></a>Funções e responsabilidades

Quatro funções são descritas aqui: Ditador benevolente, Confirmadores, Colaboradores e Usuários.

### <a name="benevolent-dictator"></a>Ditador benevolente

A equipe principal do NuGet é assume o papel de Ditador benevolente ou líder de projeto. No entanto, como a comunidade sempre tem a capacidade de criar fork, a equipe está totalmente sujeita à comunidade. É esperado que o líder de projeto entenda a comunidade como um todo e busque satisfazer as muitas necessidades conflitantes da melhor forma possível, garantindo a sobrevivência do projeto a longo prazo.

Em muitos aspectos, a função de ditador benevolente requer menos ditadura e mais diplomacia. O principal é garantir que, à medida que o projeto se expande, as pessoas corretas tenham influência sobre ele e a comunidade apoie a visão do líder de projeto. A função do líder é garantir que os confirmadores (veja abaixo) tomem as decisões corretas em nome do projeto. Em termos gerais, desde que os confirmadores estejam alinhados com a estratégia do projeto, o líder de projeto permitirá que eles prossigam como desejado.

Além disso, a equipe do .NET Foundation considera o líder de projeto como o ponto de contato primário do NuGet para fins de operações de negócios, incluindo registros de domínio e serviços técnicos (por exemplo, assinatura de código).

### <a name="committers"></a>Confirmadores

Confirmadores são colaboradores que contribuíram de forma frequente e valiosa com o NuGet e são indicados pelo Ditador benevolente. Depois de indicados, a função dos confirmadores inclui escrever código diretamente para o repositório e fazer a triagem das contribuições de outras pessoas. Confirmadores geralmente são desenvolvedores, mas podem contribuir de outras maneiras.

Normalmente, um confirmador concentra-se em um aspecto específico do projeto e oferece um nível de conhecimento e compreensão que concede a ele o respeito da comunidade e do líder de projeto. A função de confirmador não é oficial, esta é simplesmente uma função que membros influentes da comunidade assumem quando o líder de projeto os consulta em busca de orientações e suporte.

Confirmadores não têm nenhuma autoridade quanto à direção geral do NuGet. No entanto, eles têm a atenção do líder de projeto. É função do confirmador garantir que o líder esteja ciente das necessidades e objetivos coletivos da comunidade, bem como ajudar a desenvolver ou extrair contribuições apropriadas para o projeto. Geralmente, confirmadores recebem controle informal sobre suas áreas específicas de responsabilidade e recebem direitos para modificar diretamente determinadas áreas do código-fonte. Ou seja, embora confirmadores não tenham autoridade explícita para tomar decisões, eles geralmente descobrirão que suas ações são equivalentes às decisões tomadas pelo líder.

### <a name="contributors"></a>Colaboradores

Colaboradores são membros da comunidade que enviam patches para o NuGet. Esses patches podem ser uma ocorrência única ou ocorrer ao longo do tempo. É esperado que os colaboradores enviem primeiramente patches pequenos que vão crescendo à medida que o colaborador, os confirmadores e o líder do projeto confiam na qualidade dos patches do colaborador. Colaboradores são reconhecidos no documento de notas de versão do produto associado.

Antes do primeiro patch de um colaborador ser colocado no repositório, eles precisam assinar um [Contrato de Licença de Colaborador](http://en.wikipedia.org/wiki/Contributor_License_Agreement) ou um contrato de atribuição com o .NET Foundation. O patch pode ser enviado e discutido, mas não poderá ser realmente confirmado no repositório sem a devida documentação em vigor. Para obter um contrato de licença de colaborador, envie uma solicitação por email para [contributions@nuget.org](mailto:contributions@nuget.org).

Para se tornar um colaborador, envie uma solicitação de pull para um dos seguintes repositórios:

- [Cliente do NuGet](https://github.com/NuGet/NuGet.Client)
- [Galeria do NuGet](https://github.com/nuget/nugetgallery)
- [NuGet Docs](https://github.com/nuget/nugetdocs)

O processo detalhado para enviar uma solicitação de pull varia de acordo com o repositório:

- [Instruções de contribuição para o Cliente do NuGet e Galeria do NuGet](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [Instruções de contribuição para o NuGet Docs](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Usuários

Os usuários são membros da comunidade que precisam e utilizam o NuGet, como os consumidores de pacote e/ou autores. Os usuários são os membros mais importantes da comunidade: sem eles, o projeto não teria nenhuma finalidade. Qualquer pessoa pode ser um usuário; não há requisitos específicos.

Os usuários devem ser incentivados a participar da vida útil do NuGet e da comunidade tanto quanto possível. As contribuições dos usuários permitem que a equipe de projeto garanta que as necessidades desses usuários estão sendo atendidas. Atividades de usuário comuns incluem, sem limitação, o seguinte:

- Defender o uso do projeto
- Informar desenvolvedores do projeto sobre os pontos fortes e fracos do projeto da perspectiva de um novo usuário
- Oferecer apoio moral (agradecimentos são muito valiosos)
- Elaborar documentação e tutoriais
- Enviar relatórios de bugs e solicitações de recursos
- Participar em eventos da comunidade, como buscas de bugs
- Participar de fóruns de discussão

Usuários que continuam a se envolver com o projeto e sua comunidade geralmente se tornam cada vez mais envolvidos. Dessa forma, esses usuários podem se tornar colaboradores, conforme descrito acima.

## <a name="package-succession-under-special-circumstances"></a>Sucessão de pacote em circunstâncias especiais
Em situações infelizes como quando o titular de uma conta do NuGet fica incapacitado ou vez a falecer, trabalharemos junto à comunidade para adicionar os proprietários adequados ao pacote se tal conta retinha a propriedade exclusiva e o pacote foi publicado sob uma [licença OSI aprovada](https://opensource.org/licenses/alphabetical). Para solicitar a propriedade, você precisará enviar os seguintes documentos para nós:

1.  Uma cópia de um documento de identificação governamental com foto.
2.  Um dos seguintes documentos provando status do titular anterior da conta: 
    - Uma certidão de óbito oficial emitido por um órgão governamental caso o titular anterior da conta tenha falecido ou
    - Um documento certificado como um certificado assinado por um médico encarregado pelo tratamento do titular da conta incapacitado.
3.  Um dos seguintes documentos provando seu direito de propriedade: 
    - Certificado de casamento mostrando que você é o cônjuge sobrevivente do titular da conta,
    - Uma procuração assinada,
    - Cópia de um testamento ou documento similar nomeando você como executor ou beneficiário,
    - Certificado de nascimento do titular da conta, se você for um dos pais ou
    - Documentação de tutela legal se você for o tutor legal do titular da conta.
    
Se você precisa invocar essa política, envie um email para [support@nuget.org](mailto:support@nuget.org) com a ID e a versão do pacote.
    
## <a name="transparency"></a>Transparência

Ganhar a confiança da comunidade na governança de um projeto de software livre é essencial para o sucesso. Por isso, as decisões devem ser tomadas de maneira honestas e transparentes. A discussão sobre a direção do projeto deve ser pública. A comunidade nunca deve ser pega de surpresa por uma decisão do Ditador benevolente. Além disso, a discussão sobre decisões do projeto devem ser arquivadas para que os membros da comunidade entendam todo o histórico de uma decisão e seu contexto.
