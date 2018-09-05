---
title: NuGet CLI 미러 명령
description: Nuget.exe 미러 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550208"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="8f357-103">mirror 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8f357-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="8f357-104">**적용 대상:** 게시 패키지 &bullet; **지원 되는 버전:** 3.2 이상에서 사용 되지 않음</span><span class="sxs-lookup"><span data-stu-id="8f357-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="8f357-105">패키지 및 대상 저장소에 지정 된 소스 리포지토리에서 해당 종속성을 미러링합니다.</span><span class="sxs-lookup"><span data-stu-id="8f357-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="8f357-106">을 3.2 전에 NuGet 버전에 대해이 명령을 사용 하도록 설정 하려면로 이동 [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)다운로드를 안정적인 최신 릴리스를 선택 `NuGet.ServerExtensions.dll` 하 고 `Nuget-Signed.exe` 로컬 디스크 및 이름 바꾸기 `Nuget-Signed.exe` 에 `nuget.exe`입니다.</span><span class="sxs-lookup"><span data-stu-id="8f357-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="8f357-107">사용법</span><span class="sxs-lookup"><span data-stu-id="8f357-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="8f357-108">여기서 `<packageID>` 미러, 패키지 또는 `<configFilePath>` 하 게 식별 하는 `packages.config` 미러링 하는 패키지를 나열 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8f357-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="8f357-109">`<listUrlTarget>` 소스 리포지토리를 지정 하 고 `<publishUrlTarget>` 대상 리포지토리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f357-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="8f357-110">대상 리포지토리에에 있으면 `https://machine/repo` 실행 중인 [NuGet.Server](../hosting-packages/nuget-server.md), 목록 및 푸시 url 됩니다 `https://machine/repo/nuget` 및 `https://machine/repo/api/v2/package`각각.</span><span class="sxs-lookup"><span data-stu-id="8f357-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="8f357-111">옵션</span><span class="sxs-lookup"><span data-stu-id="8f357-111">Options</span></span>

| <span data-ttu-id="8f357-112">옵션</span><span class="sxs-lookup"><span data-stu-id="8f357-112">Option</span></span> | <span data-ttu-id="8f357-113">설명</span><span class="sxs-lookup"><span data-stu-id="8f357-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8f357-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="8f357-114">ApiKey</span></span> | <span data-ttu-id="8f357-115">대상 리포지토리에 대 한 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="8f357-115">The API key for the target repository.</span></span> <span data-ttu-id="8f357-116">이 헤더가 없으면 구성 파일에 지정 된 사용 됩니다 (`%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="8f357-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="8f357-117">도움말</span><span class="sxs-lookup"><span data-stu-id="8f357-117">Help</span></span> | <span data-ttu-id="8f357-118">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f357-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="8f357-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="8f357-119">NoCache</span></span> | <span data-ttu-id="8f357-120">캐시 된 패키지를 사용 하 여 NuGet을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f357-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="8f357-121">참조 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f357-121">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="8f357-122">Noop</span><span class="sxs-lookup"><span data-stu-id="8f357-122">Noop</span></span> | <span data-ttu-id="8f357-123">로그 항목가 수행 되지만; 작업을 수행 하지 않습니다. 푸시 작업에 대 한 성공을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f357-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="8f357-124">PreRelease</span><span class="sxs-lookup"><span data-stu-id="8f357-124">PreRelease</span></span> | <span data-ttu-id="8f357-125">미러링 작업에 시험판 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8f357-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="8f357-126">소스</span><span class="sxs-lookup"><span data-stu-id="8f357-126">Source</span></span> | <span data-ttu-id="8f357-127">미러 패키지 원본의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="8f357-127">A list of package sources to mirror.</span></span> <span data-ttu-id="8f357-128">항목에 정의 된 소스 없음이 지정 된 경우 구성 파일 (위의 ApiKey 참조) 되는, 지정 되지 않은 경우 nuget.org에 기본값으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f357-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="8f357-129">시간 제한</span><span class="sxs-lookup"><span data-stu-id="8f357-129">Timeout</span></span> | <span data-ttu-id="8f357-130">서버에 푸시하기 위한 초 제한 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f357-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="8f357-131">기본값은 300 초 (5 분).</span><span class="sxs-lookup"><span data-stu-id="8f357-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="8f357-132">버전</span><span class="sxs-lookup"><span data-stu-id="8f357-132">Version</span></span> | <span data-ttu-id="8f357-133">설치 패키지의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="8f357-133">The version of the package to install.</span></span> <span data-ttu-id="8f357-134">지정 하지 않으면 최신 버전 미러 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f357-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="8f357-135">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8f357-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8f357-136">예제</span><span class="sxs-lookup"><span data-stu-id="8f357-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
