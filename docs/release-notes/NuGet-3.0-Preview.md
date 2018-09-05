---
title: NuGet 3.0 미리 보기 릴리스 정보
description: NuGet 3.0 미리 보기의 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9389639476172d05556b95d589e429ddfe0e3026
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546467"
---
# <a name="nuget-30-preview-release-notes"></a>NuGet 3.0 미리 보기 릴리스 정보

[NuGet 2.9 RC 릴리스 정보](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 베타 릴리스 정보](../release-notes/nuget-3.0-beta.md)

NuGet 3.0 미리 보기는 Visual Studio 2015 Preview 릴리스의 일환으로 2014 년 11 월 12 년에 출시 되었습니다. NuGet 3.0 미리 보기를 발표 했습니다. 이 우리 회사에 대규모 릴리스의 (비록 미리 보기), 변경 내용이에서 피드백을 시작 하고자 하 고 합니다.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

이 NuGet 3.0 미리 보기는 Visual Studio 2015 Preview에 포함 됩니다. 참여 미리 보기 삭제 Visual Studio 2012 및 Visual Studio 2013 용 곧 노력 합니다. 이전에 의도 발표 했습니다 [Visual Studio 2010에 대 한 업데이트를 중단](http://blog.nuget.org/20141002/visual-studio-2010.html), 해당 결정 하기는 쉽지 않은 하며 합니다.

## <a name="brand-new-ui"></a>새로운 UI

가장 먼저 NuGet 3.0 미리 보기에 대 한 표시는 새로운 UI입니다. 모달 대화 상자가;는 더 이상 이제 전체 Visual Studio 문서 창입니다. 이 옵션을 사용 하면 한 번에 여러 프로젝트 (및/또는 솔루션)에 대 한 UI를 열고, 창을 다른 모니터로 분리 등 원하는 것 이지만 도킹 수 있습니다.

![새 NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

모달 대화 상자를 중단으로 인해 유용성 차이 외 수도 있는 다양 한 새로운 기능 새 UI에서.

### <a name="version-selection"></a>버전 선택

UI 기능 패키지 설치 및 업데이트-버전 선택을 허용 하는 가장을 요청 하는 것이 출시 되었습니다.

![패키지 버전 선택](./media/NuGet-3.0-Preview/version-selection.png)

허용 하는지 여부를 설치 하거나 패키지를 업데이트 하는 버전 드롭다운에서 쉽게 선택에 대 한 목록의 맨 위로 이동 승격 일부 주요 버전을 사용 하 여 패키지에 대 한 사용 가능한 버전 모두를 볼 수 있습니다. PowerShell 콘솔을 사용 하 여 최신 되지 않은 특정 버전을 가져올 필요가 없습니다.

### <a name="combined-installedonlineupdates-workflows"></a>설치 된/온라인/업데이트 워크플로 결합합니다.

이전 UI 온라인으로 설치 및 업데이트에 대 한 3 개의 탭을 했습니다. 나열 된 패키지에는 해당 워크플로 관련 했으며 사용 가능한 작업으로 워크플로 관련 된. 논리 많았다는 의견 종종는 많은 의견은 타당성이 있지만이 분리 하 여 중단점이 가져옵니다.

이제는 결합 된 환경을 하거나 수 있는 설치, 업데이트, 선택한 패키지를 가져온 방법에 관계 없이 패키지를 제거 했습니다. 특정 워크 로드를 지원 하기 위해 이제 표시 된 패키지를 필터링 할 수 있는 필터 드롭다운 되지만 다음 패키지에 대 한 사용 가능한 작업 일치 합니다.

![패키지 제거](./media/NuGet-3.0-Preview/uninstall-package.png)

"설치" 필터를 사용 하 여 확인할 수 있습니다 쉽게 사용할 수 있는 업데이트 사항이 있는 설치 된 패키지를 및 다음 중 하나를 제거 하거나 업데이트할 수 있습니다 패키지 보려는 버전 선택을 변경 하 여 사용 가능한 동작을 변경 합니다.

![패키지를 업데이트 합니다.](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>버전 통합

것이 일반적으로 동일한 솔루션 내에서 여러 프로젝트에 설치 패키지 있습니다. 경우에 따라 각 프로젝트에 설치 되어 있는 버전이 떨어져 드리프트 수 되며 사용 중인 버전을 통합 하는 데 필요한 것입니다. NuGet 3.0 미리 보기에이 시나리오에 새 기능이 도입 되었습니다.

솔루션 수준 패키지 관리 창 솔루션을 마우스 오른쪽 단추로 클릭 하 고 솔루션에 대 한 NuGet 패키지 관리를 선택 하 여 액세스할 수 있습니다. 여기에서 여러 프로젝트에 있지만 사용에서 서로 다른 버전을 사용 하 여 설치 된 패키지를 선택 하면 새 "통합" 작업을 사용할 수 있습니다. 아래 스크린샷에서 `Newtonsoft.Json` 에 설치 된 합니다 `SamplesClassLibrary` 버전과 `6.0.4` 에 어셈블리를 설치 하 고 `SamplesConsoleApp` 버전과 `5.0.4`합니다.

![버전 통합](./media/NuGet-3.0-Preview/consolidate.png)

단일 버전으로 통합 하기 위한 워크플로 다음과 같습니다.

1. 선택 된 `Newtonsoft.Json` 목록의 패키지
1. 선택할 `Consolidate` 에서 `Action` 드롭다운
1. 사용 된 `Version` 드롭다운을 통합할 수 버전 선택
1. (선택한 버전에 이미 있는 프로젝트를 사용할 수 있는 참고) 해당 버전에 통합 해야 하는 프로젝트에 대 한 확인란을 선택
1. 클릭 된 `Consolidate` 통합을 수행 하는 단추

### <a name="operation-previews"></a>작업 미리 보기

-수행 하는 작업에 관계 없이 설치/업데이트/제거-새 UI 이제 하는 방법을 제공 프로젝트에 적용 될 변경 내용 미리 보기. 이 미리 보기에는 새 패키지를 설치할 수 없는 변경 작업 중 패키지와 함께 제거할 수는 패키지를 패키지 하 고 업데이트 됩니다 표시 됩니다.

아래 예에서 Microsoft.AspNet.SignalR 설치 프로젝트에 몇 가지 변경 결과 볼 수 있습니다.

![SignalR을 설치 하는 미리 보기](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>설치 옵션

PowerShell 콘솔을 사용 했던 몇 가지 주목할 만한 설치 옵션에 대 한 제어 합니다. 이제 기능만 UI에 제공 합니다. 이제 종속성의 버전 선택 방법에 대 한 종속성 확인 하는 동작을 제어할 수 있습니다.

![종속성 동작](./media/NuGet-3.0-Preview/dependency-behavior.png)

또한 패키지의 콘텐츠 파일을 프로젝트에 이미 파일 충돌할 때 수행할 동작을 지정할 수 있습니다.

![파일 충돌 작업](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>무한 스크롤

UI에 대 한 피드백의 두 스크롤이 필요 상당히 가져오고 패키지를 나열할 때 패러다임을 페이징 사용 했습니다. 매우 짧은 목록 아래쪽으로 스크롤한 다음 페이지 번호를 클릭 하 고 스크롤한 다음 다시 필요가에 공통적으로 적용 했습니다. 새 UI를 사용 하 여 스크롤-더 이상 페이징 하기만 하면 되도록 패키지 목록에서 무한 스크롤 구현 했습니다.

![무한 스크롤](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>작업을 확인, 빠른, 멋진 있도록 확인

이 새 UI를 사용해에 대 한 참여를 기대 됩니다. 이 미리 보기 마일스 톤 중 되었습니다 좋은 격언 다음 "확인 작업을 빠르게 확인, 멋지게 만들기." 이 미리 보기에서는 대부분을 완료 한 것의 첫 번째 목표-작동 합니다. 매우 빠른를 아직 및 아직 상당히 매우 알게 알고 있습니다. 이제 RC 릴리스 사이의 이러한 목표에 작업할 것을 신뢰 합니다. 에 대 한 여러분의 의견을 듣고 그 동안에 *유용성* 새 UI--워크플로, 작업의 방법과 것 *느낌* 새 UI를 사용 하 합니다.

이전 UI에 비해 없어졌습니다 함수의 몇 가지 있습니다. 다음 중 하나 의도적인, 다른 하나만 하지 않은 가져오기에 시간.

#### <a name="searching-all-package-sources"></a>"All" 패키지 소스를 검색합니다.

이전 UI를 사용 하면 모든 패키지 원본에 대해 패키지 검색을 수행 하려면 수 있습니다. UI의 기능을 제거 했습니다 하 고 우리 없습니다 수 상태로 전환 다시 합니다. 모든 패키지 원본에 대 한 검색 작업을 수행 하는 데이 기능 결과 함께 응용 프로그램 및 정렬 선택에 따라 결과 정렬 하려고 합니다.

검색 관련성 하기가 정말 어렵습니다 방식과 발견 했습니다. Google 및 Bing에 대 한 검색 하 고 결과 함께 위빙을 imagine 수 있습니까? 또한이 기능은 되었으면 느린이 고, 쉽게 *실수로* 거의 실제로 도움이 되었기를 사용 하 여, 생각 합니다. 문제로 인해 수 하지 수정 된 버그 보고서를 다양을 수신 했습니다 도입 하는 기능입니다.

#### <a name="update-all"></a>모든 업데이트

이전 UI는 아직 새 UI에 없는에 "모두 업데이트" 단추를 사용 했습니다. 이 RC 릴리스에 대 한이 기능을 부활는 했습니다.

## <a name="new-clientserver-api"></a>새 클라이언트/서버 API

모든 새 패키지 관리 UI의에서 새로운 기능 외에도 것도 왔습니다 NuGet의 클라이언트/서버 프로토콜에 대 한 몇 가지 구현 세부 정보입니다. 수행한 작업을 만들 때 "API v3" NuGet 패키지 복원 및 패키지 설치와 같은 중요 한 시나리오에 대 한 고가용성 요구에 맞게 설계는 대 한 합니다. 새 API는 REST 기반으로 하 고 하이퍼미디어를 선택한 [JSON-LD](http://json-ld.org) 이 리소스 형식으로 합니다.

NuGet 3.0 미리 보기 비트 패키지 소스 드롭다운 목록에서 "preview.nuget.org" 이라는 새 패키지 소스를 볼 수 있습니다. 해당 패키지 소스를 선택 하는 경우 nuget.org에 연결 하는 대신 새 API 사용 하겠습니다. 만들었습니다 원본을 미리 보기 UI에서 사용할 수 있는 테스트, 수정 및 새로운 API를 개선 합니다. 계속 하는 동안. NuGet 3.0 rc에서는이 새 API v3 기반 패키지 소스의 v2 기반 "nuget.org" 패키지 원본을 바뀝니다.

API v3를 넣었습니다 투자에도 불구 하 고 만들었습니다 이러한 모든 새 기능 nuget.org도 아닌 기존 패키지 원본을 작업할 즉는 기존 API v2 프로토콜을 작업할 수도 있습니다.

## <a name="new-features-coming"></a>새로운 기능

이제 사이의 3.0 RTM도 노력 몇 가지 기본적인 이외에 새 NuGet 기능, UI에 표시 합니다. 가장 중요 한 투자 영역의 짧은 목록을 다음과 같습니다.

1. MSBuild를 가져오려는 팀이 고 Visual Studio와 제휴 했습니다 [플랫폼에 대 한 자세한 NuGet](http://blog.nuget.org/20141014/in-the-platform.html)합니다.
1. 설치 시 패키지 규칙을 중단 하 고 대신 새 도입 하 여 패키징 시 해당 규칙을 적용 하기 위해 노력 하 "신뢰할 수 있는" [패키지 매니페스트](http://blog.nuget.org/20141023/package-manifests.html)합니다.
1. Visual Studio에서 패키지 관리 외에 다른 도메인에 클라이언트 및 서버 구성 요소를 다시 사용할 수 있도록 하려면 코드 베이스 NuGet 리팩터링 하기 위해 노력 하 합니다.
1. 패키지는 나타낼 수 있는 "개인 종속성"의 개념을 조사 하는 것만 구현 세부 정보에 대 한 다른 패키지에 의존 하 고 해당 종속성 최상위 종속성으로 표시 해서는 안 됩니다.

## <a name="stay-tuned"></a>계속 주목해 주세요

에 유의 하세요 [블로그에서](http://blog.nuget.org) 자세한 진행률 및 NuGet 3.0에 대 한 알림!