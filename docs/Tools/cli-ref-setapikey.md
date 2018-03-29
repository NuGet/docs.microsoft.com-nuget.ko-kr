---
title: NuGet CLI setapikey 명령을 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe setapikey 명령에 대 한 참조
keywords: nuget setapikey 참조, setapikey 명령
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 696ccf9df5af487d3bf75925c1c1e0d1d1bf7f7b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="0cb0c-104">setapikey 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0cb0c-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="0cb0c-105">**적용 대상:** 패키지 소비, 게시 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="0cb0c-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0cb0c-106">에 지정 된 서버 URL에 대 한 API 키를 저장 `NuGet.Config` 후속 명령에 대 한 입력 해야 할 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cb0c-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="0cb0c-107">사용법</span><span class="sxs-lookup"><span data-stu-id="0cb0c-107">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="0cb0c-108">여기서 `<source>` 서버를 식별 하 고 `<key>` 키 또는 암호를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cb0c-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="0cb0c-109">경우 `<source>` 는 생략 하면 nuget.org 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cb0c-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="0cb0c-110">옵션</span><span class="sxs-lookup"><span data-stu-id="0cb0c-110">Options</span></span>

| <span data-ttu-id="0cb0c-111">옵션</span><span class="sxs-lookup"><span data-stu-id="0cb0c-111">Option</span></span> | <span data-ttu-id="0cb0c-112">설명</span><span class="sxs-lookup"><span data-stu-id="0cb0c-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0cb0c-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0cb0c-113">ConfigFile</span></span> | <span data-ttu-id="0cb0c-114">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0cb0c-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0cb0c-115">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cb0c-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="0cb0c-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0cb0c-116">ForceEnglishOutput</span></span> | <span data-ttu-id="0cb0c-117">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cb0c-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0cb0c-118">도움말</span><span class="sxs-lookup"><span data-stu-id="0cb0c-118">Help</span></span> | <span data-ttu-id="0cb0c-119">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cb0c-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="0cb0c-120">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="0cb0c-120">NonInteractive</span></span> | <span data-ttu-id="0cb0c-121">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cb0c-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0cb0c-122">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="0cb0c-122">Verbosity</span></span> | <span data-ttu-id="0cb0c-123">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="0cb0c-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="0cb0c-124">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0cb0c-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0cb0c-125">예제</span><span class="sxs-lookup"><span data-stu-id="0cb0c-125">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
