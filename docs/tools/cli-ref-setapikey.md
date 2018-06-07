---
title: NuGet CLI setapikey 명령
description: Nuget.exe setapikey 명령에 대 한 참조
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 66fc62074b4e7c39ff2ed6b515eee9f821530536
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817686"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="ffceb-103">setapikey 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ffceb-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="ffceb-104">**적용 대상:** 패키지 소비, 게시 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="ffceb-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ffceb-105">에 지정 된 서버 URL에 대 한 API 키를 저장 `NuGet.Config` 후속 명령에 대 한 입력 해야 할 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffceb-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="ffceb-106">사용법</span><span class="sxs-lookup"><span data-stu-id="ffceb-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="ffceb-107">여기서 `<source>` 서버를 식별 하 고 `<key>` 키 또는 암호를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffceb-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="ffceb-108">경우 `<source>` 는 생략 하면 nuget.org 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffceb-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="ffceb-109">옵션</span><span class="sxs-lookup"><span data-stu-id="ffceb-109">Options</span></span>

| <span data-ttu-id="ffceb-110">옵션</span><span class="sxs-lookup"><span data-stu-id="ffceb-110">Option</span></span> | <span data-ttu-id="ffceb-111">설명</span><span class="sxs-lookup"><span data-stu-id="ffceb-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ffceb-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ffceb-112">ConfigFile</span></span> | <span data-ttu-id="ffceb-113">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ffceb-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ffceb-114">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffceb-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ffceb-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ffceb-115">ForceEnglishOutput</span></span> | <span data-ttu-id="ffceb-116">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffceb-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ffceb-117">도움말</span><span class="sxs-lookup"><span data-stu-id="ffceb-117">Help</span></span> | <span data-ttu-id="ffceb-118">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffceb-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="ffceb-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ffceb-119">NonInteractive</span></span> | <span data-ttu-id="ffceb-120">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffceb-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ffceb-121">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="ffceb-121">Verbosity</span></span> | <span data-ttu-id="ffceb-122">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="ffceb-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ffceb-123">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ffceb-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ffceb-124">예제</span><span class="sxs-lookup"><span data-stu-id="ffceb-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
