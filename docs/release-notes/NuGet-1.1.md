---
title: NuGet 1.0 및 1.1 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하 여 NuGet 1.1에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6222a996f2fdcaaa81a1b16d1c6da2749936712a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547023"
---
# <a name="nuget-10-and-11-release-notes"></a>NuGet 1.0 및 1.1 릴리스 정보

[NuGet 1.2 릴리스 정보](../release-notes/nuget-1.2.md)

NuGet 1.0은 2011 년 1 월 13 일에 출시 되었습니다.  NuGet 1.1은 2011 년 2 월 12 일에 출시 되었습니다.

## <a name="overview"></a>개요

이 문서는 다양 한 릴리스의 주요 미리 보기 버전에 따라 그룹화 하는 NuGet 1.0에 대 한 릴리스 정보를 포함 합니다.

NuGet은 다음 구성 요소를 포함 합니다.

* *NuGet.Tools.vsix* * 구성:
  * **추가 라이브러리 패키지 대화 상자** * 찾아보기 및 패키지를 설치 하는 데 사용 되는 Visual Studio 내에서 대화 합니다.
  * **패키지 관리자 콘솔** * Powershell 기반 Visual Studio 내에서 콘솔.
* *NuGet 명령줄 도구* * 도구 패키지 만들기 (및 결과적으로 게시)를 사용 합니다.

NuGet 도구 Visual Studio 확장 (*NuGet.Tools.vsix*) 필요 합니다.

* Visual Studio 2010 또는 Visual Web Developer 2010 Express입니다.

NuGet 명령줄 도구에는 다음이 필요합니다.

* .NET framework 버전 4

## <a name="installation"></a>설치

이 사용 하도록 [최신 릴리스](http://nuget.codeplex.com/releases/view/52018):

* 먼저 이전 빌드를 제거 합니다. 이 작업을 수행 하려면 관리자 권한으로 VS를 실행 해야 합니다.
* 해야 하는 모든 기존 피드를 제거 합니다.
* 새 피드를 가리키는 추가 [ http://go.microsoft.com/fwlink/?LinkId=206669 ](http://go.microsoft.com/fwlink/?LinkId=206669)합니다.

## <a name="nuget-11"></a>NuGet 1.1

이 릴리스에서 해결 된 문제 목록을 [여기에 있음](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

한 가지 문제는 RC 이후의 RTM에 대 한 수정 되었습니다.

* [솔루션의 모든 프로젝트를 영향을 줍니다 474 문제: 패키지를 제거 합니다.](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>릴리스 후보

다음은 CTP 2 이후 릴리스 후보에서 변경 합니다. 버그의 전체 목록을 보려면 Issue Tracker를 방문 합니다.

* [콘솔에서 패키지를 업데이트 하는 중 종속성 업데이트 되지 않습니다.](http://nuget.codeplex.com/workitem/443)
* [Bin 추가 패키지 선택 하지 패키지 참조 (CTP1)](http://nuget.codeplex.com/workitem/442)
* [끊어진된 참조를 유지 하는 패키지를 업데이트 하는 중](http://nuget.codeplex.com/workitem/440)
* [패키지 가져오기-업데이트 실패 대화 상자에서 또는 콘솔에서 '모두' 집계 소스를 선택한 경우](http://nuget.codeplex.com/workitem/439)
* [패키지 확인 오류가 발생](http://nuget.codeplex.com/workitem/426)
* [추가 패키지 대화 상자에서 패키지를 설치할 수 없는 경우 사용자에 게 경으십시오](http://nuget.codeplex.com/workitem/425)
* [패키지 가져오기-많은 수의 패키지를 업데이트 하는 경우 throw 업데이트](http://nuget.codeplex.com/workitem/424)
* [Nuspec 파일 올바르게 작성 된 때의 오류 처리를 개선합니다](http://nuget.codeplex.com/workitem/423)
* [지정 된 파일을 무시 하는 Nuget 팩](http://nuget.codeplex.com/workitem/422)
* [마지막 두 번째 패키지 소스를 제거 하 고 "아래로 이동"을 클릭 한 다음에 VS 충돌](http://nuget.codeplex.com/workitem/418)
* [패키지를 설치 하는 동안 어셈블리 참조를 제거 합니다.](http://nuget.codeplex.com/workitem/413)
* [설정 대화 상자를 열 때 InvalidOperationException](http://nuget.codeplex.com/workitem/411)
* [패키지 관리자 콘솔에서 패키지 원본에 대 한 액세스 키가 작동 하지 않습니다.](http://nuget.codeplex.com/workitem/410)
* [VS NuGet 설정 대화 상자 액세스 키에 포커스를 잘못 된 필드](http://nuget.codeplex.com/workitem/409)
* [패키지 ID intellisense은 너무 많은 항목을 쿼리하지 않습니다.](http://nuget.codeplex.com/workitem/404)
* [프로젝트 이름에 점 문자를 사용 하 여 프로젝트에 패키지 추가 실패](http://nuget.codeplex.com/workitem/403)
* [Nuspec에서 지정 된 파일을 사용 하 여 발급](http://nuget.codeplex.com/workitem/400)
* [최신 빌드를 사용 하는 경우 올바른 공식 피드 등록 해야](http://nuget.codeplex.com/workitem/399)
* [태그 # 대신 공간을 사용 해야](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata 없는 몇 가지 유용한 정보](http://nuget.codeplex.com/workitem/388)
* [대화 상자에 신고 링크 추가](http://nuget.codeplex.com/workitem/386)
* [App_Data를 사용 하 여 Visual Studio에서 패키지 나누기 압축을 풀](http://nuget.codeplex.com/workitem/380)
* [태그를 구현 합니다.](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder 만들려는 종속성이 없는 빈 패키지를 수 있습니다.](http://nuget.codeplex.com/workitem/373)
* [패키지에 대 한 소유자 필드를 추가 합니다.](http://nuget.codeplex.com/workitem/365)
* [VSIX 도구 보다는 NuGet 패키지 관리자를 VSIX 매니페스트 업데이트](http://nuget.codeplex.com/workitem/364)
* [패키지 가져오기 명령을 모든 원본이 선택 되 면 오류 throw](http://nuget.codeplex.com/workitem/359)
* [옵션 대화 상자에서 패키지 소스의 순서를 허용 합니다.](http://nuget.codeplex.com/workitem/356)
* [업데이트 패키지는 이전 버전을 제거 하지 않습니다.](http://nuget.codeplex.com/workitem/352)
* [종속성에 대 한 구현 버전 범위 지정](http://nuget.codeplex.com/workitem/347)
* ["새 패키지 추가"를 클릭 하면 visual Studio가 충돌](http://nuget.codeplex.com/workitem/346)
* [추가 패키지 대화 상자에서 다운로드 및 등급을 표시](http://nuget.codeplex.com/workitem/345)
* [대화 상자에서 패키지 원본을 변경 하면 활성 원본 업데이트 되지 않습니다.](http://nuget.codeplex.com/workitem/344)
* [패키지 관리자 콘솔 창에 대 한 키 바인딩을 제거합니다](http://nuget.codeplex.com/workitem/339)
* [Install-package cmdlet의 이름으로 인식 되지 않습니다...](http://nuget.codeplex.com/workitem/338)
* [일반 공급으로 종속성을 공급 하는 로컬에서 패키지를 설치 하는 확인 되지 않습니다.](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies 사용에서 되는 종속성 건너뛰어야 합니다.](http://nuget.codeplex.com/workitem/331)
* [페이지 탐색을 취소 하는 경우 사용자 원래 페이지 요청을 반환 하는 동안 다른 페이지로 이동할 수 없습니다.](http://nuget.codeplex.com/workitem/325)
* [많은 수의 패키지를 사용 하 여 피드를 처리 하기 위한 NuPack.Server의 성능을 조사 합니다.](http://nuget.codeplex.com/workitem/324)
* [패키지에 대 한 필터링 있습니까 두 번째 시간 이전에 선택한 원본 대신 "New" 패키지 원본을 사용 합니다.](http://nuget.codeplex.com/workitem/321)
* [대화 상자에서 "Online" 탭을 선택 하는 경우 기본 패키지 소스를 선택 해야 합니다.](http://nuget.codeplex.com/workitem/320)
* [기본적으로 설치 된 패키지를 표시 해야 패키지 목록](http://nuget.codeplex.com/workitem/309)
* [어셈블리 참조 HintPaths](http://nuget.codeplex.com/workitem/294)
* [패키지 관리자 콘솔을 여는 동안 예외](http://nuget.codeplex.com/workitem/268)
* [콘솔 intellisense 다운로드 전체 피드](http://nuget.codeplex.com/workitem/259)
* [패키지 소스 '기본값' '활성'으로 바꿔야](http://nuget.codeplex.com/workitem/258)
* [패키지 원본 UI: 확인을 클릭 해야 새 원본을 추가 이름/소스 필드가 비어 있지 않은 경우](http://nuget.codeplex.com/workitem/257)
* [대화가 설치 된 패키지 수가 큰 경우 매우 느린](http://nuget.codeplex.com/workitem/243)
* [강력한 이름의 어셈블리에 대 한 바인딩 리디렉션을 지원합니다](http://nuget.codeplex.com/workitem/238)
* [패키지 참조 추가... 패키지 원본에 대 한 드롭 다운 포함 하도록 UI를](http://nuget.codeplex.com/workitem/226)
* [NuPack은 config 파일 이름의 agnostically config 변환 지원 해야 합니다.](http://nuget.codeplex.com/workitem/224)
* [BasePath를 NuPack.exe에 재정의 될 수 있습니다.](http://nuget.codeplex.com/workitem/222)
* [패키지 원본에 대 한 대체 (fallback) 동작](http://nuget.codeplex.com/workitem/204)
* [GUI에서 충돌](http://nuget.codeplex.com/workitem/201)
* [정렬 옵션을 추가 하는 패키지 대화 상자 추가](http://nuget.codeplex.com/workitem/179)
* [바로 가기 키를 패키지 관리자 콘솔 지우기](http://nuget.codeplex.com/workitem/174)
* [PowerConsole는 NuPack 콘솔 실패 발생](http://nuget.codeplex.com/workitem/166)
* [콘솔 및 패키지 대화 상자 추가 요청에 사용자 에이전트를 설정 해야](http://nuget.codeplex.com/workitem/141)
* [빌드에는 VSIX 및 NuPack.exe의 버전 번호를 설정 합니다.](http://nuget.codeplex.com/workitem/134)
* [-일반적인 PowerShell 매개 변수 숨기기](http://nuget.codeplex.com/workitem/118)
* [콘솔 명령에 대 한 자세한 도움말-추가](http://nuget.codeplex.com/workitem/110)
* [패키지 대화 상자에서 현재 패키지 소스를 선택 하면 허용 해야 추가](http://nuget.codeplex.com/workitem/88)
* [다른 네임 스페이스로 이동 NuPack.Core 클래스](http://nuget.codeplex.com/workitem/50)
* [Cmdlet 도움말 추가](http://nuget.codeplex.com/workitem/23)
* [패키지 다운로드 후 피드에서 해시를 확인 하십시오.](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

다음은 CTP 2에서 가장 중요 한 변경입니다.

* 패키지는 OData 서비스 끝점에 atom에서 피드를 전환: NuGet의 CTP2 버전으로 업그레이드 하는 경우 추가 해야 다음 URL을 패키지 소스로: `https://feed.nuget.org/ctp2/odata/v1/`합니다.
* 패키지 추가 명령은 이름을 바꿀 *Install-package*합니다.
* 업데이트 된 `.nuspec` 형식입니다. 합니다 `.nuspec` 형식을 이제는 *iconUrl* 추가 패키지 대화 상자에 표시 되는 32 x 32 png 아이콘을 지정 하기 위한 필드입니다. 따라서 패키지를 구분 하기 위해 설정 해야 합니다. 합니다 `.nuspec` 형식으로 새 포함 *projectUrl* 패키지에 대 한 자세한 정보를 제공 하는 웹 페이지를 가리키도록 하는 데 사용할 수 있는 필드입니다.

이전이이 빌드가 작동 하지 것입니다 `.nupkg` 파일입니다. 이전을 사용 하는 null 참조 예외를 가져오면 `.nupkg` 파일을 업데이트 하 여 다시 빌드해야 [NuGet 명령줄 도구](http://nuget.codeplex.com/releases/52017/download/165468)합니다.

다음은 기능 및 (사소한 코드 정리 등에 대 한 버그 포함 되지 않습니다.) NuGet CTP 2 용 해결 된 버그의 목록입니다.

* [압축 풀기 패키지 어셈블리 오류 때 어셈블리에 대 한 TargetFramework 지정 합니다.](http://nuget.codeplex.com/workitem/10)
* [NuPack 콘솔 창을 더 쉽게 검색할 수 확인](http://nuget.codeplex.com/workitem/14)
* [ILMerge nupack.exe 릴리스](http://nuget.codeplex.com/workitem/19)
* [향상 된 오류/예외 처리](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager 피드 관련 오류를 정상적으로 처리 해야](http://nuget.codeplex.com/workitem/28)
* [콘솔에 대 한 새 아이콘 필요](http://nuget.codeplex.com/workitem/29)
* [대화 상자에서 문자열 지역화](http://nuget.codeplex.com/workitem/38)
* [NuPack 캐시 메모리에.nupack 파일 다운로드](http://nuget.codeplex.com/workitem/40)
* [NuPack 콘솔: 콘솔을 표시 하는 것에 대 한 기본 바로 가기 변경](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem 공용 속성에 대 한 기본값을 지원 해야](http://nuget.codeplex.com/workitem/49)
* [해당 nuspec을 사용할지 nupack.exe 폴더에서는 하나의 nuspec 파일 실행](http://nuget.codeplex.com/workitem/52)
* [프로젝트/솔루션이 로드 될 때에 프로젝트 메뉴 표시](http://nuget.codeplex.com/workitem/54)
* [build.cmd 코드 베이스의 정리 복제본에서 실패](http://nuget.codeplex.com/workitem/56)
* [사용 가능한 기능 업데이트](http://nuget.codeplex.com/workitem/57)
* [콘솔에서 메시지를 제거 대화 상자를 통해 대화 상자:](http://nuget.codeplex.com/workitem/73)
* [시각적 피드백을 사용 하 여 느린 경우가 '설치'를 클릭 하 여 패키지 추가](http://nuget.codeplex.com/workitem/80)
* [업데이트를 포함 하는 내 설치 된 패키지는 검색할 방법이 없습니다.](http://nuget.codeplex.com/workitem/82)
* [대화 상자에서 설치 된 패키지를 업데이트할 방법이 없습니다.](http://nuget.codeplex.com/workitem/83)
* [대화 상자에서 설치 된 패키지를 제거 하려면 없으므로](http://nuget.codeplex.com/workitem/84)
* [&ldquo;패키지 참조 추가&hellip; &rdquo; 설치 참조의 상황에 맞는 메뉴에 표시 됩니다.](http://nuget.codeplex.com/workitem/85)
* [콘솔에서 패키지를 업데이트 한 후 것으로 표시 되므로 이전 버전과 새 버전 설치](http://nuget.codeplex.com/workitem/86)
* [대화 상자를 사용 하는 경우 콘솔의 작업은 사용 후 사라집니다.](http://nuget.codeplex.com/workitem/87)
* [정리 명령줄 nupack.exe에서 구문 분석](http://nuget.codeplex.com/workitem/89)
* [패키지 소스에 친숙 한 이름 추가](http://nuget.codeplex.com/workitem/98)
* [.Nuspec 패키지 아이콘 포함 하 여 지원 하도록 업데이트](http://nuget.codeplex.com/workitem/103)
* [피드 UI URL을 복사를 허용 하지 않습니다.](http://nuget.codeplex.com/workitem/105)
* [향상 된 패키지 제거 오류 처리 합니다.](http://nuget.codeplex.com/workitem/107)
* [커서 포커스에 따라 달라 집니다 콘솔 창에 입력 합니다.](http://nuget.codeplex.com/workitem/112)
* [오류 메시지를 가져오므로 좋지 않습니다 확인](http://nuget.codeplex.com/workitem/116)
* [설치 되어 있지 않은 패키지에 대 한 제거 패키지의 성능 잘못 되었습니다.](http://nuget.codeplex.com/workitem/117)
* [패키지 소스 있으면 실패 패키지 제거](http://nuget.codeplex.com/workitem/119)
* [패키지 원본을 사용할 수 없는 경우 패키지 제거 실패](http://nuget.codeplex.com/workitem/120)
* [패키지 메타 데이터를 피드 제목을 추가 합니다.](http://nuget.codeplex.com/workitem/125)
* [추가-소스 매개 변수 추가 패키지를 다시](http://nuget.codeplex.com/workitem/127)
* [패키지 목록 있어야-원본 매개 변수](http://nuget.codeplex.com/workitem/128)
* [NuPack.Server NuPack 사용자 에이전트를 다운로드 패키지를 요구 하도록 업데이트](http://nuget.codeplex.com/workitem/142)
* [라이선스 승인 대화 상자가 동의 필요로 하는 모든 종속성에 대 한 라이선스를 나열 해야 합니다.](http://nuget.codeplex.com/workitem/145)
* [피드에서 패키지를 throw 하는 경우 오류를 기록 합니다.](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe 빈을 허용 하지 않아야 &lt;licenseurl&gt; 요소](http://nuget.codeplex.com/workitem/152)
* [Get-패키지에 추가 패키지 설치-패키지 및 패키지 제거를 제거 패키지 목록 패키지 이름 바꾸기](http://nuget.codeplex.com/workitem/155)
* [솔루션 탐색기에서 패키지 참조 추가 메뉴 항목을 사용 하 여 Visual Studio 작동이 중단.](http://nuget.codeplex.com/workitem/158)
* ["사용 가능한 패키지 소스" 레이블을 콜론이 없는 합니다.](http://nuget.codeplex.com/workitem/160)
* [.Nuspec xml 요소 대/소문자 구분 일관 되 게 카멜식 대/소문자를 확인 합니다.](http://nuget.codeplex.com/workitem/161)
* [NuPack VSIX 매니페스트를 'admin' 비트를 설정 해야 합니다.](http://nuget.codeplex.com/workitem/162)
* [Null 참조 오류 메시지가 없는 피드 목록 패키지를 실행 하는 경우](http://nuget.codeplex.com/workitem/164)
* [nuget.exe: 대상 경로 지정](http://nuget.codeplex.com/workitem/171)
* [Powershell 오류 winxp 패키지 관리 콘솔을 열고](http://nuget.codeplex.com/workitem/175)
* [패키지 목록을 로드 하는 동안 VS 충돌](http://nuget.codeplex.com/workitem/176)
* [메타 패키지 (없습니다 파일, 종속성만)를 허용 합니다.](http://nuget.codeplex.com/workitem/180)
* [Powershell 스크립트를 Powershell 2.0으로 변환](http://nuget.codeplex.com/workitem/181)
* [대상 지정 되 면 PathResolver 경로 부분 앞의 와일드 카드 문자를 무시 해야](http://nuget.codeplex.com/workitem/183)
* [종속성 없음](http://nuget.codeplex.com/workitem/186)
* [Elmah를 설치 하는 오류](http://nuget.codeplex.com/workitem/192)
* [Config 변환 사용 하 여 제대로 작동 하지 않습니다 &lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [변수 ' $global: projectCache' 설정 되지 않았기 때문에 검색할 수 없습니다.](http://nuget.codeplex.com/workitem/203)
* [NuPack 패키지를 만들기 위한 MSBuild 작업 추가](http://nuget.codeplex.com/workitem/205)
* [목록 패키지를 검색 하 고 필터링을 지원 해야 합니다.](http://nuget.codeplex.com/workitem/206)
* [패키지 작성자는 라이선스 URL을 제공 하는 경우 라이선스에 대 한 링크를 항상 표시](http://nuget.codeplex.com/workitem/208)
* [패키지 제거를 사용 하 여 가끔 "액세스 거부" 예외](http://nuget.codeplex.com/workitem/213)
* [단위 테스트 실패: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [특정 프레임 워크 버전을 찾을 수 없는 경우 파일의 대체 (fallback) / 기본 집합에 대 한 허용](http://nuget.codeplex.com/workitem/223)
* [패키지 참조 추가... UI에서 패키지를 제거할 수 없습니다.](http://nuget.codeplex.com/workitem/225)
* [패키지 참조에는 하나의 studio 작동이 중단 되거나 더 많은 프로젝트를 로드 되지 추가](http://nuget.codeplex.com/workitem/228)
* [Config 변환 web.debug.config 파일에서 작동 하도록 표시 되지 않습니다.](http://nuget.codeplex.com/workitem/229)
* [init.ps1 사용자 지정 패키지에 실행 되지 않음](http://nuget.codeplex.com/workitem/237)
* [자동으로 닫히면 ENTER를 누를 경우 경로는 피드를 추가할 때 기본 단추 [확인]로 설정 되어](http://nuget.codeplex.com/workitem/240)
* [제거 하려면 행에서 2 번을 시도 하는 경우 종속성 VS 충돌](http://nuget.codeplex.com/workitem/241)
* [패키지 추가 대화 상자에서 프로젝트 URL 표시](http://nuget.codeplex.com/workitem/253)
* [기본 설치 패키지에 패키지 추가 대화 상자](http://nuget.codeplex.com/workitem/254)
* [추가 패키지 대화 상자 메뉴 항목을 변경 합니다.](http://nuget.codeplex.com/workitem/261)
* [네임 스페이스 및 어셈블리 이름 바꾸기](http://nuget.codeplex.com/workitem/274)
* [Nuget NuPack 프로젝트 이름 바꾸기](http://nuget.codeplex.com/workitem/282)
* [종속성 목록이 아래에 다음 텍스트를 추가 합니다.](http://nuget.codeplex.com/workitem/288)
* [라이선스 승인 대화 상자에서 라이선스 동의 텍스트 변경](http://nuget.codeplex.com/workitem/291)
* [패키지 목록 위의 라이선스 승인 대화 상자에서 텍스트를 변경 합니다.](http://nuget.codeplex.com/workitem/292)
* [OData는 URL을 fwlink 사용 하 여 작동 하지 않습니다.](http://nuget.codeplex.com/workitem/304)
* [패키지 관리자 UI: 페이징에 사용 되는 패키지 개수의 적극적인 캐싱에 대](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet-&gt; 패키지 관리자 콘솔 오류](http://nuget.codeplex.com/workitem/335)
* [라이선스 승인에 대 한 이미 설치 된 패키지 패키지 대화 상자에 표시 추가](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

다음은 기능 및 NuGet CTP 1에 대 한 해결 된 버그의 목록입니다.

* [패키지 확장.nupack을 바꿔야](http://nuget.codeplex.com/workitem/1)
* [폴더로 이동 하는 패키지 파일](http://nuget.codeplex.com/workitem/2)
* [설치를 병합 &amp; 추가 PS 명령](http://nuget.codeplex.com/workitem/3)
* [동사-명사 cmdlet에 대 한 별칭 만들기](http://nuget.codeplex.com/workitem/4)
* [NuPack 가져옵니다 VS에서 솔루션을 전환 하는 경우 혼동 됩니다.](http://nuget.codeplex.com/workitem/6)
* [기본적으로 '패키지' 솔루션 폴더를 숨겨야](http://nuget.codeplex.com/workitem/11)
* [콘텐츠 항목에 토큰 교체에 대 한 지원을 추가 합니다.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI는 PackageSource API를 사용 해야](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager 설치 하기 전에 설치 된 패키지 표시](http://nuget.codeplex.com/workitem/27)
* [솔루션에서 기본 프로젝트를 삭제 하는 여전히 삭제 된 프로젝트 기본값으로 표시](http://nuget.codeplex.com/workitem/30)
* [새 패키지 "파트 추가할 수 없습니다 지정된 된 URI에 대 한 패키지에 이미 있기 때문에."와 함께 실패](http://nuget.codeplex.com/workitem/32)
* [Visual Studio GUI에서 "NuPack" 문자열을 제거 합니다.](http://nuget.codeplex.com/workitem/35)
* [COPYRIGHT.txt에 Apache 헤더 파일 추가](http://nuget.codeplex.com/workitem/36)
* [업데이트 PackageSource 명령 제거](http://nuget.codeplex.com/workitem/37)
* [패키지 관리자 프로필을 로드할 때 사용할 수 없는 예외를 throw 합니다.](http://nuget.codeplex.com/workitem/39)
* [init.ps1, install.ps1 및 uninstall.ps1 추가 상태를 수신 해야](http://nuget.codeplex.com/workitem/41)
* [콘솔 및 GUI 패키지를 하나의 패키지로 결합](http://nuget.codeplex.com/workitem/42)
* [Xml 변환 논리 루트에 없는 XML에 적용 하는 경우 작동 하지 않습니다.](http://nuget.codeplex.com/workitem/43)
* [관리 패키지 원본 설정 대화 상자를 NuPack 콘솔을 업데이트 하지 않습니다](http://nuget.codeplex.com/workitem/44)
* [이름 바꾸기 '패키지 소스' '패키지 피드' 드롭 다운 목록 NuPack 콘솔 UI:](http://nuget.codeplex.com/workitem/45)
* [NuPack 콘솔 옵션: NuPack 콘솔을 사용 하 여 일치 하도록 ' 리포지토리 UI' 이름 바꾸기](http://nuget.codeplex.com/workitem/46)
* [IIS 또는 URL에서 열려 있는 웹 사이트에 대 한 패키지 추가 실패](http://nuget.codeplex.com/workitem/53)
* [패키지 관리자 원본 FwLink를 사용 하 여 작동 하지 않습니다.](http://nuget.codeplex.com/workitem/55)
* [기본 패키지 소스를 설정 합니다.](http://nuget.codeplex.com/workitem/59)
* [에 추가할 때 패키지 원본 옵션에서 하나의 원본만 제공 될 때 기본값을 가정 합니다.](http://nuget.codeplex.com/workitem/60)
* [대화 상자 UI 가짜 "최신" 패키지를 보여 줍니다.](http://nuget.codeplex.com/workitem/62)
* [옵션: 취소를 클릭 하면 취소 되지 않습니다 변경](http://nuget.codeplex.com/workitem/63)
* [추가 패키지 참조 대화 Search는 대/소문자 구분 해야 합니다.](http://nuget.codeplex.com/workitem/65)
* [AssemblyInfo.cs 파일에서 회사 메타 데이터를 수정 합니다.](http://nuget.codeplex.com/workitem/67)
* [VSIX에 대 한 버전 번호](http://nuget.codeplex.com/workitem/71)
* [-사용 하 여 제거-패키지:? 도움말을 두 번 표시](http://nuget.codeplex.com/workitem/72)
* [프로젝트 수준 패키지에 대 한 패키지 설치/제거를 실행 합니다.](http://nuget.codeplex.com/workitem/74)
* [서버 하나 nupack 유효성 검사에 실패 하는 경우 피드를 만들 수 없습니다.](http://nuget.codeplex.com/workitem/90)
* [NuPack 아이콘을 대체 해야 합니다.](http://nuget.codeplex.com/workitem/94)
* [NTLM http 프록시 패키지 피드를 인증 하지 않습니다.](http://nuget.codeplex.com/workitem/96)
* [대화 상자는 VS 창에서 항상 가운데 시작 되지 않습니다.](http://nuget.codeplex.com/workitem/100)
* [대화 상자에서 채워지고 하지 다양 한 패키지 세부 정보 필드](http://nuget.codeplex.com/workitem/102)
* [대화 상자 UI 작성자의 이름이 표시 되지 않습니다.](http://nuget.codeplex.com/workitem/108)
* [왜-제거 패키지 버전](http://nuget.codeplex.com/workitem/113)
* [대화 상자 UI에서 최근 항목 탭 제거](http://nuget.codeplex.com/workitem/115)
* [오른쪽 때 VS 충돌 하나 이상의 UI 대화 상자를 연 후 솔루션 폴더를 클릭 합니다.](http://nuget.codeplex.com/workitem/126)
* [변경 목록 패키지의 로컬 매개 변수--설치](http://nuget.codeplex.com/workitem/129)
* [Packages.xml NuPack.config에 이름 바꾸기](http://nuget.codeplex.com/workitem/132)
* [콘솔 줄의 끝에 커서를 강제로](http://nuget.codeplex.com/workitem/135)
* [제거-패키지 intellisense가 중단 됩니다.](http://nuget.codeplex.com/workitem/136)
* [.Nuspec 피드를 RequireLicenseAcceptance 플래그를 추가 합니다.](http://nuget.codeplex.com/workitem/137)
* [.Nuspec 형식을 지정 하 고 패키지의 LicenseUrl 피드 추가](http://nuget.codeplex.com/workitem/138)
* [동의 대화 상자를 표시 해야 수용 해야 하는 패키지에 대 한 설치를 클릭](http://nuget.codeplex.com/workitem/139)
* [추가 패키지 대화 상자에 고 지 사항 텍스트 추가](http://nuget.codeplex.com/workitem/140)
* [고 지 사항 때 the 패키지 콘솔이 실행 되는 처음으로 추가 합니다.](http://nuget.codeplex.com/workitem/143)
* [콘솔에서 패키지를 설치한 후에 고 지 사항 표시](http://nuget.codeplex.com/workitem/144)
* [.Nupkg.nupack 확장의 이름을](http://nuget.codeplex.com/workitem/146)