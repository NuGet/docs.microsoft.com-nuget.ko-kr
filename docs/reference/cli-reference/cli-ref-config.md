---
title: NuGet CLI 구성 명령
description: nuget.exe config 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7d0c1c51f40cba9a5b69f209ffbd995451bfeb9f
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622878"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="8adfe-103">config 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8adfe-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="8adfe-104">**적용 대상:** &bullet; **지원 되**는 모든 버전: 모두</span><span class="sxs-lookup"><span data-stu-id="8adfe-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="8adfe-105">NuGet 구성 값을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8adfe-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="8adfe-106">추가 사용에 대해서는 [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8adfe-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="8adfe-107">허용 되는 키 이름에 대 한 자세한 내용은 [NuGet 구성 파일 참조](../nuget-config-file.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8adfe-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8adfe-108">사용량</span><span class="sxs-lookup"><span data-stu-id="8adfe-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="8adfe-109">여기서 `<name>` 및는 `<value>` 구성에서 설정할 키-값 쌍을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8adfe-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="8adfe-110">원하는 수 만큼 쌍을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8adfe-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="8adfe-111">값을 제거 하려면 이름 및 기호를 지정 하 고 값은 지정 `=` 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="8adfe-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="8adfe-112">허용 되는 키 이름에 대해서는 [NuGet 구성 파일 참조](../nuget-config-file.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8adfe-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="8adfe-113">NuGet 3.4 이상에서는 `<value>` [환경 변수](cli-ref-environment-variables.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8adfe-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="8adfe-114">옵션</span><span class="sxs-lookup"><span data-stu-id="8adfe-114">Options</span></span>


- **`AsPath`**

  <span data-ttu-id="8adfe-115">구성 값을 경로로 반환 하 고가 사용 될 때 무시 됩니다 `-Set` .</span><span class="sxs-lookup"><span data-stu-id="8adfe-115">Returns the config value as a path, ignored when `-Set` is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="8adfe-116">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8adfe-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8adfe-117">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8adfe-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="8adfe-118">*(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8adfe-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="8adfe-119">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8adfe-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="8adfe-120">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8adfe-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-Set`**

  <span data-ttu-id="8adfe-121">구성에 설정할 키-값 쌍이 하나 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8adfe-121">One on more key-value pairs to be set in config.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="8adfe-122">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="8adfe-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="8adfe-123">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="8adfe-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="8adfe-124">예</span><span class="sxs-lookup"><span data-stu-id="8adfe-124">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
