---
title: 패키지를 설치하면 어떻게 되나요?
description: 패키지 설치 프로세스에 대한 자세한 정보
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 1ae030c308b14b8884fb608c1683c8c46000b0bd
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "77036905"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>NuGet 패키지를 설치하면 어떻게 되나요?

간단히 말하면 여러 NuGet 도구는 일반적으로 프로젝트 파일 또는 `packages.config`의 패키지에 대한 참조를 만든 다음, 패키지 복원을 수행하며, 결과적으로 패키지가 설치됩니다. 예외적으로 `nuget install`만 패키지를 `packages` 폴더로 확장하고 다른 파일은 수정하지 않습니다.

일반적인 과정은 다음과 같습니다.

1. (`nuget.exe`를 제외한 모든 도구) 패키지 식별자 및 버전을 프로젝트 파일 또는 `packages.config`에 기록합니다.

   설치 도구가 Visual Studio 또는 dotnet CLI인 경우 도구는 먼저 패키지를 설치하려고 시도합니다. 호환되지 않는 경우 패키지가 프로젝트 파일 또는 `packages.config`에 추가되지 않습니다.

2. 패키지 가져오기:
   - [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md)(전역 패키지 및 캐시 폴더 관리)에 설명된 대로 정확한 식별자 및 버전 번호로 패키지가 *global-packages* 폴더에 이미 설치되어 있는지 확인합니다.

   - 패키지가 *global-packages* 폴더에 없으면 [구성 파일](../consume-packages/Configuring-NuGet-Behavior.md)에 나열된 소스에서 검색하려고 합니다. 온라인 소스의 경우 `-NoCache`가 `nuget.exe` 명령에 지정되거나 `--no-cache`가 `dotnet restore`에 지정된 경우 외에는 먼저 HTTP 캐시에서 패키지를 검색하려고 합니다. (Visual Studio 및 `dotnet add package`는 항상 캐시를 사용합니다.) 패키지가 캐시에서 사용되는 경우 출력에 “CACHE”가 나타납니다. 캐시의 만료 시간은 30분입니다.

   - 패키지가 HTTP 캐시에 없으면 구성 파일에 나열된 소스에서 패키지를 다운로드하려고 합니다. 패키지가 다운로드되면 출력에 “GET” 및 “OK”가 나타납니다. NuGet은 보통 자세한 정도에 http 트래픽을 기록합니다.

   - 어떤 소스에서도 패키지를 가져올 수 없으면 이제 설치가 실패하고 [NU1103](../reference/errors-and-warnings/NU1103.md)과 같은 오류가 발생합니다. `nuget.exe` 명령의 오류에는 마지막으로 확인된 소스만 표시되지만 어떤 소스에서도 패키지를 사용할 수 없었음을 의미합니다.

   패키지를 가져올 때 다음과 같이 NuGet 구성의 소스 순서가 적용될 수 있습니다.

   - NuGet은 HTTP 소스를 확인하기 전에 로컬 폴더 및 네트워크 공유를 확인합니다.

3. [글로벌 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)에 설명된 대로 패키지의 복사본과 기타 정보를 *http-cache* 폴더에 저장합니다.

4. 다운로드되면 패키지를 사용자별 *global-packages* 폴더에 설치합니다. NuGet은 각 패키지 식별자에 대한 하위 폴더를 만든 다음, 설치된 각 패키지 버전에 대한 하위 폴더를 만듭니다.

5. NuGet은 필요에 따라 패키지 종속성을 설치합니다. [종속성 확인](../concepts/dependency-resolution.md)에 설명된 대로 이 프로세스에서 프로세스의 패키지 버전을 업데이트할 수 있습니다.

6. 다른 프로젝트 파일 및 폴더를 업데이트합니다.

    - PackageReference를 사용하는 프로젝트의 경우 `obj/project.assets.json`에 저장된 패키지 종속성 그래프를 업데이트합니다. 패키지 콘텐츠 자체는 프로젝트 폴더에 복사되지 않습니다.
    - 패키지에서 [소스 및 구성 파일 변환](../create-packages/source-and-config-file-transformations.md)을 사용하는 경우 `app.config` 및/또는 `web.config`를 업데이트합니다.

7. (Visual Studio만 해당) Visual Studio 창에서 사용 가능한 경우 패키지의 추가 정보 파일을 표시합니다.

NuGet 패키지를 사용하여 효율적인 코딩을 즐겨보세요!
