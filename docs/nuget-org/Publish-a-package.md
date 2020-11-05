---
title: NuGet 패키지를 게시하는 방법
description: NuGet 패키지를 nuget.org 또는 개인 피드에 게시하는 방법 및 nuget.org에서 패키지 소유권을 관리하는 방법에 대한 자세한 지침입니다.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: fe5625247dca51c10d82fffe82022c40a4716069
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237934"
---
# <a name="publishing-packages"></a>패키지 게시

패키지를 만들고 `.nupkg` 파일이 준비되면 공용 또는 개인용으로 다른 개발자가 사용할 수 있도록 하는 간단한 프로세스입니다.

- 공용 패키지는 이 문서에 설명된 대로 모든 개발자가 [nuget.org](https://www.nuget.org/packages/manage/upload)를 통해 전역적으로 사용할 수 있습니다(NuGet 4.1.0 이상 필요).
- 개인 패키지는 파일 공유, 개인 NuGet 서버, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) 또는 타사 리포지토리(myget, ProGet, Nexus Repository 및 Artifactory)를 호스트하여 팀 또는 조직에서만 사용할 수 있습니다. 자세한 내용은 [패키지 개요 호스트](../hosting-packages/overview.md)를 참조하세요.

이 문서에서는 nuget.org에 대한 게시를 다룹니다. Azure Artifacts에 게시하는 방법은 [패키지 관리](https://www.visualstudio.com/docs/package/nuget/publish)를 참조하세요.

## <a name="publish-to-nugetorg"></a>nuget.org에 게시

nuget.org의 경우 계정을 Microsoft 계정으로 로그인해야 하며, 이 경우 nuget.org에 계정을 등록하라는 메시지가 표시됩니다.

![NuGet 로그인 위치](media/publish_NuGetSignIn.png)

다음으로, 다음 섹션에 설명된 대로 nuget.org 웹 포털을 통해 패키지를 업로드하거나, 명령줄(`nuget.exe` 4.1.0 이상 필요)에서 nuget.org에 푸시하거나, Azure DevOps Services를 통해 CI/CD 프로세스의 일부로 게시할 수 있습니다.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>웹 포털: nuget.org에 패키지 업로드 탭 사용

1. nuget.org의 상단 메뉴에서 **업로드** 를 선택하고 패키지 위치를 찾습니다.

    ![nuget.org에 패키지 업로드](media/publish_UploadYourPackage.PNG)

1. nuget.org는 패키지 이름을 사용할 수 있는 경우 알려 줍니다. 그렇지 않으면 프로젝트에서 패키지 식별자를 변경하고 다시 빌드한 다음, 업로드를 다시 시도합니다.

1. 패키지 이름을 사용할 수 있는 경우 nuget.org는 패키지 매니페스트에서 메타데이터를 검토할 수 있는 **확인** 섹션을 엽니다. 메타데이터를 변경하려면 프로젝트(프로젝트 파일 또는 `.nuspec` 파일)을 편집하고, 다시 빌드하고, 패키지를 다시 만들고, 다시 업로드합니다.

1. **설명서 가져오기** 에서 Markdown을 붙여넣거나, URL로 문서를 가리키거나, 설명서 파일을 업로드할 수 있습니다.

1. 모든 정보가 준비되면 **제출** 단추를 선택합니다.

### <a name="command-line"></a>명령줄

nuget.org에 패키지를 푸시하려면 먼저 nuget.org에 만든 API 키가 필요합니다. 필수 NuGet 프로토콜을 구현하는 dotnet.exe(.NET Core) 또는 nuget.exe v4.1.0 이상을 사용해야 합니다.
자세한 내용은 [.NET Core](/dotnet/core/install/), [nuget.exe](https://www.nuget.org/downloads) 및 [NuGet 프로토콜](../api/nuget-protocols.md)을 참조하세요.

#### <a name="create-api-keys"></a>API 키 만들기

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>dotnet nuget push로 게시

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>nuget push로 게시

1. 명령 프롬프트에서 다음 명령을 실행합니다. 이때 `<your_API_key>`는 nuget.org에서 가져온 키로 바꿉니다.

    ```cli
    nuget setApiKey <your_API_key>
    ```

    이 명령은 NuGet 구성에 API 키를 저장하므로 동일한 컴퓨터에서 이 단계를 반복할 필요가 없습니다.

    > [!NOTE]
    > API 키는 프라이빗 피드 인증에 사용되지 않습니다. 소스 인증에 사용할 자격 증명을 관리하려면 [`nuget sources` 명령](../reference/cli-reference/cli-ref-sources.md)을 참조하세요.
    > API 키는 개별 NuGet 서버에서 가져올 수 있습니다. nuget.org용 APIKeys를 만들고 관리하려면 [API 키 만들기](#create-api-keys)를 참조하세요.

1. 다음 명령을 사용하여 NuGet 갤러리에 패키지를 푸시합니다.

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>서명된 패키지 게시

서명된 패키지를 제출하려면 먼저 패키지 서명에 사용된 [인증서를 등록](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg)해야 합니다. 

> [!Warning]
> nuget.org는 [서명된 패키지 요구 사항](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg)을 충족하지 않는 패키지를 거부합니다.

### <a name="package-validation-and-indexing"></a>패키지 유효성 검사 및 인덱싱

nuget.org에 푸시된 패키지는 바이러스 검사와 같은 여러 유효성 검사를 거칩니다. (nuget.org의 모든 패키지는 정기적으로 검사됩니다.)

패키지가 모든 유효성 검사를 통과하면 인덱싱되는 동안 시간이 걸릴 수 있으며 검색 결과에 표시됩니다. 인덱싱이 완료되면 패키지를 성공적으로 게시했는지 확인하는 전자 메일을 받게 됩니다. 패키지가 유효성 검사에 실패하면 패키지 세부 정보 페이지는 관련 오류를 표시하도록 업데이트되고 이를 알리는 전자 메일을 받을 수도 있습니다.

패키지 유효성 검사 및 인덱싱은 일반적으로 15분이 걸리지 않습니다. 패키지 게시가 예상보다 오래 걸리면 [status.nuget.org](https://status.nuget.org/)를 방문하여 nuget.org에 중단이 발생했는지를 확인합니다. 모든 시스템이 모두 제대로 작동하고 패키지가 1시간 내에 성공적으로 게시되지 않은 경우 nuget.org에 로그인하고 패키지 페이지에서 지원 문의 링크를 사용하여 문의하세요.

패키지 상태를 보려면 nuget.org의 계정 이름 아래에서 **패키지 관리** 를 선택합니다. 유효성 검사가 완료되면 확인 전자 메일을 받게 됩니다.

패키지를 인덱싱하고 다른 사용자가 찾을 수 있는 검색 결과에 표시하는 데 시간이 걸릴 수 있습니다. 이 시간 동안 패키지 페이지에 다음과 같은 메시지가 표시됩니다.

![패키지가 아직 게시되지 않았다는 메시지](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Azure DevOps Services(CI/CD)

지속적인 통합 및 배포 프로세스의 일부로 Azure DevOps를 사용하여 nuget.org에 패키지를 푸시하는 경우 NuGet 작업에서 `nuget.exe` 4.1 이상을 사용해야 합니다. 자세한 내용은 [빌드에서 최신 NuGet을 사용하는 방법](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/)(Microsoft DevOps 블로그)에서 찾을 수 있습니다.

## <a name="managing-package-owners-on-nugetorg"></a>nuget.org에서 패키지 소유자 관리

각 NuGet 패키지의 `.nuspec` 파일이 패키지의 작성자를 정의하지만 nuget.org 갤러리는 소유권을 정의하는 데 해당 메타데이터를 사용하지 않습니다. 대신 nuget.org는 패키지를 게시하는 사용자에게 초기 소유권을 할당합니다. nuget.org UI 통해 패키지를 업로드한 로그인 사용자 또는 `nuget SetApiKey`이나 `nuget push`에서 해당 API 키를 사용한 사용자입니다.

모든 패키지 소유자는 다른 소유자 추가와 제거 및 업데이트 게시를 포함하여 패키지에 대한 모든 권한을 갖습니다.

패키지의 소유권을 변경하려면 다음을 수행합니다.

1. 패키지의 현재 소유자인 계정을 사용하여 nuget.org에 로그인합니다.
1. 계정 이름을 선택하고 **패키지 관리** 를 선택한 후 **게시된 패키지** 를 확장합니다.
1. 관리할 패키지를 선택한 다음, 오른쪽에서 **소유자 관리** 를 선택합니다.

여기부터 다음과 같은 몇 가지 옵션을 사용합니다.

1. **현재 소유자** 아래에 나열된 모든 소유자를 제거합니다.
1. 사용자 이름, 메시지를 입력하고 **추가** 를 선택하여 **소유자 추가** 아래에 소유자를 추가합니다. 그러면 새로운 공동 소유자에게 확인 링크를 포함한 전자 메일을 보냅니다. 확인하면 해당 사용자에게는 소유자를 추가하고 제거하는 모든 권한이 있습니다. (확인될 때까지 **현재 소유자** 섹션에서는 해당 사용자가 승인 보류 중으로 표시됩니다.)
1. 소유권을 이전하려면(잘못된 계정에서 소유권이 변경되거나 패키지가 게시될 경우) 새 소유자를 추가합니다. 소유권을 확인하면 목록에서 제거할 수 있습니다.

회사 또는 그룹에 소유권을 할당하려면 적절한 팀 멤버에 전달되는 전자 메일 별칭을 사용하여 nuget.org 계정을 만듭니다. 예를 들어 다양한 Microsoft ASP.NET 패키지는 단순히 해당 별칭인 [microsoft](https://nuget.org/profiles/microsoft) 및 [aspnet](https://nuget.org/profiles/aspnet) 계정에서 공동 소유합니다.

### <a name="recovering-package-ownership"></a>패키지 소유권 복구

경우에 따라 패키지에는 활성 소유자가 없을 수 있습니다. 예를 들어 원래 소유자는 회사가 패키지를 생성하거나, nuget.org 자격 증명을 손실하거나, 갤러리의 이전 버그 패키지를 소유하지 않도록 둘 수 있습니다.

사용자가 패키지의 정당한 소유자이고 소유권을 다시 가져와야 하는 경우 nuget.org에서 [연락처 양식](https://www.nuget.org/policies/Contact)을 사용하여 NuGet 팀에 상황을 설명합니다. 그런 다음 패키지의 프로젝트 URL, Twitter, 전자 메일 또는 다른 수단을 통해 기존 소유자를 찾는 작업을 포함하여 패키지의 소유권을 확인하는 프로세스를 따릅니다. 하지만 모든 작업에 실패하면 소유자가 되도록 새로운 초대장을 보낼 수 있습니다.
