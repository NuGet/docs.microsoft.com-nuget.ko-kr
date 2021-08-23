---
title: NuGet 5.11 릴리스 정보
description: 새로운 기능, 버그 수정 및 DCR을 포함하여 NuGet 5.11에 대한 릴리스 정보입니다.
author: erdembayar
ms.author: eryondon
ms.date: 8/10/2021
ms.topic: conceptual
ms.openlocfilehash: 97b59be0fa3da2bfb788e540fef795522d938ed4
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2021
ms.locfileid: "122728424"
---
# <a name="nuget-511-release-notes"></a>NuGet 5.11 릴리스 정보

NuGet 배포 차량:

| NuGet 버전 | Visual Studio 버전에서 사용 가능 | .NET SDK에서 사용 가능 |
|:---|:---|:---|
| [**5.11.0**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.11](https://visualstudio.microsoft.com/downloads/) | [5.0.400](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> .NET Core 워크로드를 Visual Studio 2019와 함께 설치
  
> [!NOTE]
> Visual Studio 16.11, MSBuild 16.11 및 .NET 5.0.400 이상에는 NuGet.exe 5.11이 필요합니다.

## <a name="summary-whats-new-in-511"></a>요약: 5.11의 새로운 내용

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

**버그:**

* 도구 -> 옵션 -> NuGet 패키지 관리자 문자열이 잘립니다. - [#10779](https://github.com/NuGet/Home/issues/10779)

* PackagesMissingStatusChanged 이벤트가 발생하면 중단 - [#10854](https://github.com/NuGet/Home/issues/10854)

* NuGet 클라이언트는 NO_PROXY 설정을 [무시합니다. #10902](https://github.com/NuGet/Home/issues/10902)

**[이 릴리스에서 해결된 모든 문제 목록 - 5.11](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTk5MDE)**

**[이 릴리스의 커밋 목록 - 5.11](https://github.com/NuGet/NuGet.Client/compare/5.10.0.7240...5.11.0.17)**

## <a name="feedback-welcome"></a>피드백 환영

Microsoft는 사용자의 의견을 소중하게 생각합니다.  이 릴리스에 문제가 있는 경우 [GitHub 문제를](https://github.com/NuGet/Home/issues) 확인하고 기존 문제에 대한 개발자 Community [Visual Studio.](https://developercommunity.visualstudio.com/)  NuGet 내의 새로운 문제는 [GitHub 문제를](https://github.com/NuGet/Home/issues/new)보고하세요.
일반적인 NuGet 환경 문제의 경우 도움말 > [문제 보고](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) 아래에 있는 즐겨 찾는 IDE에 있는 **문제 보고** 옵션을 통해 알려주세요.
