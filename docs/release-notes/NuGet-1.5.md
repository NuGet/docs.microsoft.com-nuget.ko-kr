---
title: NuGet 1.5 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하 여 NuGet 1.5에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548727"
---
# <a name="nuget-15-release-notes"></a>NuGet 1.5 릴리스 정보

[NuGet 1.4 릴리스 정보](../release-notes/nuget-1.4.md) | [NuGet 1.6 릴리스 정보](../release-notes/nuget-1.6.md)

NuGet 1.5 2011 년 8 월 30 일에 출시 되었습니다.

## <a name="features"></a>기능

### <a name="project-templates-with-preinstalled-nuget-packages"></a>사전 설치 된 NuGet 패키지를 사용 하 여 프로젝트 템플릿
새 ASP.NET MVC 3 프로젝트 템플릿을 만들 때 프로젝트에 포함 된 jQuery 스크립트 라이브러리 NuGet 패키지를 설치 하 여 있습니다 배치 실제로 됩니다.

ASP.NET MVC 3 프로젝트 템플릿은 프로젝트 템플릿이 호출 될 때 설치 된 NuGet 패키지 집합을 포함 합니다. 프로젝트 템플릿 사용 하 여 NuGet 패키지를 포함 하는이 기능은 nuget 기능은 이제는 _모든_ 프로젝트 템플릿은 이제 활용할 수 있습니다.

이 기능에 대 한 자세한 내용은이 읽을 [기능을 개발자가 블로그 게시물](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)합니다.

### <a name="explicit-assembly-references"></a>명시적 어셈블리 참조

새로 추가 `<references />` 내에서 어셈블리를 명시적으로 지정 하는 데 사용 되는 요소는 패키지를 참조 해야 합니다.

예를 들어, 다음을 추가 하는 경우:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

하는 `xunit.dll` 및 `xunit.extensions.dll` 적절 한 참조 [프레임 워크/프로필 하위](../reference/nuspec.md#explicit-assembly-references) 의 `lib` 폴더에에서 있는 경우 다른 어셈블리 폴더에도 합니다.

이 요소를 생략 하면 경우에 모든 어셈블리를 참조 하는 일반적인 동작이 적용 되는 `lib` 폴더입니다.

__이 기능은 용도 무엇입니까?__

이 기능은 디자인 타임 전용 어셈블리를 지원합니다. 예를 들어, 코드 계약을 사용 하는 경우 계약 어셈블리는 해야 Visual Studio를 찾을 수 있지만 계약 어셈블리는 실제로 프로젝트에서 참조 되지 해야 하 고에 복사할 수 없음을 확장 하는 런타임 어셈블리 옆에 있습니다 `bin` 폴더입니다.

마찬가지로, 기능은 해당 도구 어셈블리를 런타임 어셈블리 옆에 있는 수는 있지만 프로젝트 참조에서 제외 해야 하는 XUnit 같은 단위 테스트 프레임 워크에 대 한에 데 사용할 수 있습니다.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>.Nuspec 파일을 제외 하는 기능 추가
합니다 `<file>` 내의 요소는 `.nuspec` 특정 파일 또는 와일드 카드를 사용 하 여 파일 집합을 포함 하도록 파일을 사용할 수 있습니다. 와일드 카드를 사용할 때 포함 된 파일의 특정 하위 집합을 제외할 없습니다 방법이 있습니다. 예를 들어, 특정 항목을 제외 하 고 폴더 내의 모든 텍스트 파일 만든다고 가정 합니다.

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

모든 백업 파일과 같은 파일의 집합을 제외 하려면 와일드 카드를 사용 하 여 또는

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>종속성을 제거 하 라는 메시지를 표시 대화 상자를 사용 하 여 패키지를 제거 합니다.
NuGet 요청, 종속성을 사용 하 여 패키지를 제거 하는 경우 패키지와 함께 패키지의 종속성의 제거를 허용 합니다.

![종속 패키지를 제거합니다.](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` 명령 개선
합니다 `Get-Package` 이제 지원 명령를 `-ProjectName` 매개 변수입니다. 따라서 명령

    Get-Package –ProjectName A

1. 프로젝트에 설치 된 모든 패키지 표시

### <a name="support-for-proxies-that-require-authentication"></a>인증이 필요한 프록시에 대 한 지원
NuGet을 사용 하 여 인증이 필요한 프록시 뒤에서 프록시 자격 증명에 대 한 NuGet 이제 묻습니다. 자격 증명을 입력 NuGet을 원격 리포지토리에 연결할 수 있습니다.

### <a name="support-for-repositories-that-require-authentication"></a>인증을 필요로 하는 리포지토리에 대 한 지원
연결할 이제 NuGet에서 지 원하는 [개인 리포지토리에서](../hosting-packages/local-feeds.md) 기본 또는 NTLM 인증을 요구 하는 합니다.

다이제스트 인증에 대 한 지원이 향후 릴리스에서 추가 됩니다.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Nuget.org 리포지토리에 성능 향상
Nuget.org 갤러리 패키지를 나열 하 고 더 빠르게 검색할 수 있도록 여러 성능 개선 했습니다.

### <a name="solution-dialog-project-filtering"></a>솔루션 대화 프로젝트 필터링
솔루션 수준 대화 상자에서 설치 하려면 프로젝트에 대 한 메시지를 표시 하는 경우, 선택한 패키지와 호환 되는 프로젝트 표시 했습니다.

### <a name="package-release-notes"></a>릴리스 패키지
NuGet 패키지에는 이제 릴리스 정보에 대 한 지원이 포함 됩니다. 이 릴리스 정보에 표시를 볼 때 _업데이트_ 패키지의 경우 있으므로 적합 하지 않습니다 첫 번째 릴리스에서 추가 합니다.

![[업데이트] 탭에서 릴리스 정보](./media/manage-nuget-packages-release-notes.png)

릴리스 패키지에 추가할 새을 사용 하 여 `<releaseNotes />` NuSpec 파일에서 메타 데이터 요소입니다.

### <a name="nuspec-ltfiles-gt-improvement"></a>.nuspec & ltfiles /&gt; 개선
`.nuspec` 파일을 이제 빈 통해 `<files />` nuget.exe를 패키지의 모든 파일을 포함 하지 않도록 지시 하는 요소입니다.

## <a name="bug-fixes"></a>버그 수정
NuGet 1.5 107의 총 작업 항목을 고정 했습니다. 이러한 103 버그로 표시 되었습니다.

작업의 전체 목록은 항목 고정 NuGet 1.5에서 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)합니다.

## <a name="bug-fixes-worth-noting"></a>주목할 만한 버그 수정:

* [문제 1273](http://nuget.codeplex.com/workitem/1273): 변경한 `packages.config` 친숙 한 패키지를 사전순으로 정렬 하 고 추가 공백을 제거 하 여 더 많은 버전 제어 합니다.
* [문제 844](http://nuget.codeplex.com/workitem/844): 버전 번호는 이제 정규화 되도록 `Install-Package 1.0` 버전을 사용 하 여 패키지에서 작동 `1.0.0`합니다.
* [문제 1060](http://nuget.codeplex.com/workitem/1060): nuget.exe를 사용 하 여 패키지를 만들 때 합니다 `-Version` 재정의 플래그는 `<version />` 요소입니다.
