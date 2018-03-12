---
title: "NuGet CLI 명령을 확인 | Microsoft Docs"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "nuget.exe에 대 한 참조 확인 명령"
keywords: "nuget 참조를 확인, 확인 명령"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 2747491eb35d8685a44e86fcc1b572013982c754
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="8985c-104">명령 (NuGet CLI)를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8985c-104">verify command (NuGet CLI)</span></span>

<span data-ttu-id="8985c-105">**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 4.6 이상</span><span class="sxs-lookup"><span data-stu-id="8985c-105">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="8985c-106">패키지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8985c-106">Verifies a package.</span></span>

## <a name="usage"></a><span data-ttu-id="8985c-107">사용법</span><span class="sxs-lookup"><span data-stu-id="8985c-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="8985c-108">여기서 `<package(s)>` 는 하나 이상의 `.nupkg` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8985c-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="8985c-109">옵션</span><span class="sxs-lookup"><span data-stu-id="8985c-109">Options</span></span>

| <span data-ttu-id="8985c-110">옵션</span><span class="sxs-lookup"><span data-stu-id="8985c-110">Option</span></span> | <span data-ttu-id="8985c-111">설명</span><span class="sxs-lookup"><span data-stu-id="8985c-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8985c-112">모두</span><span class="sxs-lookup"><span data-stu-id="8985c-112">All</span></span> | <span data-ttu-id="8985c-113">패키지에서 확인 가능한 모든 작업을 수행 해야 함을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8985c-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="8985c-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="8985c-114">CertificateFingerprint</span></span> | <span data-ttu-id="8985c-115">로 서명 된 패키지를 서명 해야 하는 인증서 (s)의 하나 이상의 sha-256 인증서 지문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8985c-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="8985c-116">S h A-256 인증서 지문에는 인증서의 s h A-256 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="8985c-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="8985c-117">여러 입력을 세미콜론으로 구분 된 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8985c-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="8985c-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8985c-118">ConfigFile</span></span> | <span data-ttu-id="8985c-119">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8985c-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8985c-120">지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8985c-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="8985c-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8985c-121">ForceEnglishOutput</span></span> | <span data-ttu-id="8985c-122">Nuget.exe 고정, 영어 기반 문화권을 사용 하 여 실행을 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8985c-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8985c-123">도움말</span><span class="sxs-lookup"><span data-stu-id="8985c-123">Help</span></span> | <span data-ttu-id="8985c-124">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8985c-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="8985c-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8985c-125">NonInteractive</span></span> | <span data-ttu-id="8985c-126">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8985c-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8985c-127">서명</span><span class="sxs-lookup"><span data-stu-id="8985c-127">Signatures</span></span> | <span data-ttu-id="8985c-128">패키지 서명 확인을 수행 해야 함을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8985c-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="8985c-129">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="8985c-129">Verbosity</span></span> | <span data-ttu-id="8985c-130">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="8985c-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="8985c-131">예제</span><span class="sxs-lookup"><span data-stu-id="8985c-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```