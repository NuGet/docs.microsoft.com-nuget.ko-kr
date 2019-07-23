---
ms.openlocfilehash: 5acdc54726e4cb07794f8ee07d5e0d357ff622a3
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842044"
---
1. [nuget.org 계정에 로그인](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)하거나 아직 계정이 없는 경우 계정을 만듭니다.

1. 사용자 이름(오른쪽 위)을 선택한 다음 **API 키**를 선택합니다.

1. **만들기**를 선택하고, 키 이름을 지정하고, **범위 선택 > 푸시**를 선택합니다. **GLOB 패턴**에 *를 입력한 후 **만들기**를 선택합니다. (범위에 대한 자세한 내용은 아래를 참조하세요.)

1. 키가 만들어지면 **복사**를 선택하여 CLI에서 필요한 액세스 키를 검색합니다.

    ![클립보드에 API 키 복사](../media/QS_Create-02-APIKey.png)

1. **중요**: 나중에 키를 다시 복사할 수 없으므로 키를 안전한 위치에 저장하세요. API 키 페이지로 돌아갈 경우 키를 복사하려면 키를 다시 생성해야 합니다. CLI를 통해 더 이상 패키지를 푸시하지 않으려는 경우 API 키를 제거할 수도 있습니다.

범위 지정을 사용하면 다른 용도의 API 키를 별도로 작성할 수 있습니다. 각 키는 만기 시간이 있으며 범위를 특정 패키지(또는 GLOB 패턴)로 지정할 수 있습니다. 각 키의 범위를 새 패키지 및 업데이트 푸시, 업데이트만 푸시 또는 목록 해제와 같은 특정 작업으로 지정할 수도 있습니다. 범위 지정을 통해 조직의 패키지를 관리하는 여러 사용자의 API 키를 만들어 필요한 권한만 가지도록 할 수 있습니다. 자세한 내용은 [Introducing scoped API keys](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html) (범위 지정된 API 키 소개)(blogs.nuget.org)를 참조하세요.