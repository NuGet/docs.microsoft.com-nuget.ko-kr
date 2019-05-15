---
title: NuGet CLI 명령 원본
description: Nuget.exe에 대 한 참조 원본 명령
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610628"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="fe8ff-103">sources 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fe8ff-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="fe8ff-104">**적용 대상:** 패키지 사용, 게시 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="fe8ff-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="fe8ff-105">사용자 범위 구성 파일 또는 지정된 된 구성 파일에 있는 원본 목록을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="fe8ff-106">사용자 범위 구성 파일에 위치한 `%appdata%\NuGet\NuGet.Config` (Windows) 및 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="fe8ff-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="fe8ff-107">nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="fe8ff-108">사용법</span><span class="sxs-lookup"><span data-stu-id="fe8ff-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="fe8ff-109">여기서 `<operation>` 중 하나인 *나열, 추가, 제거, 설정, 해제* 또는 *업데이트*를 `<name>` 원본의 이름 및 `<source>` 소스의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="fe8ff-110">한 번에 하나의 원본에서 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="fe8ff-111">옵션</span><span class="sxs-lookup"><span data-stu-id="fe8ff-111">Options</span></span>

| <span data-ttu-id="fe8ff-112">옵션</span><span class="sxs-lookup"><span data-stu-id="fe8ff-112">Option</span></span> | <span data-ttu-id="fe8ff-113">설명</span><span class="sxs-lookup"><span data-stu-id="fe8ff-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fe8ff-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fe8ff-114">ConfigFile</span></span> | <span data-ttu-id="fe8ff-115">적용할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fe8ff-116">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="fe8ff-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fe8ff-117">ForceEnglishOutput</span></span> | <span data-ttu-id="fe8ff-118">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fe8ff-119">형식</span><span class="sxs-lookup"><span data-stu-id="fe8ff-119">Format</span></span> | <span data-ttu-id="fe8ff-120">에 적용 합니다 `list` 작업 수 `Detailed` (기본값) 또는 `Short`합니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="fe8ff-121">Help</span><span class="sxs-lookup"><span data-stu-id="fe8ff-121">Help</span></span> | <span data-ttu-id="fe8ff-122">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="fe8ff-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="fe8ff-123">NonInteractive</span></span> | <span data-ttu-id="fe8ff-124">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fe8ff-125">암호</span><span class="sxs-lookup"><span data-stu-id="fe8ff-125">Password</span></span> | <span data-ttu-id="fe8ff-126">소스를 사용 하 여 인증 하기 위한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="fe8ff-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="fe8ff-127">StorePasswordInClearText</span></span> | <span data-ttu-id="fe8ff-128">암호화 된 폼을 저장 하는 기본 동작 대신 암호화 되지 않은 텍스트에서 암호를 저장 하려면이 옵션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="fe8ff-129">UserName</span><span class="sxs-lookup"><span data-stu-id="fe8ff-129">UserName</span></span> | <span data-ttu-id="fe8ff-130">소스를 사용 하 여 인증에 대 한 사용자 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="fe8ff-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="fe8ff-131">Verbosity</span></span> | <span data-ttu-id="fe8ff-132">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="fe8ff-133">패키지 원본에 액세스 하려면 nuget.exe를 나중에 사용 되는 동일한 사용자 컨텍스트에서 소스를 암호를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="fe8ff-134">암호 구성 파일에 암호화 되어 저장 될 하며만 해독할 수 동일한 사용자 컨텍스트에서 암호화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="fe8ff-135">예를 들어 사용 하는 경우 빌드 서버에 빌드 서버 작업이 실행 될 동일한 Windows 사용자를 사용 하 여 암호를 암호화 해야 하는 NuGet 패키지를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="fe8ff-136">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe8ff-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fe8ff-137">예제</span><span class="sxs-lookup"><span data-stu-id="fe8ff-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
