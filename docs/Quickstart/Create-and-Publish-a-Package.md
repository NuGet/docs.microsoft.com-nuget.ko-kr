---
title: "NuGet 패키지 만들기 및 게시를 위한 입문서 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/03/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "nuget.exe 명령줄 인터페이스와 Visual Studio를 모두 사용하여 NuGet 패키지를 만들고 게시하기 위한 연습 자습서입니다."
keywords: "NuGet 패키지 만들기, NuGet 패키지 게시, NuGet 자습서"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53d29283c9e786fc27e9a608d7d251d8d0b5b0b2
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2018
---
# <a name="create-and-publish-a-package"></a>패키지 만들기 및 게시

.NET 클래스 라이브러리에서 NuGet 패키지를 만들고 nuget.org에 게시하는 간단한 과정입니다. 이 문서에서는 NuGet CLI(명령줄 인터페이스) 및 Visual Studio를 사용하는 프로세스를 안내합니다.

## <a name="pre-requisites"></a>필수 구성 요소

1. [visualstudio.com](https://www.visualstudio.com/)에서 모든 버전의 Visual Studio 2017을 설치합니다.

1. [nuget.org/downloads](https://nuget.org/downloads)에서 최신 버전의 `nuget.exe`를 다운로드하고 PATH에 있는 위치에 `.exe`를 저장하여 `nuget.exe` NuGet CLI 도구를 설치합니다. 다운로드는 설치 관리자가 아니라 *도구 자체입니다*.

1. 패키지하려는 코드에 적합한 .NET 클래스 라이브러리 프로젝트를 만듭니다. 아직 프로젝트가 없는 경우 다음과 같이 간단한 프로젝트를 만들 수 있습니다.
    1. Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 차례로 선택하고, **Visual C# > Windows** 노드를 펼치고, "클래스 라이브러리" 템플릿을 선택하고, 프로젝트 이름을 AppLogger로 지정한 다음, **확인**을 클릭합니다.
    1. 결과 프로젝트 파일을 마우스 오른쪽 단추로 클릭하고, **빌드**를 선택하여 프로젝트가 제대로 만들어졌는지 확인합니다. DLL은 Debug(또는 해당 구성을 대신 빌드하는 경우 Release) 폴더 내에 있습니다.

    물론 실제 NuGet 패키지 내에서 다른 사람들이 응용 프로그램을 빌드할 수 있는 많은 유용한 기능을 구현할 것입니다. 그러나 이 연습에서는 템플릿의 클래스 라이브러리가 패키지를 만드는 데 충분하므로 추가 코드를 작성하지 않습니다.

## <a name="create-the-nuspec-package-manifest-file"></a>.nuspec 패키지 매니페스트 파일 만들기

모든 NuGet 패키지에는 내용과 종속성을 설명하는 매니페스트(`.nuspec` 파일)가 필요합니다. `nuget spec` 명령은 이 파일을 만든 다음 사용자 지정합니다. 다음 예제에서는 프로젝트 파일에서 `.nuspec`을 만듭니다. 또한 [패키지 만들기](../create-packages/creating-a-package.md)에서 설명한 대로 다른 방법을 통해 매니페스트를 만들 수도 있습니다.

1. 명령 프롬프트를 열고 프로젝트 파일(`.csproj`)이 있는 폴더로 이동합니다.

1. `spec` NuGet CLI 명령을 실행하여 `AppLogger.nuspec`과 같이 프로젝트의 이름을 붙인 매니페스트를 생성합니다.

    ```cli
    nuget spec
    ```

1. 텍스트 편집기에서 파일을 엽니다. 매니페스트는 패키징 프로세스 중에 `<token>` 형식(예: `$id$`)의 토큰이 프로젝트의 Properties/AssemblyInfo.cs 파일의 값으로 대체되는 아래 코드와 비슷합니다. 토큰에 대한 자세한 내용은 [.nuspec 파일 만들기](../create-packages/creating-a-package.md#creating-the-nuspec-file)를 참조하세요.

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. nuget.org에서 고유한 패키지 ID를 선택합니다. [패키지 만들기](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)에서 설명한 명명 규칙을 사용하는 것이 좋습니다. 작성자 및 설명 태그를 업데이트해야 합니다. 그렇지 않으면 다음 단계에서 오류가 발생합니다. 다음은 업데이트된 `.nuspec` 파일의 예제입니다.

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> 공용으로 빌드된 패키지의 경우 `<tags>` 요소에 특히 주의하세요. 이러한 태그는 다른 사람들이 패키지를 찾고 그 기능을 이해하는 데 도움이 됩니다.

## <a name="run-the-pack-command"></a>pack 명령 실행

프로젝트에서 NuGet 패키지(`.nupkg` 파일)를 빌드하려면 `pack` 명령을 실행합니다.

```cli
nuget pack AppLogger.csproj
```

이 명령은 `.nuspec` 파일의 패키지 이름과 버전 번호를 사용하여 `AppLogger.1.0.0.0.nupkg`를 만듭니다. `.nuspec` 파일의 다양한 필드를 기본값에서 업데이트하지 않으면 명령에서 경고를 발생시킵니다.

## <a name="publish-the-package"></a>패키지 게시

`.nupkg` 파일이 있으면 `push` 명령을 사용하여 nuget.org에 게시합니다. 또는 [nuget.org 게시 워크플로](../create-packages/publish-a-package.md#publish-to-nugetorg)를 사용할 수 있습니다.

> [!Warning]
> nuget.org에 게시한 패키지는 다른 개발자에게 공개적으로 표시됩니다. 패키지를 개인적으로 호스팅하려면 [패키지 호스팅](../hosting-packages/overview.md)을 참조하세요.

1. [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)에 체험 계정을 만듭니다. 해당 계정이 이미 있으면 로그인합니다. 새 계정을 만들면 확인 전자 메일을 보냅니다. 패키지를 업로드하려면 먼저 계정을 확인해야 합니다.

1. 로그인되면 사용자 이름(오른쪽 위)을 선택한 다음 **API 키**를 선택합니다.

1. **만들기**를 선택하고, 키 이름을 제공하고, **API 키** 아래에서 **범위 선택 > 푸시**를 선택하고, **GLOB 패턴**에 대해 *를 입력한 다음, **만들기**를 선택합니다.

1. 키가 만들어지면 **복사**를 선택하여 CLI에서 필요한 액세스 키를 검색합니다.

    ![클립보드에 API 키 복사](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > 키를 안전한 위치에 저장하고 비밀로 유지합니다. 키가 실수로 노출되는 경우 언제든지 키를 다시 생성할 수 있습니다. CLI를 통해 더 이상 패키지를 푸시하지 않으려는 경우 API 키를 제거할 수도 있습니다.

1. 명령 프롬프트에서 다음 명령을 실행하여 패키지 이름을 지정하고 키를 4단계에서 복사한 값으로 바꿉니다.

    ```cli
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe에서 게시 프로세스의 결과를 표시합니다.

    ```output
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. nuget.org의 프로필에서 **패키지 관리**를 선택하여 방금 게시한 패키지를 확인합니다. 또한 확인 전자 메일을 받게 됩니다. 패키지가 인덱싱되어 다른 사용자가 찾을 수 있는 검색 결과에 표시되는 데 시간이 걸릴 수 있습니다. 그 동안 아래 메시지가 패키지 페이지에 표시됩니다.

    ![이 패키지는 아직 인덱싱되지 않았습니다. 인덱싱이 완료되면 검색 결과에 표시되며 설치/복원하는 데 사용할 수 있습니다.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> **바이러스 검사**: nuget.org에 업로드된 모든 패키지에 대해 바이러스를 검사하고 바이러스가 발견되면 해당 패키지가 거부됩니다. nuget.org에 나열된 모든 패키지도 정기적으로 검사됩니다.

됐습니다! 방금 첫 번째 NuGet 패키지를 [nuget.org](https://www.nuget.org/)에 게시했으므로 다른 개발자가 자신의 프로젝트에서 이 패키지를 사용할 수 있습니다.

## <a name="related-topics"></a>관련 항목

- [패키지 만들기](../create-packages/creating-a-package.md)
- [패키지 게시](../create-packages/publish-a-package.md)
- [여러 대상 프레임워크 지원](../create-packages/supporting-multiple-target-frameworks.md)
- [패키지 버전 관리](../reference/package-versioning.md)
- [지역화된 패키지 만들기](../create-packages/creating-localized-packages.md)
