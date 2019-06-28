---
title: nuget.config 파일 참조
description: config, bindingRedirects, packageRestore, solution 및 packageSource 섹션이 포함된 NuGet.Config 파일 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: 2eceb6e94a353cb29b83aea114c6cea2acbac266
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426156"
---
# <a name="nugetconfig-reference"></a>nuget.config 참조

NuGet 동작은 다른 설정에 의해 제어 됩니다 `NuGet.Config` 파일에 설명 된 대로 [일반적인 NuGet 구성](../consume-packages/configuring-nuget-behavior.md)합니다.

`nuget.config`는 최상위 `<configuration>` 노드를 포함하는 XML 파일이며, 이 파일에는 이 항목에서 설명하는 섹션 요소가 포함되어 있습니다. 각 섹션에는 0 개 이상의 항목이 포함 됩니다. [config 파일 예제](#example-config-file)를 참조하세요. 설정 이름은 대/소문자를 구분하지 않으며, 값에는 [환경 변수](#using-environment-variables)를 사용할 수 있습니다.

항목 내용:

- [config 섹션](#config-section)
- [bindingRedirects 섹션](#bindingredirects-section)
- [packageRestore 섹션](#packagerestore-section)
- [solution 섹션](#solution-section)
- [패키지 원본 섹션](#package-source-sections):
  - [packageSources](#packagesources)
  - [packageSourceCredentials](#packagesourcecredentials)
  - [apikeys](#apikeys)
  - [disabledPackageSources](#disabledpackagesources)
  - [activePackageSource](#activepackagesource)
- [trustedSigners 섹션](#trustedsigners-section)
- [환경 변수 사용](#using-environment-variables)
- [config 파일 예제](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>config 섹션

[`nuget config` 명령](../tools/cli-ref-config.md)을 사용하여 설정할 수 있는 기타 구성 설정을 포함합니다.

`dependencyVersion` 및 `repositoryPath` 사용 하 여 프로젝트에만 적용 `packages.config`합니다. `globalPackagesFolder` PackageReference 형식을 사용 하 여 프로젝트에만 적용 됩니다.

| Key | 값 |
| --- | --- |
| dependencyVersion(`packages.config`만) | `-DependencyVersion` 스위치가 직접 지정되지 않은 경우 패키지 설치, 복원 및 업데이트에 대한 기본 `DependencyVersion` 값입니다. 이 값은 NuGet 패키지 관리자 UI에서도 사용됩니다. 값은 `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`입니다. |
| globalPackagesFolder (프로젝트만 PackageReference를 사용 하 여) | 기본 전역 패키지 폴더의 위치입니다. 기본값은 `%userprofile%\.nuget\packages`(Windows) 또는 `~/.nuget/packages`(Mac/Linux)입니다. 상대 경로는 프로젝트별 `nuget.config` 파일에서 사용할 수 있습니다. NUGET_PACKAGES 환경 변수로 우선 순위를 사용 하는이 설정이 무시 됩니다. |
| repositoryPath(`packages.config`만) | 기본 `$(Solutiondir)/packages` 폴더 대신 NuGet 패키지를 설치할 위치입니다. 상대 경로는 프로젝트별 `nuget.config` 파일에서 사용할 수 있습니다. NUGET_PACKAGES 환경 변수로 우선 순위를 사용 하는이 설정이 무시 됩니다. |
| defaultPushSource | 작업에 대한 다른 패키지 원본이 없을 때 기본값으로 사용해야 하는 패키지 원본의 URL 또는 경로를 식별합니다. |
| http_proxy, http_proxy.user, http_proxy.password, no_proxy | 패키지 원본에 연결할 때 사용할 프록시 설정입니다. `http_proxy`는 `http://<username>:<password>@<domain>` 형식이어야 합니다. 암호는 암호화되어 있으며, 수동으로 추가할 수 없습니다. `no_proxy`의 경우 값은 프록시 서버를 우회하는 도메인의 쉼표로 구분된 목록입니다. 이러한 값에 대해 http_proxy 및 no_proxy 환경 변수를 번갈아 사용할 수 있습니다. 자세한 내용은 [NuGet 프록시 설정](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)(skolima.blogspot.com)을 참조하세요. |
| signatureValidationMode | 패키지 설치에 대 한 패키지 서명을 확인 하 고 복원 하는 데 사용 하는 유효성 검사 모드를 지정 합니다. 값은 `accept`, `require`합니다. 기본값은 `accept`입니다.

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

합니다 `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`를 `disabledPackageSources` 및 `trustedSigners` 함께 설치, 복원 및 업데이트 작업 중 NuGet 패키지 리포지토리와 함께 작동 하는 방법을 구성 하는 모든 작업입니다.

합니다 [ `nuget sources` 명령](../tools/cli-ref-sources.md) 는 일반적으로 이러한 설정을 제외 하 고 관리 하는 데 사용 됩니다 `apikeys` 사용 하 여 관리 되는 합니다 [ `nuget setapikey` 명령](../tools/cli-ref-setapikey.md), 및 `trustedSigners` 관리 되는 사용 하 여 [ `nuget trusted-signers` 명령](../tools/cli-ref-trusted-signers.md)입니다.

nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.

### <a name="packagesources"></a>packageSources

알려진 모든 패키지 원본을 나열합니다. PackageReference 형식을 사용 하 여 모든 프로젝트와 복원 작업 중에 순서는 무시 됩니다. NuGet 소스 순서가 설치에 대 한 준수 및 업데이트 작업을 사용 하 여 프로젝트를 사용 하 여 `packages.config`입니다.

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

[`nuget setapikey` 명령](../tools/cli-ref-setapikey.md)으로 설정된 대로 API 키 인증을 사용하는 원본에 대한 키를 저장합니다.

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
## <a name="trustedsigners-section"></a>trustedSigners 섹션

저장소를 설치 하거나 복원 하는 동안 패키지를 허용 하는 데 사용 되는 서명자를 신뢰할 수 있습니다. 사용자 설정 하는 경우이 목록은 비워 둘 수 없습니다 `signatureValidationMode` 에 `require`입니다. 

이 섹션을 사용 하 여 업데이트할 수는 [ `nuget trusted-signers` 명령](../tools/cli-ref-trusted-signers.md)입니다.

**스키마**:

신뢰할 수 있는 서명자가 컬렉션인 `certificate` 지정 된 서명자를 식별 하는 모든 인증서를 등록 하는 항목입니다. 신뢰할 수 있는 서명자가 될 수 있습니다는 `Author` 또는 `Repository`합니다.

신뢰할 수 있는 *리포지토리* 도 지정 합니다 `serviceIndex` 리포지토리에 대 한 (유효한에 있는 `https` uri)는 세미콜론으로 구분 된 목록에 지정할 수 있습니다 및 `owners` 신뢰할 수 있는 누가 더욱 제한 하려면 해당 특정 리포지토리입니다.

인증서 지문에 사용 되는 지원 되는 해시 알고리즘은 `SHA256`하십시오 `SHA384` 및 `SHA512`합니다.

경우는 `certificate` 지정 `allowUntrustedRoot` 으로 `true` 서명 확인의 일부로 인증서 체인을 빌드하는 동안 지정 된 인증서 체인을 신뢰할 수 없는 루트에 허용 됩니다.

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
