---
title: NuGet 3.0 베타 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 3.0 Beta에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4608b196d19f95410f9fe20f6a22e31c15955b89
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-beta-release-notes"></a>NuGet 3.0 베타 릴리스 정보

[NuGet 3.0 미리 보기 릴리스 정보](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC 릴리스 정보](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 베타는 2015 년 2 월 23 일에 Visual Studio 2015 CTP 6 릴리스에 대 한 릴리스 되었습니다. 이 릴리스에서 횟수를 공유 하려면 아키텍처 및 성능 향상 및 nuget.org 서비스에서 성능 설정을 튜닝을 시작 하고자 우리 팀에 많은 의미 합니다.

이 새 버전을 설치 하기 전에 모든 이전 버전의 Visual Studio 2015 NuGet 확장을 제거 하는 것이 좋습니다.  이 버전의 확장에 문제가 있는 경우 되돌린는 것이 좋습니다는 [이전 버전](http://nuget.codeplex.com/downloads/get/909582) Visual Studio 2015 preview와 함께 사용할 합니다.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

이 NuGet 3.0 Beta를 Visual Studio 2015 CTP 6 확장 갤러리에서 설치할 수 있습니다. 가져오려는 미리 보기 삭제 Visual Studio 2012 및 Visual Studio 2013에 대 한 가능한 한 빨리 노력 하 고 합니다. 에서는 이전에 공유 우리의 의도 [Visual Studio 2010에 대 한 업데이트를 중단](http://blog.nuget.org/20141002/visual-studio-2010.html), 해당 어려운 결정 하도록 않았습니다 고 합니다.

## <a name="new-clientserver-api"></a>새 클라이언트/서버 API

지금까지 작업에서 NuGet의 클라이언트/서버 프로토콜에 대 한 일부 구현 세부 정보. 수행한 작업에 대 한 NuGet 패키지를 복원 하 고 패키지를 설치 하는 등의 중요 한 시나리오에 대 한 고가용성 요구에 맞게 설계을 "API v3"를 만드는 것입니다. 새로운 API REST 기반으로 하며 하이퍼미디어 되 고, 선택한 [JSON LD](http://json-ld.org) 우리의 리소스 형식으로.

NuGet 3.0 Beta 비트 패키지 소스 드롭다운에 "api.nuget.org" 라는 새 패키지 소스를 볼 수 있습니다.   해당 패키지 소스를 선택 하는 경우 새 API nuget.org에 연결 하는 대신 사용 합니다. NuGet 3.0 RC에서이 새 API v3 기반 패키지 소스를 v2 기반 "nuget.org" 패키지 소스를 바뀝니다.  다른 공용 패키지 원본을 모두를 사용 하지 않도록 설정 하는 것이 좋습니다 하 고 public 패키지 저장소로만 api.nuget.org를 그대로 둡니다.

V3 API 구축에 많은 시간을 준비 했습니다 하 고 공용 저장소에 액세스 하는 오래 된 클라이언트에 대 한 표준 v2 API를 유지 하기 위해 계속 됩니다.

## <a name="updated-ui"></a>업데이트 UI

패키지와 함께 수행할 동작을 선택할 수 있게 되 고 미리 보기 단추 화면 옵션 영역에서 확인란을 전환 하는 콤보 상자가 포함 하도록이 릴리스에서 사용자 인터페이스 개선 했습니다 했습니다.  옵션 영역을 더 이상 축소할 수 하 고 이제 사용할 수 있는 옵션을 설명 하는 도움말 링크를 제공 합니다.

![새 NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>작업 로깅

모달 창 표시 및 숨기기 설치 또는 제거 하는 동안 신속 하 게 하는 로깅 정보를 제거 했습니다.  이 창을 추가 하려는 정보를 보거나 것에서 복사 및 붙여넣기 작업을 할 수 값이 없습니다.  대신,에서는 이제 리디렉션하는 모든 로깅 출력 창의 패키지 관리자 창에 출력 합니다.  이 보다 쉽고 검사 하려는 경우를 일반적인 빌드 보고서와 비슷한 한다고 생각 합니다.


### <a name="focus-on-performance"></a>성능에 집중

NuGet 검색 및 인출 성능 향상의 이름 변경의 많은 만들었습니다.  첫 번째 하는데 갈수록 고객 으로부터 였으며 해야 할까요 하도록 하려면이 릴리스에서 해결 했습니다.  새 CDN으로 구축 하는 서버를 튜닝 고 했으므로 더 적합을 바랍니다 제공 논리와 일치 하는 쿼리를 개선 및 빠른 패키지 검색 결과 합니다.

계속 진행 하면서이 NuGet 3.0의 개발이 단계를 통해, 튜닝 하 고 모니터링 개선 된 제품 되도록 nuget.org 서비스 여야 합니다.  म 수행 하지, 가동 중지 시간을 계획 하지만 추가 되며 서비스에서 리소스를 변경 합니다.  예의 주시 우리의 [twitter 피드](http://twitter.com/nuget) 서비스 구성 변경에 대 한 내용은 합니다.

## <a name="building-nuget-with-nuget"></a>NuGet이 포함 된 빌드 NuGet

이제 자체 NuGet 패키지에 기본 제공 되 고 있는 여러 구성 요소에는 NuGet 클라이언트 재개발가 우리 합니다. 이 다시 사용 하 여 고유한 라이브러리의 다시 사용할 수 있으며 올바르게 패키지할 수 있는 구성 요소 빌드를 강제로 수행 합니다.  중복된 코드를 제거 하 여 개발 프로세스 동안 솔루션 패키지를 빌드할 필요를 지원 하도록를 구성 하는 데 하는 방법을 배웠습니다 결정 했습니다.  코드 프로젝트 구성 방법 및 우리의 빌드 프로세스의 작동 방식에 대 한 대해서는 여기서 곧 블로그 게시물을 찾습니다.

## <a name="stay-tuned"></a>기대

에 유의 하십시오 [블로그에서](http://blog.nuget.org) 자세한 진행률 및 NuGet 3.0에 대 한 공지 사항!
