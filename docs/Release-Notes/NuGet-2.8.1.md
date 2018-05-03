---
title: NuGet 2.8.1 릴리스 정보
description: NuGet 2.8.1 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8787aee36d31ed5d8071b35a8c243823029d135f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-281-release-notes"></a>NuGet 2.8.1 릴리스 정보

[NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 릴리스 정보](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 2014 년 4 월 2 일에 출시 되었습니다.

## <a name="notable-features-in-the-release"></a>릴리스에서 주목할 만한 기능

### <a name="support-for-windows-phone-81-projects"></a>Windows Phone 8.1 프로젝트에 대 한 지원
이 릴리스에서 이제 대상 Windows Phone 8.1 프로젝트에 사용할 수 있는 다음과 같은 새 대상 프레임 워크 모니커를 지원 합니다.

* WindowsPhone81 / WP81 (Windows Phone Silverlight 기반 프로젝트)의 경우
* WindowsPhoneApp81 / WPA81 (WinRT 기반 Windows Phone 앱 프로젝트)의 경우

### <a name="update-of-the-nuget-webmatrix-extension"></a>NuGet WebMatrix 확장 업데이트
이 릴리스를 WebMatrix에는 NuGet 클라이언트 업데이트 [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 맡고 XDT 변환을 같은 특징으로 사용 합니다. 2.6.1 무엇 보다도 코어 업데이트를 사용 하면 WebMatrix 클라이언트가 더 최신 버전을 포함 하는 NuGet 패키지를 설치 하는 `.nuspec` ASP.NET NuGet 패키지를 포함 하는 스키마입니다.

WebMatrix 확장을 업데이트 하는 방법에 대 한 자세한 내용은 해당 특정 참조 [릴리스 정보](../release-notes/nuget-2.6.1-for-WebMatrix.md)합니다.

### <a name="bug-fixes"></a>버그 수정
이러한 기능 외에도이 버전의 NuGet 다른 버그 수정 포함합니다. 16 총 문제는 릴리스에서 해결 했습니다. 작업의 전체 목록에 대 한 항목에서에서 수정 된 NuGet 2.8.1, 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)합니다.

### <a name="reshipping-with-visual-studio-14-ctp"></a>Visual studio "14" CTP reshipping
Visual Studio "14" ctp 3 번째 2014 년 6 월에 발표에서 NuGet 2.8.1 상자에 함께 제공 됩니다. 아니므로 지원 기능 유지 par에 다른 2.8.1와 Visual Studio 2013에 대 한 것과 같은 VSIXes 합니다.
