---
title: NuGet.org의 조직
description: NuGet.org의 조직은 그룹 또는 팀, 회사 환경에서 게시된 패키지를 관리하는 데 도움을 줍니다.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427078"
---
# <a name="your-organization-on-nugetorg"></a>NuGet.org의 조직

조직은 단일 NuGet.org ID를 사용하여 비즈니스와 오픈 소스 프로젝트가 패키지로 협업할 수 있게 합니다. 패키지 소비자의 경우 조직 계정은 NuGet.org의 기존 사용자 계정과 동일하게 나타납니다.

## <a name="organization-accounts-vs-individual-accounts"></a>조직 계정 및 개별 계정

조직 계정은 구성원으로 하나 이상의 개별(사용자) 계정을 가지고 있습니다. 이러한 멤버는 소유권에 대한 단일 ID를 유지 관리하면서 패키지 세트를 관리할 수 있습니다.

개별 계정은 NuGet.org에서 사용자의 ID이며, 여러 조직의 멤버가 될 수 있습니다. 패키지는 개별 계정에 속할 수 있는 것처럼 조직 계정에 속할 수 있습니다. 패키지 소비자는 개별 계정 또는 조직 계정 간의 차이를 보지 못합니다. 둘 다 패키지 `owners`로 나타납니다.

## <a name="adding-a-new-organization"></a>새 조직 추가

새 조직을 추가하려면 NuGet.org에서 계정을 선택한 다음, **조직 관리...**  메뉴 명령을 선택합니다.

![관리자 조직에 대한 NuGet.org의 메뉴 옵션](media/org-manage-option.png)

다음 페이지에서 **새 조직 추가** 단추를 선택합니다.

![NuGet.org에서 새 조직을 만드는 단추](media/org-add-new-option.png)

다음 페이지에서 조직 이름과 이메일 주소를 제공합니다. 조직 계정은 사용자 계정과 동일한 네임스페이스를 공유하므로 조직 이름은 기존의 다른 조직 또는 사용자 계정과 달라야 합니다. 또한 이메일 주소는 모든 계정에서 고유해야 합니다.

![NuGet.org에 새 조직 페이지 추가](media/org-add-new-page.png)

조직 계정이 생성되면 관리자가 되어 조직에 대한 패키지를 제출하고 조직 멤버를 추가할 수 있습니다.

### <a name="transform-existing-account-to-an-organization"></a>기존 계정을 조직으로 변환

> [!Warning]
> 계정 변환은 되돌릴 수 없습니다. 조직을 사용자 계정으로 다시 변환할 수 없습니다.

단일 사용자 계정을 사용하여 팀으로 패키지를 관리하고 해당 계정을 조직으로 변환하려는 경우 **조직 관리** 페이지에서 **조직으로 계정 변환**을 사용합니다.

![NuGet.org에서 기존 계정을 조직으로 변환하는 옵션](media/org-transform-option.png)

다음 페이지에서 조직의 관리자로 할당할 다른 사용자 계정을 지정한 다음, **변환**을 선택합니다.

![사용자 계정을 조직으로 변환하기 위한 정보 입력](media/org-transform-page.png)

## <a name="managing-organization-members"></a>조직 멤버 관리

조직 관리자는 각 멤버의 NuGet.org *사용자 계정 이름*을 제공하여 멤버를 추가할 수 있으며, 이메일 주소는 사용할 수 없습니다. 그런 다음, 각 멤버를 다음 사용 권한으로 협력자 또는 관리자로 표시합니다.

| 사용 권한 | 협력자 | 관리자 |
| --- | --- | --- |
| 조직의 패키지 관리<br/>(새 패키지 제출, 기존 패키지 업데이트 또는 나열 취소) | 예 | 예 |
| 조직 메타데이터 변경<br/>(이메일 주소, 알림 설정) | 아니요 | 예 |
| 조직 멤버 관리 | 아니요 | 예 |
| 조직 패키지에 대한 공동 소유권 요청 또는 작업 | 아니요 | 예 |

## <a name="managing-packages"></a>패키지 관리

[패키지 관리](https://www.nuget.org/account/Packages) 페이지의 멤버로서 계정과 모든 조직의 모든 패키지를 볼 수 있습니다. 계정 또는 특정 조직별 패키지를 보려면 페이지 오른쪽 위에 있는 계정 필터를 사용합니다.

![계정 필터를 사용하여 패키지를 관리](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>조직에 패키지 전송
일부 패키지를 새로 만든 조직으로 전송하려는 경우 조직 계정에 패키지를 공동 소유하도록 요청한 다음, 소유자에서 자신을 제거하여 패키지를 전송할 수 있습니다. 조직의 관리자인 경우 소유권을 허용하는 데 필요한 확인이 없습니다. 그러나 협력자인 경우 조직을 소유자로 추가하려면 소유권을 허용할 관리자 중 한 명이 필요합니다.

## <a name="publishing-packages"></a>패키지 게시

패키지를 NuGet.org에 직접 업로드하거나 `nuget push` 또는 `dotnet nuget push` CLI 명령을 통해 패키지를 푸시하여 사용자 계정에 패키지를 게시하는 등의 방법으로 패키지를 게시합니다.

### <a name="uploading-packages"></a>패키지 업로드

[NuGet.org 업로드](https://www.nuget.org/packages/manage/upload) 페이지에 새 패키지를 직접 업로드할 때 패키지 소유자를 사용자 또는 조직 계정에 할당합니다.

![계정 옵션을 사용하여 패키지 업로드](media/org-upload-option.png)

### <a name="using-api-keys"></a>API 키 사용

`nuget push` 또는 `dotnet nuget push` CLI 명령을 통해 패키지를 푸시하려면 해당 명령에 필요한 API 키를 가져와야 합니다. 자세한 내용은 [패키지 게시](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)를 참조하세요.

새 API 키를 만들 때 **패키지 소유자** 드롭다운에서 적절한 조직을 선택합니다. 생성한 모든 API 키는 선택한 조직에만 적용됩니다.

![계정 옵션이 있는 API 키](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>조직 제거

사용자는 조직 멤버 자격에 표시된 **X** 단추를 선택하여 조직에서 자신을 삭제할 수 있습니다.

![조직에서 사용자 계정 제거](media/org-remove-self-option.png)

관리자는 다른 관리자를 비롯하여 조직에서 모든 멤버를 제거할 수 있습니다. 조직의 유일한 관리자인 경우 다른 멤버를 관리자로 추가하지 않는 한 자신을 삭제할 수 없습니다.

### <a name="deleting-an-organization-account"></a>조직 계정 삭제

조직 페이지에 표시된 **삭제** 단추를 클릭하여 조직 계정을 삭제할 수 있습니다.

![조직 삭제](media/org-delete-option.png)

조직을 삭제하려면 **조직 삭제** 확인 단추를 클릭하여 조직 삭제를 확인해야 합니다.
