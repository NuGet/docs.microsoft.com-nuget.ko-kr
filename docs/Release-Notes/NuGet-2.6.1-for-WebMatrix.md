---
title: WebMatrix 릴리스 정보에 대 한 NuGet 2.6.1 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 2.6.1의 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 WebMatrix 용 NuGet에 대 한 릴리스 정보입니다.
keywords: NuGet 2.6.1 WebMatrix 릴리스 정보, 버그 수정, 알려진된 문제에 대 한 추가 기능을 Dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 505054e42234f313bade496315e94ad485050dbb
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 WebMatrix 릴리스 정보

[NuGet 2.6 릴리스 정보](../release-notes/nuget-2.6.md) | [NuGet 2.7 릴리스 정보](../release-notes/nuget-2.7.md)

NuGet 팀 WebMatrix 용 2014 년 3 월 26 일에 업데이트 된 NuGet 패키지 관리자 확장을 릴리스 했습니다.  이 업데이트에서 설치할 수 있습니다는 [WebMatrix 확장 갤러리](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) 다음 단계를 사용 하 여:

1. 열기 WebMatrix 3
1. 홈 리본에서 확장 아이콘을 클릭 합니다.
1. 업데이트 탭을 선택
1. 2.6.1에 NuGet 패키지 관리자를 업데이트 하려면 클릭
1. 닫고 WebMatrix 3을 다시 시작

## <a name="notable-changes"></a>중요 한 변경 내용

가장 큰 문제 사용자가이 확장 업데이트 해결 두 WebMatrix 내에서 사용 중인 NuGet 패키지를 직면 한 합니다.  첫 번째 NuGet 스키마 버전 오류 이며 두 번째에 0 바이트 Dll에 버그가 `bin` 폴더입니다.

### <a name="nuget-schema-version-error"></a>NuGet 스키마 버전 오류

WebMatrix 3이 릴리스된 이후 NuGet 패키지에 대 한 새 스키마 버전을 필요로 하는 NuGet에 새로운 기능이 도입 되었습니다.  를 웹 사이트에서 NuGet 패키지를 관리 하려고 시도할 때 이러한 새 패키지 WebMatrix에서 볼 수 있는 오류가 발생할 수 있습니다.

![오류가 발생했습니다. 스키마 버전이 호환 되지 않습니다. NuGet을 최신 버전으로 업그레이드 하십시오.](./media/NuGet-2.8/webmatrix-schema-version.png)

이 최신 릴리스의 발생이 오류를 방지 하는 최신 NuGet 패키지를와 호환성을 제공 합니다. 이제 WebMatrix에서 Microsoft.AspNet.WebPages를 포함 하 여 패키지의 새 버전을 설치할 수 있습니다.  이러한 패키지 중 일부 사용한 NuGet 기능와 같은 [XDT 구성 변환](../release-notes/nuget-2.6.md#xdt)는 지금까지 WebMatrix에서 지원 되지 않았습니다.

### <a name="zero-byte-dlls-in-bin-folder"></a>Bin 폴더에서에서 0 바이트 Dll

일부 사용자에 게 보고 하는 NuGet을 설치 하는 bin에 복사 하는 Dll을 포함 하는 WebMatrix에서 Dll 표시를 패키지에서 후의 `bin` 0 바이트 파일과 폴더입니다.  이 런타임 시 응용 프로그램을 중단합니다.

[이 문제](https://nuget.codeplex.com/workitem/4060) 이제 수정 되었습니다.

## <a name="other-recent-improvements"></a>기타 최근 개선 사항

Visual Studio 용 NuGet 패키지 관리자 2.8가 릴리스도 WebMatrix에 대 한 NuGet 패키지 관리자 2.5.0를 릴리스 했습니다.  언급 한 것이 동안는 [NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), 새로운 기능을 도입 하는 업데이트는 특정 언급 하지 않았습니다.

### <a name="update-all"></a>모두 업데이트

이제 모든 한번에 웹 사이트의 패키지를 업데이트할 수 있습니다!  WebMatrix에서 NuGet 확장을 열 때 갤러리, 등에, 설치 된 업데이트를 사용할 수 있는 모든 패키지의 목록을 참조 합니다.  이전에 모든 패키지를 개별적으로 업데이트 되어야 할 것 이지만 이제 업데이트 탭에 표시 하는 유용한 "모두 업데이트" 단추입니다.

![사용 가능한 업데이트로 업데이트 하는 모든 패키지를 모두 업데이트를 클릭합니다](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>기존 파일 덮어쓰기

웹 사이트에 이미 있는 파일이 포함 된 패키지를 설치할 때 NuGet 항상 자동으로 해당 파일 (기존 파일은 그대로 두고)를 무시 했습니다.  인상을 패키지 설치 된 또는 아니 실제로 때 제대로 업데이트 될 수 있습니다.  파일을 덮어쓸 수 이제 NuGet를 입력 합니다.

![파일 충돌 해결](./media/NuGet-2.8/webmatrix-overwrite-file.png)
