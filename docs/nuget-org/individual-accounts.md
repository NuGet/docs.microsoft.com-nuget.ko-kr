---
title: 개별 계정
description: 패키지를 게시하려면 NuGet.org의 개별 계정이 필요합니다.
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427138"
---
# <a name="individual-accounts"></a>개별 계정

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