---
title: NuGet 1.0 및 1.1 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 1.1에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdd4bad54b08d956dbfdaf54220971492fd3ab02
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777213"
---
# <a name="nuget-10-and-11-release-notes"></a>NuGet 1.0 및 1.1 릴리스 정보

[NuGet 1.2 릴리스 정보](../release-notes/nuget-1.2.md)

NuGet 1.0은 2011 년 1 월 13 일에 출시 되었습니다.  NuGet 1.1은 2011 년 2 월 12 일에 출시 되었습니다.

## <a name="overview"></a>개요

이 문서에는 주요 미리 보기 릴리스에 따라 그룹화 된 다양 한 NuGet 1.0 릴리스에 대 한 릴리스 정보가 포함 되어 있습니다.

NuGet에는 다음 구성 요소가 포함 됩니다.

* 다음으로 구성 된 *nuget.exe. Tools. vsix* *
  * 패키지를 찾아보고 설치 하는 데 사용 되는 Visual Studio 내에서 **라이브러리 패키지 추가 대화 상자** * 대화 상자
  * Visual Studio 내의 **패키지 관리자 콘솔** * Powershell 기반 콘솔.
* 패키지를 만들고 게시 하는 데 사용 되는 *NuGet 명령줄 도구* * 도구입니다.

NuGet Tools Visual Studio 확장 (*nuget.exe*)에는 다음이 필요 합니다.

* Visual Studio 2010 또는 Visual Web Developer 2010 Express

NuGet 명령줄 도구를 사용 하려면 다음이 필요 합니다.

* .NET Framework 버전 4

## <a name="installation"></a>설치

이 [최신 릴리스](http://nuget.codeplex.com/releases/view/52018)를 사용 하려면 다음을 수행 합니다.

* 먼저 이전 빌드를 제거 합니다. 이렇게 하려면 VS를 관리자 권한으로 실행 해야 합니다.
* 보유 하 고 있는 기존 피드를 모두 제거 합니다.
* 을 가리키는 새 피드를 추가 <https://go.microsoft.com/fwlink/?LinkId=206669> 합니다.

## <a name="nuget-11"></a>NuGet 1.1

이 릴리스에서 해결 된 문제 목록은 여기에서 [찾을 수 있습니다](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0) .

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

RC 이후 RTM에 대 한 문제 하나를 해결 했습니다.

* [문제 474: 패키지를 제거 하면 솔루션의 모든 프로젝트에 영향을 줍니다.](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>릴리스 후보

다음은 CTP 2 이후이 릴리스 후보에서 변경한 내용입니다. 문제 추적기를 방문 하 여 버그의 전체 목록을 확인 합니다.

* [콘솔에서 패키지를 업데이트 해도 종속성은 업데이트 되지 않습니다.](http://nuget.codeplex.com/workitem/443)
* [패키지를 추가 하는 경우 패키지 참조를 추가 하지 않음 (CTP1)](http://nuget.codeplex.com/workitem/442)
* [패키지를 업데이트 하면 손상 된 참조가 남습니다.](http://nuget.codeplex.com/workitem/440)
* [가져오기-패키지-대화 상자에서 또는 콘솔에서 ' 모든 ' 집계 원본을 선택한 경우 업데이트 실패](http://nuget.codeplex.com/workitem/439)
* [패키지 확인 오류 가져오기](http://nuget.codeplex.com/workitem/426)
* [패키지 추가 대화 상자에서 패키지를 설치할 수 없는 경우 사용자에 게 경고](http://nuget.codeplex.com/workitem/425)
* [Package-많은 수의 패키지를 업데이트할 때 업데이트를 throw 합니다.](http://nuget.codeplex.com/workitem/424)
* [Nuspec 파일이 잘못 작성 될 때 오류 처리 향상](http://nuget.codeplex.com/workitem/423)
* [Nuget 팩은 지정 된 파일을 무시 합니다.](http://nuget.codeplex.com/workitem/422)
* [두 번째와 마지막 패키지 원본을 제거한 다음 "아래로 이동"을 클릭 하 고 충돌 VS](http://nuget.codeplex.com/workitem/418)
* [패키지를 설치 하는 동안 어셈블리 참조 제거](http://nuget.codeplex.com/workitem/413)
* [설정 대화 상자를 열 때 InvalidOperationException](http://nuget.codeplex.com/workitem/411)
* [패키지 관리자 콘솔에서 패키지 원본에 대 한 액세스 키가 작동 하지 않음](http://nuget.codeplex.com/workitem/410)
* [NuGet VS 설정 대화 상자 액세스 키가 잘못 된 필드에 포커스를 제공 합니다.](http://nuget.codeplex.com/workitem/409)
* [패키지 ID intellisense에서 너무 많은 항목을 쿼리하지 않아야 함](http://nuget.codeplex.com/workitem/404)
* [프로젝트 이름에 점 문자를 사용 하 여 프로젝트에 패키지를 추가 하지 못했습니다.](http://nuget.codeplex.com/workitem/403)
* [Nuspec에서 지정 된 파일에 대 한 문제](http://nuget.codeplex.com/workitem/400)
* [최신 빌드를 사용 하는 경우 올바른 공식 피드가 등록 되어야 합니다.](http://nuget.codeplex.com/workitem/399)
* [태그는 대신 공백을 사용 해야 합니다. #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata에 도움이 되는 정보가 부족 합니다.](http://nuget.codeplex.com/workitem/388)
* [대화 상자에 보고서 불건전 링크 추가](http://nuget.codeplex.com/workitem/386)
* [Visual Studio에서 App_Data를 사용 하 여 패키지 중단 압축 풀기](http://nuget.codeplex.com/workitem/380)
* [태그 구현](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder에서는 종속성이 없는 빈 패키지를 만들 수 있습니다.](http://nuget.codeplex.com/workitem/373)
* [패키지에 대 한 소유자 필드 추가](http://nuget.codeplex.com/workitem/365)
* [Vsix 도구 대신 NuGet 패키지 관리자로 VSIX 매니페스트를 업데이트 합니다.](http://nuget.codeplex.com/workitem/364)
* [모든 원본을 선택 하면 Get-Package 명령에서 오류를 throw 합니다.](http://nuget.codeplex.com/workitem/359)
* [옵션 대화 상자에서 패키지 원본 순서 지정 허용](http://nuget.codeplex.com/workitem/356)
* [업데이트-패키지에서 이전 버전을 제거 하지 않음](http://nuget.codeplex.com/workitem/352)
* [종속성에 대 한 버전 범위 지정 구현](http://nuget.codeplex.com/workitem/347)
* ["새 패키지 추가"를 클릭 하면 Visual Studio가 충돌 함](http://nuget.codeplex.com/workitem/346)
* [패키지 추가 대화 상자에 다운로드 및 등급 표시](http://nuget.codeplex.com/workitem/345)
* [대화 상자에서 패키지 소스를 변경 해도 활성 원본이 업데이트 되지 않음](http://nuget.codeplex.com/workitem/344)
* [패키지 관리자 콘솔 창의 키 바인딩 제거](http://nuget.codeplex.com/workitem/339)
* [설치-패키지는 cmdlet의 이름으로 인식 되지 않습니다.](http://nuget.codeplex.com/workitem/338)
* [로컬 피드에서 패키지 설치 정기 피드에 대 한 종속성은 확인 되지 않습니다.](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies은 아직 사용 중인 종속성을 건너뛰어야 합니다.](http://nuget.codeplex.com/workitem/331)
* [페이지 탐색을 취소 하는 경우 사용자는 원래 페이지 요청이 반환 되는 동안 다른 페이지로 이동할 수 없습니다.](http://nuget.codeplex.com/workitem/325)
* [많은 수의 패키지를 포함 하는 피드를 제공 하기 위한 NuPack. 서버의 성능을 조사 합니다.](http://nuget.codeplex.com/workitem/324)
* [두 번째는 패키지를 필터링 할 때 이전에 선택한 원본 대신 "새" 패키지 원본을 사용 합니다.](http://nuget.codeplex.com/workitem/321)
* [대화 상자에서 "온라인" 탭을 선택 하는 경우 기본 패키지 원본을 선택 해야 합니다.](http://nuget.codeplex.com/workitem/320)
* [목록-패키지가 설치 된 패키지를 기본적으로 표시 해야 함](http://nuget.codeplex.com/workitem/309)
* [어셈블리 참조 HintPaths](http://nuget.codeplex.com/workitem/294)
* [패키지 관리자 콘솔을 여는 동안 예외가 발생 했습니다.](http://nuget.codeplex.com/workitem/268)
* [콘솔 intellisense에서 전체 피드 다운로드](http://nuget.codeplex.com/workitem/259)
* [' 기본 ' 패키지 원본의 이름을 ' 활성 '으로 변경 해야 합니다.](http://nuget.codeplex.com/workitem/258)
* [패키지 소스 UI: 이름/원본 필드가 비어 있지 않은 경우 확인을 누르면 새 원본이 추가 됩니다.](http://nuget.codeplex.com/workitem/257)
* [설치 된 패키지 수가 클 때 대화 상자가 느려지는 경우](http://nuget.codeplex.com/workitem/243)
* [강력한 이름의 어셈블리에 대 한 바인딩 리디렉션 지원](http://nuget.codeplex.com/workitem/238)
* [패키지 참조 추가 ... 패키지 원본에 대 한 드롭다운을 포함할 UI](http://nuget.codeplex.com/workitem/226)
* [NuPack는 구성 파일 이름의 구성 변환 agnostically을 지원 해야 합니다.](http://nuget.codeplex.com/workitem/224)
* [BasePath을 재정의할 수 있습니다 NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [패키지 원본 대체 동작](http://nuget.codeplex.com/workitem/204)
* [GUI에서 충돌](http://nuget.codeplex.com/workitem/201)
* [패키지 추가 대화 상자에 정렬 옵션 추가](http://nuget.codeplex.com/workitem/179)
* [패키지 관리자 콘솔을 지우기 위한 바로 가기 키](http://nuget.codeplex.com/workitem/174)
* [PowerConsole로 인해 NuPack 콘솔이 실패 함](http://nuget.codeplex.com/workitem/166)
* [콘솔 및 패키지 추가 대화 상자는 요청에서 사용자 에이전트를 설정 해야 합니다.](http://nuget.codeplex.com/workitem/141)
* [VSIX의 버전 번호를 설정 하 고 빌드에 NuPack.exe 합니다.](http://nuget.codeplex.com/workitem/134)
* [-?에서 일반적인 PowerShell 매개 변수를 숨깁니다.](http://nuget.codeplex.com/workitem/118)
* [콘솔 명령에 대 한 자세한 도움말 추가 정보](http://nuget.codeplex.com/workitem/110)
* [패키지 추가 대화 상자에서 현재 패키지 원본 선택을 허용 해야 함](http://nuget.codeplex.com/workitem/88)
* [NuPack. 핵심 클래스를 다른 네임 스페이스로 이동 합니다.](http://nuget.codeplex.com/workitem/50)
* [Cmdlet에 도움말 추가](http://nuget.codeplex.com/workitem/23)
* [패키지 다운로드 후 피드에 대 한 해시 확인](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

다음은 CTP 2에서 가장 중요 한 변경 내용입니다.

* ATOM에서 OData 서비스 끝점으로 패키지 피드 전환: NuGet의 CTP2 버전으로 업그레이드 하는 경우 패키지 원본으로 다음 URL을 추가 해야 `https://feed.nuget.org/ctp2/odata/v1/` 합니다.
* Add-Package 명령의 이름을 *Install-Package* 로 바꾸었습니다.
* 형식이 업데이트 되었습니다 `.nuspec` . `.nuspec`이제 형식에는 패키지 추가 대화 상자에 표시 되는 32x32 png 아이콘을 지정 하기 위한 *iconurl* 필드가 포함 됩니다. 따라서 패키지를 구분할 수 있도록 설정 해야 합니다. `.nuspec`이 형식에는 패키지에 대 한 자세한 정보를 제공 하는 웹 페이지를 가리키는 데 사용할 수 있는 새 *projectUrl* 필드도 포함 됩니다.

이 빌드는 이전 파일에서 작동 하지 않습니다 `.nupkg` . Null 참조 예외가 발생 하면 이전 파일을 사용 하 `.nupkg` 고 업데이트 된 [NuGet 명령줄 도구](http://nuget.codeplex.com/releases/52017/download/165468)를 사용 하 여 다시 빌드해야 합니다.

다음은 NuGet CTP 2에 대해 수정 된 기능 및 버그의 목록입니다 (사소한 코드 정리 간격 등에 대 한 버그는 포함 하지 않음).

* [어셈블리의 TargetFramework가 지정 때 패키지 어셈블리의 압축을 푸는 동안 오류가 발생 했습니다.](http://nuget.codeplex.com/workitem/10)
* [NuPack 콘솔 창을 검색 가능 하 게 만들기](http://nuget.codeplex.com/workitem/14)
* [nupack.exe 릴리스 ILMerge](http://nuget.codeplex.com/workitem/19)
* [더 나은 오류/예외 처리](http://nuget.codeplex.com/workitem/24)
* [[Nupack. Core]: PackageManager는 피드 관련 오류를 정상적으로 처리 해야 합니다.](http://nuget.codeplex.com/workitem/28)
* [콘솔에 대 한 새 아이콘이 필요 합니다.](http://nuget.codeplex.com/workitem/29)
* [대화 상자에서 문자열 지역화](http://nuget.codeplex.com/workitem/38)
* [NuPack 캐시가 다운로드 되었습니다. nupack 파일을 메모리에](http://nuget.codeplex.com/workitem/40)
* [NuPack 콘솔: 콘솔 표시를 위한 기본 바로 가기 변경](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem은 공용 속성에 대 한 기본값을 지원 해야 합니다.](http://nuget.codeplex.com/workitem/49)
* [Nuspec 파일을 하나만 포함 하는 폴더에서 nupack.exe를 실행 하려면 해당 nuspec를 사용 해야 합니다.](http://nuget.codeplex.com/workitem/52)
* [프로젝트/솔루션을 로드 하지 않은 경우에도 프로젝트 메뉴가 나타납니다.](http://nuget.codeplex.com/workitem/54)
* [코드 베이스의 클린 클론에 대 한 빌드. cmd 실패](http://nuget.codeplex.com/workitem/56)
* [업데이트 사용 가능 기능](http://nuget.codeplex.com/workitem/57)
* [대화 상자: 대화 상자를 통해 패키지를 추가 하면 콘솔에서 프롬프트가 제거 됩니다.](http://nuget.codeplex.com/workitem/73)
* [' 설치 '를 클릭 하 여 패키지를 추가 하는 것은 시각적 피드백 없이 느리게 표시 되는 경우가 많습니다.](http://nuget.codeplex.com/workitem/80)
* [설치 된 패키지 중 업데이트 된 패키지를 검색할 수 있는 방법은 없습니다.](http://nuget.codeplex.com/workitem/82)
* [대화 상자에서 설치 된 패키지를 업데이트할 수 있는 방법은 없습니다.](http://nuget.codeplex.com/workitem/83)
* [대화 상자에서 설치 된 패키지를 제거할 수 있는 방법은 없습니다.](http://nuget.codeplex.com/workitem/84)
* [&ldquo;패키지 참조 추가 &hellip; &rdquo; 는 설치 된 참조의 상황에 맞는 메뉴에 표시 됩니다.](http://nuget.codeplex.com/workitem/85)
* [콘솔에서 패키지를 업데이트 한 후에는 이전 버전과 새 버전이 설치 된 것으로 모두 표시 됩니다.](http://nuget.codeplex.com/workitem/86)
* [콘솔의 작업은 대화 상자를 사용할 때 사용 후 사라집니다.](http://nuget.codeplex.com/workitem/87)
* [nupack.exe에서 명령줄 구문 분석 정리 ](http://nuget.codeplex.com/workitem/89)
* [패키지 소스에 이름 추가](http://nuget.codeplex.com/workitem/98)
* [패키지 아이콘 포함을 지원 하기 위한 nuspec](http://nuget.codeplex.com/workitem/103)
* [피드 UI에서 URL 복사를 허용 하지 않습니다.](http://nuget.codeplex.com/workitem/105)
* [더 나은 제거 패키지 오류 처리.](http://nuget.codeplex.com/workitem/107)
* [콘솔 창에서 입력은 커서 포커스에 따라 다릅니다.](http://nuget.codeplex.com/workitem/112)
* [오류 메시지가 보입니다.](http://nuget.codeplex.com/workitem/116)
* [설치 되지 않은 패키지에 대 한 Remove-Package의 성능이 잘못 되었습니다.](http://nuget.codeplex.com/workitem/117)
* [패키지 소스가 없으면 패키지를 제거 하지 못합니다.](http://nuget.codeplex.com/workitem/119)
* [패키지 원본을 사용할 수 없을 때 패키지 제거 실패](http://nuget.codeplex.com/workitem/120)
* [패키지 메타 데이터 및 피드에 제목을 추가 합니다.](http://nuget.codeplex.com/workitem/125)
* [-Source 매개 변수를 추가 패키지에 다시 추가 합니다.](http://nuget.codeplex.com/workitem/127)
* [목록-패키지에-Source 매개 변수가 있어야 합니다.](http://nuget.codeplex.com/workitem/128)
* [Nupack 서버를 업데이트 하 여 NuPack 사용자 에이전트가 패키지를 다운로드 하도록 요청](http://nuget.codeplex.com/workitem/142)
* [승인 해야 하는 모든 종속성에 대 한 라이선스를 표시 하는 라이선스 승인 대화 상자](http://nuget.codeplex.com/workitem/145)
* [피드에서 패키지가 throw 될 때 오류 기록](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe 빈 &lt; licenseurl 요소를 허용 하면 안 됩니다. &gt;](http://nuget.codeplex.com/workitem/152)
* [List-Package 이름을 Get 패키지로, Add-Package을 설치-패키지로, Remove-Package를 제거 하려면](http://nuget.codeplex.com/workitem/155)
* [솔루션 탐색기에서 패키지 참조 추가 메뉴 항목을 사용 하면 Visual Studio가 충돌 함](http://nuget.codeplex.com/workitem/158)
* ["사용 가능한 패키지 소스" 레이블에 콜론이 없습니다.](http://nuget.codeplex.com/workitem/160)
* [Nuspec xml 요소와 대/소문자를 일관 되 게 대/소문자 구분](http://nuget.codeplex.com/workitem/161)
* [NuPack VSIX의 매니페스트는 ' 관리 비트 '를 설정 해야 합니다.](http://nuget.codeplex.com/workitem/162)
* [피드 없이 List-Package를 실행 하는 경우 null 참조 오류가 발생 합니다.](http://nuget.codeplex.com/workitem/164)
* [nuget.exe: 대상 경로 지정](http://nuget.codeplex.com/workitem/171)
* [WinXP에서 패키지 관리 콘솔을 여는 Powershell 오류](http://nuget.codeplex.com/workitem/175)
* [패키지 목록을 로드 하는 동안 VS가 충돌 합니다.](http://nuget.codeplex.com/workitem/176)
* [메타 패키지 허용 (파일 없음, 종속성만)](http://nuget.codeplex.com/workitem/180)
* [Powershell 스크립트를 Powershell 2.0 모듈로 변환](http://nuget.codeplex.com/workitem/181)
* [Target이 지정 된 경우 PathResolver는 와일드 카드 문자를 앞 경로 부분을 삭제 해야 합니다.](http://nuget.codeplex.com/workitem/183)
* [종속성 없음](http://nuget.codeplex.com/workitem/186)
* [Elmah 설치 오류](http://nuget.codeplex.com/workitem/192)
* [구성 변환이 configsections에서 제대로 작동 하지 않음 &lt;&gt;](http://nuget.codeplex.com/workitem/194)
* [' $Global:p rojectCache ' 변수는 설정 되지 않았기 때문에 검색할 수 없습니다.](http://nuget.codeplex.com/workitem/203)
* [NuPack 패키지를 만들기 위한 MSBuild 작업 추가](http://nuget.codeplex.com/workitem/205)
* [목록-패키지 검색/필터링을 지원 해야 함](http://nuget.codeplex.com/workitem/206)
* [패키지 작성자가 라이선스 URL을 제공 하는 경우 항상 라이선스에 대 한 링크를 표시 합니다.](http://nuget.codeplex.com/workitem/208)
* [패키지 제거와 관련 하 여 "액세스 거부" 예외가 가끔 발생 합니다.](http://nuget.codeplex.com/workitem/213)
* [단위 테스트 실패: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [특정 framework 버전을 찾을 수 없는 경우 대체/기본 파일 집합을 허용 합니다.](http://nuget.codeplex.com/workitem/223)
* [패키지 참조 추가 ... UI에서 패키지를 제거할 수 없습니다.](http://nuget.codeplex.com/workitem/225)
* [하나 이상의 프로젝트가 언로드될 때 패키지 참조 충돌 스튜디오 추가](http://nuget.codeplex.com/workitem/228)
* [구성 변환이 web.debug.config 파일에서 작동 하지 않는 것 같습니다.](http://nuget.codeplex.com/workitem/229)
* [ 사용자 지정 패키지에서 발생 하는init.ps1](http://nuget.codeplex.com/workitem/237)
* [Feedlist에 경로를 추가 하는 경우 기본 단추가 확인으로 설정 되어 있으므로 ENTER 키를 누르면 자동으로 닫힙니다.](http://nuget.codeplex.com/workitem/240)
* [종속성을 제거 하려고 하면 행에서 2 번 시도 하면 VS가 중단 됩니다.](http://nuget.codeplex.com/workitem/241)
* [패키지 추가 대화 상자에 프로젝트 URL 표시](http://nuget.codeplex.com/workitem/253)
* [설치 된 패키지에 대 한 Add-Package 대화 상자 기본값](http://nuget.codeplex.com/workitem/254)
* [패키지 추가 대화 상자 메뉴 항목을 변경 합니다.](http://nuget.codeplex.com/workitem/261)
* [네임 스페이스 및 어셈블리 이름 바꾸기](http://nuget.codeplex.com/workitem/274)
* [NuPack 프로젝트의 이름을 NuGet으로 바꿉니다.](http://nuget.codeplex.com/workitem/282)
* [종속성 목록 아래에 다음 텍스트를 추가 합니다.](http://nuget.codeplex.com/workitem/288)
* [라이선스 승인 대화 상자에서 라이선스 승인 텍스트를 변경 합니다.](http://nuget.codeplex.com/workitem/291)
* [패키지 목록 위의 라이선스 승인 대화 상자에서 텍스트를 변경 합니다.](http://nuget.codeplex.com/workitem/292)
* [OData가 fwlink URL을 사용 하지 않습니다.](http://nuget.codeplex.com/workitem/304)
* [패키지 관리자 UI: 페이징에 사용 되는 패키지 수의 적극적인 캐싱](http://nuget.codeplex.com/workitem/317)
* [NuPack/NuGet- &gt; 패키지 관리자 콘솔 오류](http://nuget.codeplex.com/workitem/335)
* [패키지 추가 대화 상자에 이미 설치 된 패키지에 대 한 라이선스 동의가 표시 됨](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

다음은 NuGet CTP 1에 대해 수정 된 기능 및 버그의 목록입니다.

* [패키지 확장의 이름을로 변경 해야 합니다. nupack](http://nuget.codeplex.com/workitem/1)
* [패키지 파일을 폴더로 이동](http://nuget.codeplex.com/workitem/2)
* [Merge install &amp; PS 명령 추가](http://nuget.codeplex.com/workitem/3)
* [Verb-Noun cmdlet에 대 한 별칭 만들기](http://nuget.codeplex.com/workitem/4)
* [VS에서 솔루션을 전환할 때 NuPack가 혼동 됨](http://nuget.codeplex.com/workitem/6)
* [기본적으로 ' 패키지 ' 솔루션 폴더를 숨겨야 합니다.](http://nuget.codeplex.com/workitem/11)
* [콘텐츠 항목에서 토큰 바꾸기에 대 한 지원을 추가 합니다.](http://nuget.codeplex.com/workitem/12)
* [NuPack. UI는 Register-packagesource API를 사용 해야 합니다.](http://nuget.codeplex.com/workitem/26)
* [[Nupack. Core]: PackageManager 패키지를 설치 하기 전에 설치 된 것으로 표시 합니다.](http://nuget.codeplex.com/workitem/27)
* [솔루션에서 기본 프로젝트를 삭제 해도 삭제 된 프로젝트가 기본값으로 표시 됩니다.](http://nuget.codeplex.com/workitem/30)
* [새 패키지는 "지정 된 URI가 이미 패키지에 있기 때문에 파트를 추가할 수 없습니다."와 함께 실패 합니다.](http://nuget.codeplex.com/workitem/32)
* [Visual Studio GUI에서 "NuPack" 문자열을 제거 합니다.](http://nuget.codeplex.com/workitem/35)
* [COPYRIGHT.txt 파일에 Apache 헤더 추가](http://nuget.codeplex.com/workitem/36)
* [Update-PackageSource 명령 제거](http://nuget.codeplex.com/workitem/37)
* [프로필을 로드할 때 패키지 관리자를 사용할 수 없습니다. 예외 발생](http://nuget.codeplex.com/workitem/39)
* [init.ps1, install.ps1 및 uninstall.ps1 추가 상태를 받아야 합니다.](http://nuget.codeplex.com/workitem/41)
* [콘솔과 GUI 패키지를 하나의 패키지로 결합](http://nuget.codeplex.com/workitem/42)
* [루트에 있지 않은 XML에 적용 하는 경우 xml 변환 논리가 작동 하지 않습니다.](http://nuget.codeplex.com/workitem/43)
* [패키지 원본 설정 관리 대화 상자가 NuPack 콘솔을 업데이트 하지 않음](http://nuget.codeplex.com/workitem/44)
* [NuPack 콘솔 UI: ' 패키지 피드 ' 드롭다운 목록의 이름을 ' 패키지 원본 '으로 바꿉니다.](http://nuget.codeplex.com/workitem/45)
* [NuPack 콘솔 옵션: NuPack 콘솔과 일치 하도록 ' 리포지토리 UI ' 이름 바꾸기](http://nuget.codeplex.com/workitem/46)
* [추가-패키지가 IIS 또는 URL에서 열린 웹 사이트에 대해 실패 합니다.](http://nuget.codeplex.com/workitem/53)
* [패키지 관리자 원본이 FwLink에서 작동 하지 않음](http://nuget.codeplex.com/workitem/55)
* [기본 패키지 원본 설정](http://nuget.codeplex.com/workitem/59)
* [옵션에서 패키지 소스를 추가할 때 원본 중 하나만 제공 되는 경우에는 기본 것으로 가정 합니다.](http://nuget.codeplex.com/workitem/60)
* [대화 상자 UI는 가짜 "최근" 패키지를 표시 합니다.](http://nuget.codeplex.com/workitem/62)
* [옵션: 취소를 클릭 해도 변경 내용이 취소 되지 않습니다.](http://nuget.codeplex.com/workitem/63)
* [패키지 참조 추가 대화 상자 검색은 대/소문자를 구분 하지 않아야 함](http://nuget.codeplex.com/workitem/65)
* [AssemblyInfo.cs 파일에서 회사 메타 데이터 수정](http://nuget.codeplex.com/workitem/67)
* [VSIX의 버전 번호](http://nuget.codeplex.com/workitem/71)
* [제거 패키지:-? 사용 도움말을 두 번 표시 합니다.](http://nuget.codeplex.com/workitem/72)
* [프로젝트 수준 패키지의 설치/제거 패키지 실행](http://nuget.codeplex.com/workitem/74)
* [Nupack 하나가 유효성 검사에 실패 하면 서버에서 피드를 만들 수 없음](http://nuget.codeplex.com/workitem/90)
* [NuPack 아이콘을 바꾸어야 합니다.](http://nuget.codeplex.com/workitem/94)
* [NTLM http 프록시가 패키지 피드에 대해 인증 하지 않습니다.](http://nuget.codeplex.com/workitem/96)
* [대화 상자는 항상 VS 창에서 가운데에 배치 됩니다.](http://nuget.codeplex.com/workitem/100)
* [패키지 정보의 많은 필드가 대화 상자에 채워지지 않습니다.](http://nuget.codeplex.com/workitem/102)
* [대화 상자 UI에 저자의 이름이 표시 되지 않습니다.](http://nuget.codeplex.com/workitem/108)
* [제거 패키지에 대 한 버전](http://nuget.codeplex.com/workitem/113)
* [대화 상자 UI의 최근 탭 제거](http://nuget.codeplex.com/workitem/115)
* [대화 상자 UI를 하나 이상 연 후 솔루션 폴더를 마우스 오른쪽 단추로 클릭 하면 VS가 충돌 합니다.](http://nuget.codeplex.com/workitem/126)
* [List-Package의-Local 매개 변수를-Installed로 변경 합니다.](http://nuget.codeplex.com/workitem/129)
* [NuPack.configpackages.xml 이름 바꾸기 ](http://nuget.codeplex.com/workitem/132)
* [콘솔이 줄의 끝에 커서를 강제로 적용 합니다.](http://nuget.codeplex.com/workitem/135)
* [제거-패키지 intellisense가 손상 되었습니다.](http://nuget.codeplex.com/workitem/136)
* [Nuspec 및 피드에 RequireLicenseAcceptance 플래그 추가](http://nuget.codeplex.com/workitem/137)
* [Nuspec 형식 및 패키지 피드에 LicenseUrl 추가](http://nuget.codeplex.com/workitem/138)
* [동의 해야 하는 패키지에 대해 설치를 클릭 하면 승인 대화 상자가 표시 됩니다.](http://nuget.codeplex.com/workitem/139)
* [패키지 추가 대화 상자에 부인 텍스트 추가](http://nuget.codeplex.com/workitem/140)
* [패키지 콘솔이 처음 실행 될 때 부인 추가](http://nuget.codeplex.com/workitem/143)
* [콘솔에서 패키지 설치 후의 고 지 사항 표시](http://nuget.codeplex.com/workitem/144)
* [. Nupack 확장의 이름을 nupkg로 바꿉니다.](http://nuget.codeplex.com/workitem/146)