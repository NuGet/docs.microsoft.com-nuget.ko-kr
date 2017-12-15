---
title: "NuGet CLI setapikey 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a64c0462-973d-4100-ba3f-8902a2b127f7
description: "Nuget.exe setapikey 명령에 대 한 참조"
keywords: "nuget setapikey 참조, setapikey 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a07c35b8bdd57157391e391e04a90204342b1d5c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
## <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="00650-104">setapikey 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="00650-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="00650-105">**적용 대상:** 패키지 소비, 게시 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="00650-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="00650-106">에 지정 된 서버 URL에 대 한 API 키를 저장 `NuGet.Config` 후속 명령에 대 한 입력 해야 할 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00650-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="00650-107">용도</span><span class="sxs-lookup"><span data-stu-id="00650-107">Usage</span></span>

```
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="00650-108">여기서 `<source>` 서버를 식별 하 고 `<key>` 키 또는 암호를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="00650-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="00650-109">경우 `<source>` 는 생략 하면 nuget.org 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00650-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="00650-110">옵션</span><span class="sxs-lookup"><span data-stu-id="00650-110">Options</span></span>

| <span data-ttu-id="00650-111">옵션</span><span class="sxs-lookup"><span data-stu-id="00650-111">Option</span></span> | <span data-ttu-id="00650-112">설명</span><span class="sxs-lookup"><span data-stu-id="00650-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="00650-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="00650-113">ConfigFile</span></span> | <span data-ttu-id="00650-114">*(2.5 +)*  NuGet 구성 파일을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00650-114">*(2.5+)* The NuGet configuration file to modify.</span></span> <span data-ttu-id="00650-115">지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00650-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="00650-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="00650-116">ForceEnglishOutput</span></span> | <span data-ttu-id="00650-117">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="00650-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="00650-118">도움말</span><span class="sxs-lookup"><span data-stu-id="00650-118">Help</span></span> | <span data-ttu-id="00650-119">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="00650-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="00650-120">비 대화형</span><span class="sxs-lookup"><span data-stu-id="00650-120">NonInteractive</span></span> | <span data-ttu-id="00650-121">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00650-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="00650-122">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="00650-122">Verbosity</span></span> | <span data-ttu-id="00650-123">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *세부 (2.5 이상)*합니다.</span><span class="sxs-lookup"><span data-stu-id="00650-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="00650-124">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="00650-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="00650-125">예제</span><span class="sxs-lookup"><span data-stu-id="00650-125">Examples</span></span>

```
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
