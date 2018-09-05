---
title: NuGet 3.4.3 릴리스 정보
description: NuGet 3.4.3 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549167"
---
# <a name="nuget-343-release-notes"></a>NuGet 3.4.3 릴리스 정보

[3.4.2 NuGet 릴리스 정보](../release-notes/nuget-3.4.2.md) | [3.4.4 NuGet 릴리스 정보](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 3.4 및 후속 릴리스에서 식별 된 몇 가지 문제를 해결 하기 위해 2016 년 4 월 22 일에 출시 되었습니다.

VSIX와 nuget.exe 둘 다를 다운로드할 수 있습니다 [여기](https://dist.nuget.org/index.html)합니다.

## <a name="updates-and-improvements"></a>업데이트 및 향상 된 기능

* Visual Studio 안정성 향상된입니다. Visual Studio에서 충돌을 발생 시킨 NuGet에서 몇 가지 문제를 수정 했습니다.

## <a name="fixes"></a>수정

* 몇 가지 권한 부여 문제 수정 암호로 보호 된 개인 nuget 피드 합니다.
* PCL을 복원할 수 없게 관련 문제를 해결 함 `project.json` 지정 런타임을 사용 하 여 합니다.
* 패키지를 설치 하는 경우 일부 고객은 일시적인 오류에 실행 되었습니다. 이이 릴리스에서 수정 된 이제.
* C + 복원 실패를 야기 하는 문제 해결 + CLI 사용 하 여 프로젝트 `project.json`합니다.
* 없는 푼 올바르게 mono에서 nuget을 사용 하는 경우 일부 패키지 (예: ModernHttpClient). 이이 릴리스에서 수정 된 이제.

수정 및 개선 사항이이 릴리스에서 전체 목록은 문제 목록을 보려면 [여기](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)합니다.