---
title: NuGet 2.1 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하 여 NuGet 2.1에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548599"
---
# <a name="nuget-21-release-notes"></a>NuGet 2.1 릴리스 정보

[NuGet 2.0 릴리스 정보](../release-notes/nuget-2.0.md) | [NuGet 2.2 릴리스 정보](../release-notes/nuget-2.2.md)

NuGet 2.1은 2012 년 10 월 4 일에 출시 되었습니다.

## <a name="hierarchical-nugetconfig"></a>계층적 Nuget.Config

NuGet 2.1 하면 더욱 유연 하 게 찾고 폴더 구조를 탐색 하는 재귀적으로 통해 NuGet 설정을 제어 하 고 `NuGet.Config` 파일과 다음 모든 찾은 파일 집합에서 구성을 작성 합니다.  예를 들어 여기서 팀의 다른 내부 종속성의 CI 빌드에 대 한 내부 패키지 리포지토리를 시나리오를 고려 합니다. 개별 프로젝트의 폴더 구조는 다음과 같습니다.

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

또한 패키지 복원 솔루션을 사용할 경우 다음 폴더 에서도 존재 합니다.

    C:\myteam\solution1\.nuget

팀의 내부 패키지 리포지토리를 팀이 없습니다 사용할 수 있도록 모든 프로젝트에 대 한 컴퓨터에서 하는 동안에 작동 하는 모든 프로젝트에 사용할 수 있는 권한을 가지려면 수 새 Nuget.Config 파일을 만들고 c:\myteam 폴더에 넣습니다. 방법이 없기에 지정 된 프로젝트 / 패키지 폴더.

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

이제 아래와 같이 c:\myteam 아래에 있는 모든 폴더에서 'nuget.exe 소스' 명령을 실행 하 여 원본 추가 되었는지 볼 수 있습니다.

![부모 nuget config 파일에서 패키지 원본](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` 파일에 대 한 다음과 같은 순서로 검색 됩니다.

1. `.nuget\Nuget.Config`
2. 루트 프로젝트 폴더에서 재귀적 탐색
3. 전역 `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

구성을 적용 하는 것은 *역순*, 즉 위의 순서에 따라 전역 Nuget.Config는 수 먼저 적용 뒤에 검색 된 Nuget.Config 파일에서 루트 프로젝트 폴더에, `.nuget\Nuget.Config`합니다.  이 사용 중인 경우에 특히 중요 합니다 `<clear/>` 항목 집합이 구성에서 제거할 요소입니다.

## <a name="specify-packages-folder-location"></a>'패키지' 폴더 위치를 지정 합니다.

과거에는 NuGet에 솔루션 루트 폴더 아래에 찾이 알려진된 '패키지' 폴더에서 솔루션의 패키지를 관리 합니다.  NuGet 패키지를 설치 하는 다양 한 솔루션이 있는 개발 팀은이 파일 시스템의 여러 곳에 설치 되는 동일한 패키지에서 발생할 수 있습니다.

NuGet 2.1을 통해 패키지 폴더의 위치 보다 세부적인 제어를 제공 합니다 `repositoryPath` 요소에는 `NuGet.Config` 파일입니다.  계층적 Nuget.Config 지원, 이전 예제에서 빌드 C:\myteam\ 공유 같은 패키지 폴더에서 모든 프로젝트가 하려는 것을 가정 합니다.  이렇게 하려면 다음 항목을 간단히 추가 `c:\myteam\Nuget.Config`합니다.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

이 예제에서는 공유 `Nuget.Config` 파일 수준에 관계 없이 C:\myteam, 아래에 만들어진 모든 프로젝트에 대 한 공유 패키지 폴더를 지정 합니다. 참고는 솔루션 루트 아래에 있는 기존 패키지 폴더에 있는 경우 삭제 해야 하기 전에 NuGet 패키지를 새 위치에 배치 됩니다.

## <a name="support-for-portable-libraries"></a>이식 가능한 라이브러리에 대 한 지원

[이식 가능한 라이브러리](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) 는.NET 4 버전의.net Framework에도 Xbox 및 Windows Phone silverlight에서 다른 Microsoft 플랫폼에서 수정 없이 사용할 수 있는 어셈블리를 빌드할 수 있도록 처음 도입 된 기능 360 (하지만 지금은 NuGet에는 Xbox 이식 가능한 라이브러리 대상을 지원 하지 않습니다).  확장 하 여 합니다 [규칙 패키지](../create-packages/supporting-multiple-target-frameworks.md) framework 버전 및 프로필에 대 한 NuGet 2.1 이제 이식 가능한 라이브러리 복합 프레임 워크 및 프로필 대상 있는 패키지를 만들 수 있도록 하 여 `lib` 폴더입니다.

예를 들어 다음 이식 가능한 클래스 라이브러리의 사용 가능한 대상 플랫폼을 고려 합니다.

![이식 가능한 라이브러리 만들기 대화 상자](./media/releasenotes-21-plib.png)

라이브러리를 빌드한 후 명령과 `nuget.exe pack MyPortableProject.csproj` 를 실행할 새 이식 가능한 라이브러리 패키지 폴더 구조는 생성 된 NuGet 패키지의 내용을 검사 하 여 볼 수 있습니다.

![이식 가능한 라이브러리 패키지 레이아웃](./media/releasenotes-21-plib-layout.png)

알 수 있듯이 이식 가능한 라이브러리 폴더 이름 규칙 패턴을 따릅니다. 'portable-{framework 1} + {framework n}'는 프레임 워크 식별자에 따라 기존 [프레임 워크 이름 및 버전 규칙](../reference/target-frameworks.md)합니다. 이름 및 버전 규칙의 한 가지 예외는 Windows Phone 사용 되는 프레임 워크 식별자에 있습니다.  이 모니커 'wp' (wp7, wp71 wp8) 프레임 워크 이름을 사용 해야 합니다. 오류가 발생 하면 예를 들어, ' silverlight-wp7'를 사용 하 여 합니다.

이 폴더 구조에서 만든 패키지를 설치할 때 NuGet 폴더 이름에 지정 된 대로 여러 대상에 해당 프레임 워크 및 프로필 규칙을 이제 적용할 수 있습니다.  NuGet의 일치 규칙 숨김은 "보다 구체적인" 대상 "작은" 구체적인 우선적으로 적용 됩니다는 원칙이입니다.  이 특정 플랫폼을 대상으로 하는 모니커는 항상 기본 이식 가능한 항목 위에 둘 다는 프로젝트와 호환 되는 경우를 의미 합니다.  또한 여러 휴대용 대상 프로젝트와 호환 되는 경우 NuGet는 지원 되는 플랫폼 집합 패키지 참조를 프로젝트에 "가장 가까운" 인 것을 선호 합니다.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>대상 Windows 8 및 Windows Phone 8 프로젝트

이식 가능한 라이브러리 프로젝트를 대상으로 하는 것에 대 한 지원에 추가 하는 것 외에도 NuGet 2.1 일부 새 일반 모니커 Windows 스토어 및 Windows Phone 프로젝트 될 뿐만 아니라 Windows 8 스토어 및 Windows Phone 8 프로젝트에 대 한 새 프레임 워크 모니커를 제공 각 플랫폼의 이후 버전에서 관리 하기가 더 쉽습니다.

Windows 8 스토어 응용 프로그램에 대 한 식별자를 다음과 같이 표시 합니다.

| 2.0 및 이전 버전의 NuGet | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45, .NETCore45 | Windows, Windows8, win, win8 |

<br/>
Windows Phone 프로젝트에 대 한 식별자를 다음과 같이 표시 합니다.

| Phone OS | 2.0 및 이전 버전의 NuGet | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-wp | wp, wp7, WindowsPhone, WindowsPhone7 |
| Windows Phone 7.5(mango) | silverlight4 wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (지원 되지 않음) | wp8, WindowsPhone8 |

<br/>
모든 변경에서 NuGet 2.1에서 완전히 지원 되는 이전 프레임 워크 이름을 계속 합니다.  앞으로 새 이름은 사용 해야 하므로 더 안정적인 각 플랫폼의 이후 버전에서 합니다. 새 이름이 됩니다 *되지* 수 2.1 이전 버전의 NuGet에서 지 원하는 반면 계획 적절 하 게 전환 하는 경우에 대 한 합니다.

## <a name="improved-search-in-package-manager-dialog"></a>패키지 관리자 대화 상자에서 향상 된 검색

지난 몇 가지 반복 변경 속도 및 패키지 검색 관련성을 크게 향상 하는 NuGet 갤러리에 도입 되었습니다.  그러나 이러한 향상 된이 기능 nuget.org 웹 사이트 수 있었습니다.  NuGet 2.1 NuGet 패키지 관리자 대화 상자를 통해 사용 가능한 환경을 향상 된 검색을 만듭니다.  예를 들어 Windows Azure Caching 미리 보기 패키지를 검색 하려고 한다고 가정해 보겠습니다.  이 패키지에 대 한 적절 한 검색 쿼리는 "Azure Cache" 될 수 있습니다.  이전 버전의 패키지 관리자 대화 상자에서 원하는 패키지가 나열 되지 않습니다도 결과의 첫 번째 페이지에서.  그러나 NuGet 2.1에서 원하는 패키지가 이제 표시 검색 결과의 맨 위에 있는 됩니다.

![패키지 관리자 대화 검색](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>패키지 업데이트 적용

NuGet 2.1 이전 NuGet 패키지 업데이트는 아닌 경우 건너 뛸 높은 버전 번호입니다.  이 팀 패키지 버전 번호를 각 빌드를 사용 하 여 증가 하지 않은 빌드 또는 CI 시나리오의 경우 특히 특정 시나리오에 대 한 마찰을 도입 했습니다.  원하는 동작 관계 없이 강제로 업데이트 하는 것 이었습니다.  NuGet 2.1 '다시 설치' 플래그를 사용 하 여이 문제를 해결 합니다.  예를 들어, 이전 버전의 NuGet 최신 패키지 버전 없는 패키지를 업데이트 하려고 할 때 다음에서 결과 같습니다.

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

다시 설치 플래그를 사용 하 여 패키지 업데이트될지 여부에 관계 없이 최신 버전이 있습니다.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

여기서 다시 설치 플래그를 입증 유용한 다른 시나리오의 프레임 워크 대상 다시 지정 됩니다. (예를 들어.NET 4에서.NET 4.5로), 프로젝트의 대상 프레임 워크를 변경 하는 경우 Update-package-다시 설치 프로젝트에 설치 된 모든 NuGet 패키지에 대 한 올바른 어셈블리에 대 한 참조를 업데이트할 수 있습니다.

## <a name="edit-package-sources-within-visual-studio"></a>Visual Studio 내에서 패키지 소스 편집

이전 버전의 NuGet에서 다시 패키지 소스를 추가 및 삭제 하는 데 필요한 Visual Studio 옵션 대화 상자 내에서 패키지 원본을 업데이트 합니다.  NuGet 2.1 구성 사용자 인터페이스의 첫 번째 클래스 함수로 서 업데이트를 지원 하 여이 워크플로 개선 합니다.

![패키지 관리자 구성 대화 상자](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>버그 수정

NuGet 2.1에는 여러 버그 수정을 포함 합니다. 작업의 전체 목록은 항목 고정 NuGet 2.0에서 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.
