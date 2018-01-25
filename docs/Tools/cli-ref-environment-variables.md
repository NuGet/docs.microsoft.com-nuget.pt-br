---
title: "Variáveis de ambiente do NuGet CLI | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para as variáveis de ambiente nuget.exe"
keywords: "variáveis de ambiente do NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 516a66103d6159a3d68b5383090e8e3b519a5588
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-cli-environment-variables"></a>Variáveis de ambiente do NuGet CLI

O comportamento do nuget.exe CLI pode ser configurado por meio de um número de variáveis de ambiente, que afetam o nuget.exe em todo o computador, usuário ou processo níveis.

Em geral, opções especificadas diretamente na linha de comando ou em arquivos de configuração NuGet têm precedência, mas há algumas exceções, como *FORCE_NUGET_EXE_INTERACTIVE*. Se você achar que nuget.exe se comporta de forma diferente entre computadores diferentes, uma variável de ambiente pode ser a causa. Por exemplo, Kudu de aplicativos Web do Azure (usado durante a implantação) tem *NUGET_XMLDOC_MODE* definida como *ignorar* para acelerar o desempenho de restauração do pacote e economizar espaço em disco.

| Variável | Descrição | Comentários |
| --- | --- | --- |
| http_proxy | Proxy HTTP usado para operações de HTTP do NuGet. | Isso deve ser especificado como `http://<username>:<password>@proxy.com`. |
| no_proxy | Configura os domínios para ignorar o uso do proxy. | Especificado como domínios separados por vírgula (,). |
| EnableNuGetPackageRestore | Sinalizador para se NuGet implicitamente deve conceder consentimento se exigido pelo pacote na restauração. | Sinalizador especificado for especificado | como *true* ou *1*, qualquer outro valor tratado como sinalizador não definido. |
| NUGET_EXE_NO_PROMPT | Impede que o arquivo exe para solicitar credenciais.| Qualquer valor exceto a cadeia de caracteres nula ou vazia será tratada como esse sinalizador conjunto/verdadeiro. |
FORCE_NUGET_EXE_INTERACTIVE | Variável de ambiente global para forçar o modo interativo. | Qualquer valor exceto a cadeia de caracteres nula ou vazia será tratada como esse sinalizador conjunto/verdadeiro. |
| NUGET_PACKAGES | Caminho para onde os pacotes são armazenados / em cache. | Especificado como um caminho absoluto. |
| NUGET_FALLBACK_PACKAGES | Pastas de pacotes de fallback global. | Caminhos de pasta absoluto separados por ponto e vírgula (;). |
| NUGET_HTTP_CACHE_PATH | Pasta de cache HTTP. | Especificado como um caminho absoluto. |
| NUGET_PERSIST_DG | Sinalizador que indica se devem ser persistidos dg arquivos (dados coletados do MSBuild). | Especificado como *true* ou *false* (padrão), se não definida NUGET_PERSIST_DG_PATH será armazenado para o diretório temporário (NuGetScratch pasta no diretório temp de ambiente atual). |
| NUGET_PERSIST_DG_PATH | Caminho para manter arquivos GD. | Especificado como um caminho absoluto, essa opção é usado apenas quando *NUGET_PERSIST_DG* é definido como true. |
| NUGET_RESTORE_MSBUILD_ARGS | Define os argumentos adicionais do MSBuild. |
| NUGET_RESTORE_MSBUILD_| Detalhamento |Define o nível de detalhes de log do MSBuild. | O padrão é *silencioso* ("/ v: p"). Os valores possíveis *q [uiet]*, *m [ínimo]*, *n [ormal]*, *d [etailed]*, e *diag [nostic]*. |
| NUGET_SHOW_STACK | Determina se a exceção completa (incluindo o rastreamento de pilha) deve ser exibida para o usuário. | Especificado como *true* ou *false* (padrão). |
| NUGET_XMLDOC_MODE | Determina como a extração do arquivo de documentação de XML de assemblies deve ser tratada. | Os modos suportados são *ignorar* (não extraia os arquivos de documentação XML), *compactar* (armazenam arquivos de documento XML como um arquivo zip) ou *nenhum* (padrão, trate os arquivos de documentos XML como normal arquivos). |
