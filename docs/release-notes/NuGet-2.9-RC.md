---
title: NuGet 2.9-RC 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 포함 하는 NuGet 2.9 RC에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780312"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="10138-103">NuGet 2.9-RC 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="10138-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="10138-104">[NuGet 2.8.7 릴리스 정보](../release-notes/nuget-2.8.7.md)  |  [NuGet 3.0 Preview 릴리스 정보](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="10138-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="10138-105">NuGet 2.9는 Visual Studio 2012 및 2013에 대 한 2.8.7 VSIX 업데이트로 서 2015 년 9 월 10 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="10138-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="10138-106">이 릴리스의 업데이트</span><span class="sxs-lookup"><span data-stu-id="10138-106">Updates in this release</span></span>

* <span data-ttu-id="10138-107">이제 포함 된 `.nuspec` 문서의 형식이 잘못 된 경우 처리 중인 패키지를 건너뜀 [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="10138-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="10138-108">Unix/Linux 시나리오에 대 한 \r\n의 multipartwebrequest 처리를 수정 했습니다.- [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="10138-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="10138-109">Visual Studio 2013 Community edition에서 빌드 이벤트와의 통합이 수정 됨- [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="10138-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="10138-110">이 릴리스의 전체 수정 목록은 GitHub의 [2.8.8 마일스 톤](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed) 에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10138-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
