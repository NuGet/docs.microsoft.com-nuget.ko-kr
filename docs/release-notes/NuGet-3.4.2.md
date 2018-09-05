---
title: 3.4.2 NuGet 릴리스 정보
description: 다음을 포함 하 여 NuGet 3.4.2에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549153"
---
# <a name="nuget-342-release-notes"></a>3.4.2 NuGet 릴리스 정보

[3.4.1 NuGet 릴리스 정보](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 릴리스 정보](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2는 3.4 및 3.4.1에서 식별 된 여러 문제를 해결 하 2016 년 4 월 8 일에 발표 된 릴리스 합니다.

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC 출시 되었습니다.

Nuget.exe 3.4.2의 릴리스 후보를 다운로드할 수 있습니다 [여기](https://dist.nuget.org/index.html)합니다.

## <a name="updates-and-improvements"></a>업데이트 및 향상 된 기능

* 특정 시나리오에서는 전체 종속성 그래프를 사용 하 여 패키지에서 업데이트 시간이 매우 오래 걸렸 및 Visual Studio를 중지 합니다. 여기서는 업데이트의 성능을 개선 현저 하 게 했습니다.
* 네트워크 트래픽 없이 nuget 복원 2.5 x-3 배 Visual Studio 내에서 더 빠르게 됩니다.
* 이 변경 외에도 있는 문제를 해결 했습니다 있는 VS UI의 수 업데이트를 가져오는 경우에 두 번 네트워크 적중 된 것입니다. 이 일부 시간 제한 문제 고객 경험이 3.4/3.4.1 부분적으로 담당 했습니다.
* No_proxy 설정에 대 한 지원 추가

## <a name="fixes"></a>수정

* 문제를 해결 하 고 3.4.1으로 업데이트 한 후 nuget.org 원본 NuGet 설정 또는 구성에서 누락 된 키를 누릅니다.
* 3.4.1에서 대/소문자 변경 FindPackagesById Artifactory를 중단 하는 위치는 문제가 해결 되었습니다.
* Nuget.exe 사용 하 여 NuGet 복원을 사용 하 여 실패를 야기 하는 FIPS 사용 하 여 문제를 수정 했습니다.
* 잘못 된 아이콘 URL 사용 하 여 원본을 검색할 때 충돌을 해결 했습니다.
* 버전 및 원본의' 모든' 항목을 병합 된 문제가 해결 되었습니다.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>알려진 문제 3.4.2에 Windows x86 명령줄 (RC)

이러한 문제는 RTM 도달 하기 전에 초기 다음 주 수정 됩니다.

*  솔루션 파일은 프로젝트 파일 보다 낮은 폴더 계층 구조에 저장 하는 경우 솔루션에서 실행 중인 nuget 복원이 실패 합니다.
*  Nuget delete 명령 V2 피드를 사용 하 여 패키지 실행이 실패 합니다. V3 피드를 대신 사용 합니다.


수정 및 개선 사항이이 릴리스에서 전체 목록은 문제 목록을 보려면 [여기](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)합니다.