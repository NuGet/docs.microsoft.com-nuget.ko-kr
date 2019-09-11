---
title: NuGet CLI setapikey 명령
description: Nuget.exe setapikey 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327610"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="0b1cf-103">setapikey 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0b1cf-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="0b1cf-104">**적용 대상:** 패키지 사용, &bullet; **지원 되는 버전 게시:** 모두</span><span class="sxs-lookup"><span data-stu-id="0b1cf-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0b1cf-105">지정 된 서버 URL에 대 한 API 키를 `NuGet.Config` 에 저장 하 여 후속 명령에 대해 입력이 필요 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1cf-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="0b1cf-106">사용</span><span class="sxs-lookup"><span data-stu-id="0b1cf-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="0b1cf-107">여기서 `<source>` 는 서버를 식별 `<key>` 하 고는 저장할 키 또는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="0b1cf-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="0b1cf-108">을 `<source>` 생략 하면 nuget.org이 가정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b1cf-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="0b1cf-109">변수</span><span class="sxs-lookup"><span data-stu-id="0b1cf-109">Options</span></span>

| <span data-ttu-id="0b1cf-110">옵션</span><span class="sxs-lookup"><span data-stu-id="0b1cf-110">Option</span></span> | <span data-ttu-id="0b1cf-111">설명</span><span class="sxs-lookup"><span data-stu-id="0b1cf-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0b1cf-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0b1cf-112">ConfigFile</span></span> | <span data-ttu-id="0b1cf-113">적용할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0b1cf-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0b1cf-114">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b1cf-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="0b1cf-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0b1cf-115">ForceEnglishOutput</span></span> | <span data-ttu-id="0b1cf-116">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1cf-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0b1cf-117">Help</span><span class="sxs-lookup"><span data-stu-id="0b1cf-117">Help</span></span> | <span data-ttu-id="0b1cf-118">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1cf-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="0b1cf-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="0b1cf-119">NonInteractive</span></span> | <span data-ttu-id="0b1cf-120">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1cf-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0b1cf-121">Verbosity</span><span class="sxs-lookup"><span data-stu-id="0b1cf-121">Verbosity</span></span> | <span data-ttu-id="0b1cf-122">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1cf-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="0b1cf-123">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1cf-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0b1cf-124">예제</span><span class="sxs-lookup"><span data-stu-id="0b1cf-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
