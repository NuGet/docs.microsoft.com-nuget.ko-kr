---
title: NuGet.org 질문과 대답
description: NuGet 갤러리 작업에 대한 일반적인 질문과 대답.
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 1b373f245e934f2447acec2f97472d69999ae679
ms.sourcegitcommit: 7c9f157ba02d9be543de34ab06813ab1ec10192a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999954"
---
# <a name="nugetorg-frequently-asked-questions"></a>NuGet.org 질문과 대답

## <a name="license-terms"></a>사용 조건

**패키지에서 특정 라이선스 정보를 제공하지 않는 경우 기본 사용 조건은 무엇인가요?**

각 패키지는 패키지에 포함된 사용 조건이 적용됩니다. 패키지를 액세스, 다운로드 또는 획득하기 전에 해당 사용 조건을 검토해야 합니다. NuGet.org의 패키지 페이지에 있는 **라이선스 정보** 링크를 사용합니다.

패키지에서 사용 조건을 지정하지 않은 경우 NuGet.org 패키지 페이지의 **연락처 소유자** 링크를 사용하여 패키지 소유자에게 직접 문의해 보세요. Microsoft는 타사 패키지 공급자로부터 사용자에게 지적 재산권을 부여하지 않으며 타사에서 제공한 정보에 대해 책임을 지지 않습니다.

## <a name="managing-packages-on-nugetorg"></a>NuGet.org의 패키지 관리

**패키지 메타데이터를 업로드한 후에 편집할 수 있나요?**

NuGet은 모든 패키지에 서명을 권장합니다. 패키지 서명의 디자인 원칙은 nuspec을 포함한 서명된 패키지 콘텐츠를 변경할 수 없다는 것입니다. 패키지 메타데이터를 편집하면 nuspec이 변경되고 기존 서명이 무효화됩니다. 패키지를 만든 후에 패키지 메타데이터를 편집할 필요가 없도록 기존 워크플로를 수정하는 것이 좋습니다.

패키지에 대해 나열된 종속성은 패키지 자체에서 자동으로 생성되며 편집할 수 없습니다.

또한 [int.nugettest.org](https://int.nugettest.org)에 패키지를 업로드하는 것은 공용 갤러리에서 패키지를 사용하지 않고도 패키지를 테스트하고 유효성을 검사할 수 있는 좋은 방법입니다. API 엔드포인트: https://apiint.nugettest.org/v3/index.json

**NuGet.org에 게시된 패키지를 삭제할 수 있나요?**

일반적으로 NuGet.org에 게시된 패키지 삭제를 지원하지 않습니다. [패키지 삭제에 대한 정책](policies/deleting-packages.md)에 대해 자세히 알아보세요.

**나중에 게시되는 패키지의 이름을 예약할 수 있나요?**

예. 계정에 대한 패키지 ID 접두사를 요청하여 [NuGet.org](https://www.nuget.org/)에서 패키지 ID를 예약할 수 있습니다. 패키지 ID 접두사를 요청하려면 [설명서](id-prefix-reservation.md)의 지침을 따르세요.

**패키지 소유권을 주장하려면 어떻게 할까요?**

[NuGet.org에서 패키지 소유자 관리](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg)를 참조하세요.

**소프트웨어 라이선스를 위반하는 패키지 소유자를 처리하려면 어떻게 할까요?**

NuGet 커뮤니티에서 패키지 소유자와 다른 소프트웨어 소유자 간에 발생할 수 있는 분쟁을 해결하기 위해 함께 노력하는 것이 좋습니다. NuGet.org 관리자에게 중재를 요청하기 전에 따라야 할 [분쟁 해결 절차](policies/dispute-resolution.md)가 마련되어 있습니다.

**내 테스트 패키지를 NuGet.org에 업로드하는 것이 좋을까요?**

테스트를 위해 [int.nugettest.org](https://int.nugettest.org) 또는 대체 공용 NuGet 서버(예: [myget.org](https://myget.org) 또는 [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/))를 사용할 수 있습니다.

int.nugettest.org에 업로드된 패키지는 유지되지 않을 수 있습니다.

**NuGet.org에 업로드할 수 있는 패키지의 최대 크기는 무엇인가요?**

NuGet.org는 최대 250MB의 패키지를 허용하지만, 가능한 한 패키지를 1MB 미만으로 유지하고 종속성을 사용하여 패키지를 함께 연결하는 것이 좋습니다. 경험상 패키지는 충돌을 방지하기 위해 하나의 어셈블리만 포함합니다.

NuGet은 HTTP를 사용하여 패키지를 다운로드하므로, 큰 패키지는 작은 패키지보다 설치에 실패할 가능성이 높습니다.

여러 패키지 간에 종속성을 공유하여 NuGet 패키지의 소비자에 대한 전체 다운로드 크기를 줄일 수 있습니다.

종속성은 대부분 정적이며 변경되지 않습니다. 코드에서 버그를 수정하는 경우 종속성을 업데이트할 필요가 없을 수도 있습니다. 종속성을 번들로 제공하면 매번 더 큰 패키지를 다시 전달하게 됩니다. NuGet 패키지를 관련 종속성으로 분할하면 패키지 소비자가 훨씬 더 세부적으로 업그레이드할 수 있습니다.

## <a name="nugetorg-not-accessible"></a>NuGet.org에 액세스할 수 없음

**NuGet.org에서 패키지를 다운로드하거나 업로드할 수 없는 이유는 무엇인가요?**

먼저 최신 버전의 NuGet을 사용하고 있는지 확인합니다. 해당 버전이 계속 실패하면 [지원 부서에 문의](https://www.nuget.org/policies/Contact)하여 다음을 포함한 추가 연결 문제 해결 정보를 제공합니다.

- 사용 중인 NuGet 버전
- 사용 중인 패키지 원본
- 자세한 세부 정보가 있는 복원 로그
- MTR 또는 Fiddler 추적(아래 참조)
- 사용자의 지리적 지역
- 머신이 프록시 또는 방화벽 뒤에 있는지 여부는?
- 머신이 클라우드 공급 기업의 데이터 센터(Azure, AWS 등)에 위치해 있나요? 그렇다면 공급 기업 및 지역의 이름을 제공하세요.

*MTR을 캡처하려면:*

- [http://winmtr.net/download/](http://winmtr.net/)에서 WinMTR 다운로드
- 호스트 이름으로 `api.nuget.org`를 입력하고 **시작**을 클릭합니다.
- **보냄** 열이 100개 이상이 될 때까지 기다립니다.

    ![캡처 중인 MTR](media/mtr.png)

- 클립보드에 텍스트를 복사합니다.

*Fiddler를 캡처하려면:*

- 최신 버전의 [Fiddler](http://www.telerik.com/download/fiddler)를 설치합니다.
- Fiddler를 시작하고 **파일 > 트래픽 캡처** 메뉴를 사용하여 트래픽 캡처를 사용하지 않도록 설정합니다.
- 모든 세션을 제거합니다(목록에서 모든 항목을 선택하고 **삭제** 키를 누름).
- **도구 > Fiddler 옵션...** 메뉴의 **HTTPS** 탭에서 **HTTPS 트래픽 해독**을 선택하여 HTTPS 트래픽을 캡처하도록 Fiddler를 구성합니다.
- Visual Studio를 닫습니다.
- **파일 > 트래픽 캡처** 메뉴를 활성화합니다.
- Visual Studio 또는 nuget.exe .exe를 시작하고 작동하지 않는 작업을 수행합니다. 이러한 작업으로 생성된 트래픽이 Fiddler에 표시됩니다.
- 작업이 실행되면 **파일 > 저장 > 모든 세션**을 사용하여 캡처된 세션을 저장합니다.

참고: Fiddler를 통해 NuGet 트래픽을 라우팅하기 위해 `HTTP_PROXY` 환경 변수를 `http://127.0.0.1:8888`로 설정해야 할 수도 있습니다.

실패하면 [StackOverflow 게시물에서 언급한 팁](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall)을 사용해 보세요.

## <a name="nugetorg-account-management"></a>NuGet.org 계정 관리

### <a name="how-to-recover-nugetorg-password-login"></a>NuGet.org 암호 로그인을 복구하려면 어떻게 하나요?

[NuGet.org 암호 로그인이 지원되지 않습니다](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html). NuGet.org에 로그인하는 유일한 방법은 개인 MSA(Microsoft 계정) 또는 AAD(Azure Active Directory) 계정을 사용하는 것입니다. 그러나 연결된 MSA/AAD 계정에 액세스할 수 없는 경우 NuGet.org 계정을 복구하려면 암호 로그인을 사용해야 합니다. 이 경우 다음 단계를 따릅니다.
- **요구 사항:** 암호를 복구해야 하는 계정과 연결된 이메일에 대한 액세스 권한이 있어야 합니다.
- [암호 찾기 페이지](https://www.nuget.org/account/ForgotPassword)로 이동합니다.
- 복구하려는 NuGet.org 계정과 연결된 **전자 메일** 주소를 입력합니다.
- **보내기** 단추를 클릭합니다.
- 암호를 재설정하는 링크를 사용하여 지정된 이메일 주소 계정으로 이메일을 받을 수 있습니다. 이 링크를 클릭하고 새 암호를 설정합니다. 메일을 찾을 수 없으면 "스팸" 폴더를 확인합니다.
- 완료되면 NuGet에서 사용자 이름/암호로 로그인할 수 있습니다.
- 사용자 이름/암호로 로그인하려면 [NuGet.org 로그인 페이지](https://www.nuget.org/users/account/LogOn)에서 **Nuget.org 계정을 통해 로그인** 링크를 사용합니다.

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>어떤 Microsoft 계정이 내 NuGet.org 계정에 연결되어 있나요?

NuGet.org 계정과 연결된 Microsoft 계정을 잊어버린 경우 아래 단계를 따르면 지원을 받을 수 있습니다.
1. [NuGet.org 로그인 페이지](https://www.nuget.org/users/account/LogOn)로 이동하여 **로그인하는 데 도움이 필요하나요?** 링크를 클릭합니다.
1. 그러면 지원에 대한 팝업 대화 상자가 표시됩니다. NuGet.org 계정에 대해 연결된 Microsoft 계정을 파악하려면 이 대화 상자의 단계를 따릅니다.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>NuGet.org 로그인에 사용된 Microsoft 계정을 변경하려면 어떻게 하나요?
NuGet.org 사용자에 대한 Microsoft 계정을 변경하려는 경우 다음 단계를 따릅니다. `account1@outlook.com` 전자 메일을 사용한 Microsoft 계정이 사용자 이름을 사용한 NuGet.org 계정 `MyNuGetAccount`와 연결되어 있다고 가정합니다. `account2@outlook.com` 이메일을 사용하여 다른 Microsoft 계정으로 로그인을 변경하려면
1. **Microsoft로 로그인**을 클릭한 후 [로그인 페이지](https://www.nuget.org/users/account/LogOn)에서 **현재 연결된 Microsoft 계정** 즉, `account1@outlook.com`을 사용하여 로그인하세요.
1. 로그인하면 [계정 설정](https://www.nuget.org/account) 페이지로 이동합니다.
1. **로그인 계정**의 섹션을 확장합니다. **계정 변경** 단추를 클릭합니다.
1. 이제 Microsoft 로그인 페이지로 리디렉션됩니다. 연결을 `account2@outlook.com`으로 변경하려는 계정을 사용하여 로그인하세요. **참고**: 다른 Microsoft 계정으로 로그인할 수 있으려면 로그인 흐름 중에 **다른 계정으로 로그인 및 로그아웃**을 클릭해야 할 수 있습니다.
1. 아래와 같은 오류가 표시되는 경우 자세한 내용은 [Microsoft 계정이 다른 NuGet.org 계정과 연결되어 있습니다](#microsoft-account-is-linked-with-another-nugetorg-account)를 참조하세요.
    >_'account2 <account2@outlook.com>'을 사용하여 Microsoft 계정을 업데이트하지 못했습니다. 다른 NuGet 계정에 이미 연결되어 있는 경우 이런 오류가 발생할 수 있습니다. 자세한 내용은 고객 지원팀에 문의하세요._

1. 두 번째 계정으로 로그인에 성공했으면 NuGet.org 계정 설정 페이지로 다시 리디렉션되고 이제 로그인 계정으로 연결된 새 Microsoft 계정이 표시되어야 합니다. 앞으로는 NuGet.org에 로그인할 때 이 계정을 사용해야 합니다.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Microsoft 계정이 다른 NuGet.org 계정에 연결되어 있습니다.

Microsoft 로그인을 변경했는데 아래 오류가 나타난 경우:
> _'account2 <account2@outlook.com>'을 사용하여 Microsoft 계정을 업데이트하지 못했습니다. 다른 NuGet 계정에 이미 연결되어 있는 경우 이런 오류가 발생할 수 있습니다. 자세한 내용은 고객 지원팀에 문의하세요._

Microsoft 계정 로그인을 `MyNuGetAccount1` 사용자 이름을 사용한 NuGet.org 사용자에 대한 `account1@outlook.com`에서 `account2@outlook.com` 전자 메일을 사용한 다른 Microsoft 계정으로 변경했다고 가정합니다. 그러면 위의 오류가 발생합니다.

**위의 오류가 의미하는 것은 무엇인가요?**

위의 예제에서 `MyNuGetAccount2` 사용자 이름을 사용한 다른 NuGet.org 계정과 연결된 `<account2@outlook.com>` 전자 메일을 사용하는 Microsoft 계정으로 변경하려는 Microsoft 계정과 연결된 다른 NuGet.org 계정이 있다는 의미입니다.

다른 NuGet.org 계정에 연결된 Microsoft 계정과 연결된 로그인을 변경할 수 없습니다.

**다른 NuGet.org 계정이 있다는 것을 잊은 경우 NuGet.org 계정을 확인하려면 어떻게 하나요?**

[로그인 페이지](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "로그인 페이지")에서 두 번째 Microsoft 계정으로 로그인합니다. 그러면 현재 두 번째 Microsoft 계정과 연결된 NuGet.org 계정에 로그인할 수 있습니다. 그런 다음, 업로드된 패키지를 확인하고 이 계정에서 계정 관리를 수행할 수 있습니다.

**이 두 번째 NuGet.org 계정에 대해 신경 쓰지 않고, 첫 번째 NuGet.org 계정에 대한 내 로그인을 두 번째 Microsoft 계정으로 변경하려고 합니다. 어떻게 해야 하나요?**

두 번째 NuGet.org 계정에 대해 신경 쓰지 않으면서 `account2@outlook.com` 전자 메일과 연결된 Microsoft 계정을 다시 사용하려는 경우에 해당합니다. 

NuGet.org 계정을 삭제하여 Microsoft 계정 및 NuGet.org 계정 간 연결을 해제할 수 있습니다.
1. 이 단계에 따라 `MyNuGetAccount2` 두 번째 NuGet.org 계정의 [사용자를 삭제](#how-to-delete-my-nugetorg-account)합니다. 
1. 이 계정이 삭제되면 이 단계를 다시 시도하여 [Microsoft 계정 로그인을 변경](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login)할 수 있습니다.

**잠깐. 이 두 번째 계정에도 관심이 있습니다. 이 계정은 손실되지만 첫 번째 계정에 대한 내 연결된 계정 로그인을 변경하지 않겠습니다.**

`account3@outlook.com` 이메일을 사용한 세 번째 Microsoft 계정을 만들어야/사용해야 합니다. 
1. 먼저 NuGet.org에서 `account2@outlook.com`을 사용하는 두 번째 Microsoft 계정으로 로그인해야 합니다. 위의 단계에 따라 연결된 로그인을 변경하고 이 NuGet.org 계정과 세 번째 Microsoft 계정을 연결합니다.
1. 완료되면 `account2@outlook.com` 전자 메일을 사용한 두 번째 Microsoft 계정은 자유롭게 `MyNuGetAccount1` 첫 번째 NuGet.org 계정에 연결될 수 있습니다. 위의 동일한 단계에 따라 두 번째 Microsoft 계정에 대한 Microsoft 로그인을 변경합니다.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Microsoft 계정으로 로그인하면 내 이메일이 다른 Microsoft 계정에 연결됐는지 표시됨

`account1@outlook.com` 이메일을 사용한 Microsoft 계정으로 로그인을 시도했는데 아래와 같은 오류가 발생한 경우:
> _'account1@outlook.com' 이메일을 사용한 계정이 다른 Microsoft 계정에 연결돼 있습니다._
>
> _연결된 Microsoft 계정을 업데이트하려는 경우 계정 설정 페이지에서 업데이트할 수 있습니다._

**위의 오류가 의미하는 것은 무엇인가요?**

NuGet.org에서 계정을 만드는 경우 해당 계정과 연결된 통신 전자 메일 주소가 있습니다. 일반적으로 이 주소는 연결된 Microsoft 계정에 사용되는 이메일 주소와 동일합니다. 그러나 통신용으로 다른 이메일 주소를 지정하는 것은 선택할 수 있습니다. 따라서 기술적으로 다른 Microsoft 계정 즉, 통신 전자 메일 주소로 `account1@outlook.com`을 사용하여 NuGet.org 계정에 연결하는 `account2@outlook.com`이 있을 수 있습니다.

위의 오류는 `account1@outlook.com` 통신 전자 메일 주소를 사용하는 NuGet.org 계정이 이미 있지만 `account1@outlook.com`이 **아닌** 전자 메일을 사용하여 다른 Microsoft 계정과 연결되어 있다는 것을 의미합니다.

**이 NuGet.org 계정에 어떤 Microsoft 계정이 연결되어 있는지 알려면 어떻게 하나요?**

`account1@outlook.com` 전자 메일 주소를 사용한 NuGet.org 계정에 어떤 Microsoft 계정이 연결돼 있는지 파악하려면 [로그인 지원](#which-microsoft-account-is-linked-to-my-nugetorg-account) 흐름을 사용해야 합니다.

**해당 계정을 내 Microsoft 계정으로 재정의하려 함**

기존 NuGet.org 계정을 사용하여 Microsoft 계정과 연결하려면 [Microsoft 로그인을 사용할 수 없는 경우 내 NuGet.org 계정을 복구하려면 어떻게 하나요?](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) 섹션의 단계를 따릅니다.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Microsoft 로그인을 사용할 수 없는 경우 내 NuGet.org 계정을 복구하려면 어떻게 하나요?

[로그인 지원](#which-microsoft-account-is-linked-to-my-nugetorg-account)을 사용하려는데 NuGet.org 계정과 연결된 Microsoft 계정에 액세스할 수 없는 경우 NuGet.org 계정에 새 Microsoft 계정을 연결하려면 다음 단계를 따르세요.
1. **요구 사항**: 기존의 모든 NuGet.org 계정과 연결되지 않은 Microsoft 계정에 액세스해야 합니다. 없는 경우 계정을 [만들](https://signup.live.com) 수 있습니다.
2. NuGet.org 계정의 사용자 이름 및 암호를 잊은 경우 [암호 로그인을 복구하는 단계](#how-to-recover-nugetorg-password-login)를 수행하세요.
3. 사용자 이름/암호 로그인을 사용하여 [NuGet.org에 로그인](https://www.nuget.org/users/account/LogOnNuGetAccount)합니다.
4. 로그인하면 아래와 같은 팝업 대화 상자가 표시됩니다. 이 대화 상자는 암호 중지 대화 상자입니다.
5. **참고**: 지정된 Microsoft 계정으로 로그인하라는 지침을 무시하세요. 이제 기타 모든 Microsoft 로그인에 NuGet.org 계정을 연결할 수 있습니다.
6. 1단계에서 설명한 것처럼 **Microsoft로 로그인** 단추를 클릭하고 액세스 권한이 있는 Microsoft 계정으로 로그인합니다.
7. 이제 사용자 계정은 앞으로 NuGet.org에 로그인하는 데 사용할 수 있는 새 Microsoft 계정에 연결됩니다.

    ![MSA 연결 대화 상자](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>내 NuGet.org 계정을 조직 계정으로 변환하려면 어떻게 하나요?

사용자 계정을 조직 계정으로 변환하려는 경우 이 계정이 이미 Microsoft 계정 로그인과 연결되어 있으면 [nuget.org의 조직](organizations-on-nuget-org.md)에 대한 설명서에 표시된 단계를 따릅니다.

그러나 NuGet.org 계정이 Microsoft 계정과 연결되어 있지 않은 경우 이 계정을 조직 계정으로 변환하려면 다음 단계를 따르면 됩니다.
1. **요구 사항**: 조직 계정의 관리자로 사용할 NuGet.org에서 처음 만든 개별 계정이 있어야 합니다. 없으면 [새 NuGet.org 계정을 만듭니다](individual-accounts.md).
2. NuGet.org 계정에 대한 암호 로그인이 없는 경우 해당 계정에 대한 [암호 로그인 복구 단계](#how-to-recover-nugetorg-password-login)를 따릅니다. 그러나 있는 경우 이 단계를 건너뜁니다.
3. 사용자 이름/암호 로그인을 사용하여 [NuGet.org에 로그인](https://www.nuget.org/users/account/LogOnNuGetAccount)합니다.
4. 로그인하면 아래와 같은 팝업 대화 상자가 표시됩니다. 이 대화 상자는 암호 중지 대화 상자입니다. 
    > [!Important]
    > 이 대화 상자를 무시하고 **Microsoft로 로그인** 단추를 클릭하지 **마세요**.

5. [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform)으로 이동합니다. 그러면 Microsoft 계정에 연결하지 않고서 NuGet.org 계정을 조직 계정으로 변환할 수 있습니다.
6. 개인 NuGet.org 계정/1단계에서 만든 계정에 관리 사용자 이름을 지정합니다.
7. 조직 계정으로 이 계정의 변환을 완료하려면 지침을 따릅니다.

    ![MSA 연결 대화 상자](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>관리되지 않는 테넌트가 있는 AAD 계정에서 NuGet.org 로그인 문제가 발생하면 어떻게 하나요?

전자 메일 계정 도메인(@yourdomain.com)으로 로그인 흐름 도중 아래와 같은 오류가 표시되는 경우 NuGet.org 계정을 복구하려면 다음 단계를 참조하세요.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**로그인 도중 이 관리되지 않는 상태란? 이런 일이 일어나는 이유는 무엇인가요?** 

사용자 계정이 이전에 개인 Microsoft 계정으로 등록된 것으로 보이고 문제 없이 작동했지만, 지금은 해당 계정이 Azure Active Directory에 "관리되지 않는" 테넌트로 등록된 것으로 보입니다(Microsoft 계정을 인증하는 데 사용하는 ID 서비스). 

@yourdomain.com 이메일 주소를 사용하는 조직의 누군가 또는 사용자가 AAD 통합 서비스에 등록했거나, [Azure Active Directory에 셀프 서비스 등록](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup)하여 사용한 Microsoft 계정 도메인에 이러한 "관리되지 않는" 테넌트를 만든 경우 이런 일이 발생할 수 있습니다(사용자의 경우 @yourdomain.com). 

**내 계정을 복구하려면 어떻게 해야 하나요?**

현재 NuGet.org에는 Azure Active Directory에서 이러한 “관리되지 않는” 테넌트 계정을 사용하여 계정을 인증하는 방법이 없습니다. 지금은 이러한 계정을 인증하는 더 나은 방법을 찾아보고 있습니다.

Microsoft 계정(@yourdomain.com)으로 NuGet.org에 로그인하려는 경우 사용자(또는 사용자 회사의 관리자)는 “@yourdomain.com” 전자 메일 주소를 사용하여 사용자를 인증하려면 DNS 유효성 검사를 수행하여 AAD의 소유권을 주장해야 합니다. Azure Active Directory에서 설명된 [도메인 관리자 인수](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover)에 대한 단계를 따릅니다. 이 작업이 완료되면 일반적인 로그인으로 작업이 시작되어야 합니다.

**이상 모든 작업을 수행하지 않으려는 경우 내 계정을 복구하는 다른 방법은?**

@yourdomain.com과 연결**되지 않은** 이메일을 사용하여 새 Microsoft 계정을 [만들](https://www.microsoft.com/en-us/account) 수 있습니다. [NuGet.org 계정 복구](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) 섹션에 설명된 단계를 따릅니다.

### <a name="how-do-i-change-my-nugetorg-account-username"></a>내 NuGet.org 계정 사용자 이름을 변경하려면 어떻게 하나요?

변경할 수 없습니다. 정책상 사용자 이름 변경이 아직 허용되지 않습니다. 사용자 이름을 변경하는 유일한 방법은 원하는 사용자 이름으로 새 계정을 만드는 것입니다. 새 계정을 만들기 전에 기존 계정을 삭제하는 것이 좋습니다. 그렇지 않은 경우 등록된 Microsoft 계정을 다시 사용할 수 없습니다.
> [!Important]
> 사용자를 삭제하면 여전히 `username`을 **예약**할 수 있습니다. 다시 동일한 사용자 이름을 재사용할 수 없습니다. **여기에는 대/소문자 변경도 포함됩니다**. 예를 들어 `mycoolname` 사용자 이름으로 사용자를 만든 다음, `MyCoolName`(대/소문자 변경)으로 변경하려는 경우 사용자를 삭제한 후에는 변경할 수 없습니다.

올바른 사용자 이름으로 [새 계정을 등록](individual-accounts.md)하려면 [NuGet.org 계정 삭제](#how-to-delete-my-nugetorg-account) 섹션에서 설명된 단계를 따릅니다.

### <a name="how-to-delete-my-nugetorg-account"></a>내 NuGet.org 계정을 삭제하려면 어떻게 하나요?

계정을 삭제하려면 사용자가 유일한 소유자인 모든 패키지의 소유권을 양도하는 것이 좋습니다. 소유권을 양도하는 방법은 [패키지 소유자 관리](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg)를 참조할 수 있습니다. 그러면 요청을 신속하게 처리하는 데도 도움이 됩니다.

계정을 조직으로 변환하려는 경우 [내 NuGet.org 계정을 조직으로 변환](#how-to-transform-my-nugetorg-account-to-an-organization)에 제공된 단계를 따르세요.

> [!Important]
> 사용자를 삭제하면 다음과 같이 됩니다.
>  1. 사용자 이름은 예약되며 개별 계정 또는 조직 계정을 만드는 데 해당 사용자 이름을 다시 사용할 수 없습니다.
>  1. 연결된 API 키를 취소합니다. 
>  1. 모든 자식 패키지의 소유자로서 계정을 제거합니다.
>  1. 이 계정과 기존의 모든 ID 접두사 예약을 분리합니다.
>  1. 모든 조직의 구성원으로서 계정을 제거합니다.

계정 삭제를 진행하려면 다음 단계를 따릅니다.
1. 삭제하려는 계정으로 [NuGet.org에 로그인](https://www.nuget.org/users/account/LogOn)합니다.
2. 이 URL [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete)를 클릭하고 계정 삭제 요청을 제출하는 단계를 따릅니다.

그러면 본사의 고객 지원팀은 이 요청을 처리하고 계정 삭제를 수행합니다.
