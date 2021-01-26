---
title: WebMatrix 릴리스 정보에 대 한 NuGet 2.6.1
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 포함 하 여 WebMatrix 용 NuGet 2.6.1에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780421"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>WebMatrix 릴리스 정보에 대 한 NuGet 2.6.1

[NuGet 2.6 릴리스 정보](../release-notes/nuget-2.6.md)  |  [NuGet 2.7 릴리스 정보](../release-notes/nuget-2.7.md)

NuGet 팀은 2014 년 3 월 26 일에 WebMatrix 용 업데이트 된 NuGet 패키지 관리자 확장을 릴리스 했습니다.  이 업데이트는 [WebMatrix 확장 갤러리](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) 에서 다음 단계를 사용 하 여 설치할 수 있습니다.

1. WebMatrix 3 열기
1. 홈 리본에서 확장 아이콘을 클릭 합니다.
1. 업데이트 탭 선택
1. NuGet 패키지 관리자를 2.6.1로 업데이트 하려면 클릭 하십시오.
1. WebMatrix 3을 닫고 다시 시작 합니다.

## <a name="notable-changes"></a>주목할 만한 변경 내용

이 확장 업데이트는 사용자가 WebMatrix 내에서 NuGet 패키지를 사용 하는 가장 큰 두 가지 문제를 해결 합니다.  첫 번째는 NuGet 스키마 버전 오류이 고, 두 번째는 폴더에서 0 바이트 Dll로 이어지는 버그 였습니다 `bin` .

### <a name="nuget-schema-version-error"></a>NuGet 스키마 버전 오류

WebMatrix 3이 출시 되었으므로 nuget 패키지에 대 한 새 스키마 버전을 필요로 하는 새로운 기능이 NuGet에 도입 되었습니다.  웹 사이트에서 NuGet 패키지를 관리 하려고 할 때 이러한 새 패키지를 통해 WebMatrix에 표시 되는 오류가 발생할 수 있습니다.

![오류가 발생했습니다. 스키마 버전이 호환 되지 않습니다. NuGet을 최신 버전으로 업그레이드 하세요.](./media/NuGet-2.8/webmatrix-schema-version.png)

이 최신 릴리스는 최신 NuGet 패키지와의 호환성을 제공 하 여이 오류가 발생 하지 않도록 합니다. 이제 Microsoft 웹 페이지를 포함 하는 패키지의 새 버전을 WebMatrix에 설치할 수 있습니다.  이러한 패키지 중 일부는 현재까지 WebMatrix에서 지원 되지 않는 [XDT config 변환과](../release-notes/nuget-2.6.md#xdt)같은 NuGet 기능을 사용 하 고 있습니다.

### <a name="zero-byte-dlls-in-bin-folder"></a>Bin 폴더의 Zero-Byte Dll

일부 사용자는 WebMatrix에 복사 된 Dll이 포함 된 NuGet 패키지를 설치 하 고 나면 해당 Dll이 `bin` 폴더에 0 바이트 파일로 표시 되는 것을 보고 했습니다.  이렇게 하면 런타임에 응용 프로그램이 중단 됩니다.

이제 [이 문제가](https://nuget.codeplex.com/workitem/4060) 해결 되었습니다.

## <a name="other-recent-improvements"></a>기타 최신 개선 사항

Visual Studio 용 NuGet 패키지 관리자 2.8가 릴리스되면 WebMatrix 용 NuGet 패키지 관리자 2.5.0 출시 되었습니다.  이 내용은 [NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)에 설명 되어 있지만 업데이트에서 도입 된 특정 새 기능에 대해서는 언급 하지 않았습니다.

### <a name="update-all"></a>모두 업데이트

이제 모든 웹 사이트의 패키지를 한 번에 업데이트할 수 있습니다.  WebMatrix에서 NuGet 확장을 열면 갤러리의 모든 패키지 목록, 설치 된 패키지 및 업데이트를 사용할 수 있는 패키지가 표시 됩니다.  이전에는 모든 패키지가 개별적으로 업데이트 되어야 하지만 이제 업데이트 탭에 표시 되는 유용한 "모두 업데이트" 단추가 있습니다.

![사용 가능한 업데이트가 있는 모든 패키지를 업데이트 하려면 모두 업데이트를 클릭 합니다.](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>기존 파일 덮어쓰기

웹 사이트에 이미 있는 파일을 포함 하는 패키지를 설치할 때 NuGet은 항상 해당 파일을 자동으로 무시 했습니다 (기존 파일만 남기고 있음).  이로 인해 실제로 패키지가 설치 또는 업데이트 되지 않은 것 처럼 보일 수 있습니다.  이제 NuGet에서 파일을 덮어쓸지 묻는 메시지를 표시 합니다.

![파일 충돌 해결](./media/NuGet-2.8/webmatrix-overwrite-file.png)
