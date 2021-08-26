---
title: 보안 소프트웨어 공급망에 대한 모범 사례
description: NuGet 및 GitHub를 사용하여 소프트웨어 공급망을 보호하는 모범 사례입니다.
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: 4575d4779ed90150cec667489c85875b7fb87a8d
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726979"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>보안 소프트웨어 공급망에 대한 모범 사례

오픈 소스는 어디에나 있습니다. 많은 소유 코드베이스 및 커뮤니티 프로젝트에 있습니다. 조직 및 개인의 경우 질문은 오픈 소스 코드를 사용하고 있는지가 아니라 사용 중인 오픈 소스 코드가 무엇이고 얼마나 많이 사용하는지에 관한 것입니다.

소프트웨어 공급망이 어떻게 구성되는지 잘 모르는 경우 종속성 중 하나의 업스트림 취약성이 치명적일 수 있고, 이로 인해 개발자와 고객이 잠재적 손상에 취약해질 수 있습니다. 이 문서에서는 “소프트웨어 공급망”이라는 용어의 의미, 해당 용어의 중요성, 모범 사례를 사용하여 프로젝트의 공급망을 보호하는 방법을 자세히 살펴보겠습니다.

![The State of the Octoverse 2020 - 오픈 소스](media/opensource-percent.png)

## <a name="dependencies"></a>종속성 

소프트웨어 공급망이라는 용어는 소프트웨어에 들어가는 모든 항목과 소프트웨어가 제공되는 위치를 나타내는 데 사용됩니다. 소프트웨어 공급망이 의존하는 종속성 및 해당 종속성의 속성입니다. 종속성은 소프트웨어를 실행하는 데 필요한 항목입니다. 코드, 이진 또는 기타 구성 요소와 해당 항목이 생성되는 위치(예: 리포지토리 또는 패키지 관리자)일 수 있습니다.

여기에는 코드 작성자, 코드가 제공된 시간, 코드의 보안 문제가 검토된 방법, 알려진 취약성, 지원되는 버전, 라이선스 정보, 프로세스의 특정 시점에 코드를 사용한 거의 모든 것이 포함됩니다.

공급망은 빌드 및 패키징 스크립트나 애플리케이션에서 사용하는 인프라를 실행하는 소프트웨어와 같이 단일 애플리케이션을 넘어선 해당 스택의 다른 부분도 포함합니다.

## <a name="vulnerabilities"></a>취약점

오늘날 소프트웨어 종속성은 널리 사용되고 있습니다. 프로젝트에서 직접 작성할 필요가 없는 수백 개의 오픈 소스 종속성을 기능에 사용하는 것은 아주 흔한 일입니다. 즉, 대부분 애플리케이션이 직접 작성하지 않은 코드로 구성될 수 있습니다. 

![The State of the Octoverse 2020 - 종속성](media/dependencies.png)

타사 또는 오픈 소스 종속성의 가능한 취약성은 아마도 직접 작성하는 코드만큼 긴밀하게 제어할 수 없는 종속성이므로 공급망에서 잠재적 보안 위험을 초래할 수 있습니다.

관련 종속성 중 하나에 취약성이 포함되면 개발자도 취약성을 보유하게 될 수 있습니다. 종속성 중 하나가 개발자 모르게 변경될 수 있으므로 심각한 문제가 될 수 있습니다. 현재 취약성이 종속성에 포함되지만 악용되지 않더라도 나중에 악용될 수 있습니다. 

수천 명의 오픈 소스 개발자와 라이브러리 작성자의 작업을 이용할 수 있다는 것은 수천 명의 낯선 사람이 프로덕션 코드에 직접 효과적으로 관여할 수 있음을 의미합니다. 제품은 소프트웨어 공급망을 통해 패치가 적용되지 않은 취약성, 단순한 실수 또는 종속성에 대한 악의적인 공격에서도 영향을 받습니다.

## <a name="supply-chain-compromises"></a>공급망 손상

공급망의 일반적인 정의는 제조업에서 제공됩니다. 공급망은 어떤 것을 제조하고 공급하는 데 필요한 프로세스 체인입니다. 여기에는 계획, 자재 공급, 제조 및 소매가 포함됩니다. 소프트웨어 공급망은 자재 대신 코드라는 점을 제외하고 비슷합니다. 제조 대신 개발입니다. 땅에서 광석을 캐는 대신 공급자, 상용 또는 오픈 소스에서 코드를 제공하며 일반적으로 리포지토리에서 오픈 소스 코드를 제공합니다. 리포지토리의 코드를 추가하면 제품이 해당 코드의 종속성을 사용합니다.

소프트웨어 공급망 공격의 한 가지 예는 종속성의 공급망을 사용하여 희생자에게 코드를 배포하는 악성 코드가 의도적으로 종속성에 추가된 경우 발생합니다. 공급망 공격은 실제입니다. 악성 코드를 새 기여자로 직접 삽입하는 방법부터 다른 사람이 모르게 기여자의 계정을 탈취하거나 서명 키를 손상해 공식적으로 종속성의 일부가 아닌 소프트웨어를 배포하는 방법까지 공급망을 공격하는 다양한 방법이 있습니다.

소프트웨어 공급망 공격 자체는 거의 최종 목표가 아니며, 오히려 공격자가 맬웨어를 삽입하거나 나중에 액세스하기 위해 백도어를 제공할 기회의 시작입니다.

![The State of the Octoverse 2020 - 취약성 수명 주기](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>패치가 적용되지 않은 소프트웨어

현재 오픈 소스 사용은 주목할 만하며 곧 둔화할 것 같지는 않습니다. 오픈 소스 소프트웨어 사용을 중지하지 않을 경우 공급망 보안에 대한 위협은 패치가 적용되지 않은 소프트웨어입니다. 프로젝트의 종속성에 취약성이 포함되는 위험을 해결하려면 어떻게 해야 하나요?

- **환경을 구성하는 항목 파악.** 이를 위해 종속성 및 전이적 종속성을 검색하여 취약성 또는 라이선스 제한과 같은 해당 종속성의 위험을 파악해야 합니다.
- **종속성 관리.** 새 보안 취약성이 검색되면 영향을 받는지 여부를 확인하고, 영향을 받는 경우 사용 가능한 최신 버전 및 보안 패치로 업데이트해야 합니다. 새 종속성을 도입하는 변경 내용을 검토하거나 정기적으로 이전 종속성을 감사하는 경우 해당 작업이 특히 중요합니다.
- **공급망 모니터링.** 이를 위해 종속성을 관리하기 위해 적용하는 컨트롤을 감사합니다. 해당 방법으로 종속성에 맞게 더 제한적인 조건을 적용할 수 있습니다.

![The State of the Octoverse 2020 - 권장 사항](media/advisories.png)

현재 프로젝트 내부에서 잠재적 위험을 해결하는 데 사용할 수 있는 NuGet 및 GitHub에서 제공하는 다양한 도구 및 기술을 살펴보겠습니다. 

## <a name="knowing-what-is-in-your-environment"></a>환경을 구성하는 항목 파악

### <a name="nuget-dependency-graph"></a>NuGet 종속성 그래프

**📦 패키지 소비자**

각 프로젝트 파일을 직접 확인하여 프로젝트에서 NuGet 종속성을 확인할 수 있습니다.

해당 항목은 일반적으로 다음 두 위치 중 하나에 있습니다.

-   [`packages.config`](../reference/packages-config.md) – 프로젝트 루트에 있습니다.
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – 프로젝트 파일에 있습니다. 

NuGet 종속성을 관리하는 데 사용하는 방법에 따라 Visual Studio를 사용하여 [솔루션 탐색기](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer) 또는 [NuGet 패키지 관리자](../consume-packages/install-use-packages-visual-studio.md)에서 직접 종속성을 확인할 수도 있습니다.

CLI 환경의 경우 [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) 명령을 사용하여 프로젝트 또는 솔루션의 종속성을 나열할 수 있습니다. 

NuGet 종속성 관리에 관한 자세한 내용은 [다음 설명서를 참조](../consume-packages/overview-and-workflow.md)하세요.

### <a name="github-dependency-graph"></a>GitHub 종속성 그래프 

**📦 패키지 소비자 | 📦🖊 패키지 작성자**

GitHub의 종속성 그래프를 사용하여 프로젝트가 사용하는 패키지 및 프로젝트를 사용하는 리포지토리를 확인할 수 있습니다. 이를 통해 해당 종속성에서 검색된 취약성을 확인할 수 있습니다.

GitHub 리포지토리 종속성에 관한 자세한 내용은 [다음 설명서를 참조](https://github.co/dependency-graph)하세요.

### <a name="dependency-versions"></a>종속성 버전

**📦 패키지 소비자 | 📦🖊 패키지 작성자**

종속성의 보안 공급망을 보장하기 위해 모든 종속성 및 도구를 안정적인 최신 버전으로 정기적으로 업데이트하려고 합니다. 이렇게 하면 해당 종속성과 도구에는 알려진 취약성에 대한 최신 기능 및 보안 패치가 포함됩니다. 종속성에는 사용하는 코드, 소비하는 이진, 사용하는 도구 및 기타 구성 요소가 포함될 수 있습니다. 다음을 포함할 수 있습니다.

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [.NET SDK 및 런타임](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [NuGet 패키지](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>종속성 관리

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>NuGet 사용되지 않고 취약한 종속성

**📦 패키지 소비자 | 📦🖊 패키지 작성자**

[dotnet CLI](/dotnet/core/tools/dotnet-list-package)를 사용하여 프로젝트나 솔루션 내부에 있을 수 있는 사용되지 않거나 취약한 알려진 종속성을 모두 나열할 수 있습니다. `dotnet list package --deprecated` 또는 `dotnet list package --vulnerable` 명령을 사용하여 알려진 사용 중단 또는 취약성 목록을 제공할 수 있습니다.

### <a name="github-vulnerable-dependencies"></a>GitHub 취약한 종속성

**📦 패키지 소비자 | 📦🖊 패키지 작성자**

프로젝트가 GitHub에서 호스트되는 경우 [GitHub 보안](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors)을 이용하여 프로젝트에서 보안 취약성 및 오류를 찾을 수 있으며, Dependabot은 코드베이스에 대해 끌어오기 요청을 열어 이를 해결합니다. 

취약한 종속성이 도입되기 전에 해당 종속성을 포착하는 것은 [“시프트 레프트”](https://en.wikipedia.org/wiki/Shift-left_testing) 이동의 한 가지 목표입니다. 해당 라이선스, 전이적 종속성 및 종속성 기간 등 종속성에 관한 정보를 얻을 수 있으면 해당 작업을 수행하는 데 도움이 됩니다.

Dependabot 경고 및 보안 업데이트에 관한 자세한 내용은 [다음 설명서를 참조](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies)하세요.

### <a name="nuget-feeds"></a>NuGet 피드

**📦 패키지 소비자**

여러 퍼블릭 및 프라이빗 NuGet 소스 피드를 사용하는 경우 모든 피드에서 패키지를 다운로드할 수 있습니다. 빌드가 예측 가능하고 [종속성 혼동](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)과 같은 알려진 공격으로부터 보호되도록 하기 위해 패키지를 제공하는 특정 피드가 무엇인지 알고 있는 것이 가장 좋습니다. 보호를 위해 업스트림 기능이 있는 단일 피드 또는 프라이빗 피드를 사용할 수 있습니다.

패키지 피드를 보호하는 방법에 관한 자세한 내용은 [3 Ways to Mitigate Risk When Using Private Package Feeds](https://azure.microsoft.com/resources/3-ways-to-mitigate-risk-using-private-package-feeds/)를 참조하세요.

### <a name="client-trust-policies"></a>클라이언트 트러스트 정책

**📦 패키지 소비자**

서명하는 데 사용하는 패키지가 필요한 옵트인 가능한 정책이 있습니다. 이를 통해 작성자가 서명한 경우 패키지 작성자를 신뢰하거나 NuGet.org에서 서명한 리포지토리인 특정 사용자 또는 계정이 소유하는 경우 패키지를 신뢰할 수 있습니다.

클라이언트 트러스트 정책을 구성하려면 [다음 설명서를 참조](../consume-packages/installing-signed-packages.md)하세요.

### <a name="lock-files"></a>잠금 파일

**📦 패키지 소비자**

잠금 파일은 패키지 콘텐츠의 해시를 저장합니다. 설치하려는 패키지의 콘텐츠 해시가 잠금 파일과 일치하는 경우 패키지 반복성을 보장합니다.

잠금 파일을 사용하도록 설정하려면 [다음 설명서를 참조](../consume-packages/package-references-in-project-files.md#locking-dependencies)하세요.

## <a name="monitor-your-supply-chain"></a>공급망 모니터링

### <a name="github-secret-scanning"></a>GitHub 암호 검색

**📦🖊 패키지 작성자**

GitHub는 리포지토리에서 NuGet API 키를 검색하여 실수로 커밋된 비밀의 사기성이 있는 사용을 방지합니다. 

비밀 검색에 관한 자세한 내용은 [비밀 검색 정보](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning)를 참조하세요.

### <a name="author-package-signing"></a>작성자 패키지 서명

**📦🖊 패키지 작성자**

[작성자 서명](../reference/signed-packages-reference.md)을 사용하여 패키지 작성자는 패키지에서 해당 ID에 스탬프를 지정할 수 있고 소비자는 작성자가 해당 스탬프를 제공하는지 확인할 수 있습니다. 해당 서명은 콘텐츠 변조를 방지하며 패키지 출처 및 패키지 신뢰성에 관한 단일 데이터 소스로 사용됩니다. 클라이언트 트러스트 정책과 결합할 경우 특정 작성자가 패키지를 제공했는지 확인할 수 있습니다.

패키지에 작성자 서명하려면 [패키지 서명](../create-packages/sign-a-package.md)을 참조하세요.

### <a name="two-factor-authentication-2fa"></a>2FA(2단계 인증)

**📦🖊 패키지 작성자**

2FA(2단계 인증)를 사용하면 [GitHub 계정](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) 또는 [NuGet.org 퍼블릭 패키지 리포지토리에 로그인](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa)할 때 추가 보안 계층을 추가할 수 있습니다. 계정을 보호하려면 2단계 인증을 사용하는 것이 좋습니다.

### <a name="package-id-prefix-reservation"></a>패키지 ID 접두사 예약 

**📦🖊 패키지 작성자**

패키지 ID를 보호하려면 각 네임스페이스로 패키지 ID 접두사를 예약하여 패키지 ID 접두사가 [지정된 조건](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)에 제대로 해당하는 경우 일치하는 소유자를 연결할 수 있습니다. 

ID 접두사 예약에 관한 자세한 내용은 [패키지 ID 접두사 예약](../nuget-org/id-prefix-reservation.md)을 참조하세요.

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>취약한 패키지 사용 중단 및 나열 취소

**📦🖊 패키지 작성자**

작성한 패키지에서 취약성을 발견한 경우 .NET 패키지 에코시스템을 보호하려면 패키지를 검색하는 사용자에게 표시되지 않도록 패키지를 사용 중단하고 나열 취소하는 것이 좋습니다. 사용되지 않고 나열되지 않은 패키지를 사용하고 있는 경우에는 해당 패키지를 사용하지 않아야 합니다.

패키지를 사용 중단 및 나열 취소하는 방법에 관한 자세한 내용은 [패키지 사용 중단](../nuget-org/deprecate-packages.md) 및 [나열 취소](../nuget-org/policies/deleting-packages.md#unlisting-a-package)에 관한 다음 설명서를 참조하세요.

## <a name="summary"></a>요약

소프트웨어 공급망은 코드에 들어가거나 코드에 영향을 주는 어떤 것입니다. 공급망 손상이 실제적이고 확산하고 있더라도 해당 손상은 여전히 드문 현상입니다. 따라서 할 수 있는 가장 중요한 작업은 **종속성을 인식하고, 종속성을 관리하고**, **공급망을 모니터링** 하여 공급망을 보호하는 것입니다.

현재 공급망 확인, 관리 및 모니터링 시 더 효과적일 수 있고 NuGet 및 [GitHub](/learn/modules/maintain-secure-repository-github/)에서 제공하는 다양한 방법을 알아보았습니다.

전 세계 소프트웨어를 보호하는 방법에 관한 자세한 내용은 [The State of the Octoverse 2020 보안 보고서](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf)를 참조하세요.
