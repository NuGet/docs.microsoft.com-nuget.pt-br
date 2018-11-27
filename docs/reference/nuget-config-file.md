---
title: Referência do arquivo NuGet. config
description: Referência do arquivo NuGet.Config incluindo as seções config, bindingRedirects, packageRestore, solution e packageSource.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: c294e4c188db2e90e6bcb62b60f71ed5529977fe
ms.sourcegitcommit: a1846edf70ddb2505d58e536e08e952d870931b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303513"
---
# <a name="nugetconfig-reference"></a>referência do NuGet. config

O comportamento do NuGet é controlado pelas configurações em diferentes arquivos `NuGet.Config` conforme descrito em [Configurando o comportamento de NuGet](../consume-packages/configuring-nuget-behavior.md).

`nuget.config` é um arquivo XML que contém um nó `<configuration>` de nível superior, o qual contém os elementos da seção descritos neste tópico. Cada seção contém zero ou mais itens. Consulte o [arquivo de configuração de exemplos](#example-config-file). Nomes de configuração não diferenciam maiúsculas de minúsculas e podem usar valores [variáveis de ambiente](#using-environment-variables).

Neste tópico:

- [seção de configuração](#config-section)
- [Seção bindingRedirects](#bindingredirects-section)
- [Seção packageRestore](#packagerestore-section)
- [solution section](#solution-section)
- [Seções de origem de pacote](#package-source-sections):
  - [packageSources](#packagesources)
  - [packageSourceCredentials](#packagesourcecredentials)
  - [apikeys](#apikeys)
  - [disabledPackageSources](#disabledpackagesources)
  - [activePackageSource](#activepackagesource)
- [seção trustedSigners](#trustedsigners-section)
- [Usando variáveis de ambiente](#using-environment-variables)
- [Exemplo de arquivo de configuração](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>seção de configuração

Contém diversas definições de configurações, que podem ser definidas usando o comando [`nuget config`](../tools/cli-ref-config.md).

`dependencyVersion` e `repositoryPath` se aplicam somente a projetos usando `packages.config`. `globalPackagesFolder` aplica-se somente a projetos usando o formato PackageReference.

| Chave | Valor |
| --- | --- |
| dependencyVersion (somente `packages.config`) | O valor `DependencyVersion` padrão para a instalação, restauração e atualização do pacote, quando a opção `-DependencyVersion` não tiver sido especificada diretamente. Esse valor também é usado pela interface do usuário do Gerenciador de Pacotes do NuGet. Os valores são `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (projetos que usam PackageReference apenas) | O local da pasta de pacotes global padrão. O padrão é `%userprofile%\.nuget\packages` (Windows) ou `~/.nuget/packages` (Mac/Linux). Um caminho relativo pode ser usado em arquivos `nuget.config` específicos do projeto. Essa configuração é substituída pela variável de ambiente NUGET_PACKAGES, que tem precedência. |
| repositoryPath (somente `packages.config`) | O local no qual instalar os pacotes do NuGet em vez da pasta `$(Solutiondir)/packages` padrão. Um caminho relativo pode ser usado em arquivos `nuget.config` específicos do projeto. Essa configuração é substituída pela variável de ambiente NUGET_PACKAGES, que tem precedência. |
| defaultPushSource | Identifica a URL ou o caminho da origem do pacote que deve ser usada como o padrão se nenhuma outra origem de pacote for encontrada para uma operação. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Configurações de proxy a serem usadas ao se conectar a origens de pacote; `http_proxy` deve estar no formato `http://<username>:<password>@<domain>`. As senhas são criptografadas e não podem ser adicionadas manualmente. Para `no_proxy`, o valor é uma lista separada por vírgulas de domínios a ignorar no servidor proxy. Como alternativa, você pode usar as variáveis de ambiente http_proxy e no_proxy para esses valores. Para ver detalhes adicionais, consulte [Configurações de proxy do NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Especifica o modo de validação usado para verificar as assinaturas de pacote para instalação do pacote e restauração. Os valores são `accept`, `require`. Assume o padrão de `accept`.

**Exemplo**:

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a>Seção bindingRedirects

Configura se o NuGet realiza redirecionamentos de associação automática quando um pacote é instalado.

| Chave | Valor |
| --- | --- |
| skip | Um valor booliano que indica se os redirecionamentos de associação automática devem ser ignorados. O padrão é falso. |

**Exemplo**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>Seção packageRestore

Controla a restauração de pacote durante builds.

| Chave | Valor |
| --- | --- |
| habilitado | Um valor booliano que indica se o NuGet pode executar uma restauração automática. Você também pode definir a variável de ambiente `EnableNuGetPackageRestore` com um valor de `True` em vez de configurar essa chave no arquivo de configuração. |
| automático | Um valor booliano que indica se o NuGet deve verificar se há pacotes ausentes durante um build. |

**Exemplo**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>solution section

Controla se a pasta `packages` de uma solução está incluída no controle do código-fonte. Esta seção funciona somente em arquivos `nuget.config` em uma pasta de solução.

| Chave | Valor |
| --- | --- |
| disableSourceControlIntegration | Um booliano que indica se a pasta de pacotes deve ser ignorada ao trabalhar com o controle do código-fonte. O valor padrão é false. |

**Exemplo**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Seções de origem de pacote

O `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` e `trustedSigners` trabalham todos juntos para configurar como o NuGet funciona com repositórios de pacote durante a instalação, restauração e operações de atualização.

O [ `nuget sources` comando](../tools/cli-ref-sources.md) geralmente é usado para gerenciar essas configurações, exceto para `apikeys` que é gerenciado usando o [ `nuget setapikey` comando](../tools/cli-ref-setapikey.md), e `trustedSigners` que é gerenciado usando o [ `nuget trusted-signers` comando](../tools/cli-ref-trusted-signers.md).

Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Lista todas as origens de pacotes conhecidas. A ordem é ignorada durante operações de restauração e com qualquer projeto usando o formato PackageReference. NuGet respeita a ordem das fontes para instalar e atualizar operações com projetos usando `packages.config`.

| Chave | Valor |
| --- | --- |
| (nome a ser atribuído à origem do pacote) | O caminho ou URL da origem do pacote. |

**Exemplo**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Armazena os nomes de usuário e senhas para as origens, geralmente especificado com as opções `-username` e `-password` com `nuget sources`. As senhas são criptografadas por padrão, a menos que a opção `-storepasswordincleartext` também seja usada.

| Chave | Valor |
| --- | --- |
| username | O nome de usuário para a origem em texto sem formatação. |
| password | A senha criptografada para a origem. |
| cleartextpassword | A senha não criptografada para a origem. |

**Exemplo:**

No arquivo de configuração, o elemento `<packageSourceCredentials>` contém nós filho para cada nome de origem aplicável (espaços no nome serão substituídos por `_x0020_`). Ou seja, para origens chamadas “Contoso” e “Origem de teste”, o arquivo de configuração contém o seguinte ao usar senhas criptografadas:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

Ao usar senhas não criptografadas:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a>apikeys

Armazena as chaves de origens que usam autenticação de chave de API, conforme definido com o comando [`nuget setapikey`](../tools/cli-ref-setapikey.md).

| Chave | Valor |
| --- | --- |
| (URL de origem) | A chave de API criptografada. |

**Exemplo**:

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

Identificar fontes desabilitadas no momento. Pode ficar em branco.

| Chave | Valor |
| --- | --- |
| (nome da origem) | Um valor booliano que indica se a origem está desabilitada. |

**Exemplo:**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(somente 2.x; preterido no 3.x ou superior)*

Identifica a fonte ativa no momento ou indica a agregação de todas as fontes.

| Chave | Valor |
| --- | --- |
| (nome da origem) ou `All` | Se a chave é o nome de uma fonte, o valor é o caminho ou URL da origem. Se `All`, o valor deve ser `(Aggregate source)` para combinar todas as origens de pacote que não foram desabilitadas. |

**Exemplo**:

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a>seção trustedSigners

Repositórios confiam signatários usados para permitir que o pacote durante a instalação ou restauração. Essa lista não pode estar vazia quando o usuário define `signatureValidationMode` para `require`. 

Esta seção pode ser atualizada com o [ `nuget trusted-signers` comando](../tools/cli-ref-trusted-signers.md).

**Esquema**:

Um signatário confiável tem uma coleção de `certificate` itens que inscrever-se todos os certificados que identificam um determinado assinante. Um signatário confiável pode ser um `Author` ou um `Repository`.

Um confiável *repositório* também especifica a `serviceIndex` para o repositório (que deve ser válido `https` uri) e, opcionalmente, pode especificar uma lista de delimitada por ponto e vírgula de `owners` para restringir ainda mais que é confiável meio desse repositório específico.

Os algoritmos de hash com suporte usados para uma impressão digital do certificado são `SHA256`, `SHA384` e `SHA512`.

Se um `certificate` especifica `allowUntrustedRoot` como `true` o certificado fornecido é permitido encadear para uma raiz não confiável ao criar a cadeia de certificados como parte da verificação de assinatura.

**Exemplo**:

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="using-environment-variables"></a>Usando variáveis de ambiente

Você pode usar variáveis de ambiente em valores `nuget.config` (NuGet 3.4 ou superior) para aplicar as configurações no tempo de execução.

Por exemplo, se a variável de ambiente `HOME` no Windows for definida como `c:\users\username`, o valor de `%HOME%\NuGetRepository` no arquivo de configuração é resolvido para `c:\users\username\NuGetRepository`.

Da mesma forma, se o `HOME` no Mac/Linux for definido como `/home/myStuff`, `%HOME%/NuGetRepository` no arquivo de configuração será resolvido para `/home/myStuff/NuGetRepository`.

Se uma variável de ambiente não for encontrada, o NuGet usa o valor literal do arquivo de configuração.

## <a name="example-config-file"></a>Exemplo de arquivo de configuração

Abaixo está um arquivo `nuget.config` de exemplo que ilustra diversas configurações:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
