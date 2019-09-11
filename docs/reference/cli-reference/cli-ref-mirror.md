---
title: NuGet CLI 미러 명령
description: Nuget.exe 미러 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959718"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="995b7-103">mirror 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="995b7-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="995b7-104">**적용 대상:** 패키지 게시 &bullet; **지원 버전:** 3.2 이상에서 사용 되지 않음</span><span class="sxs-lookup"><span data-stu-id="995b7-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="995b7-105">패키지와 해당 종속성을 지정 된 원본 리포지토리에서 대상 리포지토리로 미러링합니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="995b7-106">이전에 NuGet 2.x에서이 명령을 지원 (NuGet-Signed에서 nuget.exe로 이름 바꾸기) 하는 Nuget.exe 및 NuGet-Signed는 더 이상 다운로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="995b7-107">이와 유사한 명령을 사용 하려면 [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/)를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="995b7-108">사용</span><span class="sxs-lookup"><span data-stu-id="995b7-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="995b7-109">여기서 `<packageID>` 는 미러링할 패키지 이거나 `<configFilePath>` 미러링할 패키지가 나열 된 `packages.config` 파일을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="995b7-110">는 `<listUrlTarget>` 원본 리포지토리를 지정 하 고 `<publishUrlTarget>` 대상 리포지토리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="995b7-111">`https://machine/repo` 대상 리포지토리가 [NuGet. Server](../../hosting-packages/nuget-server.md)를 실행 하는 경우 목록 및 `https://machine/repo/nuget` 푸시 url은 각각 및 `https://machine/repo/api/v2/package`입니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="995b7-112">변수</span><span class="sxs-lookup"><span data-stu-id="995b7-112">Options</span></span>

| <span data-ttu-id="995b7-113">옵션</span><span class="sxs-lookup"><span data-stu-id="995b7-113">Option</span></span> | <span data-ttu-id="995b7-114">설명</span><span class="sxs-lookup"><span data-stu-id="995b7-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="995b7-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="995b7-115">ApiKey</span></span> | <span data-ttu-id="995b7-116">대상 리포지토리에 대한 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-116">The API key for the target repository.</span></span> <span data-ttu-id="995b7-117">존재 하지 않는 경우 구성 파일에 지정 된 항목 (`%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux))이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="995b7-118">Help</span><span class="sxs-lookup"><span data-stu-id="995b7-118">Help</span></span> | <span data-ttu-id="995b7-119">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="995b7-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="995b7-120">NoCache</span></span> | <span data-ttu-id="995b7-121">NuGet이 캐시 된 패키지를 사용 하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="995b7-122">[전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="995b7-122">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="995b7-123">Noop</span><span class="sxs-lookup"><span data-stu-id="995b7-123">Noop</span></span> | <span data-ttu-id="995b7-124">수행할 작업을 기록 하지만 작업을 수행 하지는 않습니다. 푸시 작업의 성공 여부를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="995b7-125">PreRelease</span><span class="sxs-lookup"><span data-stu-id="995b7-125">PreRelease</span></span> | <span data-ttu-id="995b7-126">미러링 작업에 시험판 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="995b7-127">Source</span><span class="sxs-lookup"><span data-stu-id="995b7-127">Source</span></span> | <span data-ttu-id="995b7-128">미러링할 패키지 원본의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-128">A list of package sources to mirror.</span></span> <span data-ttu-id="995b7-129">소스를 지정 하지 않으면 구성 파일에 정의 된 소스 (위 ApiKey 참조)가 사용 되 고, 아무것도 지정 되지 않은 경우 nuget.org가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="995b7-130">제한 시간</span><span class="sxs-lookup"><span data-stu-id="995b7-130">Timeout</span></span> | <span data-ttu-id="995b7-131">서버에 푸시하는 제한 시간 (초)을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="995b7-132">기본값은 300 초 (5 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="995b7-133">버전</span><span class="sxs-lookup"><span data-stu-id="995b7-133">Version</span></span> | <span data-ttu-id="995b7-134">설치할 패키지의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-134">The version of the package to install.</span></span> <span data-ttu-id="995b7-135">지정 하지 않으면 최신 버전이 미러링됩니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="995b7-136">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="995b7-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="995b7-137">예제</span><span class="sxs-lookup"><span data-stu-id="995b7-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
