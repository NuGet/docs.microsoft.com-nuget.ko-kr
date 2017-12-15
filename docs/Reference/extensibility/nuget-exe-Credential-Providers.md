---
title: "nuget.exe 자격 증명 공급자 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3cf592de-39f2-4e7f-a597-62635fdcedfa
description: "nuget.exe 자격 증명 공급자는 피드를 사용 하 여 인증 하며 특정 규칙을 따르는 명령줄 실행 파일로 구현 됩니다."
keywords: "nuget.exe 자격 증명 공급자, 자격 증명 공급자 API 피드를 사용 하 여 인증, 갤러리를 사용 하 여 인증"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82ab4d6e9be0736e008f5bd27d46e1db166d7bb4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="b525b-104">Nuget.exe 자격 증명 공급자를 사용한 피드 인증</span><span class="sxs-lookup"><span data-stu-id="b525b-104">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="b525b-105">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="b525b-105">*NuGet 3.3+*</span></span>

<span data-ttu-id="b525b-106">때 `nuget.exe` 피드를 인증 하기 위한 자격 증명이 필요 다음과 같이 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-106">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="b525b-107">NuGet의 자격 증명에 먼저 찾습니다 `Nuget.Config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-107">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="b525b-108">NuGet 아래에 나와 있는 순서에 따라 플러그 인 자격 증명 공급자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-108">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="b525b-109">(및 예제는 [Visual Studio Team Services 자격 증명 공급자](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="b525b-109">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="b525b-110">NuGet은 명령줄에 자격 증명을 묻는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-110">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="b525b-111">여기에서 설명 하는 자격 증명 공급자 에서만 작동 하는 참고 `nuget.exe` 'dotnet 복원' 또는 Visual Studio에서가 아니라 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-111">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="b525b-112">Visual Studio와 함께 자격 증명 공급자를 참조 하십시오. [nuget.exe Visual Studio에 대 한 자격 증명 공급자](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="b525b-112">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="b525b-113">nuget.exe 자격 증명 공급자는 세 가지 방법에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-113">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="b525b-114">**전역으로**: 자격 증명 공급자의 모든 인스턴스를 사용할 수 있도록 하려면 `nuget.exe` 현재 사용자의 프로필에서 실행에 추가 `%LocalAppData%\NuGet\CredentialProviders`합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-114">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="b525b-115">만들어야 할 수는 `CredentialProviders` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-115">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="b525b-116">루트에 자격 증명 공급자를 설치할 수 있습니다는 `CredentialProviders` 폴더 또는 하위 폴더 내 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-116">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="b525b-117">자격 증명 공급자는 여러 파일/어셈블리에 있는 경우에 구성 공급자를 유지 하려면 하위 폴더를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-117">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="b525b-118">**환경 변수에서**: 자격 증명 공급자를 어디에 저장 하 고 액세스할 수 `nuget.exe` 설정 하 여는 `%NUGET_CREDENTIALPROVIDERS_PATH%` 환경 변수 공급자 위치를 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-118">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="b525b-119">이 변수는 세미콜론으로 구분 된 목록이 될 수 있습니다 (예를 들어 `path1;path2`) 여러 위치에 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="b525b-119">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="b525b-120">**Nuget.exe 함께**: nuget.exe 자격 증명 공급자와 같은 폴더에 배치할 수 있습니다 `nuget.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-120">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="b525b-121">자격 증명 공급자를 로드할 때 `nuget.exe` 위의 위치 이름이 인 모든 파일에 대 한 순서 대로 검색 `credentialprovider*.exe`, 하는 순서로 해당 파일을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-121">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="b525b-122">여러 자격 증명 공급자는 같은 폴더에 있으면 알파벳 순서로 로드 일입니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-122">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="b525b-123">Nuget.exe 자격 증명 공급자 만들기</span><span class="sxs-lookup"><span data-stu-id="b525b-123">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="b525b-124">자격 증명 공급자는 명령줄 실행 파일은 폴더에서 `CredentialProvider*.exe`, 입력을 수집 하는를 적절 하 게 자격 증명을 획득 하 고 적절 한 종료 상태 코드 및 표준 출력을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-124">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="b525b-125">공급자는 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-125">A provider must do the following:</span></span>

- <span data-ttu-id="b525b-126">있는지 여부를 제공할 수 있습니다 자격 증명의 대상된 URI에 대 한 자격 증명 획득을 시작 하기 전에 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-126">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="b525b-127">그렇지 않으면 상태 코드는 자격 증명 없이 1을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-127">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="b525b-128">수정 하지 `Nuget.Config` (예: 없는 자격 증명을 설정).</span><span class="sxs-lookup"><span data-stu-id="b525b-128">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="b525b-129">핸들 HTTP 프록시 구성을으로 자체 NuGet에 플러그 인 프록시 정보를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-129">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="b525b-130">자격 증명 또는에 오류 정보를 반환 `nuget.exe` utf-8 인코딩을 사용 하 여 stdout으로 JSON 응답 개체 (아래 참조)를 작성 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-130">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="b525b-131">필요에 따라 stderr에 대 한 추가 추적 로깅을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-131">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="b525b-132">"Normal" 또는 "자세히" 자세한 정도 수준에서 추적이 표시 되 면 NuGet에서 콘솔에 있으므로 적이 없는 비밀을 stderr에 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-132">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="b525b-133">예기치 않은 매개 변수를 무시 해야 NuGet의 이후 버전과 이후 버전과 호환성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-133">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b525b-134">입력된 매개 변수</span><span class="sxs-lookup"><span data-stu-id="b525b-134">Input parameters</span></span>

| <span data-ttu-id="b525b-135">매개 변수/스위치</span><span class="sxs-lookup"><span data-stu-id="b525b-135">Parameter/Switch</span></span> |<span data-ttu-id="b525b-136">설명</span><span class="sxs-lookup"><span data-stu-id="b525b-136">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="b525b-137">{Value} Uri</span><span class="sxs-lookup"><span data-stu-id="b525b-137">Uri {value}</span></span> | <span data-ttu-id="b525b-138">패키지 원본 URI 필요한 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-138">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="b525b-139">비 대화형</span><span class="sxs-lookup"><span data-stu-id="b525b-139">NonInteractive</span></span> | <span data-ttu-id="b525b-140">있는 경우 공급자는 대화형 프롬프트를 발급 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-140">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="b525b-141">IsRetry</span><span class="sxs-lookup"><span data-stu-id="b525b-141">IsRetry</span></span> | <span data-ttu-id="b525b-142">있는 경우에이 시도이 대해서는 이전에 실패 한 시도의 다시 시도 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-142">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="b525b-143">일반적으로 공급자는 모든 기존 캐시를 무시 하 고 가능한 경우 새 자격 증명을 요청 하도록이 플래그를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-143">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="b525b-144">자세한 정도 {value}</span><span class="sxs-lookup"><span data-stu-id="b525b-144">Verbosity {value}</span></span> | <span data-ttu-id="b525b-145">있는 경우 다음 값 중 하나: "normal", "자동" 또는 "자세히"입니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-145">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="b525b-146">변수에 값이 없는 경우에 "보통" 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-146">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="b525b-147">공급자를 사용 해야이의 선택적 로깅 수준 표시로 표준 오류 스트림에 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-147">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="b525b-148">종료 코드</span><span class="sxs-lookup"><span data-stu-id="b525b-148">Exit codes</span></span>

| <span data-ttu-id="b525b-149">코드</span><span class="sxs-lookup"><span data-stu-id="b525b-149">Code</span></span> |<span data-ttu-id="b525b-150">결과</span><span class="sxs-lookup"><span data-stu-id="b525b-150">Result</span></span> | <span data-ttu-id="b525b-151">설명</span><span class="sxs-lookup"><span data-stu-id="b525b-151">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="b525b-152">0</span><span class="sxs-lookup"><span data-stu-id="b525b-152">0</span></span> | <span data-ttu-id="b525b-153">성공</span><span class="sxs-lookup"><span data-stu-id="b525b-153">Success</span></span> | <span data-ttu-id="b525b-154">자격 증명을 성공적으로 인식 한 고 stdout에 기록 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-154">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="b525b-155">1</span><span class="sxs-lookup"><span data-stu-id="b525b-155">1</span></span> | <span data-ttu-id="b525b-156">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="b525b-156">ProviderNotApplicable</span></span> | <span data-ttu-id="b525b-157">현재 공급자는 지정된 된 URI에 대 한 자격 증명을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-157">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="b525b-158">2</span><span class="sxs-lookup"><span data-stu-id="b525b-158">2</span></span> | <span data-ttu-id="b525b-159">실패</span><span class="sxs-lookup"><span data-stu-id="b525b-159">Failure</span></span> | <span data-ttu-id="b525b-160">공급자는 지정된 된 URI에 대 한 올바른 공급자 하지만 자격 증명을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-160">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="b525b-161">이 경우 nuget.exe 인증을 시도 하지 않습니다 하 고 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-161">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="b525b-162">일반적인 예는 사용자가 대화형 로그인을 취소 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-162">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="b525b-163">표준 출력</span><span class="sxs-lookup"><span data-stu-id="b525b-163">Standard output</span></span>

| <span data-ttu-id="b525b-164">속성</span><span class="sxs-lookup"><span data-stu-id="b525b-164">Property</span></span> |<span data-ttu-id="b525b-165">참고</span><span class="sxs-lookup"><span data-stu-id="b525b-165">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="b525b-166">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="b525b-166">Username</span></span> | <span data-ttu-id="b525b-167">인증 된 요청에 대 한 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-167">Username for authenticated requests.</span></span>|
| <span data-ttu-id="b525b-168">암호</span><span class="sxs-lookup"><span data-stu-id="b525b-168">Password</span></span> | <span data-ttu-id="b525b-169">인증 된 요청에 대 한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-169">Password for authenticated requests.</span></span>|
| <span data-ttu-id="b525b-170">메시지</span><span class="sxs-lookup"><span data-stu-id="b525b-170">Message</span></span> | <span data-ttu-id="b525b-171">오류 발생 시에서 추가 세부 정보를 표시 하는 데에 사용 하는 응답에 대 한 선택적 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-171">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="b525b-172">예제 stdout:</span><span class="sxs-lookup"><span data-stu-id="b525b-172">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="b525b-173">자격 증명 공급자 문제 해결</span><span class="sxs-lookup"><span data-stu-id="b525b-173">Troubleshooting a credential provider</span></span>

<span data-ttu-id="b525b-174">현재, NuGet 직접 지원 하지 않고 많은 사용자 지정 자격 증명 공급자; 디버깅을 위해 [4598 발급](https://github.com/NuGet/Home/issues/4598) 이 작업을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-174">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="b525b-175">다음 작업도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-175">You can also do the following:</span></span>

- <span data-ttu-id="b525b-176">Nuget.exe와 실행의 `-verbosity` 자세한 출력을 검사 하는 스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-176">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="b525b-177">디버그 메시지 추가 `stdout` 적절 한 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-177">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="b525b-178">3.3 이상 nuget.exe를 사용 하는 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-178">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="b525b-179">이 코드 조각으로 시작할 때 디버거를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-179">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="b525b-180">자세한 도움말 [는 nuget.org 지원 요청을 제출](https://www.nuget.org/policies/Contact)합니다.</span><span class="sxs-lookup"><span data-stu-id="b525b-180">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
