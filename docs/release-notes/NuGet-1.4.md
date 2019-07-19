---
title: NuGet 1.4 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 1.4에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de76cf610e580a36014be9274b9c2c762b1015ac
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317172"
---
# <a name="nuget-14-release-notes"></a>NuGet 1.4 릴리스 정보

[Nuget 1.3 릴리스 정보](../release-notes/nuget-1.3.md) | [nuget 1.5 릴리스 정보](../release-notes/nuget-1.5.md)

NuGet 1.4은 2011 년 6 월 17 일에 출시 되었습니다.

## <a name="features"></a>기능

### <a name="update-package-improvements"></a>업데이트-패키지 개선 사항
NuGet 1.4은 업데이트 패키지 명령에 대해 많은 향상 된 기능을 제공 하 여 솔루션의 여러 프로젝트에서 패키지를 동일한 버전으로 쉽게 유지할 수 있도록 합니다. 예를 들어 패키지를 최신 버전으로 업그레이드 하는 경우 해당 패키지를 설치 하는 모든 프로젝트를 동일한 verision 업데이트 하는 것이 매우 일반적입니다.

이제 `Update-Package` 명령을 사용 하 여 다음 작업을 쉽게 수행할 수 있습니다.

#### <a name="update-all-packages-in-a-single-project"></a>단일 프로젝트의 모든 패키지 업데이트

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>모든 프로젝트의 패키지 업데이트

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>모든 프로젝트의 모든 패키지 업데이트

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>모든 패키지에서 "안전" 업데이트 수행
플래그 `-Safe` 는 주 버전 및 부 버전 구성 요소가 동일한 버전 으로만 업그레이드를 제한 합니다. 예를 들어 패키지의 버전 1.0.0을 설치 하 고 피드에서 1.0.1, 1.0.2 및 1.1 버전을 사용할 수 있는 경우이 플래그는 `-Safe` 패키지를 1.0.2로 업데이트 합니다. `-Safe` 플래그 없이 업그레이드 하면 패키지가 최신 버전인 1.1로 업그레이드 됩니다.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>솔루션 수준에서 패키지 관리
NuGet 1.4 이전에는 대화 상자를 사용 하 여 여러 프로젝트에 패키지를 설치 하는 것이 복잡 했습니다. 프로젝트 마다 한 번씩 대화를 시작 해야 합니다.

NuGet 1.4은 동시에 여러 프로젝트에서 패키지를 설치/제거/업데이트 하기 위한 지원을 추가 합니다. 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **NuGet 패키지 관리** 메뉴 옵션을 선택 하 여를 시작 하면 됩니다.

![솔루션 수준 NuGet 패키지 관리 대화 상자](./media/manage-nuget-packages-solution-dialog.png)

이 대화 상자의 제목 표시줄에는 프로젝트 이름이 아니라 솔루션 이름이 표시 됩니다.
이제 패키지 작업은 작업을 적용 해야 하는 프로젝트 목록과 함께 확인란 목록을 제공 합니다.

![NuGet 패키지 관리 프로젝트 선택](./media/manage-nuget-packages-project-selection.png)

자세한 내용은 [솔루션에 대 한 패키지 관리](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution)항목을 참조 하십시오.

### <a name="constraining-upgrades-to-allowed-versions"></a>허용 되는 버전으로 업그레이드 제한
기본적으로 패키지에서 `Update-Package` 명령을 실행 하거나 대화 상자를 사용 하 여 패키지를 업데이트 하면 피드의 최신 버전으로 업데이트 됩니다. 모든 패키지를 업데이트 하는 새로운 지원 기능을 사용 하 여 패키지를 특정 버전 범위로 잠그는 경우가 있을 수 있습니다. 예를 들어 응용 프로그램은 패키지의 버전 2. * 에서만 작동 하지만 3.0 이상에서는 작동 하지 않는 것을 미리 알 수 있습니다. 패키지를 실수로 업데이트 하는 것을 방지 하기 위해 NuGet 1.4에서는 새 `packages.config` `allowedVersions` 특성을 사용 하 여 파일을 직접 편집 하 여 패키지를 업그레이드할 수 있는 버전 범위를 제한 하는 지원을 추가 합니다.

예를 들어 다음 예제에서는 버전 범위 2.0-3.0 `SomePackage` (제외)로 패키지를 잠그는 방법을 보여 줍니다.
특성 `allowedVersions` 은 [버전 범위 형식을](../reference/package-versioning.md#version-ranges-and-wildcards)사용 하 여 값을 허용 합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

1\.4에서는 특정 버전 범위에 대 한 패키지 잠금을 직접 편집 해야 합니다. NuGet 1.5에서는 `Install-Package` 명령을 통해이 범위를 배치 하는 지원을 추가할 계획입니다.

### <a name="package-visualizer"></a>패키지 시각화 도우미
**도구** -> **라이브러리 패키지 관리자** -> **패키지 시각화 도우미** 메뉴 옵션을 통해 시작 된 새 패키지 시각화 도우미를 사용 하면 내에서 모든 프로젝트 및 해당 패키지 종속성을 쉽게 시각화할 수 있습니다. 해결할.

_**중요 정보:** 이 기능은 Visual Studio의 DGML 지원을 활용 합니다. 시각화 만들기는 Visual Studio Ultimate 에서만 지원 됩니다. DGML 다이어그램 보기는 Visual Studio Premium 이상 에서만 지원 됩니다._

![패키지 시각화 도우미](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>NuGet 대화 상자에 대 한 자동 업데이트 확인
일부 nuget 버전에서는 파일을 `.nuspec` 통해 표현 되는 새로운 기능을 소개 합니다 .이 기능은 이전 버전의 nuget 대화 상자에서 인식 되지 않습니다.
한 가지 예는 [프레임 워크 어셈블리를 지정](../release-notes/nuget-1.2.md#framework-assembly-refs)하기 위한 NuGet 1.4에 대 한 소개입니다.
따라서 최신 버전의 NuGet을 사용 하 여 최신 기능을 활용 하는 패키지를 사용할 수 있도록 하는 것이 중요 합니다.
NuGet에 대 한 업데이트를 더 표시 하기 위해 NuGet 대화 상자에는 최신 버전을 사용할 수 있는 경우를 강조 표시 하는 논리가 포함 되어 있습니다.

_**참고**: 확인은 현재 세션에서 **온라인** 탭을 선택한 경우에만 수행 됩니다._

![새 버전을 사용할 수 있는 NuGet 패키지 관리 대화 상자](./media/manage-nuget-packages-update-notification.png)

자동 업데이트 확인을 해제 하려면 NuGet 설정 대화 상자로 이동 하 여 **자동으로 업데이트 확인**을 선택 취소 합니다.

![NuGet 설정](./media/nuget-settings.png)

이 기능은 NuGet 1.3에 실제로 추가 되었지만 NuGet 1.4와 같은 1.3 업데이트를 사용할 수 있게 되었을 때까지 표시 되지 않습니다.

### <a name="package-manager-dialog-improvements"></a>패키지 관리자 대화 상자 개선
* **향상 된 메뉴 이름**: 명확 하 게 하기 위해 대화 상자를 시작 하는 메뉴 옵션의 이름이 변경 되었습니다. 이제 메뉴 옵션이 **NuGet 패키지를 관리**합니다.
* **최신 업데이트 날짜를 표시 하는 세부 정보 창**: NuGet 대화 상자는 **온라인** 또는 **업데이트** 탭을 선택한 경우 패키지에 대 한 세부 정보 창의 최신 업데이트 날짜를 표시 합니다.
* **표시 되는 태그 목록**: Nuget 대화 상자에 태그가 표시 됩니다.

### <a name="powershell-improvements"></a>Powershell 개선 사항
* **서명 된 PowerShell 스크립트**: NuGet에는 더 제한적인 환경에서 사용 하도록 설정 된 서명 된 Powershell 스크립트가 포함 되어 있습니다.
* **지원 요청**: 이제 패키지 관리자 콘솔에서 `$host.ui.Prompt` 및 `$host.ui.PromptForChoice` 명령을 통해 프롬프트를 지원 합니다.
* **패키지 원본 이름**: 플래그를 `-Source` 사용 하 여 패키지 원본을 지정할 때 패키지 원본 이름을 제공 하는 것이 지원 됩니다.

### <a name="nugetexe-command-line-improvements"></a>nuget.exe 명령줄 개선 사항
* **Nuget 사용자 지정 명령**: NUGET.EXE는 MEF를 사용 하 여 사용자 지정 명령을 통해 확장할 수 있습니다.
* **기호 패키지를 만들기 위한 간단한 워크플로**: 이 `-Symbols` 플래그는 일반 규칙 기반 폴더 구조에 적용할 수 있습니다 .이 폴더에는 소스와 `.pdb` 파일만 포함 하 여 기호 패키지를 만들 수 있습니다.
* **여러 원본 지정**: 이 명령은 세미콜론을 구분 기호로 사용 하거나 여러 번 지정 `-Source` 하 여 여러 소스를 지정 하도록 지원 합니다. `NuGet install`
* **프록시 인증 지원**: NuGet 1.4는 인증을 필요로 하는 프록시 뒤에서 NuGet을 사용할 때 사용자 자격 증명을 묻는 메시지를 표시 합니다.
* **Nuget.exe 업데이트의 주요 변경 내용**: 이제 `-Self` 이 플래그는 nuget.exe를 업데이트 하는 데 필요 합니다. `nuget.exe Update`이제는 `packages.config` 파일에 대 한 경로를 사용 하 여 패키지 업데이트를 시도 합니다. 이 업데이트는 * * 프로젝트 파일의 콘텐츠를 업데이트, 추가, 제거 하지 않습니다.
\* * 패키지 내에서 Powershell 스크립트를 실행 합니다.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Nuget.exe를 사용 하 여 패키지를 푸시하는 NuGet 서버 지원
Nuget에는 `NuGet.Server` nuget 패키지를 통해 간단한 [웹 기반 nuget 리포지토리](../hosting-packages/nuget-server.md) 를 호스트 하는 간단한 방법이 포함 되어 있습니다. NuGet 1.4를 사용 하는 경량 서버는 nuget.exe를 사용 하 여 패키지 밀어넣기 및 삭제를 지원 합니다.
최신 버전의 `NuGet.Server` 는 이라는 `apiKey`새 `appSetting`를 추가 합니다. 키를 생략 하거나 비워 두면 피드에 패키지를 푸시할 수 없습니다. ApiKey를 값 (이상적으로는 강력한 암호)으로 설정 하면 nuget.exe를 사용 하 여 패키지를 푸시할 수 있습니다.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Windows Phone Tools 망고 Edition에 대 한 지원
이제 NuGet은 망고 용 Windows Phone Tools의 릴리스 후보 버전에서 지원 됩니다.
현재 Windows Phone 도구에는 Visual Studio 확장 관리자가 지원 되지 않으므로 Windows Phone 도구에 대 한 NuGet을 설치 하기 위해 VSIX를 수동으로 다운로드 하 여 실행 해야 할 수 있습니다.

Windows Phone Tools에 대 한 NuGet을 제거 하려면 다음 명령을 실행 합니다.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>버그 수정
NuGet 1.4에는 총 88 개의 작업 항목이 수정 되었습니다. 71는 버그로 표시 되어 있습니다.

NuGet 1.4에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)를 확인 하세요.

## <a name="bug-fixes-worth-noting"></a>버그가 수정 될 만한 문제:

* [문제 603](http://nuget.codeplex.com/workitem/603): 특정 패키지 원본을 지정할 때 서로 다른 리포지토리의 패키지 종속성이 제대로 확인 됩니다.
* [문제 1036](http://nuget.codeplex.com/workitem/1036): 빌드 `NuGet Pack SomeProject.csproj` 후 이벤트에 추가 하면 무한 루프가 발생 합니다.
* [문제 961](http://nuget.codeplex.com/workitem/961): `-Source` 플래그가 상대 경로를 지원 합니다.

## <a name="nuget-14-update"></a>NuGet 1.4 업데이트
NuGet 1.4이 출시 되는 즉시 해결 해야 하는 몇 가지 문제가 발견 되었습니다.
1\.4에 대 한이 업데이트의 특정 버전 번호는 1.4.20615.9020입니다.

### <a name="bug-fixes"></a>버그 수정
* [문제 1220](http://nuget.codeplex.com/workitem/1220): 업데이트-두 개 이상의 `install.ps1` 프로젝트가 있는 경우 모든 프로젝트에서 패키지가 실행 / `uninstall.ps1` 되지 않음
* [문제 1156](http://nuget.codeplex.com/workitem/1156): W2K3/XP에서 패키지 관리자 콘솔 정지 (Powershell 2가 설치 되지 않은 경우)
