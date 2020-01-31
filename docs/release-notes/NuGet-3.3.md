---
title: NuGet 3.3 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 3.3에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa8290c80cc500b59d1779bf76662c07382fd277
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813782"
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 릴리스 정보

Nuget [3.2.1 릴리스 정보](../release-notes/nuget-3.2.1.md) | [NUGET 3.4-RC 릴리스 정보](../release-notes/nuget-3.4-RC.md)

NuGet 3.3는 NuGet 클라이언트에 대 한 유용한 픽스 모음 뿐만 아니라 많은 사용자 인터페이스 업데이트 및 명령줄 기능을 사용 하 여 11 월 30 2015 일에 출시 되었습니다.

## <a name="new-features"></a>새 기능

* NuGet 명령줄 클라이언트가 인증 된 피드를 사용 하 여 원활 하 게 작동할 수 있도록 하는 자격 증명 공급자가 도입 되었습니다. [Visual Studio Team Services 자격 증명 공급자를 설치](../reference/extensibility/nuget-exe-credential-providers.md) 하 고 nuget 클라이언트를 사용 하도록 구성 하는 방법에 대 한 지침은 nuget 문서에서 사용할 수 있습니다.

## <a name="new-user-interface-features"></a>새 사용자 인터페이스 기능

* 찾아보기, 설치 및 업데이트 사용 가능 탭 분리
* 사용 가능한 업데이트가 있는 패키지 수를 나타내는 사용 가능한 배지 업데이트
* 패키지가 설치 되어 있거나 업데이트를 사용할 수 있는지 여부를 나타내는 패키지 목록에서 배지 패키지
* 패키지 목록에 추가 된 다운로드 수 및 만든이
* 패키지 목록에서 사용 가능한 가장 높은 버전 번호 및 현재 설치 된 버전 번호
* 패키지 목록에서 빠른 설치, 업데이트 및 제거를 허용 하는 작업 단추
* 패키지 세부 정보 패널의 보다 선명한 작업 단추
* 패키지 세부 정보 패널의 패키지 업데이트 날짜
* 솔루션 보기에서 패널 통합
* 솔루션 보기에서 프로젝트 및 설치 된 버전 번호의 정렬 가능한 표

## <a name="new-command-line-features"></a>새 명령줄 기능

이 버전에는 [nuget.exe 참조](../reference/nuget-exe-cli-reference.md)에 설명 된 대로 폴더 기반 리포지토리를 초기화 하는 `add` 및 `init` 명령이 도입 되었습니다. 이 폴더 구조를 사용 하 여 생성 및 유지 관리 되는 리포지토리는 블로그에 설명 된 대로 [상당한 성능 이점을 제공](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) 합니다.

## <a name="contentfiles"></a>ContentFiles

이제 새 `contentFiles` 폴더 및 `.nuspec` `contentFiles` 요소 표기법을 통해 관리 되는 프로젝트 `project.json`에서 콘텐츠가 지원 됩니다.  이 콘텐츠는 프로젝트 시스템과의 상호 작용을 위해 패키지 작성자가 직접 지정할 수 있습니다.  `.nuspec` 문서에서 contentFiles를 구성 하는 방법에 대 한 자세한 내용은 [Nuspec 참조](../reference/nuspec.md)에서 확인할 수 있습니다.

## <a name="nuget-locals-cache-management"></a>NuGet 로컬 캐시 관리

NuGet 명령줄은 워크스테이션에서 로컬 캐시를 관리 하는 방법에 대 한 정보를 포함 하도록 업데이트 되었습니다.  로컬 명령에 대 한 자세한 내용은 [NuGet 명령줄 참조](../reference/cli-reference/cli-ref-locals.md)에서 확인할 수 있습니다.

## <a name="fixed-issues"></a>해결 된 문제

**주목할 만한 문제**

* NuGet 명령줄 복원- [1543](https://github.com/NuGet/Home/issues/1543) 의 솔루션 파일을 사용 하 여 패키지 복원 지원

3\.3 릴리스에서 해결 된 문제에 대 한 전체 목록은 GitHub의 [3.3 마일스 톤](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)에서 찾을 수 있습니다.

3\.3 명령줄 릴리스에서 해결 된 문제 목록은 [3.3 명령줄 마일스 톤](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)에 기록 됩니다.

## <a name="known-issues"></a>알려진 문제점

Microsoft는 GitHub 문제 목록에서 찾을 수 있는 문제를 계속 추적 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)