---
title: NuGet 4.9 RTM 릴리스 정보
description: NuGet 4.9에 대한 릴리스 정보(알려진 문제, 버그 수정, 새 기능 및 DCR 포함)
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 99578c5ed7e88b7269872bf88c465bbda462870a
ms.sourcegitcommit: 585394f063e95dcbc24d7ac0ce07de643eaf6f4d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55045110"
---
# <a name="nuget-49-release-notes"></a>NuGet 4.9 릴리스 정보

NuGet 배포 차량:

| NuGet 버전 | Visual Studio 버전에서 사용 가능| .NET SDK에서 사용 가능|
|:---|:---|:---|
| [**4.9.0**](https://nuget.org/downloads) | [Visual Studio 2017 버전 15.9.0](https://visualstudio.microsoft.com/downloads/) | [2.1.500, 2.2.100](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.1**](https://nuget.org/downloads) | N/A | N/A |
| [**4.9.2**](https://nuget.org/downloads) |[Visual Studio 2017 버전 15.9.4](https://visualstudio.microsoft.com/downloads/) | [2.1.502, 2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.3**](https://nuget.org/downloads) |[Visual Studio 2017 버전 15.9.6](https://visualstudio.microsoft.com/downloads/) | N/A |


## <a name="summary-whats-new-in-490"></a>요약: 4.9.0의 새로운 기능

* 서명: ClientPolicies를 사용하여 NuGet.Config에 나열된 신뢰할 수 있는 작성자 및 리포지토리 사용 요구 - [#6961](https://github.com/NuGet/Home/issues/6961), [블로그 게시물](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)

* “.snupkg” 파일을 만들어 팩에 기호 포함 -- 기호 서버에 대해 snupkg 파일을 수락하는 nuget 프로토콜을 해석하기 위해 푸시 향상 - [#6878](https://github.com/NuGet/Home/issues/6878), [블로그 게시물](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)

* NuGet 자격 증명 플러그 인 V2 - [#6642](https://github.com/NuGet/Home/issues/6642)

* 자체 포함 NuGet 패키지 - 라이선스 - [#4628](https://github.com/NuGet/Home/issues/4628), [공지](https://github.com/NuGet/Announcements/issues/32)

* PackageReference의 옵트인 “GeneratePathProperty” 메타데이터를 사용하여 “Foo.Bar\1.0\" 디렉터리에 패키지별 MSBuild 속성 생성 - [#6949](https://github.com/NuGet/Home/issues/6949)

* NuGet 작업에서 고객 성공 개선 - [#7108](https://github.com/NuGet/Home/issues/7108)

* 잠금 파일을 사용한 반복 가능한 패키지 복원 사용 - [#5602](https://github.com/NuGet/Home/issues/5602), [공지](https://github.com/NuGet/Announcements/issues/28), [블로그 게시물](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

* PackageExtraction에 의해 발생한 오류로 승격된 경고(WarnAsErrors를 통해)가 추출된 패키지를 그대로 두지 않아야 함 - [#7445](https://github.com/NuGet/Home/issues/7445)

* 잘못 서명된 패키지가 전역 패키지 폴더에 있으면 안 됨 - [#7423](https://github.com/NuGet/Home/issues/7423)

* 바인딩 리디렉션 생성이 외관 어셈블리를 건너뛰지 않아야 함 - [#7393](https://github.com/NuGet/Home/issues/7393)

* VersionRange Equals가 부동 범위를 비교하지 않음 - [#7324](https://github.com/NuGet/Home/issues/7324)

* 복원: 새 .NET Core 2.1 HTTP 스택을 사용하여 성능 저하 - [#7314](https://github.com/NuGet/Home/issues/7314)

* 패키지 업데이트가 PackageReference의 PrivateAssets를 수정하지 않아야 함 - [#7285](https://github.com/NuGet/Home/issues/7285)

* 서명:  패키지에 항목이 너무 많은 경우(65534개 이상) 서명에 실패함 - [#7248](https://github.com/NuGet/Home/issues/7248)

* “dotnet nuget push” 코드 경로가 새 자격 증명 공급자를 지원해야 함 - [#7233](https://github.com/NuGet/Home/issues/7233)

* 고정 문화권에서 플러그 인 실행 지원(docker에서 발생) - [#7223](https://github.com/NuGet/Home/issues/7223)

* nuget 소스가 NuGet.config의 자격 증명을 삭제하지 않아야 함 - [#7200](https://github.com/NuGet/Home/issues/7200)

* devDependency PackageReference 설치가 excludeassets=compile로 기본 설정되어야 함 - [#7084](https://github.com/NuGet/Home/issues/7084)

* 마이그레이터 옵션이 모든 프로젝트에 대해 표시되도록 수정하고, 프로젝트가 호환되지 않는 경우 오류 표시 - [#6958](https://github.com/NuGet/Home/issues/6958)

* “dotnet add package”가 자산 파일에 수행하는 복원을 커밋해야 함 - [#6928](https://github.com/NuGet/Home/issues/6928)

* 서명:  서명 관련 오류 메시지 개선 - [#6906](https://github.com/NuGet/Home/issues/6906)

* [테스트 실패][zh-TW]“Package Manager Console” 문자열이 패키지 관리자 콘솔에서 지역화되지 않음  - [#6381](https://github.com/NuGet/Home/issues/6381)

* “프로젝트 정보를 찾을 수 없음” 오류 메시지가 VS 내에서 좀 더 구체적이어야 함 - [#5350](https://github.com/NuGet/Home/issues/5350)

* nuget 팩의 nuspec 버전 태그를 잘못 사용하면 도움이 되지 않는 오류 메시지가 표시됨 - [#2714](https://github.com/NuGet/Home/issues/2714)

* DCR - 서명: NuGet 프로토콜 지원: RepositorySignatures/4.9.0 리소스 - [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR - 패키지 추출 중 이제 .nupkg.metadata 파일이 생성됨 - “content-hash” 포함 - [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR - Mono에서 실행 중 플러그 인에 대한 authenticode 확인을 건너뜀 - [#7222](https://github.com/NuGet/Home/issues/7222)

[이 릴리스 4.9.0에서 수정된 모든 문제 목록](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>요약: 4.9.1의 새로운 기능

* 새 명령 trusted-signers를 통해 nuget.config에 쓰기 읽기에 대한 지원 추가 - [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

* 라이선스 링크 생성 수정 - [#7515](https://github.com/NuGet/Home/issues/7515)

* 서명 유효성 검사의 오류 코드 재발 - [#7492](https://github.com/NuGet/Home/issues/7492)

* NuGet.Build.Tasks.Pack 패키지에 라이선스 정보가 없음 - [#7379](https://github.com/NuGet/Home/issues/7379)

[이 릴리스 4.9.1에서 수정된 모든 문제 목록](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>요약: 4.9.2의 새로운 기능

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

* 원본 이름에 공백이 포함되면 VS/dotnet.exe/nuget.exe/msbuild.exe 복원에서 자격 증명을 사용하지 않음 - [#7517](https://github.com/NuGet/Home/issues/7517)

* LicenseAcceptanceWindow 및 LicenseFileWindow 접근성 문제 - [#7452](https://github.com/NuGet/Home/issues/7452)

* DateTimeConverter에서 DateTime.Parse의 FormatException 수정 - [#7539](https://github.com/NuGet/Home/issues/7539)

[이 릴리스 4.9.2에서 수정된 모든 문제 목록](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a>요약: 4.9.3의 새로운 기능

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a>“잠금 파일을 사용한 반복 가능한 패키지 복원” 문제

* 이전에 캐시된 패키지의 해시가 잘못 계산되어 잠긴 모드가 작동하지 않음 - [#7682](https://github.com/NuGet/Home/issues/7682)

* 복원이 `packages.lock.json` 파일에 정의된 것과 다른 버전으로 확인됨 - [#7667](https://github.com/NuGet/Home/issues/7667)

* ProjectReferences가 관련된 경우 ‘--locked-mode / RestoreLockedMode’로 인해 의사 복원 실패 발생 - [#7646](https://github.com/NuGet/Home/issues/7646)

* MSBuild SDK 확인자에서 packages.lock.json을 사용할 때 복원에 실패하는 SDK 패키지용 SHA의 유효성을 검사하려고 함 - [#7599](https://github.com/NuGet/Home/issues/7599)

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a>“구성 가능한 트러스트 정책을 사용하여 종속성 잠금” 문제
* 서명된 패키지가 지원되지 않는 동안에는 dotnet.exe에서 신뢰할 수 있는 서명자를 평가하지 않아야 함 - [#7574](https://github.com/NuGet/Home/issues/7574)

* 구성 파일의 trustedSigners 순서가 신뢰 평가에 영향을 줌 - [#7572](https://github.com/NuGet/Home/issues/7572)

* ISettings를 구현할 수 없음[트러스트 정책 기능을 지원하도록 설정 API 리팩터링으로 인해 발생] - [#7614](https://github.com/NuGet/Home/issues/7614)

#### <a name="improved-debugging-experience-issues"></a>“향상된 디버깅 환경” 문제

* .NET Core 전역 도구용 기호 패키지를 게시할 수 없음 - [#7632](https://github.com/NuGet/Home/issues/7632)

#### <a name="self-contained-nuget-packages---license-issues"></a>“자체 포함된 NuGet 패키지 - 라이선스” 문제

* 포함된 라이선스 파일을 사용할 때 기호 .snupkg 패키지를 빌드하는 중 오류 발생 - [#7591](https://github.com/NuGet/Home/issues/7591)

[이 릴리스 4.9.3에서 수정된 모든 문제 목록](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")
## <a name="known-issues"></a>알려진 문제

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>dotnet nuget 푸시 --interactive로 인해 Mac에서 오류가 발생합니다. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>문제
`--interactive` 인수가 dotnet CLI에 의해 전달되지 않고 오류가 발생함 `error: Missing value for option 'interactive'`

#### <a name="workaround"></a>해결 방법
`dotnet restore --interactive` 같은 대화형 옵션을 사용하여 다른 dotnet 명령을 실행하고 인증합니다. 인증은 자격 증명 공급자에 의해 캐시될 수 있습니다. 그런 다음, `dotnet nuget push`를 실행합니다.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>.NET Core SDK로 설치된 FallbackFolders의 패키지는 사용자 지정 설치되며 서명 유효성 검사에 실패합니다. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>문제
netcoreapp 1.x 및 netcoreapp 2.x 다중 대상을 지정하는 프로젝트를 복원하기 위해 dotnet.exe 2.x를 사용하면 대체 폴더가 파일 피드로 처리됩니다. 즉 복원할 때 NuGet이 대체 폴더에서 패키지를 선택하고 전역 패키지 폴더에 설치하려고 하며 일반적인 서명 유효성 검사를 수행하지만 실패합니다.

#### <a name="workaround"></a>해결 방법
`RestoreAdditionalProjectSources`를 nothing으로 설정하여 대체 폴더를 사용하지 않도록 설정합니다. `<RestoreAdditionalProjectSources/>` NuGet.org에서 많은 패키지가 다운로드되도록 하므로 주의하여 사용하세요. 그렇지 않으면 대체 폴더에서 복원될 패키지입니다.
