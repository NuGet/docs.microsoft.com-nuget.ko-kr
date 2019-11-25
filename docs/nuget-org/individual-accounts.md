---
title: 개별 계정 - NuGet.org
description: 패키지를 게시하려면 NuGet.org의 개별 계정이 필요합니다.
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 7951b3db0cdcaee0a1eb955a5bf6fedce24c79c9
ms.sourcegitcommit: fc0f8c950829ee5c96e3f3f32184bc727714cfdb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2019
ms.locfileid: "74253950"
---
# <a name="individual-accounts-on-nugetorg"></a>NuGet.org의 개별 계정

NuGet.org에서 패키지를 게시하고 관리하려면 개별 계정을 만들어야 합니다.

## <a name="individual-accounts-vs-organization-accounts"></a>개별 계정 및 조직 계정

개별(사용자) 계정은 NuGet.org에서 사용자의 ID이며, 여러 조직의 멤버가 될 수 있습니다. 패키지는 개별 계정에 속할 수 있는 것처럼 조직 계정에 속할 수 있습니다. 패키지 소비자는 개별 계정 또는 조직 계정 간의 차이를 보지 못합니다. 둘 다 패키지 `owners`로 나타납니다.

조직 계정은 구성원으로 하나 이상의 개별 계정을 가지고 있습니다. 이러한 멤버는 소유권에 대한 단일 ID를 유지 관리하면서 패키지 세트를 관리할 수 있습니다.

## <a name="add-a-new-individual-account"></a>새 개별 계정 추가

NuGet.org 계정을 만들려면 개인 MSA(Microsoft 계정) 또는 AAD(Azure Active Directory) 계정이 있어야 합니다. 없는 경우 계정을 [만들](https://signup.live.com) 수 있습니다. MSA 또는 AAD 계정이 있는 경우 다음 단계를 따릅니다.

1. [NuGet.org 로그인 페이지](https://www.nuget.org/users/account/LogOn)로 이동합니다.

1. **Microsoft로 로그인** 단추를 클릭합니다.

1. Microsoft 계정 또는 Azure Active Directory 계정 세부 정보를 입력합니다.

1. **예**를 클릭하여 *NuGet.org* 애플리케이션에 지정된 사용 권한을 수락하세요.

   ![NuGet.org에 사용 권한 부여](media/nuget-org-permissions.png)

1. *nuget.org*로 리디렉션되고 사용자 이름을 등록하라는 메시지가 표시됩니다.

1. 입력 상자에서 사용자 이름을 지정합니다. 사용자 이름은 대/소문자를 구분**하며** 나중에 변경하거나 이름을 바꿀 수 없습니다.

   ![NuGet.org에서 사용자 이름 지정](media/nuget-org-register.png) 

1. **등록** 단추를 클릭합니다.

이제 NuGet.org 계정이 있습니다. [계정 설정](https://www.nuget.org/account) 페이지에서 계정 관리를 수행할 수 있습니다.

## <a name="enable-two-factor-authentication-2fa"></a>2FA(2단계 인증) 사용

2FA(2단계 인증)는 웹 사이트나 앱에 로그인할 때 사용되는 추가 보안 계층입니다. 2FA를 사용하면 MSA(Microsoft 계정)로 로그인하고 사용자만 알고 있거나 액세스할 수 있는 다른 형식의 인증을 제공해야 합니다. 계정을 더 잘 보호하려면 2단계 인증을 사용하도록 설정합니다(권장).

1. 계정에 로그인한 경우 프로필을 열고 **로그인 계정**에서 **사용**을 선택합니다.

   ![2FA 사용](media/nuget-org-register-2fa.png)

   다음에 nuget.org  에 로그인 할 때 추가 자격 증명을 묻는 메시지가 표시 됩니다.

2. 지금 인증을 완료하려면 로그아웃했다가 다시 로그인합니다.

3. 로그인할 때 두 번째 인증 형식으로 문자 또는 메일을 선택합니다.

   Microsoft 계정에 이미 연결되어 있는 전화 번호 또는 메일을 확인합니다. 계정의 새 전화 번호 또는 메일을 입력해야 할 수 있습니다. 필요한 경우 지침에 따라 필요한 정보를 입력하고 **다음**을 클릭합니다.

   ![2FA 사용](media/nuget-org-sign-in-2fa.png)

4. 디바이스 또는 메일 계정을 확인하고 방금 받은 코드를 입력합니다.

   ![2FA 사용](media/nuget-org-enter-code-2fa.png)

5. 추가 지침에 따라 2단계 인증을 완료합니다.

> [!Tip]
> NuGet.org 계정에 대해 2FA를 사용하도록 설정해도 NuGet.org에 로그인하는 데 사용하는 Microsoft 계정에 연결될 수 있는 다른 계정 또는 서비스의 인증 설정에는 영향을 주지 않습니다.

## <a name="delete-a-nugetorg-account"></a>NuGet.org 계정 삭제

NuGet.org 계정 삭제처럼 추가 계정 관련 작업에 대해서는 [NuGet.org 계정 관리](nuget-org-faq.md#nugetorg-account-management)를 참조하세요.
