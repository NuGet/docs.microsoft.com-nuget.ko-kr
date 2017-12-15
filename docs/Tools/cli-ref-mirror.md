---
title: "NuGet CLI 미러 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 190d7010-172e-44b8-8a32-94a2a63be4f3
description: "Nuget.exe 미러 명령에 대 한 참조"
keywords: "nuget 미러 참조, 미러 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67daa1aa278b42b7974c562ba4097a525e7bb105
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="41f69-104">미러 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="41f69-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="41f69-105">**적용 대상:** 게시 패키지 &bullet; **지원 되는 버전:** 3.2 +에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="41f69-106">패키지 및 대상 저장소에 지정 된 원본 저장소에서 해당 종속성을 미러링합니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="41f69-107">3.2 전에 NuGet 버전에 대 한이 명령을 사용 하려면로 이동 [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)안정적인 최신 버전을 다운로드 `NuGet.ServerExtensions.dll` 및 `Nuget-Signed.exe` 로컬 디스크와 이름 바꾸기 `Nuget-Signed.exe` 를 `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="41f69-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="41f69-108">용도</span><span class="sxs-lookup"><span data-stu-id="41f69-108">Usage</span></span>

```
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="41f69-109">여기서 `<packageID>` 을 미러링 하는 패키지 또는 `<configFilePath>` 식별는 `packages.config` 파일을 미러링 하는 패키지를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="41f69-110">`<listUrlTarget>` 소스 리포지토리를 지정 하 고 `<publishUrlTarget>` 대상 저장소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="41f69-111">대상 저장소에 있으면 `https://machine/repo` 실행 중인 [NuGet.Server](../hosting-packages/NuGet-Server.md), 목록 및 푸시 url 됩니다 `https://machine/repo/nuget` 및 `https://machine/repo/api/v2/package`각각.</span><span class="sxs-lookup"><span data-stu-id="41f69-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/NuGet-Server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="41f69-112">옵션</span><span class="sxs-lookup"><span data-stu-id="41f69-112">Options</span></span>

| <span data-ttu-id="41f69-113">옵션</span><span class="sxs-lookup"><span data-stu-id="41f69-113">Option</span></span> | <span data-ttu-id="41f69-114">설명</span><span class="sxs-lookup"><span data-stu-id="41f69-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="41f69-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="41f69-115">ApiKey</span></span> | <span data-ttu-id="41f69-116">대상 저장소에 대 한 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-116">The API key for the target repository.</span></span> <span data-ttu-id="41f69-117">없음, 1에 지정 된 경우 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-117">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="41f69-118">도움말</span><span class="sxs-lookup"><span data-stu-id="41f69-118">Help</span></span> | <span data-ttu-id="41f69-119">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="41f69-120">캐시 없음</span><span class="sxs-lookup"><span data-stu-id="41f69-120">NoCache</span></span> | <span data-ttu-id="41f69-121">NuGet 패키지를 사용 하 여 로컬 컴퓨터 캐시에서 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="41f69-122">Noop</span><span class="sxs-lookup"><span data-stu-id="41f69-122">Noop</span></span> | <span data-ttu-id="41f69-123">기록 수행 기능 하지만; 작업을 수행 하지 않습니다. 푸시 작업에 대 한 성공을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="41f69-124">시험판</span><span class="sxs-lookup"><span data-stu-id="41f69-124">PreRelease</span></span> | <span data-ttu-id="41f69-125">미러링 작업에 시험판 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="41f69-126">소스</span><span class="sxs-lookup"><span data-stu-id="41f69-126">Source</span></span> | <span data-ttu-id="41f69-127">목록으로 미러링 하기 위해 패키지 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-127">A list of package sources to mirror.</span></span> <span data-ttu-id="41f69-128">것에 정의 된 원본이 지정 된 경우 *%AppData%\NuGet\NuGet.Config* nuget.org를 지정 하지 않으면 기본값으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-128">If no sources are specified, the ones defined in *%AppData%\NuGet\NuGet.Config* are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="41f69-129">시간 제한</span><span class="sxs-lookup"><span data-stu-id="41f69-129">Timeout</span></span> | <span data-ttu-id="41f69-130">서버에 밀어 넣는 초 제한 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="41f69-131">기본값은 300 초 (5 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="41f69-132">버전</span><span class="sxs-lookup"><span data-stu-id="41f69-132">Version</span></span> | <span data-ttu-id="41f69-133">설치할 패키지의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-133">The version of the package to install.</span></span> <span data-ttu-id="41f69-134">지정 하지 않으면 최신 버전이 미러 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f69-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="41f69-135">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="41f69-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="41f69-136">예제</span><span class="sxs-lookup"><span data-stu-id="41f69-136">Examples</span></span>

```
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
