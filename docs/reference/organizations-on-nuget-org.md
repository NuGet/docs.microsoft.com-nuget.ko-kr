---
title: Nuget.org에 조직
description: Nuget.org에서 조직을 사용 하면 그룹 또는 팀, 회사 환경에서에서 게시 된 패키지를 관리할 수 있습니다.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 7f40654a08ac221c5ec3a90c86387b6760b28994
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449580"
---
# <a name="organization-on-nugetorg"></a>Nuget.org에 조직

조직의는 비즈니스 및 오픈 소스 프로젝트를 단일 nuget.org id를 사용 하 여 패키지에서 공동 작업을 활성화 합니다. 패키지 소비자에 대 한 조직 계정을 nuget.org에 기존 사용자 계정으로 동일한 나타납니다.

## <a name="user-accounts-vs-organization-accounts"></a>조직 계정 및 사용자 계정

사용자 계정이 nuget.org 본인 이며의 조직에서는 여러의 구성원이 될 수 있습니다. 패키지는 사용자 계정에 속할 수와 같은 조직 계정에 속할 수 있습니다. 패키지 소비자는 사용자 계정 또는 조직 계정 간의 차이점을 표시 하지 않습니다: 패키지로 표시 둘 다 `owners`합니다.

조직 계정은 구성원으로 사용자 계정을 하나 이상에 있습니다. 이러한 멤버 소유권에 대 한 단일 id를 유지 하면서 패키지의 집합을 관리할 수 있습니다.

## <a name="adding-a-new-organization"></a>새 조직 추가

새 조직을 추가 하려면 계정에 nuget.org 선택 하 고 선택 된 **조직 관리...**  메뉴 명령:

![관리자 조직 nuget.org에 메뉴 옵션](media/org-manage-option.png)

다음 페이지에서 선택 된 **새 조직 추가** 단추:

![Nuget.org에 새 조직을 만들기 단추](media/org-add-new-option.png)

다음 페이지에서 조직 이름 및 전자 메일 주소를 제공 합니다. 조직 계정을 사용자 계정으로 동일한 네임 스페이스를 공유 하기 때문에 조직 이름을 다른 기존 조직 또는 사용자 계정에서 달라 야 합니다. 전자 메일 주소 모든 계정에서 고유 수도 있어야 합니다.

![새 조직 페이지 nuget.org에 추가](media/org-add-new-page.png)

조직 계정이 만들어지면 관리자 및 조직에 대 한 패키지를 전송 하 고 추가할 수 조직 구성원.

### <a name="transform-existing-account-to-an-organization"></a>조직에 기존 계정 변환

> [!Warning]
> 계정 변환과 취소할 수 없습니다: 조직의 사용자 계정으로 다시 변환할 수 없습니다.

단일 사용자 계정을 사용 하 여 팀으로 패키지를 관리 하 고 해당 계정을 사용 하 여 조직으로 변환 하려고 하는 경우는 **조직 계정을 변환** 옵션에 **관리 조직** 페이지:

![조직에 기존 계정을 변환할 nuget.org에 옵션](media/org-transform-option.png)

다음 페이지에서 조직의 관리자로 할당 한 다음를 선택 하는 데 다른 사용자 계정을 지정 **변환**합니다.

![조직에 사용자 계정을 변환에 대 한 정보를 입력 합니다.](media/org-transform-page.png)

## <a name="managing-organization-members"></a>조직 멤버 관리

조직 관리자 권한으로 각 멤버의 nuget.org를 제공 하 여 멤버를 추가할 수 있습니다 *사용자 계정 이름*; 전자 메일 주소를 사용할 수 없습니다. 협력자 또는 다음 사용 권한 가진 관리자가 각 멤버를 표시합니다.

| 사용 권한 | 공동 작업자 | 관리자 |
| --- | --- | --- |
| 조직의 패키지 관리<br/>(새 패키지를 전송, 업데이트 또는 기존 패키지를 unlist) | 예 | 예 |
| 변경 내용 조직 메타 데이터<br/>(전자 메일 주소를 알림 설정) | 아니요 | 예 |
| 조직 멤버 관리 | 아니요 | 예 |
| 요청 또는 관련 조직 패키지에 대 한 co-ownership 요청 작업 | 아니요 | 예 |

## <a name="managing-packages"></a>패키지 관리

계정 및는 구성원 인 모든 조직에서 모든 패키지를 볼 수는 [패키지 관리](https://www.nuget.org/account/Packages) 페이지. 특정 조직 또는 계정 관련 패키지를 보려면 계정을 필터 상단 사용 하 여 페이지의 오른쪽입니다.

![계정 필터를 사용 하 여 패키지를 관리](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>조직에 패키지를 전송합니다.
새로 만든된 조직에 패키지의 일부를 전송 하려는 경우 패키지를 공동 소유 조직 계정을 요청 하 고 소유자를 제거 하는 사용자가 직접 그렇게 할 수 있습니다. 조직의 관리자 인 경우 소유권에 동의 하는 데 필요한 확인 하지 않습니다. 그러나 공동 작업자 인 경우 조직 소유자로 추가의 소유권을 수락 하도록 관리자가 하나 필요 합니다.

## <a name="publishing-packages"></a>패키지 게시

사용자 계정에 패키지를 게시할와 같은 조직에 패키지를 게시할: 직접 nuget.org를 패키지를 업로드 하 여 또는 패키지를 통해 푸시하여는 `nuget push` 또는 `dotnet nuget push` CLI 명령입니다.

### <a name="uploading-packages"></a>패키지를 업로드 하는 중

직접 업로드 하는 경우 새 패키지에는 [nuget.org 업로드](https://www.nuget.org/packages/manage/upload) 사용자 또는 조직 계정에 패키지 소유자를 할당 페이지:

![계정 옵션을 사용 하 여 패키지를 업로드 합니다.](media/org-upload-option.png)

### <a name="using-api-keys"></a>API 키를 사용 하 여

통해 패키지를 푸시하는 `nuget push` 또는 `dotnet nuget push` CLI 명령을 해당 명령을 사용 하 여 필요한 API 키를 가져와야 합니다. 자세한 내용은 참조 [패키지 게시](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)합니다.

새 API 키를 만들 때 적절 한 조직에서 선택 된 **패키지 소유자** 드롭 다운 합니다. 모든 API 키를 만들면 선택한 조직에만 적용 됩니다.

![계정 옵션을 사용 하 여 API 키](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>조직 제거

사용자를 제거할 수 있습니다 직접 조직에서 선택 하 여는 `X` 조직 구성원에 의해 표시 된 단추:

![조직에서 사용자 계정 제거](media/org-remove-self-option.png)

관리자는 다른 관리자를 포함 하 여 조직에서 모든 구성원을 제거할 수 있습니다. 조직에 대 한 유일한 관리자 인 경우 관리자 권한으로 다른 멤버를 추가 하지 않으면 사용자가 직접 제거할 수 없습니다.

### <a name="deleting-an-organization-account"></a>조직 계정 삭제

이 기능은 곧 제공 됩니다.
