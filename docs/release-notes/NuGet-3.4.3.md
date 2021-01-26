---
title: NuGet 3.4.3 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 3.4.3를 포함 하는 NuGet에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776469"
---
# <a name="nuget-343-release-notes"></a>NuGet 3.4.3 릴리스 정보

[NuGet 3.4.2 릴리스 정보](../release-notes/nuget-3.4.2.md)  |  [NuGet 3.4.4 릴리스 정보](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3는 3.4 및 이후 릴리스에서 확인 된 몇 가지 문제를 해결 하기 위해 2016 년 4 월 22 일에 릴리스 되었습니다.

VSIX를 다운로드 하 고 [여기](https://dist.nuget.org/index.html)에서 nuget.exe 수 있습니다.

## <a name="updates-and-improvements"></a>업데이트 및 개선 사항

* 향상 된 Visual Studio 안정성. Visual Studio에서 충돌을 일으킨 NuGet 문제를 해결 했습니다.

## <a name="fixes"></a>수정 프로그램

* 암호로 보호 되는 개인 nuget 피드의 몇 가지 권한 부여 문제를 수정 했습니다.
* 지정 된 런타임을 사용 하 여 PCL을 복원할 수 없는 문제를 해결 `project.json` 했습니다.
* 일부 고객은 패키지를 설치할 때 일시적인 오류가 발생 했습니다. 이제이 릴리스에서 수정 되었습니다.
* 를 사용 하 여 c + +/CLI 프로젝트에서 복원 실패를 야기 하는 문제를 해결 `project.json` 했습니다.
* Mono에서 nuget을 사용할 때 제대로 압축 해제 되지 않는 일부 패키지 (예: ModernHttpClient)입니다. 이제이 릴리스에서 수정 되었습니다.

이 릴리스의 수정 사항 및 개선 사항에 대 한 전체 목록은 [여기](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)에서 문제 목록을 확인 하세요.