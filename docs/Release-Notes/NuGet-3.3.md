---
title: "NuGet 3.3 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 3.3에 대 한 릴리스 정보입니다."
keywords: "NuGet 3.3 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c83f87231497e14c36f1b8100b7bec720bb63b1c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 릴리스 정보

[3.2.1 NuGet 릴리스 정보](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC 릴리스 정보](../release-notes/nuget-3.4-RC.md)

NuGet 3.3에 많은 수의 사용자 인터페이스 업데이트 및 명령줄 기능으로는 NuGet 클라이언트에 유용한 수정 프로그램의 모음 2015 년 11 월 30 일에 발표 되었습니다.

## <a name="new-features"></a>새 기능

* NuGet 명령줄 클라이언트는 인증 된 피드를 원활 하 게 작업할 수 있게 되기를 허용 하는 자격 증명 공급자 도입 되었습니다. [Visual Studio Team Services를 설치 하는 방법에 대 한 지침 공급자 자격 증명 ](../API/nuget-exe-Credential-Providers.md) NuGet 구성 NuGet 문서에서 사용할 수 있는 클라이언트가 사용할 수 있습니다.

## <a name="new-user-interface-features"></a>새로운 사용자 인터페이스 기능

* 찾아보기, 설치 됨, 및 업데이트를 사용할 수 있는 별도 탭
* 사용 가능한 업데이트가 있는 패키지 수를 나타내는 사용할 수 있는 배지를 업데이트 합니다.
* 패키지를 패키지가 설치 되어 있는지를 나타내는 패키지 목록에 배지 또는 사용 가능한 업데이트가
* 개수 및 패키지 목록에 추가 하는 작성자를 다운로드 합니다.
* 사용할 수 있는 버전 번호가 가장 높은 및 패키지 목록에 현재 설치 된 버전 번호
* 업데이트 하 고 패키지 목록에서 제거 하는 빠른 설치를 허용 하도록 실행 단추
* 패키지 세부 정보 패널에 더 명확 하 게 실행 단추
* 패키지 세부 정보 패널에 패키지 업데이트 날짜
* 솔루션 뷰 패널 통합
* 프로젝트 및 솔루션 뷰에 설치 된 버전 번호의 정렬 가능한 표

## <a name="new-command-line-features"></a>새로운 명령줄 기능

이 버전에서 도입 되었습니다는 `add` 및 `init` 명령에 설명 된 대로 폴더 기반 저장소를 초기화 하는 [nuget.exe 참조](../tools/nuget-exe-cli-reference.md)합니다. 생성 되 고이 폴더와 유지 관리 하는 저장소는 구조 [성능을 크게 향상](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) 블로그에서에 설명 된 대로 합니다.

## <a name="contentfiles"></a>ContentFiles

콘텐츠를 사용할 수 이제 `project.json` 관리 되는 새로운 프로젝트 `contentFiles` 폴더 및 `.nuspec` `contentFiles` 요소 표기법입니다.  이 콘텐츠는 프로젝트 시스템과 상호 작용에 대 한 패키지 작성자가 보다 직접 지정할 수 있습니다.  콘텐츠 파일을 구성 하는 방법에 대 한 자세한 정보는 `.nuspec` 문서에서 확인할 수 있습니다는 [.nuspec 참조](../schema/nuspec.md)합니다.

## <a name="nuget-locals-cache-management"></a>NuGet 지역 캐시 관리

명령줄 NuGet 워크스테이션에서 로컬 캐시를 관리 하는 방법에 대 한 정보를 포함 하도록 업데이트 되었습니다.  지역 명령에 대 한 자세한 정보가 표시 됩니다는 [NuGet 명령줄 참조](../tools/cli-ref-locals.md)합니다.

## <a name="fixed-issues"></a>해결 된 문제

**주목할 만한 문제**

* NuGet 복원에 대 한 명령줄 복원된 지원 모노-에 솔루션 파일이 포함 된 패키지 [1543](https://github.com/NuGet/Home/issues/1543)

GitHub에서의 전체 목록은 3.3 릴리스에서 해결 된 문제를 찾을 수는 [3.3 마일스 톤](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)합니다.

3.3 명령줄 릴리스에서 해결 된 문제 목록에 기록 되는 [3.3 명령줄 마일스 톤](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)합니다.

## <a name="known-issues"></a>알려진 문제

찾을 수 있는 GitHub 문제 목록에서 문제를 추적 하려면 계속 하기: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)