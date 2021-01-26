---
title: NuGet 2.1 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 2.1에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777034"
---
# <a name="nuget-21-release-notes"></a>NuGet 2.1 릴리스 정보

[NuGet 2.0 릴리스 정보](../release-notes/nuget-2.0.md)  |  [NuGet 2.2 릴리스 정보](../release-notes/nuget-2.2.md)

NuGet 2.1은 2012 년 10 월 4 일에 출시 되었습니다.

## <a name="hierarchical-nugetconfig"></a>계층 구조 Nuget.Config

NuGet 2.1은 `NuGet.Config` 파일을 찾은 다음, 검색 된 모든 파일 집합에서 구성을 빌드하여 폴더 구조를 재귀적으로 탐색 하는 방법으로 nuget 설정을 더욱 유연 하 게 제어할 수 있습니다.  예를 들어 팀에 다른 내부 종속성의 CI 빌드에 대 한 내부 패키지 리포지토리가 있는 시나리오를 살펴보겠습니다. 개별 프로젝트에 대 한 폴더 구조는 다음과 같습니다.

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

또한 솔루션에 대해 패키지 복원이 사용 되는 경우 다음 폴더도 존재 합니다.

```
C:\myteam\solution1\.nuget
```

팀에서 작업 하는 모든 프로젝트에 대해 팀의 내부 패키지 리포지토리를 사용할 수 있도록 하 고, 컴퓨터의 모든 프로젝트에서 사용할 수 있도록 하는 것은 아니지만 새 Nuget.Config 파일을 만들어 c:\myteam 폴더에 저장할 수 있습니다. 프로젝트 마다 패키지 폴더를 변수와 방법이 없습니다.

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

이제 아래와 같이 c:\myteam 아래의 모든 폴더에서 ' nuget.exe sources ' 명령을 실행 하 여 소스가 추가 되었음을 확인할 수 있습니다.

![부모 nuget 구성의 패키지 소스](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` 파일은 다음 순서로 검색 됩니다.

1. `.nuget\Nuget.Config`
2. 프로젝트 폴더에서 루트로의 재귀 연습
3. Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )

이러한 구성은 *역순* 으로 적용 되는 것을 의미 합니다. 즉, 위의 순서에 따라 전역 Nuget.Config 먼저 적용 된 다음, 검색 된 Nuget.Config 파일의 루트에서 프로젝트 폴더로 차례로 적용 됩니다 `.nuget\Nuget.Config` .  요소를 사용 하 여 `<clear/>` 구성에서 항목 집합을 제거 하는 경우에 특히 중요 합니다.

## <a name="specify-packages-folder-location"></a>' 패키지 ' 폴더 위치 지정

이전에는 NuGet이 솔루션 루트 폴더 아래에 있는 알려진 ' 패키지 ' 폴더에서 솔루션 패키지를 관리 했습니다.  NuGet 패키지를 설치 하는 다양 한 솔루션을 포함 하는 개발 팀의 경우 동일한 패키지가 파일 시스템의 여러 위치에 설치 될 수 있습니다.

NuGet 2.1은 파일의 요소를 통해 패키지 폴더의 위치를 보다 세밀 하 게 제어 합니다 `repositoryPath` `NuGet.Config` .  계층 Nuget.Config 지원의 이전 예제를 기반으로 하 여 C:\myteam\의 모든 프로젝트가 동일한 패키지 폴더를 공유 한다고 가정 합니다.  이를 수행 하려면에 다음 항목을 추가 하면 됩니다 `c:\myteam\Nuget.Config` .

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

이 예에서 공유 `Nuget.Config` 파일은 깊이에 관계 없이 C:\myteam 아래에 생성 되는 모든 프로젝트에 대 한 공유 패키지 폴더를 지정 합니다. 솔루션 루트 아래에 기존 패키지 폴더가 있는 경우 NuGet이 새 위치에 패키지를 배치 하기 전에 삭제 해야 합니다.

## <a name="support-for-portable-libraries"></a>이식 가능한 라이브러리에 대 한 지원

[이식 가능한 라이브러리](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) 는 .net 4에서 처음 도입 된 기능으로,이 기능을 사용 하면 the.NET Framework 버전에서 Silverlight로 Windows Phone 및 xbox 360에 이르기까지 다양 한 Microsoft 플랫폼에서 수정 하지 않고도 작업할 수 있는 어셈블리를 빌드할 수 있습니다. 그러나 이번에는 NuGet이 xbox 이식 가능한 라이브러리 대상을 지원 하지 않습니다.  이제 NuGet 2.1은 프레임 워크 버전 및 프로필에 대 한 [패키지 규칙](../create-packages/supporting-multiple-target-frameworks.md) 을 확장 하 여 복합 프레임 워크 및 프로필 대상 폴더를 포함 하는 패키지를 만들 수 있도록 하 여 이식 가능한 라이브러리를 지원 합니다 `lib` .

예를 들어 다음과 같은 이식 가능한 클래스 라이브러리의 사용 가능한 대상 플랫폼을 살펴보겠습니다.

![이식 가능한 라이브러리 만들기 대화 상자](./media/releasenotes-21-plib.png)

라이브러리가 빌드되고 명령이 실행 된 후에는 `nuget.exe pack MyPortableProject.csproj` 생성 된 NuGet 패키지의 콘텐츠를 검사 하 여 새 이식 가능한 라이브러리 패키지 폴더 구조를 볼 수 있습니다.

![이식 가능한 라이브러리 패키지 레이아웃](./media/releasenotes-21-plib-layout.png)

여기에서 볼 수 있듯이 이식 가능한 라이브러리 폴더 이름 규칙은 프레임 워크 식별자가 기존 [프레임 워크 이름 및 버전 규칙](../reference/target-frameworks.md)을 따르는 ' 이식 가능한-{framework 1} + {framework n} ' 패턴을 따릅니다. 이름 및 버전 표기 규칙에 대 한 한 가지 예외는 Windows Phone에 사용 되는 프레임 워크 식별자에 있습니다.  이 모니커는 프레임 워크 이름 ' wp ' (wp7, wp71 또는 wp8)를 사용 해야 합니다. 예를 들어 ' wp7 '를 사용 하면 오류가 발생 합니다.

이 폴더 구조에서 만들어진 패키지를 설치할 때 NuGet은 이제 폴더 이름에 지정 된 대로 여러 대상에 프레임 워크 및 프로필 규칙을 적용할 수 있습니다.  NuGet의 일치 규칙을 사용 하는 경우 "보다 구체적인" 대상이 "less"의 대상 보다 우선적으로 적용 됩니다.  즉, 특정 플랫폼을 대상으로 하는 모니커는 모두 프로젝트와 호환 되는 경우 항상 이식 가능한 것 보다 우선적으로 적용 됩니다.  또한 여러 휴대용 대상이 프로젝트와 호환 되는 경우 NuGet은 지원 되는 플랫폼 집합이 패키지를 참조 하는 프로젝트에 "가장 가까운" 것을 선호 합니다.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Windows 8 및 Windows Phone 8 프로젝트를 대상으로 지정

NuGet 2.1은 이식 가능한 라이브러리 프로젝트를 대상으로 하는 지원을 추가 하는 것 외에도 Windows 8 스토어 및 Windows Phone 8 프로젝트에 대 한 새로운 프레임 워크 모니커와 각 플랫폼의 이후 버전에서 보다 쉽게 관리할 수 있는 Windows 스토어 및 Windows Phone 프로젝트에 대 한 새로운 일반 모니커를 제공 합니다.

Windows 8 스토어 응용 프로그램의 경우 식별자는 다음과 같습니다.

| NuGet 2.0 및 이전 버전 | NuGet 2.1 |
| ---------------- | ----------- |
| W i n,. NETCore45 | Windows, Windows8, win, win8 |

<br/>
Windows Phone 프로젝트의 경우 식별자는 다음과 같습니다.

| 전화 OS | NuGet 2.0 및 이전 버전 | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-wp | wp, wp7, Appname.windowsphone, WindowsPhone7 |
| Windows Phone 7.5 (망고) | silverlight4-wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (지원되지 않음) | wp8, WindowsPhone8 |

<br/>
위의 모든 변경 내용에서 이전 프레임 워크 이름은 NuGet 2.1에서 계속 완벽 하 게 지원 됩니다.  앞으로 새 이름을 사용 하면 이후 버전의 해당 플랫폼에서 더 안정적으로 사용할 수 있습니다. 그러나 2.1 이전 버전에서는 새 이름이 지원 *되지* 않으므로 스위치를 만들 때 적절 하 게 계획 해야 합니다.

## <a name="improved-search-in-package-manager-dialog"></a>패키지 관리자 대화 상자에서 향상 된 검색 기능

지난 몇 번의 반복을 통해 패키지 검색의 속도와 관련성이 크게 향상 된 NuGet 갤러리에 대 한 변경 내용이 도입 되었습니다.  그러나 이러한 향상 된 기능은 nuget.org 웹 사이트로 제한 되었습니다.  NuGet 2.1은 NuGet 패키지 관리자 대화 상자를 통해 향상 된 검색 환경을 제공 합니다.  예를 들어 Windows Azure 캐싱 미리 보기 패키지를 찾으려고 한다고 가정 합니다.  이 패키지에 대 한 적절 한 검색 쿼리는 "Azure Cache" 일 수 있습니다.  이전 버전의 패키지 관리자 대화 상자에서 원하는 패키지는 결과의 첫 번째 페이지에도 나열 되지 않습니다.  그러나 NuGet 2.1에서는 원하는 패키지가 검색 결과의 맨 위에 표시 됩니다.

![패키지 관리자 대화 상자 검색](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>패키지 강제 업데이트

NuGet 2.1 이전 버전에서는 NuGet이 패키지 업데이트를 건너뜁니다.  이는 특정 시나리오에 대 한 마찰을 도입 했습니다. 특히 팀에서 각 빌드와 함께 패키지 버전 번호를 증분 하지 않으려는 빌드 또는 CI 시나리오의 경우에는 특히 그렇습니다.  필요한 동작은에 관계 없이 업데이트를 적용 하는 것입니다.  NuGet 2.1은 ' 다시 설치 ' 플래그를 사용 하 여이를 해결 합니다.  예를 들어 이전 버전의 NuGet은 최신 패키지 버전이 없는 패키지를 업데이트 하려고 할 때 다음과 같은 결과가 발생 합니다.

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

다시 설치 플래그를 사용 하면 최신 버전이 있는지 여부에 관계 없이 패키지가 업데이트 됩니다.

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

다시 설치 플래그가 도움이 되는 또 다른 시나리오는 프레임 워크를 다시 대상으로 하는 것입니다. 프로젝트의 대상 프레임 워크를 변경 하는 경우 (예: .NET 4에서 .NET 4.5으로) Update-Package-다시 설치는 프로젝트에 설치 된 모든 NuGet 패키지에 대 한 올바른 어셈블리에 대 한 참조를 업데이트할 수 있습니다.

## <a name="edit-package-sources-within-visual-studio"></a>Visual Studio 내에서 패키지 소스 편집

이전 버전의 NuGet에서 Visual Studio 옵션 대화 상자 내에서 패키지 소스를 업데이트 하려면 패키지 원본을 삭제 하 고 다시 추가 해야 합니다.  NuGet 2.1은 업데이트를 구성 사용자 인터페이스의 첫 번째 클래스 함수로 지원 하 여이 워크플로를 개선 합니다.

![패키지 관리자 구성 대화 상자](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>버그 픽스

NuGet 2.1에는 많은 버그 수정이 포함 되어 있습니다. NuGet 2.0에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)를 확인 하세요.
