---
title: nuget.exe 자격 증명 공급자
description: nuget.exe 자격 증명 공급자는 피드를 통해 인증하며 특정 규칙을 따르는 명령줄 실행 파일로 구현됩니다.
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 4f0a5a2355b34c39a435d24691a3f8ea10ee9c00
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323832"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="0aedb-103">nuget.exe 자격 증명 공급자를 통해 피드 인증</span><span class="sxs-lookup"><span data-stu-id="0aedb-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="0aedb-104">버전에서 `3.3` 특정 자격 증명 공급자에 대한 지원이 `nuget.exe` 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-104">In version `3.3` support was added for `nuget.exe` specific credential providers.</span></span> <span data-ttu-id="0aedb-105">그 이후로 `4.8` 모든 명령줄 시나리오(, , )에서 작동하는 [자격 증명 공급자에 대한](NuGet-Cross-Platform-Authentication-Plugin.md) 버전 지원이 `nuget.exe` `dotnet.exe` `msbuild.exe` 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-105">Since then, in version `4.8` [support for credential providers](NuGet-Cross-Platform-Authentication-Plugin.md) that work across all command line scenarios (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) was added.</span></span>

<span data-ttu-id="0aedb-106">에 대한 모든 인증 방법에 대한 자세한 내용은 [인증된 피드에서 패키지](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) 사용 을 참조하세요. `nuget.exe`</span><span class="sxs-lookup"><span data-stu-id="0aedb-106">See [Consuming Packages from authenticated feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) for more details on all authentication approaches for `nuget.exe`</span></span>

## <a name="nugetexe-credential-provider-discovery"></a><span data-ttu-id="0aedb-107">자격 증명 공급자 검색 nuget.exe</span><span class="sxs-lookup"><span data-stu-id="0aedb-107">nuget.exe credential provider discovery</span></span>

<span data-ttu-id="0aedb-108">nuget.exe 자격 증명 공급자는 다음 세 가지 방법으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-108">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="0aedb-109">**전역적으로:** 현재 사용자의 프로필에서 실행 중인 모든 인스턴스에서 자격 증명 공급자를 사용할 수 있도록 하려면 에 `nuget.exe` `%LocalAppData%\NuGet\CredentialProviders` 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-109">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="0aedb-110">폴더를 만들어야 할 수도 `CredentialProviders` 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-110">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="0aedb-111">자격 증명 공급자는 폴더의 루트 또는 하위 폴더 내에 설치할 수 `CredentialProviders`  있습니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-111">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="0aedb-112">자격 증명 공급자에 여러 파일/어셈블리가 있는 경우 하위 폴더를 사용하여 공급자를 구성 상태로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-112">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="0aedb-113">**환경 변수에서:** 환경 `nuget.exe` 변수를 공급자 위치로 설정하여 자격 증명 공급자를 어디에나 저장하고 액세스할 수 `%NUGET_CREDENTIALPROVIDERS_PATH%` 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-113">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="0aedb-114">이 변수는 여러 위치가 있는 경우 세미콜론으로 구분된 목록(예: )일 수 `path1;path2` 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-114">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="0aedb-115">**nuget.exe함께:** nuget.exe 자격 증명 공급자를 와 동일한 폴더에 배치할 수 `nuget.exe` 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-115">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="0aedb-116">자격 증명 공급자를 로드할 때 `nuget.exe` 는 위의 위치에서 라는 파일을 순서대로 `credentialprovider*.exe` 검색한 다음, 해당 파일을 찾은 순서대로 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-116">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="0aedb-117">동일한 폴더에 여러 자격 증명 공급자가 있는 경우 사전순으로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-117">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="0aedb-118">nuget.exe 자격 증명 공급자 만들기</span><span class="sxs-lookup"><span data-stu-id="0aedb-118">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="0aedb-119">자격 증명 공급자는 형식으로 명명된 명령줄 실행 `CredentialProvider*.exe` 파일로, 입력을 수집하고, 자격 증명을 적절하게 획득한 다음, 적절한 종료 상태 코드 및 표준 출력을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-119">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="0aedb-120">공급자는 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-120">A provider must do the following:</span></span>

- <span data-ttu-id="0aedb-121">자격 증명 획득을 시작하기 전에 대상 URI에 대한 자격 증명을 제공할 수 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-121">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="0aedb-122">그렇지 않은 경우 자격 증명 없이 상태 코드 1을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-122">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="0aedb-123">수정하지 `NuGet.Config` 않습니다(예: 자격 증명 설정).</span><span class="sxs-lookup"><span data-stu-id="0aedb-123">Not modify `NuGet.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="0aedb-124">NuGet은 플러그 인에 프록시 정보를 제공하지 않으므로 HTTP 프록시 구성을 자체적으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-124">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="0aedb-125">`nuget.exe`UTF-8 인코딩을 사용하여 stdout에 JSON 응답 개체(아래 참조)를 작성하여 자격 증명 또는 오류 세부 정보를 에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-125">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="0aedb-126">필요에 따라 추가 추적 로깅을 stderr로 내림합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-126">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="0aedb-127">세부 정보 표시 수준에서 "정상" 또는 "자세히" 이러한 추적은 NuGet에서 콘솔에 에코되므로 비밀은 stderr에 기록되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-127">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="0aedb-128">예기치 않은 매개 변수는 무시해야 하며, 향후 버전의 NuGet과의 호환성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-128">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0aedb-129">입력 매개 변수</span><span class="sxs-lookup"><span data-stu-id="0aedb-129">Input parameters</span></span>

| <span data-ttu-id="0aedb-130">매개 변수/스위치</span><span class="sxs-lookup"><span data-stu-id="0aedb-130">Parameter/Switch</span></span> |<span data-ttu-id="0aedb-131">Description</span><span class="sxs-lookup"><span data-stu-id="0aedb-131">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="0aedb-132">Uri {value}</span><span class="sxs-lookup"><span data-stu-id="0aedb-132">Uri {value}</span></span> | <span data-ttu-id="0aedb-133">자격 증명이 필요한 패키지 원본 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-133">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="0aedb-134">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="0aedb-134">NonInteractive</span></span> | <span data-ttu-id="0aedb-135">있는 경우 공급자는 대화형 프롬프트를 발급하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-135">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="0aedb-136">IsRetry</span><span class="sxs-lookup"><span data-stu-id="0aedb-136">IsRetry</span></span> | <span data-ttu-id="0aedb-137">있는 경우 이 시도가 이전에 실패한 시도의 재시도임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-137">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="0aedb-138">공급자는 일반적으로 이 플래그를 사용하여 기존 캐시를 무시하고 가능한 경우 새 자격 증명을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-138">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="0aedb-139">자세한 정보 {value}</span><span class="sxs-lookup"><span data-stu-id="0aedb-139">Verbosity {value}</span></span> | <span data-ttu-id="0aedb-140">있는 경우 "normal", "quiet" 또는 "detailed" 값 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-140">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="0aedb-141">값을 제공하지 않으면 기본값은 "normal"입니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-141">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="0aedb-142">공급자는 표준 오류 스트림으로 내역할 선택적 로깅 수준을 나타내는 표시로 이 을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-142">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="0aedb-143">종료 코드</span><span class="sxs-lookup"><span data-stu-id="0aedb-143">Exit codes</span></span>

| <span data-ttu-id="0aedb-144">코드</span><span class="sxs-lookup"><span data-stu-id="0aedb-144">Code</span></span> |<span data-ttu-id="0aedb-145">결과</span><span class="sxs-lookup"><span data-stu-id="0aedb-145">Result</span></span> | <span data-ttu-id="0aedb-146">Description</span><span class="sxs-lookup"><span data-stu-id="0aedb-146">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="0aedb-147">0</span><span class="sxs-lookup"><span data-stu-id="0aedb-147">0</span></span> | <span data-ttu-id="0aedb-148">성공</span><span class="sxs-lookup"><span data-stu-id="0aedb-148">Success</span></span> | <span data-ttu-id="0aedb-149">자격 증명이 성공적으로 획득되었고 stdout에 기록되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-149">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="0aedb-150">1</span><span class="sxs-lookup"><span data-stu-id="0aedb-150">1</span></span> | <span data-ttu-id="0aedb-151">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="0aedb-151">ProviderNotApplicable</span></span> | <span data-ttu-id="0aedb-152">현재 공급자는 지정된 URI에 대한 자격 증명을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-152">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="0aedb-153">2</span><span class="sxs-lookup"><span data-stu-id="0aedb-153">2</span></span> | <span data-ttu-id="0aedb-154">실패</span><span class="sxs-lookup"><span data-stu-id="0aedb-154">Failure</span></span> | <span data-ttu-id="0aedb-155">공급자는 지정된 URI에 대한 올바른 공급자이지만 자격 증명을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-155">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="0aedb-156">이 경우 nuget.exe 인증을 다시 시도하지 않고 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-156">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="0aedb-157">일반적인 예는 사용자가 대화형 로그인을 취소하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-157">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="0aedb-158">표준 출력</span><span class="sxs-lookup"><span data-stu-id="0aedb-158">Standard output</span></span>

| <span data-ttu-id="0aedb-159">속성</span><span class="sxs-lookup"><span data-stu-id="0aedb-159">Property</span></span> |<span data-ttu-id="0aedb-160">참고</span><span class="sxs-lookup"><span data-stu-id="0aedb-160">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="0aedb-161">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="0aedb-161">Username</span></span> | <span data-ttu-id="0aedb-162">인증된 요청의 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-162">Username for authenticated requests.</span></span>|
| <span data-ttu-id="0aedb-163">암호</span><span class="sxs-lookup"><span data-stu-id="0aedb-163">Password</span></span> | <span data-ttu-id="0aedb-164">인증된 요청에 대한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-164">Password for authenticated requests.</span></span>|
| <span data-ttu-id="0aedb-165">메시지</span><span class="sxs-lookup"><span data-stu-id="0aedb-165">Message</span></span> | <span data-ttu-id="0aedb-166">응답에 대한 선택적 세부 정보로, 실패 사례에서 추가 세부 정보를 표시하는 데만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-166">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="0aedb-167">stdout 예제:</span><span class="sxs-lookup"><span data-stu-id="0aedb-167">Example stdout:</span></span>

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="0aedb-168">자격 증명 공급자 문제 해결</span><span class="sxs-lookup"><span data-stu-id="0aedb-168">Troubleshooting a credential provider</span></span>

<span data-ttu-id="0aedb-169">현재 NuGet은 사용자 지정 자격 증명 공급자 디버깅에 대한 직접적인 지원을 제공하지 않습니다. [문제 4598이](https://github.com/NuGet/Home/issues/4598) 이 작업을 추적하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-169">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="0aedb-170">다음 작업도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-170">You can also do the following:</span></span>

- <span data-ttu-id="0aedb-171">스위치로 nuget.exe `-verbosity` 실행하여 자세한 출력을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-171">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="0aedb-172">적절한 위치에 디버그 메시지를 에 `stdout` 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-172">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="0aedb-173">nuget.exe 3.3 이상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-173">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="0aedb-174">시작 시 이 코드 조각을 통해 디버거를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0aedb-174">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
