---
title: NuGet CLI 확인 명령
description: nuget.exe에 대 한 참조 확인 명령
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="3d9b8-103">verify 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3d9b8-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="3d9b8-104">**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 4.6 이상</span><span class="sxs-lookup"><span data-stu-id="3d9b8-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="3d9b8-105">패키지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3d9b8-105">Verifies a package.</span></span>

<span data-ttu-id="3d9b8-106">서명 된 패키지 확인 모노, 또는 Windows 이외의 플랫폼에서.NET Core에서는 아직 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d9b8-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="3d9b8-107">사용법</span><span class="sxs-lookup"><span data-stu-id="3d9b8-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="3d9b8-108">여기서 `<package(s)>` 는 하나 이상의 `.nupkg` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3d9b8-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="3d9b8-109">nuget 확인-모두</span><span class="sxs-lookup"><span data-stu-id="3d9b8-109">nuget verify -All</span></span>

<span data-ttu-id="3d9b8-110">패키지에서 확인 가능한 모든 작업을 수행 해야 함을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d9b8-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="3d9b8-111">nuget 서명 확인</span><span class="sxs-lookup"><span data-stu-id="3d9b8-111">nuget verify -Signatures</span></span>

<span data-ttu-id="3d9b8-112">패키지 서명 확인을 수행 해야 함을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d9b8-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="3d9b8-113">"-서명 확인"에 대 한 옵션</span><span class="sxs-lookup"><span data-stu-id="3d9b8-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="3d9b8-114">옵션</span><span class="sxs-lookup"><span data-stu-id="3d9b8-114">Option</span></span> | <span data-ttu-id="3d9b8-115">설명</span><span class="sxs-lookup"><span data-stu-id="3d9b8-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3d9b8-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="3d9b8-116">CertificateFingerprint</span></span> | <span data-ttu-id="3d9b8-117">로 서명 된 패키지를 서명 해야 하는 인증서 (s)의 하나 이상의 sha-256 인증서 지문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d9b8-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="3d9b8-118">S h A-256 인증서 지문에는 인증서의 s h A-256 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="3d9b8-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="3d9b8-119">여러 입력을 세미콜론으로 구분 된 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d9b8-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="3d9b8-120">옵션</span><span class="sxs-lookup"><span data-stu-id="3d9b8-120">Options</span></span>

| <span data-ttu-id="3d9b8-121">옵션</span><span class="sxs-lookup"><span data-stu-id="3d9b8-121">Option</span></span> | <span data-ttu-id="3d9b8-122">설명</span><span class="sxs-lookup"><span data-stu-id="3d9b8-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3d9b8-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3d9b8-123">ConfigFile</span></span> | <span data-ttu-id="3d9b8-124">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3d9b8-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3d9b8-125">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d9b8-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3d9b8-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3d9b8-126">ForceEnglishOutput</span></span> | <span data-ttu-id="3d9b8-127">Nuget.exe 고정, 영어 기반 문화권을 사용 하 여 실행을 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d9b8-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3d9b8-128">도움말</span><span class="sxs-lookup"><span data-stu-id="3d9b8-128">Help</span></span> | <span data-ttu-id="3d9b8-129">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d9b8-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="3d9b8-130">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="3d9b8-130">Verbosity</span></span> | <span data-ttu-id="3d9b8-131">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="3d9b8-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="3d9b8-132">예제</span><span class="sxs-lookup"><span data-stu-id="3d9b8-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```