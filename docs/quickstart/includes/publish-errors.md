---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496015"
---
Os erros do comando `push` geralmente indicam o problema. Por exemplo, talvez você tenha esquecido de atualizar o número de versão em seu projeto e, portanto, tentar publicar um pacote que já existe.

Você também vê erros quando tenta publicar um pacote usando um identificador que já existe no host. O nome "AppLogger", por exemplo, já existe. Nesse caso, o comando `push` fornece o seguinte erro:

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

Se você estiver usando uma chave de API válida que acabou de criar, essa mensagem indicará um conflito de nome, que não fica totalmente claro na parte "permissão" do erro. Altere o identificador do pacote, recompile o projeto, recrie o arquivo `.nupkg` e tente novamente o comando `push`.