---
title: NuGet CLI 삭제 명령
description: Nuget.exe delete 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548512"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="46048-103">delete 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="46048-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="46048-104">**모든 버전에서 모두 지원됩니다.**</span><span class="sxs-lookup"><span data-stu-id="46048-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="46048-105">패키지 소스 또는 패키지 목록에서 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="46048-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="46048-106">Nuget.org에서 delete 명령어는 [패키지 목록에서 삭제](../policies/deleting-packages.md)의 의미를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="46048-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="46048-107">사용법</span><span class="sxs-lookup"><span data-stu-id="46048-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="46048-108">여기서 `<packageID>` 및 `<packageVersion>` 는 패키지를 삭제하거나 목록에서 지울 특정 패키지를 지정하는데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="46048-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="46048-109">패키지 원본에 따라 동작이 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46048-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="46048-110">예를 들어, 로컬 폴더 내부에서 사용할 경우에는 패키지를 삭제하지만, nuget.org의 패키지에서 사용할 경우에는 목록에서 지우는 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="46048-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="46048-111">옵션</span><span class="sxs-lookup"><span data-stu-id="46048-111">Options</span></span>

| <span data-ttu-id="46048-112">옵션</span><span class="sxs-lookup"><span data-stu-id="46048-112">Option</span></span> | <span data-ttu-id="46048-113">설명</span><span class="sxs-lookup"><span data-stu-id="46048-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="46048-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="46048-114">ApiKey</span></span> | <span data-ttu-id="46048-115">대상 리포지토리에 대한 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="46048-115">The API key for the target repository.</span></span> <span data-ttu-id="46048-116">키가 없는 경우 구성 파일에 지정된 값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="46048-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="46048-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="46048-117">ConfigFile</span></span> | <span data-ttu-id="46048-118">수정할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="46048-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="46048-119">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="46048-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="46048-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="46048-120">ForceEnglishOutput</span></span> | <span data-ttu-id="46048-121">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="46048-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="46048-122">도움말</span><span class="sxs-lookup"><span data-stu-id="46048-122">Help</span></span> | <span data-ttu-id="46048-123">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="46048-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="46048-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="46048-124">NonInteractive</span></span> | <span data-ttu-id="46048-125">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="46048-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="46048-126">소스</span><span class="sxs-lookup"><span data-stu-id="46048-126">Source</span></span> | <span data-ttu-id="46048-127">서버 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="46048-127">Specifies the server URL.</span></span> <span data-ttu-id="46048-128">Nuget.org에 대한 URL은 `https://api.nuget.org/v3/index.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="46048-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="46048-129">개인적인 피드의 경우 예를 들어 *%hostname%/api/v3*와 같이 호스트 이름을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="46048-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="46048-130">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="46048-130">Verbosity</span></span> | <span data-ttu-id="46048-131">출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="46048-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="46048-132">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46048-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="46048-133">예제</span><span class="sxs-lookup"><span data-stu-id="46048-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
