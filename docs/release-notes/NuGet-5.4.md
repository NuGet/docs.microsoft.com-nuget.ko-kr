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
# <a name="nuget-54-release-notes"></a><span data-ttu-id="5a42c-103">NuGet 5.4 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="5a42c-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="5a42c-104">NuGet 배포 차량:</span><span class="sxs-lookup"><span data-stu-id="5a42c-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="5a42c-105">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="5a42c-105">NuGet version</span></span> | <span data-ttu-id="5a42c-106">Visual Studio 버전에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="5a42c-106">Available in Visual Studio version</span></span>| <span data-ttu-id="5a42c-107">.NET SDK에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="5a42c-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="5a42c-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="5a42c-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="5a42c-109">Visual Studio 2019 버전 16.4</span><span class="sxs-lookup"><span data-stu-id="5a42c-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="5a42c-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="5a42c-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="5a42c-111"><sup>1</sup> .NET Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨</span><span class="sxs-lookup"><span data-stu-id="5a42c-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="5a42c-112">요약: 5.4의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="5a42c-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="5a42c-113">빠른 솔루션 로드 시간-첫 번째 솔루션 로드 중 NuGet 코드를 실행 하는 오버 헤드가 JIT 비용을 줄이기 위해 부분 ngen을 통해 축소 되었습니다 [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="5a42c-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="5a42c-114">새 도우미 함수-패키지 id 및 버전 목록이 제공 될 경우 최상위 패키지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5a42c-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="5a42c-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="5a42c-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

* <span data-ttu-id="5a42c-116">[GitHub 작업](https://github.com/features/actions)에서 nuget.exe를 설치 하 고 구성 하기 위한 새로운 [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="5a42c-116">New [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) action for installing and configuring NuGet.exe on [GitHub Actions](https://github.com/features/actions).</span></span><span data-ttu-id="5a42c-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span><span class="sxs-lookup"><span data-stu-id="5a42c-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="5a42c-118">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="5a42c-118">Issues fixed in this release</span></span>

<span data-ttu-id="5a42c-119">**버그**</span><span class="sxs-lookup"><span data-stu-id="5a42c-119">**Bugs**</span></span>

* <span data-ttu-id="5a42c-120">플러그 인: linux/Mac에서 로깅 시간 정확성이 off- [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="5a42c-120">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="5a42c-121">플러그 인을 삭제 하면 경우에 따라 전체 작업이 throw 및 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a42c-121">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="5a42c-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="5a42c-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="5a42c-123">PMUI- [#8679](https://github.com/NuGet/Home/issues/8679) 의 허용 및 차단 된 버전 목록에서 버전 중복 표시를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a42c-123">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="5a42c-124">잠금 파일이 제대로 생성 되지 않음-lockedmode로 복원에 영향을 주지 않습니다.- [#8645](https://github.com/NuGet/Home/issues/8645)</span><span class="sxs-lookup"><span data-stu-id="5a42c-124">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="5a42c-125">SDK 3.0.100에 <RuntimeIdentifiers> 집합이 설정 된 프로젝트에 대해 LockFile 유효성 검사가 실패 합니다.- [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="5a42c-125">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="5a42c-126">서명 유효성 검사는 이제 동일한 OID에 2 개의 값이 있는 타임 스탬프를 사용 하 여 서명을 올바르게 거부 합니다. [#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="5a42c-126">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="5a42c-127">라이선스 목록 업데이트- [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="5a42c-127">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="5a42c-128">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="5a42c-128">**DCRs**</span></span>

* <span data-ttu-id="5a42c-129">IFeedbackDiagnosticFileProvider에 진단 파일 온 보 딩- [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="5a42c-129">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="5a42c-130">**[이 릴리스에서 해결 된 모든 문제 목록-5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="5a42c-130">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
