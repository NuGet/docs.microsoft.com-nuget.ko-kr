---
title: nuget .config 파일 참조
description: config, bindingRedirects, packageRestore, solution 및 packageSource 섹션이 포함된 NuGet.Config 파일 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: a2955617b899bfadab42d1ae98dd20c8fc6ddca9
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020043"
---
# <a name="nugetconfig-reference"></a>nuget.exe 참조

Nuget 동작은 [일반적인 nuget 구성](../consume-packages/configuring-nuget-behavior.md)에 설명 된 `NuGet.Config` 대로 다른 파일의 설정에 의해 제어 됩니다.

`nuget.config`는 최상위 `<configuration>` 노드를 포함하는 XML 파일이며, 이 파일에는 이 항목에서 설명하는 섹션 요소가 포함되어 있습니다. 각 섹션에는 0 개 이상의 항목이 포함 되어 있습니다. [config 파일 예제](#example-config-file)를 참조하세요. 설정 이름은 대/소문자를 구분하지 않으며, 값에는 [환경 변수](#using-environment-variables)를 사용할 수 있습니다.

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>config 섹션

[`nuget config` 명령](../reference/cli-reference/cli-ref-config.md)을 사용하여 설정할 수 있는 기타 구성 설정을 포함합니다.

`dependencyVersion`및 `repositoryPath` 는를 사용 하 `packages.config`는 프로젝트에만 적용 됩니다. `globalPackagesFolder`PackageReference 형식을 사용 하는 프로젝트에만 적용 됩니다.

| Key | 값 |
| --- | --- |
| dependencyVersion(`packages.config`만) | `-DependencyVersion` 스위치가 직접 지정되지 않은 경우 패키지 설치, 복원 및 업데이트에 대한 기본 `DependencyVersion` 값입니다. 이 값은 NuGet 패키지 관리자 UI에서도 사용됩니다. 값은 `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`입니다. |
| globalPackagesFolder (PackageReference만 사용 하는 프로젝트) | 기본 전역 패키지 폴더의 위치입니다. 기본값은 `%userprofile%\.nuget\packages`(Windows) 또는 `~/.nuget/packages`(Mac/Linux)입니다. 상대 경로는 프로젝트별 `nuget.config` 파일에서 사용할 수 있습니다. 이 설정은 NUGET_PACKAGES 환경 변수에 의해 재정의 되며이는 우선적으로 적용 됩니다. |
| repositoryPath(`packages.config`만) | 기본 `$(Solutiondir)/packages` 폴더 대신 NuGet 패키지를 설치할 위치입니다. 상대 경로는 프로젝트별 `nuget.config` 파일에서 사용할 수 있습니다. 이 설정은 NUGET_PACKAGES 환경 변수에 의해 재정의 되며이는 우선적으로 적용 됩니다. |
| defaultPushSource | 작업에 대한 다른 패키지 원본이 없을 때 기본값으로 사용해야 하는 패키지 원본의 URL 또는 경로를 식별합니다. |
| http_proxy, http_proxy.user, http_proxy.password, no_proxy | 패키지 원본에 연결할 때 사용할 프록시 설정입니다. `http_proxy`는 `http://<username>:<password>@<domain>` 형식이어야 합니다. 암호는 암호화되어 있으며, 수동으로 추가할 수 없습니다. `no_proxy`의 경우 값은 프록시 서버를 우회하는 도메인의 쉼표로 구분된 목록입니다. 이러한 값에 대해 http_proxy 및 no_proxy 환경 변수를 번갈아 사용할 수 있습니다. 자세한 내용은 [NuGet 프록시 설정](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)(skolima.blogspot.com)을 참조하세요. |
| signatureValidationMode | 패키지 설치 및 복원에 대 한 패키지 서명을 확인 하는 데 사용 되는 유효성 검사 모드를 지정 합니다. 값은 `accept`, `require`입니다. 기본값은 `accept`입니다.

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

| Key | 값 |
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

| Key | 값 |
| --- | --- |
| 사용 | NuGet에서 자동 복원을 수행할 수 있는지 여부를 나타내는 부울입니다. config 파일에서 이 키를 설정하는 대신 `EnableNuGetPackageRestore` 환경 변수를 `True` 값으로 설정할 수도 있습니다. |
| 자동 | NuGet에서 빌드하는 동안 누락된 패키지를 확인해야 하는지 여부를 나타내는 부울입니다. |

**예제**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>solution 섹션

솔루션의 `packages` 폴더가 원본 제어에 포함되는지 여부를 제어합니다. 이 섹션은 솔루션 폴더의 `nuget.config` 파일에서만 작동합니다.

| Key | 값 |
| --- | --- |
| disableSourceControlIntegration | 원본 제어로 작업할 때 패키지 폴더를 무시할지 여부를 나타내는 부울입니다. 기본값은 false입니다. |

**예제**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>패키지 원본 섹션

`packageSources` ,`packageSourceCredentials`, ,`trustedSigners` 및는 모두 함께 작동 하 여 설치, 복원 및 업데이트 작업 중에 NuGet이 패키지 리포지토리와 함께 작동 하는 방식을 구성 합니다. `activePackageSource` `apikeys` `disabledPackageSources`

`apikeys` `trustedSigners` [명령은 명령을 사용`nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md)하 여 관리 되 고 [명령을 `nuget trusted-signers` ](../reference/cli-reference/cli-ref-trusted-signers.md)사용 하 여 관리 되는를 제외 하 고는 일반적으로 이러한 설정을 관리 하는 데 사용 됩니다. [ `nuget sources` ](../reference/cli-reference/cli-ref-sources.md)

nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.

### <a name="packagesources"></a>packageSources

알려진 모든 패키지 원본을 나열합니다. PackageReference 형식을 사용 하는 모든 프로젝트와 복원 작업 중에 순서는 무시 됩니다. NuGet은를 사용 하 여 `packages.config`프로젝트에 대 한 설치 및 업데이트 작업의 소스 순서를 고려 합니다.

| Key | 값 |
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

### <a name="packagesourcecredentials"></a>packageSourceCredentials

원본에 대한 사용자 이름과 암호를 저장하며, 일반적으로 `nuget sources`와 함께 `-username` 및 `-password` 스위치로 지정됩니다. 또한 `-storepasswordincleartext` 옵션을 사용하지 않는 한 암호는 기본적으로 암호화됩니다.

| Key | 값 |
| --- | --- |
| 사용자 이름 | 일반 텍스트 형식의 원본에 대한 사용자 이름입니다. |
| password | 원본에 대한 암호화된 암호입니다. |
| cleartextpassword | 원본에 대한 암호화되지 않은 암호입니다. |

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

### <a name="apikeys"></a>apikeys

[`nuget setapikey` 명령](../reference/cli-reference/cli-ref-setapikey.md)으로 설정된 대로 API 키 인증을 사용하는 원본에 대한 키를 저장합니다.

| Key | 값 |
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

| Key | 값 |
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

| Key | 값 |
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

설치 또는 복원 중 패키지를 허용 하는 데 사용 되는 신뢰할 수 있는 서명자를 저장 합니다. 사용자가로 설정 `signatureValidationMode` 된 경우에 `require`는이 목록을 비워 둘 수 없습니다. 

이 섹션은 [ `nuget trusted-signers` 명령을](../reference/cli-reference/cli-ref-trusted-signers.md)사용 하 여 업데이트할 수 있습니다.

**스키마**:

신뢰할 수 있는 서명자는 지정 된 `certificate` 서명자를 식별 하는 모든 인증서를 등록 하는 항목의 컬렉션을 포함 합니다. 신뢰할 수 있는 서명자는 `Author` `Repository`또는 일 수 있습니다.

또한 신뢰할 수 있는 *리포지토리* 는 `serviceIndex` 유효한 `https` uri 여야 하는 리포지토리에 대 한을 지정 하 고, 선택적으로 세미콜론으로 구분 된 목록을 `owners` 지정 하 여 해당 특정에서 신뢰할 수 있는 사용자를 제한할 수 있습니다. 리포지토리로.

인증서 지문에 사용 되는 지원 되는 해시 `SHA256`알고리즘 `SHA384` 은 `SHA512`, 및입니다.

가 `certificate` 서명 확인의 `true` 일부로 인증서 체인을 빌드하는 동안 지정 된 인증서를 신뢰할 수 없는 루트에 체인으로 연결할 수 있는 것으로 지정 `allowUntrustedRoot` 하면입니다.

**예제**:

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

## <a name="fallbackpackagefolders-section"></a>fallbackPackageFolders 섹션

*(3.5 +)* 는 패키지가 대체 폴더에 있는 경우 작업을 수행 하지 않아도 되도록 패키지를 사전 설치 하는 방법을 제공 합니다. 대체 패키지 폴더는 전역 패키지 폴더와 정확히 같은 폴더 및 파일 구조를 포함 합니다. *. nupkg* 가 있고 모든 파일이 추출 됩니다.

이 구성에 대 한 조회 논리는 다음과 같습니다.

- 전역 패키지 폴더를 확인 하 여 패키지/버전이 이미 다운로드 되었는지 확인 합니다.

- 대체 폴더에서 패키지/버전 일치를 확인 합니다.

조회 중 하나가 성공 하면 다운로드가 필요 하지 않습니다.

일치 항목을 찾을 수 없는 경우 NuGet은 파일 원본 및 http 원본을 확인 한 다음 패키지를 다운로드 합니다.

| Key | 값 |
| --- | --- |
| (대체 폴더 이름) | 대체 폴더의 경로입니다. |

**예제**:

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>packageManagement 섹션

기본 패키지 관리 형식 (PackageReference 또는 )을 설정 합니다. SDK 스타일 프로젝트는 항상 PackageReference을 사용 합니다.

| Key | 값 |
| --- | --- |
| 형식 | 기본 패키지 관리 형식을 나타내는 부울입니다. 이면 `1`format은 PackageReference입니다. 인 `0`경우 format은 *패키지인*입니다. |
| 비활성화됨 | 첫 번째 패키지를 설치할 때 기본 패키지 형식을 선택 하 라는 메시지를 표시할지 여부를 나타내는 부울입니다. `False`프롬프트를 숨깁니다. |

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

마찬가지로, Mac/Linux의 `HOME`이 `/home/myStuff`로 설정되면 구성 파일의 `%HOME%/NuGetRepository`가 `/home/myStuff/NuGetRepository`로 해석됩니다.

환경 변수가 없으면 NuGet에서 구성 파일의 리터럴 값을 사용합니다.

## <a name="example-config-file"></a>config 파일 예제

아래는 몇 가지 설정을 보여 주는 `nuget.config` 파일의 예제입니다.

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
