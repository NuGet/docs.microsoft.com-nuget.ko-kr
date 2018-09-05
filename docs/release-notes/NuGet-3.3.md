---
title: NuGet 3.3 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하는 NuGet 3.3 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546649"
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 릴리스 정보

[NuGet 3.2.1 릴리스 정보](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC 릴리스 정보](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 많은 NuGet 클라이언트에 유용한 픽스 모음이 뿐만 아니라 사용자 인터페이스 업데이트 및 명령줄 기능을 사용 하 여 2015 년 11 월 30 년에 출시 되었습니다.

## <a name="new-features"></a>새 기능

* NuGet 명령줄 클라이언트를 인증 된 피드를 원활 하 게 작업할 수 있도록 자격 증명 공급자 도입 되었습니다. [Visual Studio Team Services를 설치 하는 방법에 대 한 지침 공급자 자격 증명 ](../api/nuget-exe-credential-providers.md) NuGet 구성 및 사용 하도록 클라이언트를 NuGet 문서에서 사용할 수 있습니다.

## <a name="new-user-interface-features"></a>새로운 사용자 인터페이스 기능

* 찾아보기, 설치 및 사용 가능한 업데이트에 대 한 별도 탭
* 사용 가능한 업데이트가 있는 패키지 수를 나타내는 사용 가능한 배지 업데이트
* 패키지 설치에 사용 가능한 업데이트가 하는지 여부를 나타내기 위해 패키지 목록에서 패키지 배지
* 개수 및 패키지 목록에 추가 하는 작성자를 다운로드 합니다.
* 최대 사용 가능한 버전 및 패키지 목록에 현재 설치 된 버전 번호
* 빠른 설치를 허용 하도록 실행 단추 업데이트 및 패키지 목록에서 제거
* 패키지 세부 정보 패널에 명확 하 게 실행 단추
* 패키지 세부 정보 패널에서 패키지 업데이트 날짜
* 솔루션 보기에서 패널 통합
* 프로젝트 및 솔루션 보기에서 설치 된 버전 번호의 정렬 가능한 표

## <a name="new-command-line-features"></a>새 명령줄 기능

이 버전에서 도입 되었습니다 합니다 `add` 및 `init` 에 설명 된 대로 폴더 기반 리포지토리를 초기화 하는 명령 합니다 [nuget.exe 참조](../tools/nuget-exe-cli-reference.md)합니다. 생성 되 고이 폴더를 사용 하 여 유지 관리 하는 리포지토리는 구조체 [성능을 크게 향상](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) 블로그에서 설명한 대로 합니다.

## <a name="contentfiles"></a>contentFiles

콘텐츠는 이제 지원 `project.json` 관리 되는 새로운 프로젝트 `contentFiles` 폴더와 `.nuspec` `contentFiles` 요소 표기법입니다.  이 콘텐츠는 프로젝트 시스템과 상호 작용에 대 한 패키지 작성자가 직접 더 지정할 수 있습니다.  contentFiles를 구성 하는 방법에 대 한 자세한 정보를 `.nuspec` 문서에서 찾을 수 있습니다 합니다 [.nuspec 참조](../reference/nuspec.md)합니다.

## <a name="nuget-locals-cache-management"></a>로컬 NuGet 캐시 관리

NuGet 명령줄을 워크스테이션의 로컬 캐시를 관리 하는 방법에 대 한 정보를 포함 하도록 업데이트 되었습니다.  로컬 명령에 대 한 자세한 정보는 사용할 수 있습니다 합니다 [NuGet 명령줄 참조](../tools/cli-ref-locals.md)합니다.

## <a name="fixed-issues"></a>수정 된 문제

**주목할 만한 문제**

* Mono-에서 솔루션 파일을 사용 하 여 패키지 복원에 대 한 NuGet 명령줄 복원된 지원 [1543](https://github.com/NuGet/Home/issues/1543)

3.3 릴리스에서 해결 된 문제의 전체 목록은 GitHub에서 찾을 수 있습니다 합니다 [3.3 마일스 톤](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)합니다.

3.3 명령줄 릴리스에서 해결 된 문제 목록에 기록 되는 [3.3 명령줄 마일스 톤](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)합니다.

## <a name="known-issues"></a>알려진 문제

찾을 수 있는 GitHub 문제 목록에서 문제를 추적 하려면 계속 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)