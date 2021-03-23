---
title: Referência de arquivo de nuget.config
description: Referência do arquivo NuGet.Config incluindo as seções config, bindingRedirects, packageRestore, solution e packageSource.
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: afc06c81bf0344f2086efd19111cc60d24d7f723
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859506"
---
# <a name="nugetconfig-reference"></a>Referência de nuget.config

O comportamento do NuGet é controlado por configurações `NuGet.Config` em `nuget.config` arquivos diferentes ou conforme descrito em [configurações comuns do NuGet](../consume-packages/configuring-nuget-behavior.md).

`nuget.config` é um arquivo XML que contém um nó `<configuration>` de nível superior, o qual contém os elementos da seção descritos neste tópico. Cada seção contém zero ou mais itens. Consulte o [arquivo de configuração de exemplos](#example-config-file). Nomes de configuração não diferenciam maiúsculas de minúsculas e podem usar valores [variáveis de ambiente](#using-environment-variables).

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>seção de configuração

Contém diversas definições de configuração, que podem ser definidas usando o [ `nuget config` comando](../reference/cli-reference/cli-ref-config.md).

`dependencyVersion` e `repositoryPath` aplicam-se somente a projetos que usam o `packages.config` . `globalPackagesFolder` aplica-se somente a projetos que usam o formato PackageReference.

| Chave | Valor |
| --- | --- |
| dependencyVersion (somente `packages.config`) | O valor `DependencyVersion` padrão para a instalação, restauração e atualização do pacote, quando a opção `-DependencyVersion` não tiver sido especificada diretamente. Esse valor também é usado pela interface do usuário do Gerenciador de Pacotes do NuGet. Os valores são `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (projetos usando apenas PackageReference) | O local da pasta de pacotes global padrão. O padrão é `%userprofile%\.nuget\packages` (Windows) ou `~/.nuget/packages` (Mac/Linux). Um caminho relativo pode ser usado em arquivos `nuget.config` específicos do projeto. Essa configuração é substituída pela `NUGET_PACKAGES` variável de ambiente, que tem precedência. |
| repositoryPath (somente `packages.config`) | O local no qual instalar os pacotes do NuGet em vez da pasta `$(Solutiondir)/packages` padrão. Um caminho relativo pode ser usado em arquivos `nuget.config` específicos do projeto. Essa configuração é substituída pela `NUGET_PACKAGES` variável de ambiente, que tem precedência. |
| defaultPushSource | Identifica a URL ou o caminho da origem do pacote que deve ser usada como o padrão se nenhuma outra origem de pacote for encontrada para uma operação. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Configurações de proxy a serem usadas ao se conectar a origens de pacote; `http_proxy` deve estar no formato `http://<username>:<password>@<domain>`. As senhas são criptografadas e não podem ser adicionadas manualmente. Para `no_proxy`, o valor é uma lista separada por vírgulas de domínios a ignorar no servidor proxy. Como alternativa, você pode usar as variáveis de ambiente http_proxy e no_proxy para esses valores. Para ver detalhes adicionais, consulte [Configurações de proxy do NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Especifica o modo de validação usado para verificar assinaturas de pacote para instalação do pacote e restauração. Os valores são `accept` , `require` . Assume o padrão de `accept`.

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
| Habilitado | Um valor booliano que indica se o NuGet pode executar uma restauração automática. Você também pode definir a variável de ambiente `EnableNuGetPackageRestore` com um valor de `True` em vez de configurar essa chave no arquivo de configuração. |
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

O `packageSources` , `packageSourceCredentials` , `apikeys` , `activePackageSource` , `disabledPackageSources` e `trustedSigners` todos trabalham juntos para configurar como o NuGet funciona com repositórios de pacotes durante operações de instalação, restauração e atualização.

O [ `nuget sources` comando](../reference/cli-reference/cli-ref-sources.md) geralmente é usado para gerenciar essas configurações, exceto para o `apikeys` que é gerenciado usando o [ `nuget setapikey` comando](../reference/cli-reference/cli-ref-setapikey.md)e `trustedSigners` que é gerenciado usando o [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).

Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Lista todas as origens de pacotes conhecidas. A ordem é ignorada durante as operações de restauração e com qualquer projeto usando o formato PackageReference. O NuGet respeita a ordem de fontes para operações de instalação e atualização com projetos usando o `packages.config` .

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

> [!Tip]
> Quando `<clear />` está presente para um nó específico, o NuGet ignora os valores de configuração definidos anteriormente para esse nó. [Leia mais sobre como as configurações são aplicadas](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Armazena os nomes de usuário e senhas para as origens, geralmente especificado com as opções `-username` e `-password` com `nuget sources`. As senhas são criptografadas por padrão, a menos que a opção `-storepasswordincleartext` também seja usada.
Opcionalmente, os tipos de autenticação válidos podem ser especificados com a `-validauthenticationtypes` opção.

| Chave | Valor |
| --- | --- |
| Nome de Usuário | O nome de usuário para a origem em texto sem formatação. |
| password | A senha criptografada para a origem. As senhas criptografadas só têm suporte no Windows e só podem ser descriptografadas quando usadas no mesmo computador e por meio do mesmo usuário que a criptografia original. |
| cleartextpassword | A senha não criptografada para a origem. Observação: as variáveis de ambiente podem ser usadas para aumentar a segurança. |
| validauthenticationtypes | Lista separada por vírgulas de tipos de autenticação válidos para esta fonte. Defina isso como `basic` se o servidor anunciar NTLM ou negociar e suas credenciais devem ser enviadas usando o mecanismo básico, por exemplo, ao usar uma Pat com Azure DevOps Server locais. Outros valores válidos incluem `negotiate` , `kerberos` , `ntlm` e `digest` , mas esses valores são improvável de ser úteis. |

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

Ao usar senhas não criptografadas armazenadas em uma variável de ambiente:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
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

Além disso, os métodos de autenticação válidos podem ser fornecidos:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
        <add key="ValidAuthenticationTypes" value="basic" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
        <add key="ValidAuthenticationTypes" value="basic, negotiate" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a>apikeys

Armazena chaves para fontes que usam autenticação de chave de API, conforme definido com o [ `nuget setapikey` comando](../reference/cli-reference/cli-ref-setapikey.md).

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

Armazena os assinantes confiáveis usados para permitir o pacote durante a instalação ou restauração. Esta lista não pode estar vazia quando o usuário define `signatureValidationMode` como `require` . 

Esta seção pode ser atualizada com o [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).

**Esquema**:

Um assinante confiável tem uma coleção de `certificate` itens que inscrevem todos os certificados que identificam um determinado signatário. Um signatário confiável pode ser um `Author` ou um `Repository` .

Um *repositório* confiável também especifica o `serviceIndex` para o repositório (que deve ser um URI válido `https` ) e pode, opcionalmente, especificar uma lista delimitada por ponto e vírgula de `owners` para restringir ainda mais o que é confiável desse repositório específico.

Os algoritmos de hash com suporte usados para uma impressão digital de certificado são `SHA256` `SHA384` e `SHA512` .

Se um `certificate` especifica `allowUntrustedRoot` que `true` o certificado fornecido pode encadear a uma raiz não confiável ao criar a cadeia de certificados como parte da verificação de assinatura.

**Exemplo**:

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a>seção fallbackPackageFolders

*(3,5 +)* Fornece uma maneira de pré-instalar pacotes para que nenhum trabalho precise ser feito se o pacote for encontrado nas pastas de fallback. As pastas de pacote de fallback têm exatamente a mesma estrutura de pasta e arquivo que a pasta de pacote global: *. nupkg* está presente e todos os arquivos são extraídos.

A lógica de pesquisa para essa configuração é:

- Procure na pasta de pacote global para ver se o pacote/versão já foi baixado.

- Procure uma correspondência de pacote/versão nas pastas de fallback.

Se a pesquisa for bem-sucedida, nenhum download será necessário.

Se uma correspondência não for encontrada, o NuGet verificará as fontes de arquivo e, em seguida, as fontes http e baixará os pacotes.

| Chave | Valor |
| --- | --- |
| (nome da pasta de fallback) | Caminho para a pasta de fallback. |

**Exemplo**:

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>seção packageManagement

Define o formato de gerenciamento de pacote padrão, *packages.config* ou PackageReference. Projetos no estilo SDK sempre usam PackageReference.

| Chave | Valor |
| --- | --- |
| format | Um booliano que indica o formato de gerenciamento de pacote padrão. Se `1` , Format for PackageReference. Se `0` , o formato é *packages.config*. |
| desabilitado | Um booliano que indica se o prompt deve ser mostrado para selecionar um formato de pacote padrão na instalação do primeiro pacote. `False` oculta o prompt. |

**Exemplo**:

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a>Usando variáveis de ambiente

Você pode usar variáveis de ambiente em valores `nuget.config` (NuGet 3.4 ou superior) para aplicar as configurações no tempo de execução.

Por exemplo, se a variável de ambiente `HOME` no Windows for definida como `c:\users\username`, o valor de `%HOME%\NuGetRepository` no arquivo de configuração é resolvido para `c:\users\username\NuGetRepository`.

Observe que você precisa usar variáveis de ambiente no estilo do Windows (começa e termina com%) mesmo no Mac/Linux. Ter `$HOME/NuGetRepository` em um arquivo de configuração não será resolvido. No Mac/Linux, o valor de `%HOME%/NuGetRepository` será resolvido para `/home/myStuff/NuGetRepository` .

Se uma variável de ambiente não for encontrada, o NuGet usa o valor literal do arquivo de configuração. Por exemplo, `%MY_UNDEFINED_VAR%/NuGetRepository` será resolvido como `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`

A tabela abaixo mostra a sintaxe da variável ambiente e o suporte ao separador de caminho para arquivos de NuGet.Config.

### <a name="nugetconfig-environment-variable-support"></a>Suporte à variável de ambiente NuGet.Config

| Sintaxe | Separador de dir | nuget.exe do Windows | dotnet.exe do Windows | nuget.exe do Mac (em mono) | dotnet.exe Mac |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | Sim | Sim | Sim | Sim |
| `%MY_VAR%` | `\`  | Sim | Sim | Não | Não |
| `$MY_VAR` | `/`  | Não | Não | Não | Não |
| `$MY_VAR` | `\`  | Não | Não | Não | Não |


## <a name="example-config-file"></a>Exemplo de arquivo de configuração

Abaixo está um `nuget.config` arquivo de exemplo que ilustra várias configurações, incluindo as opcionais:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable.
            This syntax works on Windows/Mac/Linux
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%/External" />

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
            <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <certificate fingerprint="5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
