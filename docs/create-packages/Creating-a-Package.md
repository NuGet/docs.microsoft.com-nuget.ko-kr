---
title: NuGet 패키지를 만드는 방법
description: 파일 및 버전 관리와 같은 주요 결정 사항을 포함하여 NuGet 패키지를 디자인하고 만드는 과정을 자세히 안내합니다.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: e3a40a521a3b16d9757ef1bbf2511a1537d8bddb
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425812"
---
# <a name="creating-nuget-packages"></a>NuGet 패키지 만들기

패키지의 기능 또는 포함된 코드와 관계없이 CLI 도구인 `nuget.exe` 또는 `dotnet.exe`를 사용하여 해당 기능을 임의 수의 다른 개발자와 공유하고 사용할 수 있는 구성 요소로 패키지할 수 있습니다. NuGet CLI 도구를 설치하려면 [NuGet 클라이언트 도구 설치](../install-nuget-client-tools.md)를 참조하세요. Visual Studio에는 CLI 도구가 자동으로 포함되지 않습니다.

- SDK 스타일 형식([SDK 특성](/dotnet/core/tools/csproj#additions))을 사용하는 .NET Core 및 .NET Standard 프로젝트와 또 다른 SDK 스타일 프로젝트의 경우, NuGet은 프로젝트 파일의 정보를 직접 사용하여 패키지를 만듭니다. 자세한 내용은 [Visual Studio를 사용하여 .NET Standard 패키지 만들기](../quickstart/create-and-publish-a-package-using-visual-studio.md) 및 [MSBuild 대상으로서의 NuGet pack 및 restore](../reference/msbuild-targets.md)를 참조하세요.

- SDK 스타일이 아닌 프로젝트의 경우에는 이 문서에 설명된 단계에 따라 패키지를 만듭니다.

- `packages.config`에서 [PackageReference](../consume-packages/package-references-in-project-files.md)로 마이그레이션된 프로젝트의 경우에는 [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)를 사용합니다.

엄밀히 말해, NuGet 패키지는 `.nupkg` 확장명으로 이름이 변경되고 내용이 특정 규칙과 일치하는 ZIP 파일입니다. 규칙을 충족하는 패키지를 만드는 자세한 프로세스에 대해 설명합니다. 집중적인 연습에 대해서는 [빠른 시작: 패키지 만들기 및 게시](../quickstart/create-and-publish-a-package.md)를 참조하세요.

패키징은 패키지로 전달하려는 컴파일된 코드(어셈블리), 기호 및/또는 기타 파일로 시작됩니다([개요 및 워크플로](overview-and-workflow.md) 참조). 이 프로세스는 프로젝트 파일의 정보에서 끌어오기를 사용하여 컴파일된 어셈블리 및 패키지를 동기화된 상태로 유지할 수 있지만, 패키지에 포함된 파일을 컴파일하거나 생성하는 프로세스와는 관련이 없습니다.

> [!Note]
> 이 항목은 SDK 스타일이 아닌 프로젝트 즉, 일반적으로 Visual Studio 2017 이상 버전 및 NuGet 4.0+를 사용하는 .NET Core 및 .NET Standard 프로젝트가 아닌 프로젝트에 적용됩니다.

## <a name="deciding-which-assemblies-to-package"></a>패키지할 어셈블리 결정

가장 일반적인 용도의 패키지에는 다른 개발자가 자신의 프로젝트에서 사용할 수 있는 하나 이상의 어셈블리가 포함되어 있습니다.

- 일반적으로 각 어셈블리가 독립적으로 유용한 경우 NuGet 패키지당 하나의 어셈블리가 있는 것이 가장 좋습니다. 예를 들어 `Parser.dll`에 종속된 `Utilities.dll`이 있고 `Parser.dll`이 자체적으로 유용할 경우 각각에 대해 하나의 패키지를 만듭니다. 이렇게 하면 개발자가 `Utilities.dll`과는 독립적으로 `Parser.dll`을 사용할 수 있습니다.

- 라이브러리가 독립적으로 유용하지 않은 여러 어셈블리로 구성된 경우 이를 하나의 패키지로 결합하는 것이 좋습니다. 앞의 예제를 사용하여 `Utilities.dll`에서만 사용되는 코드가 `Parser.dll`에 포함된 경우 동일한 패키지에 `Parser.dll`을 유지하는 것이 좋습니다.

- 마찬가지로, `Utilities.dll`이 `Utilities.resources.dll`에 종속되고 후자가 자체적으로 유용하지 않은 경우 두 라이브러리를 모두 동일한 패키지에 넣습니다.

실제로 리소스는 특별한 경우입니다. 패키지가 프로젝트에 설치되면 어셈블리 참조가 지역화된 위성 어셈블리로 간주되므로 NuGet은 `.resources.dll`이라는 DLL을 *제외한* 패키지의 DLL에 해당 어셈블리 참조를 자동으로 추가합니다([지역화된 패키지 만들기](creating-localized-packages.md) 참조). 이러한 이유로 다른 경우에 필수 패키지 코드가 포함되는 파일에는 `.resources.dll`을 사용하지 마세요.

라이브러리에 COM interop 어셈블리가 포함되어 있으면 [COM interop 어셈블리가 포함된 패키지 제작](#authoring-packages-with-com-interop-assemblies)의 지침을 추가로 수행하세요.

## <a name="the-role-and-structure-of-the-nuspec-file"></a>.nuspec 파일의 역할 및 구조

패키지하려는 파일을 알고 있으면 다음 단계는 `.nuspec` XML 파일에 패키지 매니페스트를 만드는 것입니다.

매니페스트:

1. 패키지의 내용을 설명하며 패키지에 직접 포함됩니다.
1. 패키지를 만들도록 구동하고 프로젝트에 해당 패키지를 설치하는 방법을 NuGet에 지시합니다. 예를 들어 매니페스트는 다른 패키지 종속성을 식별하여 NuGet에서 기본 패키지를 설치할 때 해당 종속성을 설치할 수도 있습니다.
1. 아래에서 설명한 대로 필수 및 선택적 속성을 모두 포함합니다. 여기서 언급하지 않은 다른 속성을 포함하여 정확한 세부 정보는 [.nuspec 참조](../reference/nuspec.md)를 참조하세요.

필수 속성:

- 패키지를 호스팅하는 갤러리에서 고유해야 하는 패키지 식별자
- *Major.Minor.Patch[-Suffix]* 형식의 특정 버전 번호(여기서 *-Suffix*는 [시험판 버전](prerelease-packages.md)을 식별함)
- 호스트에 표시되어야 하는 패키지 제목(예: nuget.org)
- 작성자 및 소유자 정보
- 패키지에 대한 자세한 설명

선택적 일반 속성:

- 릴리스 정보
- 저작권 정보
- [Visual Studio의 패키지 관리자 UI](../tools/package-manager-ui.md)에 대한 간단한 설명
- 로캘 ID
- 프로젝트 URL
- 라이선스(식 또는 파일로 사용)(`licenseUrl`은 사용되지 않으며, [`license`nusec 메타데이터 요소](../reference/nuspec.md#license)를 사용함)
- 아이콘 URL
- 종속성 및 참조 목록
- 갤러리 검색을 지원하는 태그

다음은 속성을 설명하는 주석이 포함된 가상의 일반적인 `.nuspec` 파일입니다.

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

종속성 선언 및 버전 번호 지정에 대한 자세한 내용은 [패키지 버전 관리](../reference/package-versioning.md)를 참조하세요. `dependency` 요소의 `include` 및 `exclude` 특성을 사용하여 패키지에 종속성의 자산을 직접 공개할 수도 있습니다. [.nuspec 참조 - 종속성](../reference/nuspec.md#dependencies)을 참조하세요.

매니페스트는 이 매니페스트에서 만든 패키지에 포함되어 있으므로 기존 패키지를 검사하여 임의 개수의 추가 예제를 찾을 수 있습니다. 좋은 소스는 컴퓨터에 있는 *global-packages* 폴더이며, 해당 위치는 다음 명령으로 반환됩니다.

```cli
nuget locals -list global-packages
```

*package\version* 폴더로 이동하여 `.nupkg` 파일을 `.zip` 파일에 복사한 다음, 해당 `.zip` 파일을 열고 그 안에 있는 `.nuspec` 파일을 검사합니다.

> [!Note]
> Visual Studio 프로젝트에서 `.nuspec`을 만드는 경우 패키지를 빌드할 때 프로젝트의 정보로 대체되는 토큰이 매니페스트에 포함됩니다. [Visual Studio 프로젝트에서 .nuspec 만들기](#from-a-visual-studio-project)를 참조하세요.

## <a name="creating-the-nuspec-file"></a>.nuspec 파일 만들기

완전한 매니페스트를 만드는 것은 일반적으로 다음 방법 중 하나를 통해 생성된 기본 `.nuspec` 파일로 시작합니다.

- [규칙 기반 작업 디렉터리](#from-a-convention-based-working-directory)
- [어셈블리 DLL](#from-an-assembly-dll)
- [Visual Studio 프로젝트](#from-a-visual-studio-project)    
- [기본값이 있는 새 파일](#new-file-with-default-values)

그런 다음 최종 패키지에 원하는 정확한 내용을 설명하도록 파일을 직접 편집합니다.

> [!Important]
> 생성된 `.nuspec` 파일에는 `nuget pack` 명령을 사용하여 패키지를 만들기 전에 수정해야 하는 자리 표시자가 포함되어 있습니다. `.nuspec`에 자리 표시자가 있으면 이 명령이 실패합니다.

### <a name="from-a-convention-based-working-directory"></a>원본: 규칙 기반 작업 디렉터리

NuGet 패키지는 `.nupkg` 확장명으로 이름이 바뀐 ZIP 파일일 뿐이므로 로컬 파일 시스템에서 원하는 폴더 구조를 만든 다음, 해당 구조에서 `.nuspec` 파일을 직접 만드는 것이 가장 쉽습니다. 그런 다음, `nuget pack` 명령은 해당 폴더 구조의 모든 파일을 자동으로 추가합니다(동일한 구조의 개인 파일을 유지할 수 있도록 `.`로 시작하는 폴더는 제외함).

이 방식의 장점은 이 항목의 뒷부분에서 설명한 대로 패키지에 포함하려는 파일을 매니페스트에 지정할 필요가 없다는 것입니다. 빌드 프로세스에서 패키지로 이동하는 정확한 폴더 구조를 생성하기만 하면 되고, 그렇지 않은 경우 프로젝트의 일부가 아닌 다른 파일을 쉽게 포함할 수 있습니다.

- 대상 프로젝트에 삽입해야 하는 콘텐츠 및 소스 코드
- PowerShell 스크립트
- 프로젝트의 기존 구성 및 소스 코드 파일로의 변환

폴더 규칙은 다음과 같습니다.

| 폴더 | 설명 | 패키지 설치 시의 작업 |
| --- | --- | --- |
| (루트) | readme.txt에 대한 위치 | 패키지를 설치할 때 Visual Studio에서 패키지 루트에 readme.txt 파일을 표시합니다. |
| lib/{tfm} | 지정된 TFM(대상 프레임워크 모니커)에 대한 어셈블리(`.dll`), 문서(`.xml`) 및 기호(`.pdb`) 파일 | 어셈블리는 컴파일 및 런타임에 대한 참조로 추가됩니다. `.xml` 및 `.pdb`는 프로젝트 폴더에 복사됩니다. 프레임워크 대상 특정의 하위 폴더를 만들려면 [여러 대상 프레임워크 지원](supporting-multiple-target-frameworks.md)을 참조하세요. |
| ref/{tfm} | 지정된 TFM(대상 프레임워크 모니커)에 대한 어셈블리(`.dll`) 및 기호(`.pdb`) 파일 | 어셈블리는 컴파일 시간에 대한 참조로만 추가됩니다. 따라서 프로젝트 bin 폴더에 아무것도 복사되지 않습니다. |
| runtimes | 아키텍처 특정 어셈블리(`.dll`), 기호(`.pdb`) 및 네이티브 리소스(`.pri`) 파일 | 어셈블리는 런타임에 대한 참조로만 추가되고, 다른 파일은 프로젝트 폴더에 복사됩니다. 해당 컴파일 시간 어셈블리를 제공하려면 항상 `/ref/{tfm}` 폴더 아래에 해당하는 (TFM) `AnyCPU` 특정 어셈블리가 있어야 합니다. [여러 대상 프레임워크 지원](supporting-multiple-target-frameworks.md)을 참조하세요. |
| 내용 | 임의 파일 | 콘텐츠가 프로젝트 루트에 복사됩니다. **content** 폴더를 궁극적으로 패키지를 사용하는 대상 애플리케이션의 루트로 간주합니다. 패키지에서 애플리케이션의 */images* 폴더에 이미지를 추가하도록 하려면 패키지의 *content/images* 폴더에 배치합니다. |
| 빌드 | MSBuild `.targets` 및 `.props` 파일 | 프로젝트 파일 또는 `project.lock.json`(NuGet 3.x 이상)에 자동으로 삽입됩니다. |
| 도구 | 패키지 관리자 콘솔에서 액세스할 수 있는 Powershell 스크립트 및 프로그램 | `tools` 폴더는 패키지 관리자 콘솔에 대한 `PATH` 환경 변수에만 추가 됩니다(특히 프로젝트를 빌드할 때는 MSBuild에 설정한 대로 `PATH`에 *추가되지 않음*). |

폴더 구조에는 임의 개수의 대상 프레임워크에 대해 임의 개수의 어셈블리가 포함될 수 있으므로, 이 방법은 여러 프레임워크를 지원하는 패키지를 만들 때 필요합니다.

어떤 경우이든 원하는 폴더 구조를 배치한 후에는 해당 폴더에서 다음 명령을 실행하여 `.nuspec` 파일을 만듭니다.

```cli
nuget spec
```

또 다시 말하지만, 생성된 `.nuspec`에는 폴더 구조의 파일에 대한 명시적 참조가 없습니다. NuGet은 패키지를 만들 때 자동으로 모든 파일을 포함합니다. 그러나 매니페스트의 다른 부분에서 자리 표시자 값을 편집해야 합니다.

### <a name="from-an-assembly-dll"></a>원본 : 어셈블리 DLL

어셈블리에서 패키지를 만드는 간단한 경우 다음 명령을 사용하여 어셈블리의 메타데이터에서 `.nuspec` 파일을 생성할 수 있습니다.

```cli
nuget spec <assembly-name>.dll
```

이 형식을 사용하면 매니페스트의 몇 가지 자리 표시자를 어셈블리의 특정 값으로 바꿉니다. 예를 들어 `<id>` 속성은 어셈블리 이름으로 설정되고, `<version>`은 어셈블리 버전으로 설정됩니다. 그러나 매니페스트의 다른 속성은 어셈블리의 값과 일치하지 않으므로 여전히 자리 표시자를 포함하고 있습니다.

### <a name="from-a-visual-studio-project"></a>원본: Visual Studio 프로젝트

`.csproj` 또는 `.vbproj` 파일에서 `.nuspec`을 만드는 것은 프로젝트에 설치된 다른 패키지가 자동으로 종속성으로 참조되기 때문에 편리합니다. 프로젝트 파일과 동일한 폴더에서 다음 명령을 사용하기만 하면 됩니다.

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

결과 `<project-name>.nuspec` 파일에는 패키지 시간에 프로젝트의 값(이미 설치된 다른 패키지에 대한 참조 포함)으로 대체되는 *토큰*이 포함됩니다.

토큰은 프로젝트 속성의 양쪽에 `$` 기호로 구분됩니다. 예를 들어 이 방식으로 생성된 매니페스트의 `<id>` 값은 일반적으로 다음과 같이 나타납니다.

```xml
<id>$id$</id>
```

이 토큰은 패키지 시간에 프로젝트 파일의 `AssemblyName` 값으로 바뀝니다. `.nuspec` 토큰에 대한 프로젝트 값의 정확한 매핑은 [대체 토큰 참조](../reference/nuspec.md#replacement-tokens)를 참조하세요.

토큰을 사용하면 프로젝트를 업데이트할 때 `.nuspec`의 버전 번호와 같은 중요한 값을 업데이트할 필요가 없습니다. (원하는 경우 언제든지 토큰을 리터럴 값으로 바꿀 수 있습니다.) 

뒤에 나오는 [nuget pack을 실행하여 .nupkg 파일 생성](#running-nuget-pack-to-generate-the-nupkg-file)에서 설명한 대로 Visual Studio 프로젝트에서 작업할 때 사용할 수 있는 몇 가지 추가 패키징 옵션이 있습니다.

#### <a name="solution-level-packages"></a>솔루션 수준 패키지

*NuGet 2.x에만 해당, NuGet 3.0 이상에서는 사용할 수 없음*

NuGet 2.x는 패키지 관리자 콘솔(`tools` 폴더의 콘텐츠)용 도구 또는 추가 명령을 설치하는 솔루션 수준 패키지에 대한 개념을 지원하지만, 솔루션의 어떠한 프로젝트에도 참조, 콘텐츠 또는 빌드 사용자 지정을 추가하지 않습니다. 이러한 패키지는 `lib`, `content` 또는 `build` 폴더에 파일을 직접 포함하지 않으며, 해당되는 어떤 종속성에도 해당 `lib`, `content` 또는 `build` 폴더의 파일이 없습니다.

NuGet은 설치된 솔루션 수준 패키지를 프로젝트의 `packages.config` 파일이 아닌 `.nuget` 폴더의 `packages.config` 파일에서 추적합니다.

### <a name="new-file-with-default-values"></a>기본값이 있는 새 파일

다음 명령은 자리 표시자를 사용하여 기본 매니페스트를 만들므로 적절한 파일 구조로 시작할 수 있습니다.

```cli
nuget spec [<package-name>]
```

\<package-name\>을 생략하면 결과 파일은 `Package.nuspec`입니다. `Contoso.Utility.UsefulStuff`와 같은 이름을 제공하면 파일은 `Contoso.Utility.UsefulStuff.nuspec`입니다.

결과 `.nuspec`에는 `projectUrl`과 같은 값에 대한 자리 표시자가 포함됩니다. 파일을 사용하기 전에 편집하여 최종 `.nupkg` 파일을 만들어야 합니다.

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a>고유한 패키지 식별자 선택 및 버전 번호 설정

패키지 식별자(`<id>` 요소)와 버전 번호(`<version>` 요소)는 패키지에 포함된 정확한 코드를 고유하게 식별하므로 매니페스트에서 가장 중요한 두 가지 값입니다.

**패키지 식별자에 대한 모범 사례:**

- **고유성**: 식별자는 nuget.org 또는 패키지를 호스팅하는 모든 갤러리에서 고유해야 합니다. 식별자를 결정하기 전에 해당 갤러리를 검색하여 해당 이름이 이미 사용 중인지 확인합니다. 충돌을 방지하기 위한 좋은 패턴은 회사 이름을 식별자의 첫 번째 부분(예: `Contoso.`)으로 사용하는 것입니다.
- **네임스페이스 형식의 이름**: 하이픈 대신 점 표기법을 사용하여 .NET의 네임스페이스와 비슷한 패턴을 따릅니다. 예를 들어 `Contoso-Utility-UsefulStuff` 또는 `Contoso_Utility_UsefulStuff` 대신 `Contoso.Utility.UsefulStuff`를 사용합니다. 패키지 식별자가 코드에 사용된 네임스페이스와 일치할 때 소비자가 이 형식의 이름이 유용하다는 것을 알게 됩니다.
- **샘플 패키지**: 다른 패키지를 사용하는 방법을 보여 주는 샘플 코드 패키지를 생성하는 경우 `Contoso.Utility.UsefulStuff.Sample`(와)과 같이 `.Sample`을(를) 접미사로 식별자에 붙입니다. (물론 샘플 패키지에는 다른 패키지에 대한 종속성이 있습니다.) 샘플 패키지를 만드는 경우 앞에서 설명한 규칙 기반 작업 디렉터리 방법을 사용합니다. `content` 폴더에서 `\Samples\Contoso.Utility.UsefulStuff.Sample`과 같이 `\Samples\<identifier>`라는 폴더에 샘플 코드를 정렬합니다.

**패키지 버전에 대한 모범 사례:**

- 일반적으로 반드시 필요한 것은 아니지만 라이브러리의 버전과 일치하도록 패키지의 버전을 설정합니다. 이는 앞서의 [패키지할 어셈블리 결정](#deciding-which-assemblies-to-package)에서 설명한 대로 패키지를 단일 어셈블리로 제한할 때의 간단한 문제입니다. 전반적으로 NuGet 자체는 종속성을 확인할 때 어셈블리 버전이 아니라 패키지 버전을 처리합니다.
- 비표준 버전 구성표를 사용하는 경우 [패키지 버전 관리](../reference/package-versioning.md)에서 설명한 대로 NuGet 버전 관리 규칙을 고려해야 합니다.

> 다음과 같은 일련의 간단한 블로그 게시물도 버전 관리를 이해하는 데 도움이 됩니다.
>
> - [1부: DLL 지옥에서 가져오기](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [2부: 핵심 알고리즘](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [3부: 바인딩 리디렉션을 통한 통합](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a>패키지 유형 설정

NuGet 3.5 이상을 사용하면 의도한 용도를 나타내기 위해 패키지를 특정 *패키지 유형*으로 표시할 수 있습니다. 이전 버전의 NuGet으로 만든 모든 패키지를 포함하여 유형으로 표시되지 않은 패키지의 기본값은 `Dependency` 유형입니다.

- `Dependency` 유형 패키지는 라이브러리 또는 애플리케이션에 빌드 시간 자산 또는 런타임 자산을 추가하며, 모든 프로젝트 형식에 설치할 수 있습니다(호환된다고 가정할 경우).

- `DotnetCliTool` 유형 패키지는 [.NET CLI](/dotnet/articles/core/tools/index)의 확장이며, 명령줄에서 호출됩니다. 이러한 패키지는 .NET Core 프로젝트에만 설치할 수 있으며 복원 작업에는 영향을 주지 않습니다. 이러한 프로젝트별 확장에 대한 자세한 내용은 [.NET Core 확장성](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) 설명서를 참조하세요.

- 사용자 지정 유형 패키지는 패키지 ID와 동일한 형식 규칙을 준수하는 임의 형식의 식별자를 사용합니다. 그러나 `Dependency` 및 `DotnetCliTool` 이외의 유형은 Visual Studio의 NuGet 패키지 관리자에서 인식되지 않습니다.

패키지 형식은 `.nuspec` 파일에 설정됩니다. 이전 버전과의 호환성에서 `Dependency` 유형을 명시적으로 *설정하지 않고*, 유형을 지정하지 않은 경우 이 유형을 가정하여 NuGet을 대신 사용하는 것이 가장 좋습니다.

- `.nuspec`: `<metadata>` 요소 아래의 `packageTypes\packageType` 노드 내에서 패키지 유형을 나타냅니다.

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a>추가 정보 및 기타 파일 추가

패키지에 포함할 파일을 직접 지정 하려면 `.nuspec` 파일에서 `<metadata>` 태그 *다음에 오는* `<files>` 노드를 사용합니다.

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> 규칙 기반 작업 디렉터리 방식을 사용하는 경우 패키지 루트에 readme.txt를 배치하고, `content` 폴더에는 다른 콘텐츠를 배치할 수 있습니다. 매니페스트에는 `<file>` 요소가 필요하지 않습니다.

패키지 루트에 `readme.txt`라는 파일이 포함되면 Visual Studio에서 패키지를 직접 설치한 직후 해당 파일의 내용을 일반 텍스트로 표시합니다. 종속성으로 설치된 패키지에는 추가 정보 파일이 표시되지 않습니다. 예를 들어 HtmlAgilityPack 패키지에 대한 추가 정보가 다음과 같이 표시됩니다.

![설치 시 NuGet 패키지에 대한 추가 정보 파일 표시](media/Create_01-ShowReadme.png)

> [!Note]
> `.nuspec` 파일에서 빈 `<files>` 노드가 포함되면 NuGet은 `lib` 폴더에 있는 것 이외의 다른 콘텐츠를 패키지에 포함하지 않습니다.

## <a name="including-msbuild-props-and-targets-in-a-package"></a>패키지에 MSBuild props 및 targets 포함

경우에 따라 패키지를 사용하는 프로젝트에 사용자 지정 빌드 대상 또는 속성(예: 빌드하는 동안 사용자 지정 도구 또는 프로세스 실행)을 추가할 수 있습니다. 이렇게 하려면 프로젝트의 `\build` 폴더 내에 `<package_id>.targets` 또는 `<package_id>.props`(예: `Contoso.Utility.UsefulStuff.targets`) 형식의 파일을 배치합니다.

루트 `\build` 폴더의 파일은 모든 대상 프레임워크에 적합한 파일로 간주됩니다. 프레임워크별 파일을 제공하려면 먼저 다음과 같이 적절한 하위 폴더 내에 배치합니다.

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

그런 다음 `.nuspec` 파일의 `<files>` 노드에서 이러한 파일을 참조합니다.

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

패키지에 MSBuild props 및 targets 포함은 [NuGet 2.5부터 도입](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files)되었으므로 `minClientVersion="2.5"` 특성을 `metadata` 요소에 추가하여 패키지를 사용하는 데 필요한 최소 NuGet 클라이언트 버전을 나타내는 것이 좋습니다.

NuGet에서 `\build` 파일이 포함된 패키지를 설치하는 경우 `.targets` 및 `.props` 파일을 가리키는 MSBuild `<Import>` 요소를 프로젝트 파일에 추가합니다. (`.props`는 프로젝트 파일의 위쪽에 추가되고, `.targets`는 아래쪽에 추가됩니다.) 각 대상 프레임워크에 대해 별도의 조건부 MSBuild `<Import>` 요소가 추가됩니다.

프레임워크 간 대상 지정을 위한 MSBuild `.props` 및 `.targets` 파일은 `\buildMultiTargeting` 폴더에 넣을 수 있습니다. 패키지 설치 중 NuGet은 해당 `<Import>` 요소를 프로젝트 파일에 추가하고, 대상 프레임워크를 설정하지 않는다는 조건(MSBuild 속성 `$(TargetFramework)`가 비어 있어야 함)을 함께 지정합니다.

NuGet 3.x를 사용하면 대상이 프로젝트에 추가되지 않고 대신 `project.lock.json`을 통해 사용할 수 있게 됩니다.

## <a name="authoring-packages-with-com-interop-assemblies"></a>COM interop 어셈블리가 포함된 패키지 제작

COM interop 어셈블리가 포함된 패키지에는 적절한 [targets 파일](#including-msbuild-props-and-targets-in-a-package)이 포함되어야 올바른 `EmbedInteropTypes` 메타데이터가 PackageReference 형식을 사용하여 프로젝트에 추가됩니다. 기본적으로 PackageReference를 사용하는 경우 `EmbedInteropTypes` 메타데이터는 모든 어셈블리에 대해 항상 false이므로 targets 파일에는 이 메타데이터가 명시적으로 추가됩니다. 충돌을 방지하기 위해 대상 이름은 고유해야 합니다. 이상적으로는 패키지 이름과 포함되는 어셈블리의 조합을 사용하여 아래 예제의 `{InteropAssemblyName}`을 해당 값으로 바꿉니다. (예제는 [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop)을 참조하세요.)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

`packages.config` 관리 형식을 사용하는 경우 패키지에서 어셈블리에 대한 참조를 추가하면 NuGet 및 Visual Studio에서 COM interop 어셈블리를 확인하고 프로젝트 파일에서 `EmbedInteropTypes`를 true로 설정합니다. 이 경우 targets 파일이 재정의됩니다.

또한 기본적으로 [빌드 자산은 전이적으로 이동하지 않습니다](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). 여기서 설명한 대로 작성된 패키지는 프로젝트 간 참조에서 전이 종속성으로 끌어올 때 다르게 작동합니다. 패키지 소비자는 빌드를 포함하지 않도록 PrivateAssets 기본값을 수정하여 패키지를 이동할 수 있도록 합니다.

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a>nugkg pack을 실행하여 .nupkg 파일 생성

어셈블리 또는 규칙 기반 작업 디렉터리를 사용하는 경우 `.nuspec` 파일이 포함된 `nuget pack`을 실행하고 `<project-name>`을 특정 파일 이름으로 바꿔 패키지를 만듭니다.

```cli
nuget pack <project-name>.nuspec
```

Visual Studio 프로젝트를 사용하는 경우 프로젝트 파일이 포함된 `nuget pack`을 실행하면 프로젝트 파일의 값을 사용하여 프로젝트의 `.nuspec` 파일을 자동으로 로드하고 그 안에 있는 모든 토큰을 바꿉니다.

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> 프로젝트가 토큰 값의 원본이므로 토큰 대체의 경우 프로젝트 파일을 직접 사용해야 합니다. `.nuspec` 파일이 포함된 `nuget pack`을 사용하면 토큰 대체가 발생하지 않습니다.

모든 경우에 `nuget pack`은 마침표로 시작하는 폴더(예: `.git` 또는 `.hg`)를 제외합니다.

NuGet은 매니페스트의 자리 표시자 값을 변경하지 않은 경우와 같이 수정이 필요한 오류가 `.nuspec` 파일에 있는지 여부를 나타냅니다.

`nuget pack`이 성공하면 [패키지 게시](../nuget-org/publish-a-package.md)에서 설명한 대로 적합한 갤러리에 게시할 수 있는 `.nupkg` 파일이 있습니다.

> [!Tip]
> 패키지를 만든 후 검사하는 유용한 방법은 [패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) 도구에서 해당 패키지를 여는 것입니다. 이렇게 하면 패키지의 내용과 해당 매니페스트를 보여 주는 그래픽 뷰가 제공됩니다. 또한 결과 `.nupkg` 파일의 이름을 `.zip` 파일로 바꾸고 그 내용을 직접 탐색할 수도 있습니다.

### <a name="additional-options"></a>추가 옵션

`nuget pack`에서 다양한 명령줄 스위치를 사용하여 파일을 제외하고, 매니페스트의 버전 번호를 재정의하고, 다른 기능 중에서 출력 폴더를 변경할 수 있습니다. 전체 목록은 [pack 명령 참조](../tools/cli-ref-pack.md)를 참조하세요.

다음은 Visual Studio 프로젝트에서 일반적으로 사용되는 몇 가지 옵션입니다.

- **참조된 프로젝트**: 프로젝트에서 다른 프로젝트를 참조하는 경우 `-IncludeReferencedProjects` 옵션을 사용하여 참조된 프로젝트를 패키지의 일부로 또는 종속성으로 추가할 수 있습니다.

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    이 포함 프로세스는 재귀적이므로, `MyProject.csproj`에서 B와 C 프로젝트를 참조하고 해당 프로젝트에서 D, E 및 F를 참조하면, B, C, D, E 및 F의 파일이 패키지에 포함됩니다.

    참조된 프로젝트에 자체의 `.nuspec` 파일이 포함되어 있으면 NuGet은 참조된 프로젝트를 종속성으로 대신 추가합니다.  해당 프로젝트를 별도로 패키지하고 게시해야 합니다.

- **빌드 구성**: 기본적으로 NuGet은 프로젝트 파일에 설정된 기본 빌드 구성(일반적으로 *Debug*)을 사용합니다. *Release*와 같은 다른 빌드 구성의 파일을 압축하려면 다음과 같이 구성에 `-properties` 옵션을 사용합니다.

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **기호**: 소비자가 디버거에서 패키지 코드를 단계별로 실행할 수 있게 하는 기호를 포함하려면 `-Symbols` 옵션을 사용합니다.

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a>패키지 설치 테스트

일반적으로 패키지를 게시하기 전에 프로젝트에 패키지를 설치하는 프로세스를 테스트하려고 합니다. 테스트를 통해 모든 파일이 프로젝트의 올바른 위치에 있는지 반드시 확인합니다.

일반적인 [패키지 설치 단계](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)를 사용하여 Visual Studio 또는 명령줄에서 수동으로 설치를 테스트할 수 있습니다.

자동 테스트의 경우 기본 프로세스는 다음과 같습니다.

1. `.nupkg` 파일을 로컬 폴더에 복사합니다.
1. `nuget sources add -name <name> -source <path>` 명령([nuget sources](../tools/cli-ref-sources.md) 참조)을 사용하여 패키지 원본에 폴더를 추가합니다. 지정된 컴퓨터에서 이 로컬 원본을 한 번만 설정하면 됩니다.
1. `nuget install <packageID> -source <name>`을 사용하여 해당 원본에서 패키지를 설치합니다. 여기서 `<name>`은 `nuget sources`에 지정된 원본 이름과 일치합니다. 원본을 지정하면 해당 원본에서만 패키지가 설치됩니다.
1. 파일 시스템을 검사하여 파일이 올바르게 설치되었는지 확인합니다.

## <a name="next-steps"></a>다음 단계

패키지(`.nupkg` 파일)를 만들었으면 [패키지 게시](../nuget-org/publish-a-package.md)에서 설명한 대로 원하는 갤러리에 게시할 수 있습니다.

다음 항목에서 설명한 대로 패키지의 기능을 확장하거나 그렇지 않고 다른 시나리오를 지원할 수도 있습니다.

- [패키지 버전 관리](../reference/package-versioning.md)
- [여러 대상 프레임워크 지원](../create-packages/supporting-multiple-target-frameworks.md)
- [원본 및 구성 파일 변환](../create-packages/source-and-config-file-transformations.md)
- [지역화](../create-packages/creating-localized-packages.md)
- [시험판 버전](../create-packages/prerelease-packages.md)

마지막으로 주의해야 할 추가 패키지 유형이 있습니다.

- [네이티브 패키지](../create-packages/native-packages.md)
- [기호 패키지](../create-packages/symbol-packages.md)
