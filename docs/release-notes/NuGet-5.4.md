---
title: NuGet 5.4 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.4에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: c7fb9c1e587b6603abe63581c662571abfd4506b
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384113"
---
# <a name="nuget-54-release-notes"></a>NuGet 5.4 릴리스 정보

NuGet 배포 차량:

| NuGet 버전 | Visual Studio 버전에서 사용 가능| .NET SDK에서 사용 가능|
|:---|:---|:---|
| [**5.4.0**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.4](https://visualstudio.microsoft.com/downloads/) | [3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> .NET Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨

## <a name="summary-whats-new-in-54"></a>요약: 5.4의 새로운 기능

* 빠른 솔루션 로드 시간-첫 번째 솔루션 로드 중 NuGet 코드를 실행 하는 오버 헤드가 JIT 비용을 줄이기 위해 부분 ngen을 통해 축소 되었습니다 [#6007](https://github.com/NuGet/Home/issues/6007)

* 새 도우미 함수-패키지 id 및 버전 목록이 제공 될 경우 최상위 패키지를 가져옵니다. - [#8316](https://github.com/NuGet/Home/issues/8316)

* [GitHub 작업](https://github.com/features/actions)에서 nuget.exe를 설치 하 고 구성 하기 위한 새로운 [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) 동작입니다. - [#8818](https://github.com/NuGet/Home/issues/8818)

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

**버그**

* 플러그 인: linux/Mac에서 로깅 시간 정확성이 off- [#8747](https://github.com/NuGet/Home/issues/8747)

* 플러그 인을 삭제 하면 경우에 따라 전체 작업이 throw 및 실패할 수 있습니다. - [#8732](https://github.com/NuGet/Home/issues/8732)

* PMUI- [#8679](https://github.com/NuGet/Home/issues/8679) 의 허용 및 차단 된 버전 목록에서 버전 중복 표시를 중지 합니다.

* 잠금 파일이 제대로 생성 되지 않음-lockedmode로 복원에 영향을 주지 않습니다.- [#8645](https://github.com/NuGet/Home/issues/8645)

* SDK 3.0.100에 <RuntimeIdentifiers> 집합이 설정 된 프로젝트에 대해 LockFile 유효성 검사가 실패 합니다.- [#8639](https://github.com/NuGet/Home/issues/8639)

* 서명 유효성 검사는 이제 동일한 OID에 2 개의 값이 있는 타임 스탬프를 사용 하 여 서명을 올바르게 거부 합니다. [#8629](https://github.com/NuGet/Home/issues/8629)

* 라이선스 목록 업데이트- [#8544](https://github.com/NuGet/Home/issues/8544)

**DCRs**

* IFeedbackDiagnosticFileProvider에 진단 파일 온 보 딩- [#8535](https://github.com/NuGet/Home/issues/8535)

**[이 릴리스에서 해결 된 모든 문제 목록-5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**
