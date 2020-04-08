---
title: dotnet CLI를 사용하여 NuGet 패키지 만들기 및 게시
description: .NET Core CLI, dotnet을 사용하여 NuGet 패키지를 만들고 게시하는 방법에 대한 연습 자습서입니다.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 8c09d6d5662ed6ff0deffa5d45b823ad0992f399
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231307"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>빠른 시작: 패키지 만들기 및 게시(dotnet CLI)

.NET 클래스 라이브러리에서 NuGet 패키지를 만들고 `dotnet` CLI(명령줄 인터페이스)를 사용하여 nuget.org에 게시하는 간단한 과정입니다.

## <a name="prerequisites"></a>사전 요구 사항

1. [ CLI를 포함하는 ](https://www.microsoft.com/net/download/).NET Core SDK`dotnet`를 설치합니다. Visual Studio 2017부터 dotnet CLI는 모든 .NET Core 관련 워크로드와 함께 자동으로 설치됩니다.

1. 아직 없는 경우 [nuget.org에 체험 계정을 등록](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)합니다. 새 계정을 만들면 확인 전자 메일을 보냅니다. 패키지를 업로드하려면 먼저 계정을 확인해야 합니다.

## <a name="create-a-class-library-project"></a>클래스 라이브러리 프로젝트 만들기

패키지할 코드에 대해 기존 .NET 클래스 라이브러리 프로젝트를 사용하거나 다음과 같이 간단한 프로젝트를 만듭니다.

1. `AppLogger`라는 폴더를 만듭니다.

1. 명령 프롬프트를 열고 `AppLogger` 폴더로 전환합니다.

1. 프로젝트의 현재 폴더 이름을 사용하는 `dotnet new classlib`를 입력합니다.

   이렇게 하면 새 프로젝트가 생성됩니다.

## <a name="add-package-metadata-to-the-project-file"></a>프로젝트 파일에 패키지 메타데이터 추가

모든 NuGet 패키지에는 패키지의 콘텐츠와 종속성을 설명하는 매니페스트가 필요합니다. 마지막 패키지에서 매니페스트는 프로젝트 파일에 포함하는 NuGet 메타데이터 속성에서 생성되는 `.nuspec` 파일입니다.

1. 프로젝트 파일(`.csproj`)을 열고 종료 `<PropertyGroup>` 태그 내부에 다음 최소 속성을 추가하여 값을 적절하게 변경합니다.

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > nuget.org 또는 무엇이든 사용 중인 호스트에서 고유한 식별자를 패키지에 제공합니다. 이 연습에서는 나중 게시 단계에서 패키지를 공개적으로 표시할 수 있도록 이름에 “샘플” 또는 “테스트”를 포함하는 것이 좋습니다(실제로 아무도 사용할 가능성이 없더라도).

1. [NuGet 메타데이터 속성](/dotnet/core/tools/csproj#nuget-metadata-properties)에 설명된 선택적 속성을 추가합니다.

    > [!Note]
    > 공용으로 빌드된 패키지의 경우 **PackageTags** 속성에 특히 주의하세요. 이러한 태그는 다른 사람들이 패키지를 찾고 그 기능을 이해하는 데 도움이 됩니다.

## <a name="run-the-pack-command"></a>pack 명령 실행

프로젝트에서 NuGet 패키지(`.nupkg` 파일)를 빌드하려면 `dotnet pack` 명령을 실행합니다. 이 명령은 프로젝트도 자동으로 빌드합니다.

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

출력에는 `.nupkg` 파일의 경로가 표시됩니다.

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>빌드 시 패키지를 자동으로 생성

`dotnet pack`를 실행할 때 `dotnet build`을 자동으로 실행하려면 프로젝트 파일의 `<PropertyGroup>` 내에 다음 줄을 추가합니다.

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>패키지 게시

`.nupkg` 파일이 있으면 nuget.org에서 얻은 API 키와 함께 `dotnet nuget push` 명령을 사용하여 nuget.org에 게시합니다.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API 키 얻기

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>dotnet nuget push로 게시

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>게시 오류

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>게시된 패키지 관리

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-video"></a>관련 동영상

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-the-NET-CLI-5-of-5/player]

[Channel 9](https://channel9.msdn.com/Series/NuGet-101) 및 [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)에서 더 많은 NuGet 비디오를 확인하세요.

## <a name="next-steps"></a>다음 단계

첫 번째 NuGet 패키지 만들기를 진행하시게 된 것을 축하드립니다.

> [!div class="nextstepaction"]
> [패키지 만들기](../create-packages/creating-a-package-dotnet-cli.md)

NuGet에서 제공하는 다른 기능을 탐색하려면 아래 링크를 선택합니다.

- [패키지 게시](../nuget-org/publish-a-package.md)
- [시험판 패키지](../create-packages/Prerelease-Packages.md)
- [여러 대상 프레임워크 지원](../create-packages/multiple-target-frameworks-project-file.md)
- [패키지 버전 관리](../concepts/package-versioning.md)
- [지역화된 패키지 만들기](../create-packages/creating-localized-packages.md)
- [기호 패키지 만들기](../create-packages/symbol-packages-snupkg.md)
- [패키지 서명](../create-packages/Sign-a-package.md)
