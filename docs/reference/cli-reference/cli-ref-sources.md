---
title: NuGet CLI 소스 명령
description: Nuget.exe 소스 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327600"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="88d5c-103">sources 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="88d5c-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="88d5c-104">**적용 대상:** 패키지 사용, &bullet; **지원 되는 버전 게시:** 모두</span><span class="sxs-lookup"><span data-stu-id="88d5c-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="88d5c-105">사용자 범위 구성 파일 또는 지정 된 구성 파일에 있는 원본 목록을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="88d5c-106">사용자 범위 구성 파일은 (Windows) `%appdata%\NuGet\NuGet.Config` 및 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="88d5c-107">nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="88d5c-108">사용</span><span class="sxs-lookup"><span data-stu-id="88d5c-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="88d5c-109">여기서 `<operation>` 는 *목록, 추가, 제거, 사용, 사용 안 함* 또는 *업데이트*, `<name>` 는 원본의 `<source>` 이름,는 소스의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="88d5c-110">한 번에 하나의 원본 에서만 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="88d5c-111">변수</span><span class="sxs-lookup"><span data-stu-id="88d5c-111">Options</span></span>

| <span data-ttu-id="88d5c-112">옵션</span><span class="sxs-lookup"><span data-stu-id="88d5c-112">Option</span></span> | <span data-ttu-id="88d5c-113">설명</span><span class="sxs-lookup"><span data-stu-id="88d5c-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88d5c-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="88d5c-114">ConfigFile</span></span> | <span data-ttu-id="88d5c-115">적용할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="88d5c-116">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="88d5c-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="88d5c-117">ForceEnglishOutput</span></span> | <span data-ttu-id="88d5c-118">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="88d5c-119">형식</span><span class="sxs-lookup"><span data-stu-id="88d5c-119">Format</span></span> | <span data-ttu-id="88d5c-120">`list` 작업에 적용 되며 (기본값) `Detailed` 또는 `Short`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="88d5c-121">Help</span><span class="sxs-lookup"><span data-stu-id="88d5c-121">Help</span></span> | <span data-ttu-id="88d5c-122">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="88d5c-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="88d5c-123">NonInteractive</span></span> | <span data-ttu-id="88d5c-124">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="88d5c-125">암호</span><span class="sxs-lookup"><span data-stu-id="88d5c-125">Password</span></span> | <span data-ttu-id="88d5c-126">원본으로 인증 하는 데 사용할 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="88d5c-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="88d5c-127">StorePasswordInClearText</span></span> | <span data-ttu-id="88d5c-128">암호화 된 형식을 저장 하는 기본 동작 대신 암호를 암호화 되지 않은 텍스트로 저장 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="88d5c-129">UserName</span><span class="sxs-lookup"><span data-stu-id="88d5c-129">UserName</span></span> | <span data-ttu-id="88d5c-130">원본으로 인증 하는 데 사용할 사용자 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="88d5c-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="88d5c-131">Verbosity</span></span> | <span data-ttu-id="88d5c-132">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="88d5c-133">나중에 nuget.exe를 사용 하 여 패키지 원본에 액세스 하는 것과 같은 사용자 컨텍스트에서 소스의 암호를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="88d5c-134">암호는 구성 파일에 암호화 되어 저장 되며 암호화 된 것과 동일한 사용자 컨텍스트에서 암호를 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="88d5c-135">예를 들어 빌드 서버를 사용 하 여 NuGet 패키지를 복원 하는 경우 암호는 빌드 서버 태스크가 실행 되는 동일한 Windows 사용자로 암호화 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="88d5c-136">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88d5c-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="88d5c-137">예제</span><span class="sxs-lookup"><span data-stu-id="88d5c-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
