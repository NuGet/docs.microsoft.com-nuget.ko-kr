---
title: NuGet CLI 구성 명령
description: Nuget.exe config 명령에 대 한 참조
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 414eb8386f949347772f33170de881534dc71482
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="862bc-103">구성 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="862bc-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="862bc-104">**적용 대상:** 모든 &bullet; **지원 되는 버전**: 모든</span><span class="sxs-lookup"><span data-stu-id="862bc-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="862bc-105">NuGet 구성 값을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="862bc-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="862bc-106">추가 사용에 대 한 참조 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="862bc-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="862bc-107">허용 가능한 키 이름에 대 한 자세한 내용은 참조는 [NuGet config 파일 참조](../reference/nuget-config-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="862bc-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="862bc-108">사용법</span><span class="sxs-lookup"><span data-stu-id="862bc-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="862bc-109">여기서 `<name>` 및 `<value>` 구성에서 설정할 키-값 쌍을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="862bc-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="862bc-110">필요에 따라 쌍을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="862bc-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="862bc-111">값을 제거 하려면 이름을 지정 및 `=` 기호 있지만 값이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="862bc-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="862bc-112">허용 가능한 키 이름에 대 한 참조는 [NuGet config 파일 참조](../reference/nuget-config-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="862bc-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="862bc-113">NuGet 3.4 +에서 `<value>` צ ְ ײ [환경 변수](cli-ref-environment-variables.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="862bc-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="862bc-114">옵션</span><span class="sxs-lookup"><span data-stu-id="862bc-114">Options</span></span>

| <span data-ttu-id="862bc-115">옵션</span><span class="sxs-lookup"><span data-stu-id="862bc-115">Option</span></span> | <span data-ttu-id="862bc-116">설명</span><span class="sxs-lookup"><span data-stu-id="862bc-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="862bc-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="862bc-117">AsPath</span></span> | <span data-ttu-id="862bc-118">경로, 구성 값이 반환 될 때 무시 `-Set` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="862bc-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="862bc-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="862bc-119">ConfigFile</span></span> | <span data-ttu-id="862bc-120">NuGet 구성 파일 수정입니다.</span><span class="sxs-lookup"><span data-stu-id="862bc-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="862bc-121">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="862bc-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="862bc-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="862bc-122">ForceEnglishOutput</span></span> | <span data-ttu-id="862bc-123">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="862bc-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="862bc-124">도움말</span><span class="sxs-lookup"><span data-stu-id="862bc-124">Help</span></span> | <span data-ttu-id="862bc-125">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="862bc-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="862bc-126">비 대화형</span><span class="sxs-lookup"><span data-stu-id="862bc-126">NonInteractive</span></span> | <span data-ttu-id="862bc-127">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="862bc-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="862bc-128">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="862bc-128">Verbosity</span></span> | <span data-ttu-id="862bc-129">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="862bc-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="862bc-130">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="862bc-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="862bc-131">예제</span><span class="sxs-lookup"><span data-stu-id="862bc-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
