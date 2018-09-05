---
title: 2.8.5 NuGet 릴리스 정보
description: NuGet 2.8.5 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548627"
---
# <a name="nuget-285-release-notes"></a>2.8.5 NuGet 릴리스 정보

[NuGet 2.8.3 릴리스 정보](../release-notes/nuget-2.8.3.md) | [2.8.6 NuGet 릴리스 정보](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 2015 년 3 월 30 일에 출시 되었습니다. 사소한 업데이트는 2.8.3 VSIX 일부를 사용 하 여 대상 수정 합니다.

이 릴리스에서 NuGet 패키지 관리자 대화 상자에 대 한 지원에 대 한 추가 되었습니다 [DNX 대상 프레임 워크 모니커의](https://github.com/aspnet/dnx)합니다.  지원 되는 이러한 새 프레임 워크 모니커는 다음과 같습니다.

* **core50** -'base' 대상 Core CLR 호환 되는 프레임 워크 모니커 (TFM).
* **dnx452** -전체 4.5.2를 사용 하는 TFM DNX 기반 특정 앱 프레임 워크의 버전
* **dnx46** -프레임 워크의 전체 4.6 버전을 사용 하는 TFM DNX 기반 특정 앱
* **dnxcore50** -Core 5.0 버전의 framework 사용 하 여는 TFM DNX 기반 관련 앱

하나의 버그가 방지 패키지를 사용 하는 FSharp 프로젝트에 제대로 설치에서 수정 된:

https://nuget.codeplex.com/workitem/4400