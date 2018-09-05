---
title: 2.8.2 NuGet 릴리스 정보
description: NuGet 2.8.2 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551150"
---
# <a name="nuget-282-release-notes"></a>2.8.2 NuGet 릴리스 정보

[2.8.1 NuGet 릴리스 정보](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 릴리스 정보](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2는 2014 년 5 월 22 일에 출시 되었습니다.  이 릴리스에서 다른 NuGet 패키지, 명령줄 nuget.exe 및 NuGet.Server 패키지를 변경만 포함 됩니다.  업데이트 된 Visual Studio 확장 또는 WebMatrix 확장을 릴리스에 포함 되지 않았습니다.

## <a name="notable-updates"></a>중요 한 업데이트

명령줄 nuget.exe에 NuGet.Server 패키지 (자체 호스트 된 NuGet 피드)에 대 한 가장 중요 한 업데이트 되었습니다.

### <a name="important-nugetexe-bug-fixes"></a>중요 한 nuget.exe 버그 수정

1. [nuget.exe Push 실패 하 고 다시 시도 유지](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe Push 기본 인증 자격 증명을 올바르게 전송 하지 않습니다.](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe Push 임시 리디렉션 수행 되지 않습니다.](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>NuGet.Server 중요 한 버그 수정

1. [NuGet.Server를 반환한 IsAbsoluteLatestVersion의 잘못 된 값](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>패키지 업데이트

Nuget.exe 명령줄 및 NuGet.Server 수정 NuGet 패키지에 대 한 업데이트로 제공 됩니다.  다른 패키지도 2.8.2로 업데이트 했습니다.

업데이트 된 패키지 목록에는 다음과 같습니다.

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [참고로, NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (패키지, 확장명이 아닌)

## <a name="all-changes"></a>모든 변경 내용
릴리스에서 해결 10 문제가 있었습니다. 작업의 전체 목록은 항목 고정 2.8.2, nuget에서 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)합니다.
