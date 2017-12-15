---
title: "NuGet 2.8.2 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: bb547f5d-3c0e-4721-b2c7-3fc7e09c34de
description: "NuGet 2.8.2 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다."
keywords: "NuGet 2.8.2 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 221b8970663ca80a986fc3ee542b99971c5e2018
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-282-release-notes"></a>NuGet 2.8.2 릴리스 정보

[NuGet 2.8.1 릴리스 정보](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 릴리스 정보](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 2014 년 5 월 22 일에 출시 되었습니다.  이 릴리스에서 명령줄 nuget.exe, NuGet.Server 패키지 및 기타 NuGet 패키지에 대 한 변경만 포함 합니다.  릴리스는 업데이트 된 Visual Studio 확장명 또는 WebMatrix 확장 포함 되지 않았습니다.

## <a name="notable-updates"></a>주목할 만한 업데이트

가장 주목할 만한 업데이트 명령줄 nuget.exe 및 자체 호스트 된 NuGet 피드) (용 NuGet.Server 패키지에 있었습니다.

### <a name="important-nugetexe-bug-fixes"></a>Nuget.exe 중요 한 버그 수정

1. [nuget.exe 푸시 실패 하 고 다시 시도 유지 합니다.](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe 푸시 기본 인증 자격 증명을 올바르게 전송 하지 않습니다.](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe 푸시 임시 리디렉션 수행 되지 않습니다.](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>중요 한 NuGet.Server 버그 수정

1. [NuGet.Server 반환한 IsAbsoluteLatestVersion의 잘못 된 값](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>업데이트 패키지

Nuget.exe 명령줄 및 NuGet.Server 수정에 NuGet 패키지에 대 한 업데이트로 제공 됩니다.  다른 패키지도 2.8.2로 업데이트 했습니다.

업데이트 된 패키지 목록은 다음과 같습니다.

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (패키지, 확장명이 아닌)

## <a name="all-changes"></a>모든 변경 내용
릴리스가 10 읽어 있었습니다. 작업의 전체 목록에 대 한 항목에서에서 수정 된 NuGet 2.8.2, 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)합니다.
