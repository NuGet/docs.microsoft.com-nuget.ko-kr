---
title: NuGet 3.0 베타 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하 여 NuGet 3.0 베타에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f9fec6a1af8dfbcfdcfa05a301ff52409521228
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550915"
---
# <a name="nuget-30-beta-release-notes"></a>NuGet 3.0 베타 릴리스 정보

[NuGet 3.0 미리 보기 릴리스 정보](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC 릴리스 정보](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 베타는 2015 년 2 월 23 일에 Visual Studio 2015 CTP 6 릴리스에 대 한 출시 되었습니다. 이 릴리스를 공유 하려면 아키텍처 및 성능 향상 된 여러와 nuget.org 서비스의 성능 설정을 조정 하려면 기쁘게 우리 팀에 훨씬 의미 합니다.

이 새 버전을 설치 하기 전에 모든 이전 버전의 NuGet Visual Studio 2015 확장을 제거 하는 것이 좋습니다.  이 버전의 확장을 사용 하 여 문제가 되돌리려면는 것이 좋습니다 합니다 [이전 버전](http://nuget.codeplex.com/downloads/get/909582) Visual Studio 2015 preview 사용 합니다.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

이 NuGet 3.0 베타를 Visual Studio 2015 CTP 6 확장 갤러리에서 설치할 수 있습니다. 참여 미리 보기 삭제 Visual Studio 2012 및 Visual Studio 2013 용 곧 노력 합니다. 이전에 의도 발표 했습니다 [Visual Studio 2010에 대 한 업데이트를 중단](http://blog.nuget.org/20141002/visual-studio-2010.html), 해당 결정 하기는 쉽지 않은 하며 합니다.

## <a name="new-clientserver-api"></a>새 클라이언트/서버 API

지금까지 작업 NuGet의 클라이언트/서버 프로토콜에 대 한 몇 가지 구현 세부 정보입니다. 수행한 작업을 만들 때 "API v3" NuGet 패키지 복원 및 패키지 설치와 같은 중요 한 시나리오에 대 한 고가용성 요구에 맞게 설계는 대 한 합니다. 새 API는 REST 기반으로 하 고 하이퍼미디어를 선택한 [JSON-LD](http://json-ld.org) 이 리소스 형식으로 합니다.

NuGet 3.0 베타 비트 패키지 소스 드롭다운 목록에서 "api.nuget.org" 이라는 새 패키지 소스를 볼 수 있습니다.   해당 패키지 소스를 선택 하는 경우 nuget.org에 연결 하는 대신 새 API 사용 하겠습니다. NuGet 3.0 rc에서는이 새 API v3 기반 패키지 소스의 v2 기반 "nuget.org" 패키지 원본을 바뀝니다.  모든 다른 공용 패키지 소스를 사용 하지 않도록 설정 하는 것이 좋습니다 하 고 패키지를 유일한 공용 리포지토리에 api.nuget.org 그대로입니다.

V3 API 구축에 많은 시간을 준비 했습니다 하 고 이전 버전의 공용 리포지토리에 액세스 하려는 클라이언트에 대 한 표준 v2 API를 유지 하기 위해 계속 됩니다.

## <a name="updated-ui"></a>업데이트 UI

패키지에서 수행할 작업을 선택 하면 미리 보기 단추 화면 옵션 영역에서 확인란으로 전환 하는 콤보 상자를 포함 하도록이 릴리스에서 사용자 인터페이스 개선 했습니다.  옵션 영역을 더 이상 축소할 수 하 고 이제 사용할 수 있는 옵션을 설명 하는 도움말 링크를 제공 합니다.

![새 NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>작업 로깅

모달 창으로 로깅 정보를 신속 하 게 표시 하 고 숨길 설치 또는 제거 하는 동안 제거 했습니다.  이 창 정보를 보거나 것에서 복사 및 붙여넣기 수 있으려면 실제로 하려는 경우 값이 없는 추가.  대신에서는 이제 리디렉션하는 모든 로깅 출력 창에서 패키지 관리자 창으로 출력 합니다.  생각 하이 고 더 편리 하 게 검사 하려고 하는 일반적인 빌드 보고서와 비슷합니다.


### <a name="focus-on-performance"></a>성능에 집중

많은 NuGet 검색 및 인출의 성능 향상의 이름을 변경 했습니다.  고객의 첫째 하는데 이것이 하 고 싶은이 릴리스에서 해결 하겠습니다 되도록 합니다.  새 CDN, 빌드 서버를 튜닝와 바랍니다 관련성이을 제공 하는 논리와 일치 하는 쿼리를 개선 했습니다 및 더 빠른 패키지 검색 결과입니다.

이 단계의 개발 NuGet 3.0을 통해 계속 진행 하면서 수 튜닝 하 고 향상 된 경험을 제공 하는 것을 확인 하려면 nuget.org 서비스를 모니터링 합니다.  에서는 수행 되지 모든 가동 중지 시간에 참여 하려면 있지만 추가 되며 서비스에서 리소스를 변경 합니다.  주시 하세요 [twitter 피드](http://twitter.com/nuget) 서비스 구성을 변경 하 고 대 한 자세한 내용은 합니다.

## <a name="building-nuget-with-nuget"></a>NuGet 사용 하 여 NuGet 구성

이제 NuGet 패키지에 포함 된 자체는 여러 구성 요소를 NuGet 클라이언트 재개발 있어야 했습니다. 이 다시 사용 하 여 고유한 라이브러리의 구성 요소 다시 사용할 수 있으며 제대로 패키지할 수 있는 빌드를 강제로 수행 합니다.  중복된 코드를 제거 하 여 솔루션 전체 패키지를 빌드할 필요를 지원 하기 위해 개발 프로세스를 구성 하는 데 하는 방법을 배웠습니다 결정 했습니다.  여기서 설명 하는 코드 프로젝트 구조화는 방식과 빌드 프로세스의 작동 방식 및 곧 블로그 게시물을 찾습니다.

## <a name="stay-tuned"></a>계속 주목해 주세요

에 유의 하세요 [블로그에서](http://blog.nuget.org) 자세한 진행률 및 NuGet 3.0에 대 한 알림!
