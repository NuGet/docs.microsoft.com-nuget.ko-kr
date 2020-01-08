---
title: NuGet 1.5 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 1.5에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383351"
---
# <a name="nuget-15-release-notes"></a>NuGet 1.5 릴리스 정보

Nuget [1.4 릴리스 정보](../release-notes/nuget-1.4.md) | [Nuget 1.6 릴리스 정보](../release-notes/nuget-1.6.md)

NuGet 1.5은 2011 년 8 월 30 일에 출시 되었습니다.

## <a name="features"></a>기능

### <a name="project-templates-with-preinstalled-nuget-packages"></a>사전 설치 된 NuGet 패키지를 사용 하는 프로젝트 템플릿
새 ASP.NET MVC 3 프로젝트 템플릿을 만들 때 프로젝트에 포함 된 jQuery 스크립트 라이브러리는 NuGet 패키지를 설치 하 여 실제로 배치 됩니다.

ASP.NET MVC 3 프로젝트 템플릿에는 프로젝트 템플릿이 호출 될 때 설치 되는 NuGet 패키지 집합이 포함 되어 있습니다. 프로젝트 템플릿에 NuGet 패키지를 포함 하는이 기능은 이제 _모든_ 프로젝트 템플릿이 활용할 수 있는 nuget의 기능입니다.

이 기능에 대 한 자세한 내용은 [기능 개발자가이 블로그 게시물](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)을 참조 하세요.

### <a name="explicit-assembly-references"></a>명시적 어셈블리 참조

패키지 내에서 참조할 어셈블리를 명시적으로 지정 하는 데 사용 되는 새로운 `<references />` 요소를 추가 했습니다.

예를 들어 다음을 추가 합니다.

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

그런 다음 폴더에 다른 어셈블리가 있는 경우에도 `xunit.dll` 및 `xunit.extensions.dll` `lib` 폴더의 해당 [프레임 워크/프로필 하위 폴더](../reference/nuspec.md#explicit-assembly-references) 에서 참조 됩니다.

이 요소를 생략 하면 `lib` 폴더의 모든 어셈블리를 참조 하는 일반적인 동작이 적용 됩니다.

__이 기능은 어떻게 사용 되나요?__

이 기능은 디자인 타임 전용 어셈블리를 지원 합니다. 예를 들어 코드 계약을 사용 하는 경우 Visual Studio에서 해당 계약 어셈블리를 찾을 수 있도록 확장 하는 런타임 어셈블리 옆에 계약 어셈블리가 있어야 하지만, 계약 어셈블리는 실제로 프로젝트에서 참조 되지 않으므로 `bin` 폴더에 복사 하면 안 됩니다.

마찬가지로, 기능을 XUnit과 같은 단위 테스트 프레임 워크에 사용할 수 있습니다 .이 경우 도구 어셈블리는 런타임 어셈블리 옆에 배치 해야 하지만 프로젝트 참조에서는 제외 됩니다.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Nuspec에서 파일을 제외 하는 기능이 추가 되었습니다.
`.nuspec` 파일 내의 `<file>` 요소는 와일드 카드를 사용 하 여 특정 파일이 나 파일 집합을 포함 하는 데 사용할 수 있습니다. 와일드 카드를 사용 하는 경우 포함 된 파일의 특정 하위 집합을 제외할 수 있는 방법이 없습니다. 예를 들어 특정 폴더에 있는 모든 텍스트 파일을 제외 하 고 모든 텍스트 파일을 사용할 수 있습니다.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

여러 파일을 지정 하려면 세미콜론을 사용 합니다.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

또는 와일드 카드를 사용 하 여 모든 백업 파일과 같은 파일 집합을 제외 합니다.

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>종속성을 제거 하 라는 대화 상자를 사용 하 여 패키지 제거
종속성이 포함 된 패키지를 제거 하면 NuGet 프롬프트가 표시 되어 패키지와 함께 패키지의 종속성을 제거할 수 있습니다.

![종속 패키지 제거](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` 명령 향상
`Get-Package` 명령은 이제 `-ProjectName` 매개 변수를 지원 합니다. 따라서 명령

    Get-Package –ProjectName A

프로젝트 A에 설치 된 모든 패키지를 나열 합니다.

### <a name="support-for-proxies-that-require-authentication"></a>인증이 필요한 프록시에 대 한 지원
인증을 필요로 하는 프록시 뒤에 NuGet을 사용할 때 NuGet은 이제 프록시 자격 증명을 묻는 메시지를 표시 합니다. 자격 증명을 입력 하면 NuGet에서 원격 리포지토리에 연결할 수 있습니다.

### <a name="support-for-repositories-that-require-authentication"></a>인증을 요구 하는 리포지토리에 대 한 지원
이제 NuGet에서 기본 또는 NTLM 인증을 요구 하는 [개인 리포지토리에](../hosting-packages/local-feeds.md) 연결할 수 있습니다.

다이제스트 인증에 대 한 지원은 향후 릴리스에 추가 될 예정입니다.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Nuget.org 리포지토리의 성능 향상
Nuget.org 갤러리에 대 한 몇 가지 성능 향상으로 패키지 목록 및 검색을 더 빠르게 수행할 수 있습니다.

### <a name="solution-dialog-project-filtering"></a>솔루션 대화 상자 프로젝트 필터링
솔루션 수준 대화 상자에서 설치할 프로젝트를 묻는 메시지가 표시 되 면 선택한 패키지와 호환 되는 프로젝트만 표시 됩니다.

### <a name="package-release-notes"></a>패키지 릴리스 정보
이제 NuGet 패키지에 릴리스 정보에 대 한 지원이 포함 됩니다. 릴리스 정보는 패키지에 대 한 _업데이트_ 를 볼 때만 표시 되므로 첫 번째 릴리스에 추가 하는 것은 적합 하지 않습니다.

![업데이트 탭 내 릴리스 정보](./media/manage-nuget-packages-release-notes.png)

패키지에 릴리스 정보를 추가 하려면 NuSpec 파일에 새 `<releaseNotes />` metadata 요소를 사용 합니다.

### <a name="nuspec-ltfiles-gt-improvement"></a>. nuspec & ltfiles/&gt; 개선
이제 `.nuspec` 파일에 빈 `<files />` 요소가 허용 됩니다. 그러면 nuget.exe는 패키지에 파일을 포함 하지 않도록 합니다.

## <a name="bug-fixes"></a>버그 수정
NuGet 1.5에는 총 107 개의 작업 항목이 수정 되었습니다. 103는 버그로 표시 되어 있습니다.

NuGet 1.5에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)를 확인 하세요.

## <a name="bug-fixes-worth-noting"></a>버그가 수정 될 만한 문제:

* [문제 1273](http://nuget.codeplex.com/workitem/1273): 패키지를 사전순으로 정렬 하 고 추가 공백을 제거 하 여 더 많은 버전 제어를 `packages.config` 했습니다.
* [문제 844](http://nuget.codeplex.com/workitem/844): 버전이 `1.0.0`인 패키지에서 `Install-Package 1.0` 작동 하도록 버전 번호가 정규화 되었습니다.
* [문제 1060](http://nuget.codeplex.com/workitem/1060): nuget.exe를 사용 하 여 패키지를 만들 때 `-Version` 플래그가 `<version />` 요소를 재정의 합니다.
