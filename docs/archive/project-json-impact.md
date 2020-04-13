---
title: Impacto do project.json em autores de pacote do NuGet
description: Detalhes sobre como a implementação do project.json no NuGet 3.x afeta autores de pacote, como recursos incompatíveis, conteúdo e formato do pacote.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 34b08f06f04efdcf7bf73efc2cbdb5a5494ae2d9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488193"
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Impacto do project.json durante a criação de pacotes

> [!Important]
> Este conteúdo foi preterido. Os projetos devem usar os formatos `packages.config` ou PackageReference.

O sistema `project.json` usado no NuGet 3 ou superior afeta os autores de pacote de várias maneiras, conforme descrito nas seções a seguir.

## <a name="changes-affecting-existing-packages-usage"></a>Alterações que afetam o uso de pacotes existentes

Pacotes do NuGet tradicionais são compatíveis com diversos recursos que não são refletidos no mundo transitivo.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Scripts de instalação e desinstalação são ignorados

O modelo de restauração transitiva, descrito em [Resolução de dependência](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference), não tem um conceito de “tempo de instalação do pacote”. Um pacote existe ou não, porém não há nenhum processo consistente que ocorre quando um pacote é instalado.

Além disso, scripts de instalação são compatíveis apenas com o Visual Studio. Outros IDEs precisavam simular a API de extensibilidade do Visual Studio para tentar ser compatíveis com tais scripts e não há compatibilidade em editores e ferramentas de linha de comando comuns.

### <a name="content-transforms-are-not-supported"></a>As transformações de conteúdo não são compatíveis

Semelhante a scripts de instalação, as transformações são executadas na instalação do pacote e geralmente não são idempotentes. Como não há mais nenhum tempo de instalação, o XDT Transform e recursos semelhantes são incompatíveis e serão ignorados se esse tipo de pacote for usado em um cenário transitivo.

### <a name="content"></a>Conteúdo

Pacotes do NuGet tradicionais fornecem arquivos de conteúdo como código-fonte e arquivos de configuração. Geralmente, eles são usados em dois cenários:

1. Arquivos iniciais são colocados no projeto para que o usuário possa editá-los mais tarde. O exemplo comum são os arquivos de configuração padrão.

1. Arquivos de conteúdo usados como complementos para os assemblies instalados no projeto. Este exemplo seria uma imagem de logotipo usada por um assembly.

Não há compatibilidade para o conteúdo pelos mesmos motivos dos scripts e transformações, porém já estamos desenvolvendo a compatibilidade para o conteúdo.

Arquivos de conteúdo ainda podem ser transportados dentro de pacotes e são ignorados no momento, porém o usuário final ainda pode copiá-los para o ponto certo.

Você pode ver uma das propostas para trazer de volta [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)arquivos de conteúdo, e acompanhar seu progresso, aqui: .

## <a name="impact-for-package-authors"></a>Impacto para os autores de pacote

Pacotes que usam os recursos acima precisariam usar um mecanismo diferente. O mecanismo normalmente mais útil para isso seria os destinos/objetos do MSBuild que continuam a ter compatibilidade total. O sistema de build pode optar por escolher outras convenções no pacote. É assim que os destinos do MSBuild são compatíveis, bem como os analisadores de Roslyn. É possível criar pacotes compatíveis com destinos e analisadores para cenários de `packages.config` e `project.json`.

Pacotes que tentam modificar o projeto para facilitar a inicialização normalmente funcionam em uma variedade muito limitada de cenários e devem fornecer um arquivo leiame ou orientação sobre como usar o pacote.

A maioria dos pacotes existentes não deve precisar usar o formato de pacote descrito abaixo.

O formato habilita conteúdo nativo como um cenário de primeira classe. Isso significa que assemblies gerenciados dependem de implementações próximas a hardware para enviar implementações binárias juntamente com os assemblies gerenciados, dependendo da plataforma de destino. O pacote System.IO.Compression, por exemplo, utiliza essa tecnologia. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

Resumindo, se a funcionalidade acima não é absolutamente necessária, recomendamos continuar usando o formato de pacote existente, visto que o formato descrito aqui é compatível somente com o NuGet 3.x ou superior.

Seria possível compilar pacotes para funcionar com ambos os cenários `packages.config` e `project.json` por meio de correções, no entanto, geralmente é mais simples apenas estruturar os pacotes de forma tradicional, sem os recursos preteridos mencionados acima.

## <a name="3x-package-format"></a>Formato de pacote do 3.x

O formato de pacote 3.x permite usar vários recursos adicionais além do NuGet 2.x:

1. A definição de um assembly de referência usado para compilação e um conjunto de assemblies de implementação usados para o runtime em diferentes plataformas/dispositivos. Isso permite aproveitar APIs específicas da plataforma e fornecer uma área de superfície comum para seus clientes. Especificamente, isso facilita a criação de bibliotecas portáteis intermediárias.

1. Permite que os pacotes circulem entre as plataformas como, por exemplo, sistemas operacionais ou arquiteturas de CPU.

1. Possibilita a separação de implementações específicas de plataforma para pacotes complementares.

1. Dependências de suporte nativo como cidadão de primeira classe.
