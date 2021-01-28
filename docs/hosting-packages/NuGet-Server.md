---
title: NuGet.Server를 사용하여 NuGet 피드 호스트
description: NuGet.Server를 사용하여 IIS를 실행하는 모든 서버에서 NuGet 패키지 피드를 만들고 호스트하는 방법입니다. OData 및 HTTP를 통해 패키지를 사용할 수 있습니다.
author: JonDouglas
ms.author: jodou
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 3a9fb843f071eda72b9469292a7276ad81f8c24d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774076"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server는 IIS를 실행하는 모든 서버에서 패키지 피드를 호스트할 수 있는 ASP.NET 애플리케이션을 만드는 .NET Foundation에서 제공하는 패키지입니다. 간단히 말해 NuGet.Server를 사용하면 HTTP(S)(특히 OData)를 통해 사용할 수 있는 서버에서 폴더를 만들 수 있습니다. 쉽게 설정할 수 있고 간단한 시나리오에 가장 적합합니다.

1. Visual Studio에서 빈 ASP.NET 웹 애플리케이션을 만들고 여기에 NuGet.Server 패키지를 추가합니다.
1. 애플리케이션에서 `Packages` 폴더를 구성하고 패키지를 추가합니다.
1. 애플리케이션을 적합한 서버에 배포합니다.

다음 섹션에서는 C#을 사용하여 이 프로세스를 설명합니다.

NuGet.Server에 대해 추가 질문이 있으면 [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)에서 문제를 제출하세요.

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>NuGet.Server를 사용하여 ASP.NET 웹 애플리케이션 만들기 및 배포

1. Visual Studio에서 **파일 > 새로 만들기 > 프로젝트** 를 선택하고 “ASP.NET 웹 애플리케이션(.NET Framework)”을 검색하고 **C#** 에 대해 일치하는 템플릿을 선택합니다.

    ![.NET Framework 웹 프로젝트 템플릿 선택](media/Hosting_00-NuGet.Server-ProjectType.png)

1. **Framework** 를 “.NET Framework 4.6”으로 설정합니다.

    ![새 프로젝트의 대상 프레임워크 설정](media/Hosting_01-NuGet.Server-Set4.6.png)

1. 애플리케이션에 NuGet.Server가 *아닌* 적합한 이름을 입력하고, 확인을 선택하고, 다음 대화 상자에서 **빈** 템플릿을 선택한 다음, **확인** 을 선택합니다.

    ![빈 웹 프로젝트 선택](media/Hosting_02-NuGet.Server-Empty.png)

1. 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리** 를 선택합니다.

1. .NET Framework 4.6을 대상으로 하는 경우 패키지 관리자 UI에서 **찾아보기** 탭을 선택한 후, 최신 버전의 NuGet.Server 패키지를 검색하고 설치합니다. (`Install-Package NuGet.Server`를 사용하여 패키지 관리자 콘솔에서 설치할 수도 있습니다.) 메시지가 표시되면 사용 약관에 동의합니다.

    ![NuGet.Server 패키지 설치](media/Hosting_03-NuGet.Server-Package.png)

1. NuGet.Server를 설치하면 빈 웹 애플리케이션을 패키지 소스로 변환합니다. 애플리케이션에서 다양한 기타 패키지를 설치하고, `Packages` 폴더를 만들고, `web.config`를 수정하여 추가 설정이 포함됩니다(자세한 내용은 해당 파일에 있는 설명 참조).

    > [!Important]
    > NuGet.Server 패키지가 해당 파일에 대한 수정을 완료한 후에는 `web.config`를 자세히 살펴봅니다. NuGet.Server는 기존 요소를 덮어쓰지 않는 대신 중복 요소를 만들 수 있습니다. 나중에 프로젝트를 실행하려고 할 때 이러한 중복 요소로 인해 "내부 서버 오류"가 발생합니다. 예를 들어 NuGet.Server를 설치하기 전에 `web.config`에 `<compilation debug="true" targetFramework="4.5.2" />`가 포함된 경우 패키지에서 이를 덮어쓰는 대신 두 번째 `<compilation debug="true" targetFramework="4.6" />`을 삽입합니다. 이 경우 이전 프레임워크 버전을 사용하여 요소를 삭제합니다.

1. Visual Studio에서 로컬로 사이트를 실행합니다(**디버그 > 디버깅 없이 시작** 또는 Ctrl+F5 사용). 홈 페이지에서는 아래 표시된 것처럼 패키지 피드 URL을 제공합니다. 오류가 표시될 경우 앞에서 설명한 것처럼 중복 요소가 있는지 `web.config`를 자세히 살펴보세요.

    ![NuGet.Server에서 애플리케이션의 기본 홈페이지](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  처음으로 애플리케이션을 실행하면 NuGet.Server에서는 각 패키지에 대한 폴더를 포함하도록 `Packages` 폴더를 다시 구성합니다. 이렇게 하면 NuGet 3.3에서 도입한 [로컬 스토리지 레이아웃](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands)과 일치하여 성능을 향상시킵니다. 패키지를 추가하는 경우 이 구조를 계속 진행합니다.

1. 로컬 배포를 테스트하면 필요에 따라 다른 내부 또는 외부 사이트에 애플리케이션을 배포합니다.

1. `http://<domain>`에 배포되면 패키지 원본에 사용하는 URL은 `http://<domain>/nuget`입니다.

## <a name="adding-packages-to-the-feed-externally"></a>외부에서 피드에 패키지 추가

NuGet.Server 사이트를 실행하면 `web.config`에서 API 키 값을 설정하기 위해 제공된 [nuget push](../reference/cli-reference/cli-ref-push.md)를 사용하여 패키지를 추가할 수 있습니다.

NuGet.Server 패키지를 설치한 후에 `web.config`에는 빈 `appSetting/apiKey` 값이 포함됩니다.

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

`apiKey`를 생략하거나 비워 두면 피드에 패키지를 푸시하는 작업이 비활성화됩니다.

이 기능을 사용하려면 `apiKey`를 값(이상적으로 강력한 암호)으로 설정하고 `true` 값을 포함한 `appSettings/requireApiKey`라는 키를 추가합니다.

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

서버가 이미 보호되거나 그렇지 않은 경우 API 키가 필요하지 않는 경우(예: 로컬 팀 네트워크에서 프라이빗 서버를 사용하는 경우) `requireApiKey`를 `false`로 설정할 수 있습니다. 서버에 액세스할 수 있는 모든 사용자는 패키지를 푸시할 수 있습니다.

3\.0.0부터 패키지를 푸시하는 URL이 `http://<domain>/nuget`로 변경되었습니다. 3\.0.0 릴리스 이전에는 푸시 URL이 `http://<domain>/api/v2/package`였습니다.

NuGet 3.2.1 이상에서는 `/nuget` 외에도 기본적으로 시작 구성(기본적으로 `NuGetODataConfig.cs`)의 `enableLegacyPushRoute: true` 옵션을 통해 이 레거시 URL `/api/v2/package`를 사용할 수 있습니다. 여러 피드가 동일한 프로젝트에서 호스팅되는 경우 이 기능은 작동하지 않습니다.

## <a name="removing-packages-from-the-feed"></a>피드에서 패키지 제거

NuGet.Server에서 [nuget delete](../reference/cli-reference/cli-ref-delete.md) 명령은 주석과 API 키를 포함한 경우 리포지토리에서 패키지를 제거합니다.

이 동작을 패키지 목록을 해제하는 것으로 변경하려면(패키지 복원에 사용할 수 있게 유지) `web.config`의 `enableDelisting` 키를 true로 변경하세요.

## <a name="configuring-the-packages-folder"></a>패키지 폴더 구성

`NuGet.Server` 1.5 이상에서는 `web.config`의 `appSettings/packagesPath` 값을 사용하여 패키지 폴더를 사용자 지정할 수 있습니다.

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath`는 절대 또는 가상 경로일 수 있습니다.

`packagesPath`를 생략하거나 비워 두면 패키지 폴더는 기본적으로 `~/Packages`입니다.

## <a name="making-packages-available-when-you-publish-the-web-app"></a>웹앱을 게시할 때 패키지를 사용할 수 있도록 설정

서버에 애플리케이션을 게시할 때 피드에서 패키지를 사용하려면 각 `.nupkg` 파일을 Visual Studio의 `Packages` 폴더에 추가한 다음, **빌드 작업** 을 **콘텐츠** 로 설정하고, **출력 디렉터리로 복사** 를 **항상 복사** 로 설정합니다.

![프로젝트의 패키지 폴더에 패키지 복사](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a>릴리스 정보

NuGet.Server에 대한 릴리스 정보는 [GitHub 릴리스 페이지](https://github.com/NuGet/NuGet.Server/releases)에서 사용할 수 있습니다.
여기에는 버그 수정 및 새로 추가된 기능에 대한 세부 정보가 포함됩니다.

## <a name="nugetserver-support"></a>NuGet.Server 지원

NuGet.Server 사용 시 추가 도움이 필요할 경우 [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)에서 문제를 제출하세요.
