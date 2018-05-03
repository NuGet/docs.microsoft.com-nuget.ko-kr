---
title: NuGet 3.4.3 릴리스 정보
description: NuGet 3.4.3 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6c25d3b678e6e72eca3e1157f91a75bfa8cbb18e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-343-release-notes"></a>NuGet 3.4.3 릴리스 정보

[NuGet 3.4.2 릴리스 정보](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 릴리스 정보](../release-notes/nuget-3.4.4.md)

3.4.3 NuGet 3.4 및 이후 버전에서 식별 된 몇 가지 문제를 해결 하기 위해 2016 년 4 월 22 일에 출시 되었습니다.

VSIX와 nuget.exe를 다운로드할 수 있습니다 [여기](https://dist.nuget.org/index.html)합니다.

## <a name="updates-and-improvements"></a>업데이트 및 향상 기능

* Visual Studio 안정성이 향상된 됩니다. Visual Studio에서 충돌 발생 시킨 NuGet에서 몇 가지 문제를 해결 했습니다.

## <a name="fixes"></a>수정 프로그램

* 피드 암호로 보호 된 개인 nuget이 포함 된 일부 인증 문제가 해결 되었습니다.
* 주위에서 PCL 복원할 수 없는 문제가 해결 되었습니다. `project.json` 지정 런타임을 사용 하 여 합니다.
* 일부 고객 실행 중이 던 일시적인 오류가 발생에 패키지를 설치할 때. 이제이 릴리스에서 수정 되었습니다.
* C + 복원 실패를 발생 시킨 문제가 해결 되었습니다. + /CLI 프로젝트와 `project.json`합니다.
* 사용 되 고 있지 푼 올바르게 모노에서 nuget을 사용할 때 일부 패키지 (예: ModernHttpClient). 이제이 릴리스에서 수정 되었습니다.

수정 사항 및이 릴리스에서 향상 된 전체 목록은 체크 아웃 문제 목록 [여기](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)합니다.