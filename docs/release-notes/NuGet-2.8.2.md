---
title: NuGet 2.8.2 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 2.8.2를 포함 하는 NuGet에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780369"
---
# <a name="nuget-282-release-notes"></a>NuGet 2.8.2 릴리스 정보

[NuGet 2.8.1 릴리스 정보](../release-notes/nuget-2.8.1.md)  |  [NuGet 2.8.3 릴리스 정보](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2는 2014 년 5 월 22 일에 릴리스 되었습니다.  이 릴리스에는 nuget.exe 명령줄, NuGet. 서버 패키지 및 기타 NuGet 패키지에 대 한 변경 내용만 포함 되었습니다.  릴리스에 업데이트 된 Visual Studio 확장 또는 WebMatrix 확장이 포함 되어 있지 않습니다.

## <a name="notable-updates"></a>주목할 만한 업데이트

가장 주목할 만한 업데이트는 nuget.exe 명령줄과 NuGet. 서버 패키지 (자체 호스팅 NuGet 피드의 경우)에 있습니다.

### <a name="important-nugetexe-bug-fixes"></a>중요 nuget.exe 버그 수정

1. [nuget.exe 푸시가 실패 하 고 다시 시도 합니다.](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe Push는 기본 인증 자격 증명을 올바르게 보내지 않습니다.](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe 푸시는 임시 리디렉션을 따르지 않습니다.](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>중요 NuGet. 서버 버그 수정

1. [NuGet. 서버에서 반환 된 IsAbsoluteLatestVersion의 값이 잘못 되었습니다.](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>패키지가 업데이트 됨

nuget.exe 명령줄 및 NuGet. 서버 픽스는 NuGet 패키지 업데이트로 제공 됩니다.  2.8.2으로 업데이트 된 다른 패키지도 있습니다.

업데이트 된 패키지 목록은 다음과 같습니다.

1. [NuGet. 핵심](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet 명령줄](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet 빌드](https://www.nuget.org/packages/NuGet.Build/)
1. [VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (확장명이 아닌 패키지)

## <a name="all-changes"></a>모든 변경 내용
릴리스에서는 10 개의 문제가 해결 되었습니다. NuGet 2.8.2에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)를 확인 하세요.
