---
title: NuGet 1.4 릴리스 정보
description: NuGet 1.4 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550633"
---
# <a name="nuget-14-release-notes"></a>NuGet 1.4 릴리스 정보

[1.3 NuGet 릴리스 정보](../release-notes/nuget-1.3.md) | [1.5 NuGet 릴리스 정보](../release-notes/nuget-1.5.md)

NuGet 1.4는 2011 년 6 월 17 일에 출시 되었습니다.

## <a name="features"></a>기능

### <a name="update-package-improvements"></a>업데이트 패키지 기능 향상
NuGet 1.4 많은 솔루션에 여러 프로젝트에서 동일한 버전에서 패키지를 쉽게 만드는 Update-package 명령에 향상 된 기능을 소개 합니다. 예를 들어 패키지를 최신 버전으로 업그레이드 하는 경우 동일한 verision 업데이트할 설치 패키지를 사용 하 여 모든 프로젝트를 매우 일반적인 됩니다.

`Update-Package` 명령 이제 하기가 쉬워집니다.

#### <a name="update-all-packages-in-a-single-project"></a>단일 프로젝트의 모든 패키지 업데이트

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>모든 프로젝트에서 패키지를 업데이트 합니다.

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>모든 프로젝트의 모든 패키지 업데이트

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>모든 패키지에는 "안전한" 업데이트를 수행 합니다.
`-Safe` 플래그 제한만 동일한 주 버전과 부 버전 구성 요소 버전으로 업그레이드 합니다. 예를 들어 패키지 버전 1.0.0 설치 되어 있으며 1.0.1, 1.0.2 및 1.1 버전이 피드에서 제공 되는 `-Safe` 플래그는 패키지를 1.0.2로 업데이트 합니다. 업그레이드 하지 않고는 `-Safe` 플래그는 최신 버전 1.1로 패키지를 업그레이드 합니다.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>솔루션 수준 패키지 관리
NuGet 1.4 하기 전에 여러 프로젝트로 패키지를 설치 된 대화 상자를 사용 하 여 복잡 합니다. 이 프로젝트에 한 번씩 대화 상자를 시작 해야 합니다.

NuGet 1.4 동시에 여러 프로젝트에서 패키지 설치/제거/업데이트에 대 한 지원을 추가합니다. 실행 하면는 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 합니다 **NuGet 패키지 관리** 메뉴 옵션입니다.

![솔루션 수준 NuGet 패키지 관리 대화 상자](./media/manage-nuget-packages-solution-dialog.png)

대화 상자의 제목 표시줄에서 솔루션의 이름을 표시 됩니다, 그리고 프로젝트 이름은 아닙니다.
패키지 작업에는 이제 작업에 적용 해야 하는 프로젝트의 목록 사용 하 여 확인란의 목록을 제공 합니다.

![NuGet 패키지 프로젝트 선택을 관리합니다](./media/manage-nuget-packages-project-selection.png)

에 대 한 자세한 내용은 항목을 참고 [솔루션용 패키지 관리](../tools/package-manager-ui.md#managing-packages-for-the-solution)합니다.

### <a name="constraining-upgrades-to-allowed-versions"></a>버전 허용 업그레이드 제한
기본적으로 실행 하는 경우는 `Update-Package` 패키지 (또는 대화 상자를 사용 하 여 패키지를 업데이트) 명령을 피드의 최신 버전으로 업데이트 됩니다. 모든 패키지를 업데이트 하는 것에 대 한 새로운 지원, 패키지를 특정 버전 범위를 잠글 수 하려는 경우 있을 수 있습니다. 예를 들어, 수를 이미 아는 응용 프로그램 패키지를 하지만 하지 3.0 이상 버전 2. *를 사용 하 여 에서만 작동 합니다. 실수로 3 패키지를 업데이트를 방지 하기 위해 NuGet 1.4는 패키지를 직접 편집 하 여 업그레이드할 수 있는 버전의 범위를 제한 하는 것에 대 한 지원을 추가 합니다 `packages.config` 사용 하 여 새 파일 `allowedVersions` 특성입니다.

다음 예제에서는 차단 하는 방법을 표시 하는 예를 들어를 `SomePackage` 패키지 버전 범위 2.0 ~ 3.0 (제외).
합니다 `allowedVersions` 특성은 사용 하 여 값을 허용 합니다 [버전 범위 형식이](../reference/package-versioning.md#version-ranges-and-wildcards)합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

1.4의 특정 버전 범위로 하는 패키지를 잠금 되도록 직접 편집한 note 합니다. NuGet 1.5에서 배치를 통해이 범위에 대 한 지원을 추가할 계획을 `Install-Package` 명령입니다.

### <a name="package-visualizer"></a>시각화 도우미 패키지
새 패키지 시각화 도우미를 통해 시작 합니다 **도구** -> **라이브러리 패키지 관리자** -> **시각화 도우미 패키지** 메뉴 옵션을 수 있습니다. 모든 프로젝트 및 솔루션 내에서 해당 패키지 종속성을 쉽게 시각화 합니다.

_**중요 참고:** 이 기능은 Visual Studio에서는 DGML 지원 활용 합니다. Visual Studio Ultimate에 시각화를 만들기만 지원 됩니다. DGML 다이어그램 보기에서 Visual Studio Premium 또는 고급만 지원 됩니다._

![시각화 도우미 패키지](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>NuGet 대화에 대 한 자동 업데이트 확인
일부 버전의 NuGet 통해 표현 하는 새 기능을 소개 합니다 `.nuspec` 이전 버전의 NuGet 대화 상자에서 인식 하지 파일입니다.
에 대 한 NuGet 1.4에서 소개 하는 예로 [프레임 워크 어셈블리 지정](../release-notes/nuget-1.2.md#framework-assembly-refs)합니다.
이 때문에 최신 기능을 활용 하는 패키지를 사용할 수 있도록 최신 버전의 NuGet 사용 하는 것이 반드시 합니다.
업데이트 NuGet에 보다 편리 하 게, NuGet 대화 상자에는 최신 버전을 사용할 수 있는 경우를 강조 표시 하는 논리가 포함 됩니다.

_**참고**: 경우에 확인 됩니다 합니다 **Online** 현재 세션에서 탭을 선택 합니다._

![사용 가능한 새 버전을 사용 하 여 NuGet 패키지 대화 상자 관리](./media/manage-nuget-packages-update-notification.png)

업데이트 자동 확인을 해제 하려면 NuGet 설정 대화 상자를 이동 및 선택 취소 **자동으로 업데이트 확인**합니다.

![NuGet 설정](./media/nuget-settings.png)

이 기능은 보이지 않을 것, 물론 NuGet 1.4 같은 1.3에 대 한 업데이트 될 때까지 하지만 사용할 수 있었던 실제로 NuGet 1.3에 추가 되었습니다.

### <a name="package-manager-dialog-improvements"></a>패키지 관리자 대화 상자 개선
* **메뉴 이름 향상**: 대화 상자를 시작 하는 메뉴 옵션을 쉽게 구별할 수 있도록 바뀌었습니다. 메뉴 옵션은 이제 **NuGet 패키지 관리**합니다.
* **세부 정보 창 표시 최신 업데이트 날짜**: 패키지에 대 한 세부 정보 창에서 최신 업데이트의 날짜를 표시 하는 NuGet 대화 경우는 **Online** 또는 **업데이트** 탭을 선택 합니다.
* **표시 된 태그 목록을**: Nuget 대화 태그를 표시 합니다.

### <a name="powershell-improvements"></a>향상 된 Powershell
* **PowerShell 스크립트를 서명**: NuGet 제한적인 환경에서 사용량을 사용 하도록 설정 하는 서명 된 Powershell 스크립트를 포함 합니다.
* **지원 요청**: 패키지 관리자 콘솔 이제 통해 프롬프트를 지원 합니다 `$host.ui.Prompt` 및 `$host.ui.PromptForChoice` 명령입니다.
* **패키지 원본 이름**: 사용 하 여 패키지 소스를 지정 하는 경우 지원 되는 패키지 원본의 이름을 제공 합니다 `-Source` 플래그입니다.

### <a name="nugetexe-command-line-improvements"></a>nuget.exe 명령줄 개선 사항
* **사용자 지정 NuGet 명령을**: nuget.exe는 MEF를 사용 하 여 사용자 지정 명령을 통해 확장이 가능 합니다.
* **간단한 기호 패키지를 만들기 위한 워크플로**: 합니다 `-Symbols` 만 원본을 포함 하 여 기호 패키지를 만드는 일반적인 규칙 기반 폴더 구조에 플래그를 적용할 수 있습니다 및 `.pdb` 폴더 내의 파일입니다.
* **여러 소스를 지정**: 합니다 `NuGet install` 명령 구분 기호로 또는 지정 하 여 세미콜론을 사용 하 여 여러 소스를 지정 하도록 지원 `-Source` 여러 번입니다.
* **프록시 인증 지원**: NuGet 1.4에는 인증이 필요한 프록시 뒤 NuGet을 사용 하는 경우 사용자 자격 증명 프롬프트에 대 한 지원이 추가 되었습니다.
* **주요 변경 내용 업데이트 nuget.exe**:는 `-Self` 플래그는 이제 nuget.exe 자동으로 업데이트 하는 데 필요한 합니다. `nuget.exe Update` 경로 더 길어진는 `packages.config` 파일과 패키지를 업데이트 하려고 합니다. 그렇지 않은이 업데이트는 제한 됩니다. * * 업데이트 추가 및 프로젝트 파일의 콘텐츠를 제거 합니다.
* * 패키지 내에서 Powershell 스크립트를 실행 합니다.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Nuget.exe를 사용 하 여 푸시 패키지에 대 한 NuGet 서버 지원
간단 하 게 호스트를 포함 하는 NuGet을 [간단한 웹 기반 NuGet 리포지토리](../hosting-packages/nuget-server.md) 를 통해는 `NuGet.Server` NuGet 패키지. NuGet 1.4를 사용 하 여 간단한 서버 푸시 및 nuget.exe를 사용 하 여 패키지를 삭제를 지원 합니다.
최신 버전의 `NuGet.Server` 새 `appSetting`명명 된 `apiKey`합니다. 키를 생략 하거나 비워 피드에 패키지를 푸시 비활성화 됩니다. (이상적으로 강력한 암호)로 apiKey를 설정 하면 nuget.exe를 사용 하 여 푸시 패키지 있습니다.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Windows Phone 도구 Mango 버전에 대 한 지원
이제 NuGet 릴리스 후보 버전의 Windows Phone Mango 도구에서 지원 됩니다.
현재 Windows Phone 도구에서 Windows Phone 도구에 대 한 NuGet을 설치 하기 위해서는 Visual Studio 확장 관리자에 대해 지원 되지 않은, 다운로드 및 VSIX를 수동으로 실행 해야 할 수 있습니다.

Windows Phone 도구에 대 한 NuGet을 제거 하려면 다음 명령을 실행 합니다.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>버그 수정
NuGet 1.4 88 총 작업 항목을 고정 했습니다. 이러한 71 버그로 표시 되었습니다.

작업의 전체 목록은 항목 고정 NuGet 1.4에서 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.

## <a name="bug-fixes-worth-noting"></a>주목할 만한 버그 수정:

* [문제 603](http://nuget.codeplex.com/workitem/603): 특정 패키지 소스를 지정 하는 경우 서로 다른 리포지토리에서 패키지 종속성을 올바르게 해결 합니다.
* [문제 1036](http://nuget.codeplex.com/workitem/1036): 추가 `NuGet Pack SomeProject.csproj` 이벤트를 더 이상 빌드 후에 무한 루프가 발생 합니다.
* [문제 961](http://nuget.codeplex.com/workitem/961): `-Source` 플래그 상대 경로 지원 합니다.

## <a name="nuget-14-update"></a>NuGet 1.4 업데이트
NuGet 1.4의 릴리스 후 즉시 해결 해야 했던 문제가 몇을 알게 되었습니다.
1.4이이 업데이트의 특정 버전 번호가 1.4.20615.9020입니다.

### <a name="bug-fixes"></a>버그 수정
* [문제 1220](http://nuget.codeplex.com/workitem/1220): 업데이트 패키지 실행 되지 않습니다 `install.ps1` / `uninstall.ps1` 프로젝트가 여러 개 있으면 모든 프로젝트에서
* [문제 1156](http://nuget.codeplex.com/workitem/1156): (Powershell 2가 설치 되지 않음) 하는 경우 패키지 관리자 콘솔 W2K3/xp 중단
