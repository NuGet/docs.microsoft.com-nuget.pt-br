---
title: Variáveis de ambiente da CLI do NuGet
description: Referência para as variáveis de ambiente nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: fd5824d1c5e05df08301dac1cf656ba1d5ca75cd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551732"
---
# <a name="nuget-cli-environment-variables"></a>Variáveis de ambiente da CLI do NuGet

O comportamento do nuget.exe CLI pode ser configurado por meio de um número de variáveis de ambiente, o que afeta nuget.exe em todo o computador, usuário ou processo níveis. Variáveis de ambiente sempre substituem as configurações em `NuGet.Config` arquivos, que permite criar servidores para alterar as configurações apropriadas sem modificar todos os arquivos.

Em geral, as opções especificadas diretamente na linha de comando ou em arquivos de configuração do NuGet têm precedência, mas há algumas exceções, como *FORCE_NUGET_EXE_INTERACTIVE*. Se você encontrar que esse nuget.exe tem um comportamento diferente entre computadores diferentes, uma variável de ambiente pode ser a causa. Por exemplo, o Kudu de aplicativos Web do Azure (usada durante a implantação) tem *NUGET_XMLDOC_MODE* definido como *ignorar* para acelerar o desempenho de restauração de pacote e economizar espaço em disco.

| Variável | Descrição | Comentários |
| --- | --- | --- |
| http_proxy | Proxy HTTP usado para operações de HTTP do NuGet. | Isso deve ser especificado como `http://<username>:<password>@proxy.com`. |
| no_proxy | Configura os domínios para ignorar o proxy que usa. | Especificado como domínios separados por vírgula (,). |
| EnableNuGetPackageRestore | Sinalizador para se NuGet implicitamente deve conceder consentimento se exigido pelo pacote de restauração. | Sinalizador especificado é tratado como *verdadeira* ou *1*, qualquer outro valor tratado como sinalizador não definido. |
| NUGET_EXE_NO_PROMPT | Impede que o arquivo exe para solicitar credenciais. | Qualquer valor exceto a cadeia de caracteres nula ou vazia será tratada como esse sinalizador conjunto/verdadeiro. |
| FORCE_NUGET_EXE_INTERACTIVE | Variável de ambiente global para forçar o modo interativo. | Qualquer valor exceto a cadeia de caracteres nula ou vazia será tratada como esse sinalizador conjunto/verdadeiro. |
| NUGET_PACKAGES | Caminho a ser usado para o *global-packages* pasta conforme descrito em [gerenciar as pastas de cache e de pacotes globais](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Especificado como o caminho absoluto. |
| NUGET_FALLBACK_PACKAGES | Pastas de pacotes globais de fallback. | Caminhos de pasta absoluto separados por ponto e vírgula (;). |
| NUGET_HTTP_CACHE_PATH | Caminho a ser usado para o *http-cache* pasta conforme descrito em [gerenciar as pastas de cache e de pacotes globais](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Especificado como o caminho absoluto. |
| NUGET_PERSIST_DG | Sinalizador que indica se os arquivos de dg (dados coletados do MSBuild) devem ser persistentes. | Especificado como *verdadeira* ou *falso* será armazenado (padrão), se NUGET_PERSIST_DG_PATH não definida para o diretório temporário (NuGetScratch pasta no diretório temporário do atual ambiente). |
| NUGET_PERSIST_DG_PATH | Caminho para manter os arquivos de GD. | Especificado como o caminho absoluto, essa opção é usada apenas quando *NUGET_PERSIST_DG* é definido como true. |
| NUGET_RESTORE_MSBUILD_ARGS | Define os argumentos adicionais do MSBuild. | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Define o nível de detalhes de log do MSBuild. | O padrão é *silencioso* ("/ v: q"). Os valores possíveis *q [uiet]*, *Minimal*, *n [ormal]*, *Detailed*, e *diag [nostic]*. |
| NUGET_SHOW_STACK | Determina se a exceção completa (incluindo o rastreamento de pilha) deve ser exibida ao usuário. | Especificado como *verdadeira* ou *falso* (padrão). |
| NUGET_XMLDOC_MODE | Determina como a extração do arquivo de documentação de XML de assemblies deve ser tratada. | Os modos suportados são *ignore* (não extraia os arquivos de documentação XML), *compactar* (armazenar arquivos de documento XML como um arquivo zip) ou *none* (padrão, trate os arquivos de documento XML como normal arquivos). |
| NUGET_CERT_REVOCATION_MODE | Determina como para verificar o status de revogação do certificado usado para assinar um pacote, é pefromed quando um pacote assinado é instalado ou restaurado. Quando não definido, o padrão é `online`.| Os valores possíveis *on-line* (padrão), *offline*.  Relacionado ao [NU3028](../reference/errors-and-warnings/NU3028.md) |
