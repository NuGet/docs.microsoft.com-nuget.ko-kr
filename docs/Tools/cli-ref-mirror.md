---
title: NuGet CLI 미러 명령을 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 미러 명령에 대 한 참조
keywords: nuget 미러 참조, 미러 명령
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 512bd72d568cda81eb7c6a1555c36ead66b5c438
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="96bb4-104">미러 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="96bb4-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="96bb4-105">**적용 대상:** 게시 패키지 &bullet; **지원 되는 버전:** 3.2 +에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="96bb4-106">패키지 및 대상 저장소에 지정 된 원본 저장소에서 해당 종속성을 미러링합니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="96bb4-107">3.2 전에 NuGet 버전에 대 한이 명령을 사용 하려면로 이동 [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)안정적인 최신 버전을 다운로드 `NuGet.ServerExtensions.dll` 및 `Nuget-Signed.exe` 로컬 디스크와 이름 바꾸기 `Nuget-Signed.exe` 를 `nuget.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="96bb4-108">사용법</span><span class="sxs-lookup"><span data-stu-id="96bb4-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="96bb4-109">여기서 `<packageID>` 을 미러링 하는 패키지 또는 `<configFilePath>` 식별는 `packages.config` 파일을 미러링 하는 패키지를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="96bb4-110">`<listUrlTarget>` 소스 리포지토리를 지정 하 고 `<publishUrlTarget>` 대상 저장소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="96bb4-111">대상 저장소에 있으면 `https://machine/repo` 실행 중인 [NuGet.Server](../hosting-packages/nuget-server.md), 목록 및 푸시 url 됩니다 `https://machine/repo/nuget` 및 `https://machine/repo/api/v2/package`각각.</span><span class="sxs-lookup"><span data-stu-id="96bb4-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="96bb4-112">옵션</span><span class="sxs-lookup"><span data-stu-id="96bb4-112">Options</span></span>

| <span data-ttu-id="96bb4-113">옵션</span><span class="sxs-lookup"><span data-stu-id="96bb4-113">Option</span></span> | <span data-ttu-id="96bb4-114">설명</span><span class="sxs-lookup"><span data-stu-id="96bb4-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="96bb4-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="96bb4-115">ApiKey</span></span> | <span data-ttu-id="96bb4-116">대상 저장소에 대 한 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-116">The API key for the target repository.</span></span> <span data-ttu-id="96bb4-117">없음, 구성 파일에 지정 된 사용 됩니다 (`%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="96bb4-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="96bb4-118">도움말</span><span class="sxs-lookup"><span data-stu-id="96bb4-118">Help</span></span> | <span data-ttu-id="96bb4-119">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="96bb4-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="96bb4-120">NoCache</span></span> | <span data-ttu-id="96bb4-121">캐시 된 패키지를 사용 하 여 NuGet을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="96bb4-122">참조 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-122">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="96bb4-123">Noop</span><span class="sxs-lookup"><span data-stu-id="96bb4-123">Noop</span></span> | <span data-ttu-id="96bb4-124">기록 수행 기능 하지만; 작업을 수행 하지 않습니다. 푸시 작업에 대 한 성공을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="96bb4-125">시험판</span><span class="sxs-lookup"><span data-stu-id="96bb4-125">PreRelease</span></span> | <span data-ttu-id="96bb4-126">미러링 작업에 시험판 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="96bb4-127">소스</span><span class="sxs-lookup"><span data-stu-id="96bb4-127">Source</span></span> | <span data-ttu-id="96bb4-128">목록으로 미러링 하기 위해 패키지 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-128">A list of package sources to mirror.</span></span> <span data-ttu-id="96bb4-129">것에 정의 된 원본이 지정 된 경우 구성 파일 (참조 ApiKey 위의)는 사용을 지정 하지 않으면 nuget.org가 기본값으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="96bb4-130">시간 제한</span><span class="sxs-lookup"><span data-stu-id="96bb4-130">Timeout</span></span> | <span data-ttu-id="96bb4-131">서버에 밀어 넣는 초 제한 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="96bb4-132">기본값은 300 초 (5 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="96bb4-133">버전</span><span class="sxs-lookup"><span data-stu-id="96bb4-133">Version</span></span> | <span data-ttu-id="96bb4-134">설치할 패키지의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-134">The version of the package to install.</span></span> <span data-ttu-id="96bb4-135">지정 하지 않으면 최신 버전이 미러 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96bb4-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="96bb4-136">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="96bb4-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="96bb4-137">예제</span><span class="sxs-lookup"><span data-stu-id="96bb4-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
