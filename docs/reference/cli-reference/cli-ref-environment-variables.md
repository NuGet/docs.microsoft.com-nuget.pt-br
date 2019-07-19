---
title: Variáveis de ambiente da CLI do NuGet
description: Referência para as variáveis de ambiente NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b04efaecce1d5bc892dfc48ae3e872d80aad209d
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327823"
---
# <a name="nuget-cli-environment-variables"></a>Variáveis de ambiente da CLI do NuGet

O comportamento da CLI do NuGet. exe pode ser configurado por meio de várias variáveis de ambiente, que afetam o NuGet. exe nos níveis de todo o computador, usuário ou processo. Variáveis de ambiente sempre substituem quaisquer `NuGet.Config` configurações em arquivos, permitindo que os servidores de compilação alterem as configurações apropriadas sem modificar nenhum arquivo.

Em geral, as opções especificadas diretamente na linha de comando ou nos arquivos de configuração do NuGet têm precedência, mas há algumas exceções, como *FORCE_NUGET_EXE_INTERACTIVE*. Se você descobrir que o NuGet. exe se comporta de forma diferente entre computadores diferentes, uma variável de ambiente poderá ser a causa. Por exemplo, os aplicativos Web do Azure kudu (usados durante a implantação) têm *NUGET_XMLDOC_MODE* definido como *ignorar* para acelerar o desempenho da restauração do pacote e economizar espaço em disco.

A CLI do NuGet usa o MSBuild para ler os arquivos do projeto. Todas as variáveis de ambiente estão disponíveis como [Propriedades](/visualstudio/msbuild/msbuild-command-line-reference) durante a avaliação do MSBuild.
A lista de propriedades documentadas em [NuGet Pack e restaurar como destinos do MSBuild](../msbuild-targets.md#restore-properties) também pode ser definida como variáveis de ambiente.

| Variável | Descrição | Comentários |
| --- | --- | --- |
| http_proxy | Proxy HTTP usado para operações HTTP do NuGet. | Isso seria especificado como `http://<username>:<password>@proxy.com`. |
| no_proxy | Configura os domínios para bypass do uso do proxy. | Especificado como domínios separados por vírgula (,). |
| EnableNuGetPackageRestore | Sinalizador para se o NuGet deve conceder autorização implicitamente, caso isso seja exigido pelo pacote na restauração. | O sinalizador especificado é tratado como *verdadeiro* ou *1*, qualquer outro valor tratado como sinalizador não definido. |
| NUGET_EXE_NO_PROMPT | Impede o exe para solicitar credenciais. | Qualquer valor, exceto nulo ou cadeia de caracteres vazia, será tratado como esse sinalizador definido/verdadeiro. |
| FORCE_NUGET_EXE_INTERACTIVE | Variável de ambiente global para forçar o modo interativo. | Qualquer valor, exceto nulo ou cadeia de caracteres vazia, será tratado como esse sinalizador definido/verdadeiro. |
| NUGET_PACKAGES | Caminho a ser usado para a pasta *global-Packages* , conforme descrito em [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). | Especificado como caminho absoluto. |
| NUGET_FALLBACK_PACKAGES | Pastas de pacotes de fallback globais. | Caminhos de pasta absolutos separados por ponto e vírgula (;). |
| NUGET_HTTP_CACHE_PATH | Caminho a ser usado para a pasta *http-cache* , conforme descrito em [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). | Especificado como caminho absoluto. |
| NUGET_PERSIST_DG | Sinalizador que indica se os arquivos DG (dados coletados do MSBuild) devem ser persistidos. | Especificado como *verdadeiro* ou *falso* (padrão), se NUGET_PERSIST_DG_PATH não estiver definido, será armazenado no diretório temporário (pasta NuGetScratch no diretório temporário do ambiente atual). |
| NUGET_PERSIST_DG_PATH | Caminho para persistir arquivos DG. | Especificado como caminho absoluto, essa opção só é usada quando *NUGET_PERSIST_DG* é definido como true. |
| NUGET_RESTORE_MSBUILD_ARGS | Define argumentos adicionais do MSBuild. | Passe argumentos idênticos a como você os passaria para MSBuild. exe. Um exemplo de configuração de uma propriedade de projeto foo da linha de comando para a barra de valores seria/p: foo = bar |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Define o detalhamento do log do MSBuild. | O padrão é *Quiet* ("/v: q"). Os valores possíveis *q [uiet]* , *m [ínimo]* , *n [ormal]* , *d [ethados]* e *diag [nóstico]* . |
| NUGET_SHOW_STACK | Determina se a exceção completa (incluindo rastreamento de pilha) deve ser exibida para o usuário. | Especificado como *true* ou *false* (padrão). |
| NUGET_XMLDOC_MODE | Determina como a extração de arquivo de documentação XML de assemblies deve ser manipulada. | Os modos com suporte são *Skip* (não extraem arquivos de documentação XML), *compactar* (armazenar arquivos de documentos XML como um arquivo zip) ou *nenhum* (padrão, tratar arquivos de documento XML como arquivos regulares). |
| NUGET_CERT_REVOCATION_MODE | Determina como a verificação de status de revogação do certificado usado para assinar um pacote é executada quando um pacote assinado é instalado ou restaurado. Quando não definido, o padrão é `online`.| Os valores possíveis estão *online* (padrão), *offline*.  Relacionado a [NU3028](../errors-and-warnings/NU3028.md) |

