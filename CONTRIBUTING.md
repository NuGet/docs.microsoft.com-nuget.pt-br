---
ms.openlocfilehash: 585537c5e3c7b27e0c7c312db19723d952421ce3
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859543"
---
Nenhuma contribuição é muito grande ou muito pequena.

1. Visite a página para editar em [docs.Microsoft.com/NuGet](https://docs.microsoft.com/nuget/)e clique no botão **Editar** no canto superior direito. Isso leva você para a página de redução apropriada no repositório.
1. Edite a redução:
    1. Se você estiver incluindo imagens (use PNGs, geralmente), coloque-as na pasta de mídia que está na pasta do tópico. Os links são então `media/<image_name>.png` .
    1. Os links relativos a outras páginas neste docset devem estar no formato, `../<folder>/<topic-file>.md` incluindo o treinamento `.md` . Se você estiver vinculando a outro tópico na mesma pasta, `../<folder>/` poderá ser omitido. Ao usar âncoras, lembre-se sempre de incluir o `.md` antes de `#` .
    1. Ao usar links externos, especialmente para docs.microsoft.com (ou msdn.microsoft.com para qualquer conteúdo mais antigo), omita qualquer marca de idioma como "en-US" para que um leitor em outro idioma fique em uma página de destino na mesma linguagem, se estiver disponível.
1. Quando terminar, insira uma mensagem de confirmação abaixo e clique em **propor alteração de arquivo**.
1. Envie uma solicitação de pull para sua alteração. Analisamos PRs regularmente.
1. Obrigado!

Se você estiver criando um novo tópico, lembre-se também do seguinte:

1. Sempre coloque o novo tópico em uma subpasta apropriada e siga as convenções para nomes de filecomo você vê-los usados aqui.
1. Você deve incluir um bloco de metadados como você vê em outros tópicos. Os padrões típicos (como para MS. Workload e MS. revisor) são definidos em docs/docjx.jsem, portanto, você precisa alterar apenas o seguinte:

  - Título: o título que aparece nos resultados da pesquisa. Para a SEO, isso ideal não é o mesmo que o # de nível superior (H1) do artigo.
  - Descrição: o resumo do artigo que aparece nos resultados da pesquisa.
  - Autor: a ID do GitHub do autor, para a qual os arquivos de problemas deste artigo são atribuídos.
  - MS. Author: se o autor for um funcionário da Microsoft, esse será o alias da Microsoft. Usado para relatar e encaminhar comentários de outros canais.
  - Gerenciador: alias da Microsoft do gerente do autor, se aplicável.
  - MS. Date: a data da última revisão ou revisão do artigo no formato mm/dd/aaaa (use zeros à esquerda). Essa é uma comunicação com o leitor sobre a atualização, portanto, ela não é atualizada para pequenas alterações, apenas para revisões mais significativas ou quando o artigo é reverificado, mesmo que não haja nenhuma alteração.
  - MS. Topic: usado para categorizar o artigo em relatórios. Consulte a tabela abaixo. A maioria dos artigos é "conceitual". 
1. Além de adicionar sua página, edite docs/TOC. MD para adicionar um link a essa página.
1. Se você estiver adicionando um nó de nível superior ao Sumário, também será feita uma entrada para ele em docs/index. MD.

| Categoria MS. Topic | Description |
| --- | --- |
| conceptual | Use para qualquer conteúdo que não se enquadrar em outro. Isso é definido como o padrão no docfx.jsem. |
| visão geral | Use para qualquer artigo de visão geral ou de guia do usuário, normalmente apenas aqueles que residem em um nó "visão geral" no sumário. |
| TUTORIAIS | Qualquer coisa no nó "início rápido" no sumário que é criado de acordo com as diretrizes de início rápido. |
| tutorial | Qualquer coisa sob o nó "tutorial" no sumário que é criado de acordo com as diretrizes do tutorial. |
| reference | Qualquer artigo de tipo de referência que não seja gerado automaticamente. |
| artigo | Use para conteúdo contribuído pela Comunidade (ou seja, qualquer coisa de fora da equipe de engenharia ou da equipe de docs da Microsoft. |
