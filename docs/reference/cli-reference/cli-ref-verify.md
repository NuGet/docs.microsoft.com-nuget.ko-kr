---
title: NuGet CLI verify 명령
description: nuget.exe verify 명령에 대 한 참조
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 2c501753a16820c5d027441001561c6b637ccda9
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622605"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="1d4d8-103">verify 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1d4d8-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="1d4d8-104">**적용 대상:** 패키지 사용 &bullet; **지원 버전:** 4.6 이상</span><span class="sxs-lookup"><span data-stu-id="1d4d8-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="1d4d8-105">패키지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-105">Verifies a package.</span></span>

<span data-ttu-id="1d4d8-106">서명 된 패키지의 확인은 .NET Core, Mono 또는 비 Windows 플랫폼에서 아직 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="1d4d8-107">사용량</span><span class="sxs-lookup"><span data-stu-id="1d4d8-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="1d4d8-108">여기서 `<package(s)>` 는 하나 이상의 `.nupkg` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="1d4d8-109">nuget 확인-모두</span><span class="sxs-lookup"><span data-stu-id="1d4d8-109">nuget verify -All</span></span>

<span data-ttu-id="1d4d8-110">패키지에 대해 가능한 모든 확인을 수행 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="1d4d8-111">nuget verify 서명</span><span class="sxs-lookup"><span data-stu-id="1d4d8-111">nuget verify -Signatures</span></span>

<span data-ttu-id="1d4d8-112">패키지 서명 확인을 수행 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="1d4d8-113">"서명 확인"에 대 한 옵션</span><span class="sxs-lookup"><span data-stu-id="1d4d8-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="1d4d8-114">서명 된 패키지에 서명 해야 하는 인증서의 SHA-256 인증서 지문을 하나 이상 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="1d4d8-115">인증서 SHA-256 지문을 인증서의 SHA-256 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="1d4d8-116">여러 입력은 세미콜론으로 구분 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="1d4d8-117">옵션</span><span class="sxs-lookup"><span data-stu-id="1d4d8-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="1d4d8-118">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1d4d8-119">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="1d4d8-120">고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="1d4d8-121">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="1d4d8-122">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="1d4d8-123">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="1d4d8-124">예</span><span class="sxs-lookup"><span data-stu-id="1d4d8-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```