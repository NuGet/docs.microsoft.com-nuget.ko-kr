---
title: "NuGet CLI config 명령 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a50295ff-8be9-47d9-a260-822e899334cb
description: "Nuget.exe config 명령에 대 한 참조"
keywords: "nuget 구성 참조, config 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f49751d9747687177e3b6c1890ee9d2919be8d0e
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/10/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="a7adf-104">구성 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a7adf-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="a7adf-105">**적용 대상:** 모든 &bullet; **지원 되는 버전**: 모든</span><span class="sxs-lookup"><span data-stu-id="a7adf-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="a7adf-106">NuGet 구성 값을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7adf-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="a7adf-107">추가 사용에 대 한 참조 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7adf-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="a7adf-108">허용 가능한 키 이름에 대 한 자세한 내용은 참조는 [NuGet config 파일 참조](../Schema/nuget-config-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7adf-108">For details on allowable key names, refer to the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a7adf-109">사용법</span><span class="sxs-lookup"><span data-stu-id="a7adf-109">Usage</span></span>

```
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="a7adf-110">여기서 `<name>` 및 `<value>` 구성에서 설정할 키-값 쌍을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7adf-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="a7adf-111">필요에 따라 쌍을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7adf-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="a7adf-112">값을 제거 하려면 이름을 지정 및 `=` 기호 있지만 값이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7adf-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="a7adf-113">허용 가능한 키 이름에 대 한 참조는 [NuGet config 파일 참조](../Schema/nuget-config-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7adf-113">For allowable key names, see the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

<span data-ttu-id="a7adf-114">NuGet 3.4 +에서 `<value>` צ ְ ײ [환경 변수](cli-ref-environment-variables.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7adf-114">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="a7adf-115">옵션</span><span class="sxs-lookup"><span data-stu-id="a7adf-115">Options</span></span>

| <span data-ttu-id="a7adf-116">옵션</span><span class="sxs-lookup"><span data-stu-id="a7adf-116">Option</span></span> | <span data-ttu-id="a7adf-117">설명</span><span class="sxs-lookup"><span data-stu-id="a7adf-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a7adf-118">AsPath</span><span class="sxs-lookup"><span data-stu-id="a7adf-118">AsPath</span></span> | <span data-ttu-id="a7adf-119">경로, 구성 값이 반환 될 때 무시 `-Set` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7adf-119">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="a7adf-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a7adf-120">ConfigFile</span></span> | <span data-ttu-id="a7adf-121">*(2.5 +)*  NuGet 구성 파일을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7adf-121">*(2.5+)* The NuGet configuration file to modify.</span></span> <span data-ttu-id="a7adf-122">지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7adf-122">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="a7adf-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a7adf-123">ForceEnglishOutput</span></span> | <span data-ttu-id="a7adf-124">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7adf-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a7adf-125">도움말</span><span class="sxs-lookup"><span data-stu-id="a7adf-125">Help</span></span> | <span data-ttu-id="a7adf-126">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7adf-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="a7adf-127">비 대화형</span><span class="sxs-lookup"><span data-stu-id="a7adf-127">NonInteractive</span></span> | <span data-ttu-id="a7adf-128">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7adf-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a7adf-129">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="a7adf-129">Verbosity</span></span> | <span data-ttu-id="a7adf-130">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *세부 (2.5 이상)*합니다.</span><span class="sxs-lookup"><span data-stu-id="a7adf-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="a7adf-131">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a7adf-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="a7adf-132">예제</span><span class="sxs-lookup"><span data-stu-id="a7adf-132">Examples</span></span>

```
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
