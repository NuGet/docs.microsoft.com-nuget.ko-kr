---
title: NuGet 4.9 RTM 릴리스 정보
description: NuGet 4.9에 대한 릴리스 정보(알려진 문제, 버그 수정, 새 기능 및 DCR 포함)
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453779"
---
# <a name="nuget-49-release-notes"></a>NuGet 4.9 릴리스 정보

[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)는 NuGet 4.9.0 기능과 함께 제공됩니다.


동일한 기능의 명령줄 버전도 사용 가능합니다.
* NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)
* dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-490"></a>요약: 4.9.0의 새로운 기능

* 서명: ClientPolicies를 사용하여 NuGet.Config에 나열된 신뢰할 수 있는 작성자 및 리포지토리 사용 요구 - [#6961](https://github.com/NuGet/Home/issues/6961)

* “.snupkg” 파일을 만들어 팩에 기호 포함 -- 기호 서버에 대해 snupkg 파일을 수락하는 nuget 프로토콜을 해석하기 위해 푸시 향상 - [#6878](https://github.com/NuGet/Home/issues/6878)

* NuGet 자격 증명 플러그 인 V2 - [#6642](https://github.com/NuGet/Home/issues/6642)

* 자체 포함된 NuGet 패키지 - 라이선스 - [#4628](https://github.com/NuGet/Home/issues/4628)

* PackageReference의 옵트인 “GeneratePathProperty” 메타데이터를 사용하여 “Foo.Bar\1.0” 디렉터리에 패키지별 MSBuild 속성 생성 - [#6949](https://github.com/NuGet/Home/issues/6949)

* NuGet 작업에서 고객 성공 개선 - [#7108](https://github.com/NuGet/Home/issues/7108)

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

* DCR - 서명:  NuGet 프로토콜 지원: RepositorySignatures/4.9.0 리소스 - [#7421](https://github.com/NuGet/Home/issues/7421)

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

## <a name="known-issues"></a>알려진 문제

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a>소스 이름에 공백이 포함되면 dotnet.exe/nuget.exe가 자격 증명을 사용하지 않음 - [#7517](https://github.com/NuGet/Home/issues/7517)

#### <a name="issue"></a>문제
소스 이름에 공백이 있으면 nuget.exe가 `The ' ' character, hexadecimal value 0x20, cannot be included in a name.` 같은 오류를 throw함

#### <a name="workaround"></a>해결 방법
소스 이름에 공백이 포함되지 않도록 변경합니다.

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>dotnet nuget 푸시 --interactive로 인해 Mac에서 오류가 발생합니다. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>문제
`--interactive` 인수가 dotnet CLI에 의해 전달되지 않고 오류가 발생함 `error: Missing value for option 'interactive'`

#### <a name="workaround"></a>해결 방법
`dotnet restore --interactive` 같은 대화형 옵션을 사용하여 다른 dotnet 명령을 실행하고 인증합니다. 인증은 자격 증명 공급자에 의해 캐시될 수 있습니다. 그런 다음, `dotnet nuget push`를 실행합니다.

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a>LicenseAcceptanceWindow 및 LicenseFileWindow 접근성 문제 - [#7452](https://github.com/NuGet/Home/issues/7452)

#### <a name="issue"></a>문제
화면 읽기 프로그램 및 JAWS를 사용한 내레이션 및 키보드 탐색과 관련해서 라이선스 동의 창 및 라이선스 파일 창에 접근성 문제가 있습니다.

#### <a name="workaround"></a>해결 방법
해결 방법이 없습니다.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>.NET Core SDK로 설치된 FallbackFolders의 패키지는 사용자 지정 설치되며 서명 유효성 검사에 실패합니다. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>문제
netcoreapp 1.x 및 netcoreapp 2.x 다중 대상을 지정하는 프로젝트를 복원하기 위해 dotnet.exe 2.x를 사용하면 대체 폴더가 파일 피드로 처리됩니다. 즉 복원할 때 NuGet이 대체 폴더에서 패키지를 선택하고 전역 패키지 폴더에 설치하려고 하며 일반적인 서명 유효성 검사를 수행하지만 실패합니다.

#### <a name="workaround"></a>해결 방법
`RestoreAdditionalProjectSources`를 nothing으로 설정하여 대체 폴더를 사용하지 않도록 설정합니다. `<RestoreAdditionalProjectSources/>` NuGet.org에서 많은 패키지가 다운로드되도록 하므로 주의하여 사용하세요. 그렇지 않으면 대체 폴더에서 복원될 패키지입니다.
