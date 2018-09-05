---
title: nuget.exe 자격 증명 공급자
description: nuget.exe 자격 증명 공급자는 피드를 사용 하 여 인증 하 고 특정 규칙을 따르는 명령줄 실행 파일로 구현 됩니다.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550191"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="42b49-103">Nuget.exe 자격 증명 공급자를 사용 하 여 피드 인증</span><span class="sxs-lookup"><span data-stu-id="42b49-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="42b49-104">*NuGet 3.3 이상*</span><span class="sxs-lookup"><span data-stu-id="42b49-104">*NuGet 3.3+*</span></span>

<span data-ttu-id="42b49-105">때 `nuget.exe` 피드를 사용 하 여 인증 하려면 자격 증명이 필요에 다음과 같은 방식으로 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-105">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="42b49-106">NuGet에서 자격 증명을 먼저 찾습니다 `Nuget.Config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-106">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="42b49-107">NuGet에는 아래에 나와 있는 순서에 따라 플러그 인 자격 증명 공급자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-107">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="42b49-108">(예제 이며 합니다 [Visual Studio Team Services 자격 증명 공급자](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="42b49-108">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="42b49-109">NuGet은 명령줄에 자격 증명을 묻는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-109">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="42b49-110">여기에 설명 된 자격 증명 공급자 에서만 작동 하는 참고 `nuget.exe` 및 'dotnet restore' 또는 Visual Studio에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-110">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="42b49-111">Visual Studio를 사용 하 여 자격 증명 공급자를 참조 하세요. [nuget.exe Visual Studio에 대 한 자격 증명 공급자](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="42b49-111">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="42b49-112">nuget.exe 자격 증명 공급자는 3 가지 방법으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-112">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="42b49-113">**전 세계**: 자격 증명 공급자의 모든 인스턴스를 사용할 수 있도록 `nuget.exe` 현재 사용자의 프로필에서 실행, 추가 `%LocalAppData%\NuGet\CredentialProviders`합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-113">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="42b49-114">만들어야 할 수 있습니다는 `CredentialProviders` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-114">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="42b49-115">자격 증명 공급자의 루트에 설치할 수는 `CredentialProviders` 폴더 또는 하위 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-115">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="42b49-116">자격 증명 공급자를 여러 파일/어셈블리에 있는 경우에 구성 공급자를 유지 하려면 하위 폴더를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-116">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="42b49-117">**환경 변수에서**: 자격 증명 공급자를 어디서 나 저장에 액세스할 수 있게 `nuget.exe` 설정 하 여는 `%NUGET_CREDENTIALPROVIDERS_PATH%` 공급자 위치에 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-117">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="42b49-118">이 변수는 세미콜론으로 구분 된 목록을 사용할 수 있습니다 (예를 들어 `path1;path2`) 여러 위치가 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="42b49-118">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="42b49-119">**Nuget.exe와 함께**: nuget.exe 자격 증명 공급자와 같은 폴더에 배치할 수 있습니다 `nuget.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-119">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="42b49-120">자격 증명 공급자를 로드할 때 `nuget.exe` 위의 위치를 모든 파일에 대 한 순서 대로 검색 `credentialprovider*.exe`, 발견 될 순서에서 해당 파일을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-120">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="42b49-121">여러 자격 증명 공급자 동일한 폴더에 있는 경우 사전순으로 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-121">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="42b49-122">Nuget.exe 자격 증명 공급자 만들기</span><span class="sxs-lookup"><span data-stu-id="42b49-122">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="42b49-123">자격 증명 공급자는 명령줄 실행 파일을 형태로 `CredentialProvider*.exe`, 입력을 수집 하는, 적절 하 게 자격 증명을 획득 하 고 적절 한 종료 상태 코드 및 표준 출력을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-123">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="42b49-124">공급자는 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-124">A provider must do the following:</span></span>

- <span data-ttu-id="42b49-125">여부를 제공할 수 있습니다 자격 증명을 대상으로 지정 된 URI에 대 한 자격 증명 획득을 시작 하기 전에 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-125">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="42b49-126">그렇지 않은 경우 상태 코드 1 자격 증명이 없는 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-126">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="42b49-127">수정 하지 `Nuget.Config` (예: 자격 증명 설정을).</span><span class="sxs-lookup"><span data-stu-id="42b49-127">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="42b49-128">핸들 HTTP 프록시 구성으로 자체 NuGet에서 플러그 인 프록시 정보를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-128">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="42b49-129">자격 증명 또는 오류 세부 정보를 반환 `nuget.exe` stdout으로 utf-8 인코딩을 사용 하 여 JSON 응답 개체 (아래 참조)를 작성 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-129">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="42b49-130">필요에 따라 stderr에 로깅을 추가 추적을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-130">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="42b49-131">"Normal" 또는 "자세히" 세부 정보 표시 수준에서 추적이 표시 되 면 NuGet에서 콘솔에 있으므로 적이 없습니다 비밀을 stderr에 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-131">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="42b49-132">예기치 않은 매개 변수를 무시 해야 나중 버전의 NuGet 사용 하 여 이후 버전과 호환성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-132">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="42b49-133">입력된 매개 변수</span><span class="sxs-lookup"><span data-stu-id="42b49-133">Input parameters</span></span>

| <span data-ttu-id="42b49-134">매개 변수/스위치</span><span class="sxs-lookup"><span data-stu-id="42b49-134">Parameter/Switch</span></span> |<span data-ttu-id="42b49-135">설명</span><span class="sxs-lookup"><span data-stu-id="42b49-135">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="42b49-136">Uri {value}</span><span class="sxs-lookup"><span data-stu-id="42b49-136">Uri {value}</span></span> | <span data-ttu-id="42b49-137">패키지 원본 URI 필요한 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-137">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="42b49-138">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="42b49-138">NonInteractive</span></span> | <span data-ttu-id="42b49-139">있는 경우 공급자는 대화형 프롬프트 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-139">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="42b49-140">isRetry</span><span class="sxs-lookup"><span data-stu-id="42b49-140">IsRetry</span></span> | <span data-ttu-id="42b49-141">있는 경우이 시도 재시도는 이전에 실패 한 시도 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-141">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="42b49-142">일반적으로 공급자는 모든 기존 캐시 무시 하 고 가능한 경우 새 자격 증명을 요청 하도록이 플래그를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-142">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="42b49-143">{Value} 세부 정보 표시</span><span class="sxs-lookup"><span data-stu-id="42b49-143">Verbosity {value}</span></span> | <span data-ttu-id="42b49-144">있는 경우 다음 값 중 하나: "normal", "quiet" 또는 "자세히"입니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-144">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="42b49-145">변수에 값이 없는 경우 "normal" 기본값은입니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-145">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="42b49-146">공급자를 사용 해야이의 선택적 로깅 수준 확인 하기 위해 표준 오류 스트림에 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-146">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="42b49-147">종료 코드</span><span class="sxs-lookup"><span data-stu-id="42b49-147">Exit codes</span></span>

| <span data-ttu-id="42b49-148">코드</span><span class="sxs-lookup"><span data-stu-id="42b49-148">Code</span></span> |<span data-ttu-id="42b49-149">결과</span><span class="sxs-lookup"><span data-stu-id="42b49-149">Result</span></span> | <span data-ttu-id="42b49-150">설명</span><span class="sxs-lookup"><span data-stu-id="42b49-150">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="42b49-151">0</span><span class="sxs-lookup"><span data-stu-id="42b49-151">0</span></span> | <span data-ttu-id="42b49-152">성공</span><span class="sxs-lookup"><span data-stu-id="42b49-152">Success</span></span> | <span data-ttu-id="42b49-153">자격 증명 성공적으로 획득 된 및 stdout에 기록 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-153">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="42b49-154">1</span><span class="sxs-lookup"><span data-stu-id="42b49-154">1</span></span> | <span data-ttu-id="42b49-155">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="42b49-155">ProviderNotApplicable</span></span> | <span data-ttu-id="42b49-156">현재 공급자는 지정된 된 URI에 대 한 자격 증명을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-156">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="42b49-157">2</span><span class="sxs-lookup"><span data-stu-id="42b49-157">2</span></span> | <span data-ttu-id="42b49-158">실패</span><span class="sxs-lookup"><span data-stu-id="42b49-158">Failure</span></span> | <span data-ttu-id="42b49-159">공급자는 지정된 된 URI에 대 한 올바른 공급자 하지만 자격 증명을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-159">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="42b49-160">이 경우 nuget.exe 인증 다시 시도 하지 않습니다 하 고 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-160">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="42b49-161">일반적인 예제는 사용자가 대화형 로그인을 취소 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-161">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="42b49-162">표준 출력</span><span class="sxs-lookup"><span data-stu-id="42b49-162">Standard output</span></span>

| <span data-ttu-id="42b49-163">속성</span><span class="sxs-lookup"><span data-stu-id="42b49-163">Property</span></span> |<span data-ttu-id="42b49-164">노트</span><span class="sxs-lookup"><span data-stu-id="42b49-164">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="42b49-165">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="42b49-165">Username</span></span> | <span data-ttu-id="42b49-166">인증 된 요청에 대 한 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-166">Username for authenticated requests.</span></span>|
| <span data-ttu-id="42b49-167">암호</span><span class="sxs-lookup"><span data-stu-id="42b49-167">Password</span></span> | <span data-ttu-id="42b49-168">인증 된 요청에 대 한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-168">Password for authenticated requests.</span></span>|
| <span data-ttu-id="42b49-169">메시지</span><span class="sxs-lookup"><span data-stu-id="42b49-169">Message</span></span> | <span data-ttu-id="42b49-170">실패할 경우에서 추가 세부 정보를 표시 하는 데에 사용 하는 응답에 대 한 세부 정보 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-170">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="42b49-171">예제에서는 stdout:</span><span class="sxs-lookup"><span data-stu-id="42b49-171">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="42b49-172">자격 증명 공급자 문제 해결</span><span class="sxs-lookup"><span data-stu-id="42b49-172">Troubleshooting a credential provider</span></span>

<span data-ttu-id="42b49-173">현재, NuGet 직접 지원 하지 않고 많은 사용자 지정 자격 증명 공급자, 디버깅 [4598 발급](https://github.com/NuGet/Home/issues/4598) 이 작업을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-173">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="42b49-174">다음 작업도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-174">You can also do the following:</span></span>

- <span data-ttu-id="42b49-175">Nuget.exe 사용 하 여 실행을 `-verbosity` 스위치를 자세한 출력을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-175">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="42b49-176">디버그 메시지를 추가 `stdout` 적절 한 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-176">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="42b49-177">Nuget.exe 3.3 이상을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-177">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="42b49-178">이 코드 조각 사용 하 여 시작 시는 디버거를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-178">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="42b49-179">추가 도움말을 보려면 [는 nuget.org 지원 요청을 제출](https://www.nuget.org/policies/Contact)합니다.</span><span class="sxs-lookup"><span data-stu-id="42b49-179">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
