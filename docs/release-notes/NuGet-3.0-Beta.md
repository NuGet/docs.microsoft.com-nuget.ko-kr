---
title: NuGet 3.0 베타 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 3.0 베타에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7970c3d81c724edc743d7b2d38c4c157237a0271
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776620"
---
# <a name="nuget-30-beta-release-notes"></a>NuGet 3.0 베타 릴리스 정보

[NuGet 3.0 Preview 릴리스 정보](../release-notes/nuget-3.0-preview.md)  |  [NuGet 3.0 RC 릴리스 정보](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 Beta는 Visual Studio 2015 CTP 6 릴리스를 위한 2015 년 2 월 23 일에 출시 되었습니다. 이 릴리스는 수많은 아키텍처와 향상 된 성능을 제공 하는 팀에 많은 것을 의미 하며, nuget.org 서비스에 대 한 성능 설정 조정을 시작 합니다.

이 새 버전을 설치 하기 전에 이전 버전의 NuGet Visual Studio 2015 확장을 제거 하는 것이 좋습니다.  이 버전의 확장에 문제가 있는 경우 Visual Studio 2015 preview에서 사용 하기 위해 [이전 버전](http://nuget.codeplex.com/downloads/get/909582) 으로 되돌리는 것이 좋습니다.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

이 NuGet 3.0 베타는 Visual Studio 2015 CTP 6 확장 갤러리에서 설치할 수 있습니다. Visual Studio 2012 및 Visual Studio 2013에 대 한 미리 보기를 제공 하기 위해 노력 하 고 있습니다. 이전에는 [Visual Studio 2010에 대 한 업데이트를 중단](http://blog.nuget.org/20141002/visual-studio-2010.html)하는 것을 이전에 공유 했으며,이는 어려운 결정을 내리는 것입니다.

## <a name="new-clientserver-api"></a>새 클라이언트/서버 API

NuGet의 클라이언트/서버 프로토콜에 대 한 몇 가지 구현 세부 정보를 작업 하 고 있습니다. 수행한 작업은 패키지 복원 및 패키지 설치와 같은 중요 한 시나리오에 대 한 고가용성을 중심으로 작성 된 NuGet에 대해 "API v3"을 만드는 것입니다. 새 API는 REST 및 하이퍼 미디어를 기반으로 하며, [JSON-LD](http://json-ld.org) 를 리소스 형식으로 선택 했습니다.

NuGet 3.0 베타 비트에서는 패키지 원본 드롭다운에서 "api.nuget.org" 라는 새 패키지 원본이 표시 됩니다.   해당 패키지 원본을 선택 하는 경우 nuget.org에 연결 하는 대신 새 API를 사용 합니다. NuGet 3.0 RC에서이 새 API v3 기반 패키지 원본은 v2 기반 "nuget.org" 패키지 원본을 대체 합니다.  다른 모든 공용 패키지 원본을 사용 하지 않도록 설정 하는 것이 좋으며 유일한 공용 패키지 리포지토리로 api.nuget.org 합니다.

V3 API를 구축 하는 데 많은 시간이 소요 되었으며 공용 리포지토리에 액세스 하려는 이전 클라이언트에 대해 표준 v2 API를 계속 유지 합니다.

## <a name="updated-ui"></a>업데이트 된 UI

패키지를 사용 하 여 작업을 선택 하 고 미리 보기 단추를 화면 옵션 영역의 확인란으로 전환 하는 데 사용할 수 있는 combobox를 포함 하도록이 릴리스의 사용자 인터페이스를 향상 시켰습니다.  옵션 영역은 더 이상 축소할 수 없습니다. 이제 사용할 수 있는 옵션을 설명 하는 도움말 링크를 제공 합니다.

![새 NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>작업 로깅

를 설치 하거나 제거 하는 동안 빠르게 표시 하 고 숨길 수 있는 로깅 정보를 사용 하 여 모달 창을 제거 했습니다.  이 창에는 정보를 보거나 복사 하 여 붙여넣을 수 있는 경우 값이 추가 되지 않습니다.  대신, 이제 모든 출력 로깅을 출력 창의 패키지 관리자 창으로 리디렉션합니다.  이는 조사 하려는 일반적인 빌드 보고서와 더 편안 하 고 유사한 것으로 간주 됩니다.


### <a name="focus-on-performance"></a>성능에 집중

NuGet 검색의 성능 향상 및 페치에 대 한 많은 변경 내용이 있습니다.  이는 고객의 중요 한 한 가지 중요 한 것 이며,이 릴리스에서이를 해결 하려고 했습니다.  서버를 조정 하 고, 새 CDN을 구축 하 고, 보다 관련성이 높은 패키지 검색 결과를 제공 하기 위해 쿼리 일치 논리를 개선 했습니다.

NuGet 3.0 개발의이 단계를 진행 하면서 개선 된 환경을 제공 하기 위해 nuget.org 서비스를 조정 하 고 모니터링 하 게 될 것입니다.  가동 중지 시간에 참여할 계획은 없지만 서비스에서 리소스를 추가 하 고 변경 하 게 됩니다.  서비스 구성을 변경 하는 경우에 대 한 자세한 내용은 [twitter 피드에](http://twitter.com/nuget) 유의 하세요.

## <a name="building-nuget-with-nuget"></a>NuGet을 사용 하 여 NuGet 빌드

이제 nuget 클라이언트를 NuGet 패키지에 기본 제공 되는 여러 구성 요소로 다시 설계 했습니다. 자체 라이브러리를 다시 사용 하면 다시 사용할 수 있고 제대로 패키지할 수 있는 구성 요소를 빌드할 수 있습니다.  중복 된 코드를 제거 하 고 솔루션 전반에서 패키지를 빌드하는 데 필요한 기능을 지원 하도록 개발 프로세스를 보다 효율적으로 구성 하는 방법을 배웠습니다.  코드 프로젝트가 구조화 되는 방법 및 빌드 프로세스의 작동 방식에 대해 설명 하는 블로그 게시물을 곧 찾아볼 수 있습니다.

## <a name="stay-tuned"></a>계속 조정

NuGet 3.0에 대 한 자세한 진행률과 공지 사항은 [블로그](http://blog.nuget.org) 를 확인 하세요.
