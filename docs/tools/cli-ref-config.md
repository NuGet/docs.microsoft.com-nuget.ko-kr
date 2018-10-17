---
title: NuGet CLI 구성 명령
description: Nuget.exe config 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 376b69186ad22d4d94a1df51146b833a1f6f9bd9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546480"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="082e6-103">구성 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="082e6-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="082e6-104">**적용 대상:** 모든 &bullet; **지원 되는 버전**: 모두</span><span class="sxs-lookup"><span data-stu-id="082e6-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="082e6-105">NuGet 구성 값을 불러오거나 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="082e6-106">추가 사용법에 대한 정보는 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)을 통해 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="082e6-107">사용할 수 있는 키 값에 대한 자세한 내용은 [NuGet 구성 파일 참조](../reference/nuget-config-file.md)를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="082e6-108">사용법</span><span class="sxs-lookup"><span data-stu-id="082e6-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="082e6-109">여기서 `<name>`과 `<value>`는 구성 파일에서 설정할 키-값 쌍을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="082e6-110">필요에 따라 쌍을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="082e6-111">값을 제거하려면 이름과 `=`로 해당 키에 빈 값을 지정해주시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="082e6-112">허용되는 키 이름은 [NuGet 구성 파일 참조](../reference/nuget-config-file.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="082e6-113">NuGet 3.4 이상에서 `<value>`는 [환경 변수](cli-ref-environment-variables.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="082e6-114">옵션</span><span class="sxs-lookup"><span data-stu-id="082e6-114">Options</span></span>

| <span data-ttu-id="082e6-115">옵션</span><span class="sxs-lookup"><span data-stu-id="082e6-115">Option</span></span> | <span data-ttu-id="082e6-116">설명</span><span class="sxs-lookup"><span data-stu-id="082e6-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="082e6-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="082e6-117">AsPath</span></span> | <span data-ttu-id="082e6-118">구성 파일의 경로를 반환합니다. `-Set`이 사용될 때 옵션은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="082e6-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="082e6-119">ConfigFile</span></span> | <span data-ttu-id="082e6-120">수정할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="082e6-121">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="082e6-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="082e6-122">ForceEnglishOutput</span></span> | <span data-ttu-id="082e6-123">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="082e6-124">도움말</span><span class="sxs-lookup"><span data-stu-id="082e6-124">Help</span></span> | <span data-ttu-id="082e6-125">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="082e6-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="082e6-126">NonInteractive</span></span> | <span data-ttu-id="082e6-127">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="082e6-128">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="082e6-128">Verbosity</span></span> | <span data-ttu-id="082e6-129">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="082e6-130">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="082e6-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="082e6-131">예제</span><span class="sxs-lookup"><span data-stu-id="082e6-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
