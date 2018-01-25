---
title: "NuGet CLI 명령 원본 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "nuget.exe에 대 한 참조의 소스가 명령"
keywords: "nuget 원본 참조, 명령 원본"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c1cd909c0c35d52f0269d267367669df46f9db55
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="d9ffd-104">소스 명령은 NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d9ffd-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="d9ffd-105">**적용 대상:** 패키지 소비, 게시 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="d9ffd-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d9ffd-106">원본에 있는 목록 관리 `%AppData%\NuGet\NuGet.Config` 또는 지정된 된 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

<span data-ttu-id="d9ffd-107">nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="d9ffd-108">사용법</span><span class="sxs-lookup"><span data-stu-id="d9ffd-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="d9ffd-109">여기서 `<operation>` 중 하나입니다 *목록, 추가, 제거, 설정, 해제* 또는 *업데이트*, `<name>` 에 원본의 이름 및 `<source>` 원본의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="d9ffd-110">옵션</span><span class="sxs-lookup"><span data-stu-id="d9ffd-110">Options</span></span>

| <span data-ttu-id="d9ffd-111">옵션</span><span class="sxs-lookup"><span data-stu-id="d9ffd-111">Option</span></span> | <span data-ttu-id="d9ffd-112">설명</span><span class="sxs-lookup"><span data-stu-id="d9ffd-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d9ffd-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d9ffd-113">ConfigFile</span></span> | <span data-ttu-id="d9ffd-114">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d9ffd-115">지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="d9ffd-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d9ffd-116">ForceEnglishOutput</span></span> | <span data-ttu-id="d9ffd-117">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d9ffd-118">형식</span><span class="sxs-lookup"><span data-stu-id="d9ffd-118">Format</span></span> | <span data-ttu-id="d9ffd-119">에 적용 됩니다는 `list` 작업 수 및 `Detailed` (기본값) 또는 `Short`합니다.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="d9ffd-120">도움말</span><span class="sxs-lookup"><span data-stu-id="d9ffd-120">Help</span></span> | <span data-ttu-id="d9ffd-121">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="d9ffd-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d9ffd-122">NonInteractive</span></span> | <span data-ttu-id="d9ffd-123">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d9ffd-124">암호</span><span class="sxs-lookup"><span data-stu-id="d9ffd-124">Password</span></span> | <span data-ttu-id="d9ffd-125">소스에 인증 하기 위해 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="d9ffd-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="d9ffd-126">StorePasswordInClearText</span></span> | <span data-ttu-id="d9ffd-127">암호화 된 형식에 저장할 경우의 기본 동작 대신 암호화 되지 않은 텍스트에서 암호를 저장 하려면 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="d9ffd-128">UserName</span><span class="sxs-lookup"><span data-stu-id="d9ffd-128">UserName</span></span> | <span data-ttu-id="d9ffd-129">소스를 사용 하 여 인증에 대 한 사용자 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="d9ffd-130">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="d9ffd-130">Verbosity</span></span> | <span data-ttu-id="d9ffd-131">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="d9ffd-132">nuget.exe 패키지 원본에 액세스 하는 데 사용 나중에 동일한 사용자 컨텍스트에서 소스 암호를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="d9ffd-133">암호 구성 파일에 암호화 된 저장 되 고 암호화 된 대로 동일한 사용자 컨텍스트에서 해독할만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="d9ffd-134">예를 사용 하면 빌드 서버 빌드 서버 작업이 실행 될 Windows 사용자가 암호를 암호화 해야 하는 NuGet 패키지를 복원 하려면.</span><span class="sxs-lookup"><span data-stu-id="d9ffd-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="d9ffd-135">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d9ffd-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d9ffd-136">예제</span><span class="sxs-lookup"><span data-stu-id="d9ffd-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
