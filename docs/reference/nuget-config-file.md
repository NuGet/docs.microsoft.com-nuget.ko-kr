---
title: nuget.config 파일 참조
description: config, bindingRedirects, packageRestore, solution 및 packageSource 섹션이 포함된 NuGet.Config 파일 참조입니다.
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 9b15550d0e6e8aec4d526391d77c654a756f343e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777665"
---
# <a name="nugetconfig-reference"></a>nuget.config 참조

NuGet 동작은 `NuGet.Config` `nuget.config` [일반적인 nuget 구성](../consume-packages/configuring-nuget-behavior.md)에 설명 된 대로 다른 또는 파일의 설정에 의해 제어 됩니다.

`nuget.config`는 최상위 `<configuration>` 노드를 포함하는 XML 파일이며, 이 파일에는 이 항목에서 설명하는 섹션 요소가 포함되어 있습니다. 각 섹션에는 0 개 이상의 항목이 포함 되어 있습니다. [config 파일 예제](#example-config-file)를 참조하세요. 설정 이름은 대/소문자를 구분하지 않으며, 값에는 [환경 변수](#using-environment-variables)를 사용할 수 있습니다.

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>config 섹션

에는 [ `nuget config` 명령을](../reference/cli-reference/cli-ref-config.md)사용 하 여 설정할 수 있는 기타 구성 설정이 포함 되어 있습니다.

`dependencyVersion` 및는 `repositoryPath` 를 사용 하는 프로젝트에만 적용 `packages.config` 됩니다. `globalPackagesFolder` PackageReference 형식을 사용 하는 프로젝트에만 적용 됩니다.

| 키 | 값 |
| --- | --- |
| dependencyVersion(`packages.config`만) | `-DependencyVersion` 스위치가 직접 지정되지 않은 경우 패키지 설치, 복원 및 업데이트에 대한 기본 `DependencyVersion` 값입니다. 이 값은 NuGet 패키지 관리자 UI에서도 사용됩니다. 값은 `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`입니다. |
| globalPackagesFolder (PackageReference만 사용 하는 프로젝트) | 기본 전역 패키지 폴더의 위치입니다. 기본값은 `%userprofile%\.nuget\packages`(Windows) 또는 `~/.nuget/packages`(Mac/Linux)입니다. 상대 경로는 프로젝트별 `nuget.config` 파일에서 사용할 수 있습니다. 이 설정은 NUGET_PACKAGES 환경 변수에 의해 재정의 되며이는 우선적으로 적용 됩니다. |
| repositoryPath(`packages.config`만) | 기본 `$(Solutiondir)/packages` 폴더 대신 NuGet 패키지를 설치할 위치입니다. 상대 경로는 프로젝트별 `nuget.config` 파일에서 사용할 수 있습니다. 이 설정은 NUGET_PACKAGES 환경 변수에 의해 재정의 되며이는 우선적으로 적용 됩니다. |
| defaultPushSource | 작업에 대한 다른 패키지 원본이 없을 때 기본값으로 사용해야 하는 패키지 원본의 URL 또는 경로를 식별합니다. |
| http_proxy, http_proxy.user, http_proxy.password, no_proxy | 패키지 원본에 연결할 때 사용할 프록시 설정입니다. `http_proxy`는 `http://<username>:<password>@<domain>` 형식이어야 합니다. 암호는 암호화되어 있으며, 수동으로 추가할 수 없습니다. `no_proxy`의 경우 값은 프록시 서버를 우회하는 도메인의 쉼표로 구분된 목록입니다. 이러한 값에 대해 http_proxy 및 no_proxy 환경 변수를 번갈아 사용할 수 있습니다. 자세한 내용은 [NuGet 프록시 설정](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)(skolima.blogspot.com)을 참조하세요. |
| 서명 Validationmode | 패키지 설치 및 복원에 대 한 패키지 서명을 확인 하는 데 사용 되는 유효성 검사 모드를 지정 합니다. 값은 `accept` , `require` 입니다. 기본값은 `accept`입니다.

**예제**:

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a>bindingRedirects 섹션

패키지가 설치될 때 NuGet에서 자동 바인딩 리디렉션을 수행할지 여부를 구성합니다.

| 키 | 값 |
| --- | --- |
| skip | 자동 바인딩 리디렉션을 건너뛸지 여부를 나타내는 부울입니다. 기본값은 false입니다. |

**예제**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>packageRestore 섹션

빌드하는 동안의 패키지 복원을 제어합니다.

| 키 | 값 |
| --- | --- |
| 사용 | NuGet에서 자동 복원을 수행할 수 있는지 여부를 나타내는 부울입니다. config 파일에서 이 키를 설정하는 대신 `EnableNuGetPackageRestore` 환경 변수를 `True` 값으로 설정할 수도 있습니다. |
| automatic | NuGet에서 빌드하는 동안 누락된 패키지를 확인해야 하는지 여부를 나타내는 부울입니다. |

**예제**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>solution 섹션

솔루션의 `packages` 폴더가 원본 제어에 포함되는지 여부를 제어합니다. 이 섹션은 솔루션 폴더의 `nuget.config` 파일에서만 작동합니다.

| 키 | 값 |
| --- | --- |
| disableSourceControlIntegration | 원본 제어로 작업할 때 패키지 폴더를 무시할지 여부를 나타내는 부울입니다. 기본값은 false입니다. |

**예제**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>패키지 원본 섹션

`packageSources`,, `packageSourceCredentials` `apikeys` , 및 `activePackageSource` 는 `disabledPackageSources` `trustedSigners` 모두 함께 작동 하 여 설치, 복원 및 업데이트 작업 중에 NuGet이 패키지 리포지토리와 함께 작동 하는 방식을 구성 합니다.

명령은 [ `nuget sources` 명령을](../reference/cli-reference/cli-ref-sources.md) `apikeys` 사용 하 여 관리 되 [ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md)고 `trustedSigners` [ `nuget trusted-signers` 명령을](../reference/cli-reference/cli-ref-trusted-signers.md)사용 하 여 관리 되는를 제외 하 고는 일반적으로 이러한 설정을 관리 하는 데 사용 됩니다.

nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.

### <a name="packagesources"></a>packageSources

알려진 모든 패키지 원본을 나열합니다. PackageReference 형식을 사용 하는 모든 프로젝트와 복원 작업 중에 순서는 무시 됩니다. NuGet은를 사용 하 여 프로젝트에 대 한 설치 및 업데이트 작업의 소스 순서를 고려 합니다 `packages.config` .

| 키 | 값 |
| --- | --- |
| (패키지 원본에 할당할 이름) | 패키지 원본의 경로 또는 URL입니다. |

**예제**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> 지정된 노드에 대해 `<clear />`가 있으면 NuGet은 해당 노드에 대해 이전에 정의된 구성 값을 무시합니다. [설정이 적용 되는 방법에 대해 자세히](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)알아보세요.

### <a name="packagesourcecredentials"></a>packageSourceCredentials

원본에 대한 사용자 이름과 암호를 저장하며, 일반적으로 `nuget sources`와 함께 `-username` 및 `-password` 스위치로 지정됩니다. 또한 `-storepasswordincleartext` 옵션을 사용하지 않는 한 암호는 기본적으로 암호화됩니다.
필요에 따라 스위치를 사용 하 여 유효한 인증 유형을 지정할 수 있습니다 `-validauthenticationtypes` .

| 키 | 값 |
| --- | --- |
| 사용자 이름 | 일반 텍스트 형식의 원본에 대한 사용자 이름입니다. |
| password | 원본에 대한 암호화된 암호입니다. 암호화 된 암호는 Windows 에서만 지원 되며 동일한 컴퓨터에서 사용 하는 경우와 원래 암호화와 동일한 사용자를 통해 암호를 해독할 수 있습니다. |
| cleartextpassword | 원본에 대한 암호화되지 않은 암호입니다. 참고: 환경 변수를 사용 하 여 보안을 향상 시킬 수 있습니다. |
| 유효한 authenticationtypes | 이 소스에 대한 유효한 인증 형식의 쉼표로 구분된 목록입니다. 서버에서 NTLM 또는 Negotiate를 보급하고 기본 메커니즘을 사용하여 자격 증명을 전송해야 하는 경우(예를 들어 온-프레미스 Azure DevOps Server에서 PAT를 사용하는 경우) `basic`으로 설정합니다. 다른 유효한 값은 `negotiate`, `kerberos`, `ntlm` 및 `digest`이지만 이러한 값은 유용하지 않을 수 있습니다. |

**예제:**

config 파일에서 `<packageSourceCredentials>` 요소에는 적용 가능한 원본 이름 각각에 대한 자식 노드가 포함됩니다(이름에 포함된 공백은 `_x0020_`로 바뀜). 즉 "Contoso" 및 "Test Source"라는 원본의 경우 암호화된 암호를 사용하면 config 파일에는 다음이 포함됩니다.

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

환경 변수에 저장 된 암호화 되지 않은 암호를 사용 하는 경우:

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

암호화되지 않은 암호를 사용하는 경우:

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

또한 올바른 인증 방법을 제공할 수 있습니다.

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

[ `nuget setapikey` 명령](../reference/cli-reference/cli-ref-setapikey.md)으로 설정 된 대로 API 키 인증을 사용 하는 원본에 대 한 키를 저장 합니다.

| 키 | 값 |
| --- | --- |
| (원본 URL) | 암호화된 API 키입니다. |

**예제**:

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

현재 사용할 수 없는 원본을 식별합니다. 비어 있을 수 있습니다.

| 키 | 값 |
| --- | --- |
| (원본 이름) | 원본을 사용할 수 없는지 여부를 나타내는 부울입니다. |

**예제:**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(2.x만, 3.x 이상에서는 사용되지 않음)*

현재 활성 중인 원본을 식별하거나 모든 원본의 집계를 나타냅니다.

| 키 | 값 |
| --- | --- |
| (원본 이름) 또는 `All` | 키가 원본의 이름이면 값은 원본 경로 또는 URL입니다. `All`이면 값은 `(Aggregate source)`여야 하며, 그렇지 않으면 사용할 수 없는 모든 패키지 원본이 결합됩니다. |

**예제**:

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a>해당 서명자 섹션

설치 또는 복원 중 패키지를 허용 하는 데 사용 되는 신뢰할 수 있는 서명자를 저장 합니다. 사용자가로 설정 된 경우에는이 목록을 비워 둘 수 없습니다 `signatureValidationMode` `require` . 

이 섹션은 [ `nuget trusted-signers` 명령을](../reference/cli-reference/cli-ref-trusted-signers.md)사용 하 여 업데이트할 수 있습니다.

**스키마**:

신뢰할 수 있는 서명자는 지정 된 `certificate` 서명자를 식별 하는 모든 인증서를 등록 하는 항목의 컬렉션을 포함 합니다. 신뢰할 수 있는 서명자는 또는 일 수 있습니다 `Author` `Repository` .

또한 신뢰할 수 있는 *리포지토리* 는 `serviceIndex` 유효한 uri 여야 하는 리포지토리의를 지정 하며, `https` 선택적으로 세미콜론으로 구분 된 목록을 지정 하 여 `owners` 해당 특정 리포지토리에서 신뢰할 수 있는 사용자를 제한할 수 있습니다.

인증서 지문에 사용 되는 지원 되는 해시 알고리즘은 `SHA256` , `SHA384` 및 `SHA512` 입니다.

가 `certificate` `allowUntrustedRoot` `true` 서명 확인의 일부로 인증서 체인을 빌드하는 동안 지정 된 인증서를 신뢰할 수 없는 루트에 체인으로 연결할 수 있는 것으로 지정 하면입니다.

**예제**:

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a>fallbackPackageFolders 섹션

*(3.5 +)* 는 패키지가 대체 폴더에 있는 경우 작업을 수행 하지 않아도 되도록 패키지를 사전 설치 하는 방법을 제공 합니다. 대체 패키지 폴더는 전역 패키지 폴더와 정확히 같은 폴더 및 파일 구조를 포함 합니다. *. nupkg* 가 있고 모든 파일이 추출 됩니다.

이 구성에 대 한 조회 논리는 다음과 같습니다.

- 전역 패키지 폴더를 확인 하 여 패키지/버전이 이미 다운로드 되었는지 확인 합니다.

- 대체 폴더에서 패키지/버전 일치를 확인 합니다.

조회 중 하나가 성공 하면 다운로드가 필요 하지 않습니다.

일치 항목을 찾을 수 없는 경우 NuGet은 파일 원본 및 http 원본을 확인 한 다음 패키지를 다운로드 합니다.

| 키 | 값 |
| --- | --- |
| (대체 폴더 이름) | 대체 폴더의 경로입니다. |

**예제**:

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>packageManagement 섹션

*packages.config* 또는 PackageReference의 기본 패키지 관리 형식을 설정 합니다. SDK 스타일 프로젝트는 항상 PackageReference을 사용 합니다.

| 키 | 값 |
| --- | --- |
| format | 기본 패키지 관리 형식을 나타내는 부울입니다. 이면 `1` format은 PackageReference입니다. 이면 `0` format이 *packages.config* 됩니다. |
| disabled | 첫 번째 패키지를 설치할 때 기본 패키지 형식을 선택 하 라는 메시지를 표시할지 여부를 나타내는 부울입니다. `False` 프롬프트를 숨깁니다. |

**예제**:

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a>환경 변수 사용

`nuget.config` 값(NuGet 3.4 이상)의 환경 변수를 사용하여 런타임에 설정을 적용할 수 있습니다.

예를 들어 Windows의 `HOME` 환경 변수가 `c:\users\username`으로 설정되면 구성 파일의 `%HOME%\NuGetRepository` 값이 `c:\users\username\NuGetRepository`로 해석됩니다.

Windows 스타일 환경 변수를 사용 해야 합니다 (시작 및 종료%). Mac/Linux 에서도 마찬가지입니다. `$HOME/NuGetRepository`구성 파일에 있는 것은 확인 되지 않습니다. Mac/Linux에서 값은 `%HOME%/NuGetRepository` 로 확인 됩니다 `/home/myStuff/NuGetRepository` .

환경 변수가 없으면 NuGet에서 구성 파일의 리터럴 값을 사용합니다. 예를 들어 다음 `%MY_UNDEFINED_VAR%/NuGetRepository` 으로 확인 됩니다. `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`

다음 표에서는 NuGet.Config 파일에 대 한 환경 변수 구문 및 경로 구분 기호 지원을 보여 줍니다.

### <a name="nugetconfig-environment-variable-support"></a>NuGet.Config 환경 변수 지원

| Syntax | Dir 구분 기호 | Windows nuget.exe | Windows dotnet.exe | Mac nuget.exe (Mono) | Mac dotnet.exe |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | 예 | 예 | 예 | 예 |
| `%MY_VAR%` | `\`  | 예 | 예 | 예 | 예 |
| `$MY_VAR` | `/`  | 예 | 예 | 예 | 예 |
| `$MY_VAR` | `\`  | 예 | 예 | 예 | 예 |


## <a name="example-config-file"></a>config 파일 예제

다음은 `nuget.config` 선택적 항목을 비롯 한 다양 한 설정을 보여 주는 예제 파일입니다.

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
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
