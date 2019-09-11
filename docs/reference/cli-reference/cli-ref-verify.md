---
title: NuGet CLI verify 명령
description: Nuget.exe verify 명령에 대 한 참조입니다.
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327500"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="04d46-103">verify 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="04d46-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="04d46-104">**적용 대상:** 패키지 &bullet; 사용 **지원 버전:** 4.6 이상</span><span class="sxs-lookup"><span data-stu-id="04d46-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="04d46-105">패키지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="04d46-105">Verifies a package.</span></span>

<span data-ttu-id="04d46-106">서명 된 패키지의 확인은 .NET Core, Mono 또는 비 Windows 플랫폼에서 아직 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04d46-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="04d46-107">사용</span><span class="sxs-lookup"><span data-stu-id="04d46-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="04d46-108">여기서 `<package(s)>` 는 하나 `.nupkg` 이상의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="04d46-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="04d46-109">nuget 확인-모두</span><span class="sxs-lookup"><span data-stu-id="04d46-109">nuget verify -All</span></span>

<span data-ttu-id="04d46-110">패키지에 대해 가능한 모든 확인을 수행 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04d46-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="04d46-111">nuget verify 서명</span><span class="sxs-lookup"><span data-stu-id="04d46-111">nuget verify -Signatures</span></span>

<span data-ttu-id="04d46-112">패키지 서명 확인을 수행 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04d46-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="04d46-113">"서명 확인"에 대 한 옵션</span><span class="sxs-lookup"><span data-stu-id="04d46-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="04d46-114">옵션</span><span class="sxs-lookup"><span data-stu-id="04d46-114">Option</span></span> | <span data-ttu-id="04d46-115">Description</span><span class="sxs-lookup"><span data-stu-id="04d46-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04d46-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="04d46-116">CertificateFingerprint</span></span> | <span data-ttu-id="04d46-117">서명 된 패키지에 서명 해야 하는 인증서의 SHA-256 인증서 지문을 하나 이상 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04d46-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="04d46-118">인증서 SHA-256 지문을 인증서의 SHA-256 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="04d46-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="04d46-119">여러 입력은 세미콜론으로 구분 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04d46-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="04d46-120">변수</span><span class="sxs-lookup"><span data-stu-id="04d46-120">Options</span></span>

| <span data-ttu-id="04d46-121">옵션</span><span class="sxs-lookup"><span data-stu-id="04d46-121">Option</span></span> | <span data-ttu-id="04d46-122">설명</span><span class="sxs-lookup"><span data-stu-id="04d46-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04d46-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="04d46-123">ConfigFile</span></span> | <span data-ttu-id="04d46-124">적용할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="04d46-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="04d46-125">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="04d46-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="04d46-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="04d46-126">ForceEnglishOutput</span></span> | <span data-ttu-id="04d46-127">고정 영어 기반 문화권을 사용 하 여 nuget.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="04d46-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="04d46-128">Help</span><span class="sxs-lookup"><span data-stu-id="04d46-128">Help</span></span> | <span data-ttu-id="04d46-129">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="04d46-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="04d46-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="04d46-130">Verbosity</span></span> | <span data-ttu-id="04d46-131">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="04d46-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="04d46-132">예</span><span class="sxs-lookup"><span data-stu-id="04d46-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```