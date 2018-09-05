---
title: Nuget.org의 조직
description: Nuget.org의 조직에는 그룹 또는 팀을 회사 환경에서 게시 된 패키지를 관리할 수 있습니다.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: ea1ca607f169cd31c0a1b59d575d1a743763420c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551230"
---
# <a name="organization-on-nugetorg"></a>Nuget.org의 조직

조직은은 비즈니스 및 공동 작업 하 고 단일 nuget.org id를 사용 하 여 패키지를 오픈 소스 프로젝트를 설정 합니다. 패키지 소비자를 조직 계정이 nuget.org에서 기존 사용자 계정으로 동일한 나타납니다.

## <a name="user-accounts-vs-organization-accounts"></a>조직 계정 및 사용자 계정

사용자 계정이 nuget.org에서 사용자의 신원을 이며 임의 개수의 조직의 멤버일 수 있습니다. 패키지는 사용자 계정에 속할 수와 같은 조직 계정에 속할 수 있습니다. 패키지 소비자는 사용자 계정 또는 조직 계정 간의 차이점을 표시 하지 않습니다: 모두 표시 패키지로 `owners`합니다.

조직 계정이 구성원으로 사용자 계정을 하나 이상에 있습니다. 이러한 멤버 소유권에 대 한 단일 id를 유지 관리 하는 동안 패키지 집합을 관리할 수 있습니다.

## <a name="adding-a-new-organization"></a>새 조직 추가

새 조직에 추가 하려면 nuget.org에서 사용자 계정을 선택한 다음 선택 된 **조직 관리 하는 중...**  메뉴 명령:

![Nuget.org의 조직 관리자에 대 한 메뉴 옵션](media/org-manage-option.png)

다음 페이지에서 선택 합니다 **새 조직 추가** 단추:

![Nuget.org에서 새 조직을 만든 단추](media/org-add-new-option.png)

다음 페이지에서 조직 이름 및 전자 메일 주소를 제공 합니다. 조직 계정을 사용자 계정과 동일한 네임 스페이스를 공유 하기 때문에 조직 이름을 기존 조직 또는 사용자 계정에서 달라 야 합니다. 전자 메일 주소 모든 계정에서 고유 수도 있어야 합니다.

![Nuget.org의 새 조직 페이지를 추가 합니다.](media/org-add-new-page.png)

조직 계정이 만들어지면 관리자 및 조직에 대 한 패키지를 제출 하 조직의 구성원을 추가 합니다.

### <a name="transform-existing-account-to-an-organization"></a>조직에 기존 계정 변환

> [!Warning]
> 계정 변환이 되돌릴 수 없는: 조직의 사용자 계정으로 다시 변환할 수는 없습니다.

단일 사용자 계정을 사용 하 여 팀으로 패키지를 관리 하 고 해당 계정을 사용 하 여 조직에서 변환 하려는 경우는 **변환 하는 조직 계정의** 옵션을 **관리 조직** 페이지:

![Nuget.org의 조직에 기존 계정 변환할 옵션](media/org-transform-option.png)

다음 페이지에서 조직의 관리자로 할당 한 다음 선택 다른 사용자 계정을 지정 **변환**합니다.

![사용자 계정을 조직에 변환에 대 한 정보를 입력 합니다.](media/org-transform-page.png)

## <a name="managing-organization-members"></a>조직의 구성원 관리

조직 관리자 각 멤버의 nuget.org를 제공 하 여 멤버를 추가할 수 있습니다 *사용자 계정 이름*; 전자 메일 주소를 사용할 수 없습니다. 다음 권한이 있는 관리자나 공동 작업자와 각 멤버를 표시합니다.

| 사용 권한 | 협력자 | 관리자 |
| --- | --- | --- |
| 조직의 패키지 관리<br/>(새 패키지를 제출, 업데이트 또는 기존 패키지의 나열을 취소) | 예 | 예 |
| 조직 메타 데이터 변경<br/>(전자 메일 주소, 알림 설정) | 아니요 | 예 |
| 조직 구성원 관리 | 아니요 | 예 |
| 요청 또는 조직 패키지에 대 한 co-ownership 요청 작업 | 아니요 | 예 |

## <a name="managing-packages"></a>패키지 관리

계정 및의 구성원 인 모든 조직에서 모든 패키지를 볼 수 있습니다 합니다 [패키지 관리](https://www.nuget.org/account/Packages) 페이지입니다. 특정 조직 또는 계정 관련 패키지를 보려면 위쪽의 계정을 필터 사용 페이지의 오른쪽입니다.

![계정 필터를 사용 하 여 패키지를 관리](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>조직에 패키지를 전송합니다.
새로 만든된 조직에 패키지의 일부를 전송 하려는 경우 조직 계정을 공동 소유 하는 패키지를 요청 하 고 소유자를 제거 하는 직접 여 하면 됩니다. 조직의 관리자 인 경우 소유권을 허용 하는 데 필요한 확인 하지 않습니다. 그러나 협력자 인 경우 소유자로 서 조직 추가의 소유권을 허용 하도록 관리자가 하나 필요 합니다.

## <a name="publishing-packages"></a>패키지 게시

사용자 계정에 패키지를 게시 하는 같은 조직에 패키지를 게시: nuget.org에 패키지를 직접 업로드 하거나 패키지를 푸시하여 합니다 `nuget push` 또는 `dotnet nuget push` CLI 명령입니다.

### <a name="uploading-packages"></a>패키지를 업로드합니다.

직접 업로드 하는 경우 새 패키지에는 [nuget.org 업로드](https://www.nuget.org/packages/manage/upload) 사용자 또는 조직 계정에 패키지 소유자를 할당 페이지:

![계정 옵션을 사용 하 여 패키지를 업로드 합니다.](media/org-upload-option.png)

### <a name="using-api-keys"></a>API 키를 사용 하 여

통해 패키지를 푸시하는 `nuget push` 또는 `dotnet nuget push` CLI 명령, 해당 명령을 사용 하 여 필요한 API 키를 가져와야 합니다. 자세한 내용은 참조 하세요 [패키지 게시](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)합니다.

새 API 키를 만들 때에 적절 한 조직을 선택 합니다 **패키지 소유자** 드롭다운 합니다. 만든 모든 API 키 선택한 조직에만 적용 됩니다.

![계정 옵션을 사용 하 여 API 키](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>조직 제거

사용자를 제거할 수 있습니다 직접 조직에서 선택 하 여는 `X` 단추 조직 멤버 자격으로 표시 합니다.

![조직에서 사용자 계정 제거](media/org-remove-self-option.png)

관리자는 다른 관리자를 비롯 하 여 조직에서 모든 멤버를 제거할 수 있습니다. 조직에 대 한 유일한 관리자 인 경우 관리자 권한으로 다른 멤버를 추가 하지 않을 경우 직접 제거할 수 없습니다.

### <a name="deleting-an-organization-account"></a>조직 계정 삭제

이 기능은 곧 제공 됩니다.
