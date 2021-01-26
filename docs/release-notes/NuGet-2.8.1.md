---
title: NuGet 2.8.1 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 2.8.1를 포함 하는 NuGet에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776773"
---
# <a name="nuget-281-release-notes"></a>NuGet 2.8.1 릴리스 정보

[NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md)  |  [NuGet 2.8.2 릴리스 정보](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1는 2014 년 4 월 2 일에 릴리스 되었습니다.

## <a name="notable-features-in-the-release"></a>릴리스의 주요 기능

### <a name="support-for-windows-phone-81-projects"></a>Windows Phone 8.1 프로젝트 지원
이제이 릴리스에서는 Windows Phone 8.1 프로젝트를 대상으로 하는 데 사용할 수 있는 다음과 같은 새 대상 프레임 워크 모니커를 지원 합니다.

* WindowsPhone81/WP81 (Silverlight 기반 Windows Phone 프로젝트의 경우)
* WindowsPhoneApp81/WPA81 (WinRT 기반 Windows Phone 앱 프로젝트용)

### <a name="update-of-the-nuget-webmatrix-extension"></a>NuGet WebMatrix 확장의 업데이트
이 릴리스는 WebMatrix에서 발견 된 NuGet 클라이언트를 [nuget. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 업데이트 하 고 XDT 변환과 같은 it 기능을 제공 합니다. 무엇 보다도 2.6.1 core 업데이트를 통해 WebMatrix 클라이언트는 ASP.NET NuGet 패키지를 포함 하는 최신 버전의 스키마를 포함 하는 NuGet 패키지를 설치할 수 있습니다 `.nuspec` .

WebMatrix 확장 업데이트에 대 한 자세한 내용은 해당 특정 [릴리스 정보](../release-notes/nuget-2.6.1-for-WebMatrix.md)를 참조 하세요.

### <a name="bug-fixes"></a>버그 픽스
이러한 기능 외에도이 NuGet 릴리스에는 다른 버그 수정이 포함 되어 있습니다. 릴리스에서는 총 16 개 문제가 해결 되었습니다. NuGet 2.8.1에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)를 확인 하세요.

### <a name="reshipping-with-visual-studio-14-ctp"></a>매번 with Visual Studio "14" CTP
6 월 3 일 2014에 출시 된 Visual Studio "14" CTP에서는 NuGet 2.8.1이 상자에 제공 됩니다. 지원 되는 기능은 Visual Studio 2013에 대 한 것과 같은 다른 2.8.1 VSIXes와 동일 하 게 유지 됩니다.
