---
title: NuGet 패키지를 설치하는 방법
description: 디스크 및 적용 가능한 프로젝트 파일에서 수행되는 작업을 포함하여 NuGet 패키지를 프로젝트에 설치하는 프로세스를 설명합니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 02/12/2018
ms.topic: overview
ms.openlocfilehash: 028fb9710e808974348d9cca3c56103c087d5390
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>NuGet 패키지를 설치하는 다양한 방법

NuGet 패키지는 다음 표의 방법 중 하나를 사용하여 다운로드 및 설치됩니다(아직 설치하지 않은 경우 [NuGet 클라이언트 도구 설치](../install-nuget-client-tools.md) 참조). 패키지를 다운로드하는 대신 캐시에서 검색할 수도 있습니다.

| 메서드 | 설명 |
| --- | --- |
| dotnet.exe CLI<br/>`dotnet add package <package_name>` | (모든 플랫폼) \<package_name\>으로 식별되는 패키지를 검색하고, 해당 콘텐츠를 현재 디렉터리의 폴더로 확장하고, 참조를 프로젝트 파일에 추가합니다. 종속성도 검색하고 설치합니다.<ul><li>[패키지 설치 및 사용(dotnet CLI)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[dotnet add package 명령](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| 패키지 관리자 UI(Visual Studio) | (Windows 및 Mac) 지정된 패키지 소스에서 패키지와 종속성을 찾고, 선택하고, 프로젝트에 설치할 수 있는 UI를 제공합니다. 설치된 패키지에 대한 참조를 프로젝트 파일에 추가합니다.<ul><li>[패키지 설치 및 사용(Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[패키지 관리자 UI 참조(Windows)](../tools/package-manager-ui.md)</li><li>[프로젝트에 NuGet 패키지 포함(Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| 패키지 관리자 콘솔(Visual Studio)<br/>`Install-Package <package_name>` | (Windows만) 선택된 소스에서 \<package_name\>으로 식별되는 패키지를 검색하여 솔루션의 지정된 프로젝트에 설치하고 참조를 프로젝트 파일에 추가합니다. 종속성도 검색하고 설치합니다.<ul><li>[패키지 설치 및 사용(Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[패키지 관리자 콘솔 가이드](../tools/package-manager-console.md)</li></ul> |
| nuget.exe CLI<br/>`nuget install <package_name>` | (모든 플랫폼) \<package_name\>으로 식별되는 패키지를 검색하고 해당 콘텐츠를 현재 디렉터리의 폴더로 확장합니다. `packages.config` 파일에 나열된 모든 패키지를 검색할 수도 있습니다. 종속성도 검색하고 설치하지만 프로젝트 파일 또는 `packages.config`는 변경하지 않습니다.<ul><li>[install 명령](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>패키지를 설치하면 어떻게 되나요?

간단히 말하면 여러 NuGet 도구는 일반적으로 프로젝트 파일 또는 `packages.config`의 패키지에 대한 참조를 만든 다음, 패키지 복원을 수행하며, 결과적으로 패키지가 설치됩니다. 예외적으로 `nuget install`만 패키지를 `packages` 폴더로 확장하고 다른 파일은 수정하지 않습니다.

일반적인 과정은 다음과 같습니다.

1. (`nuget.exe`를 제외한 모든 도구) 패키지 ID 및 버전을 프로젝트 파일 또는 `packages.config`에 기록합니다.

2. 패키지 가져오기:
   - [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md)(전역 패키지 및 캐시 폴더 관리)에 설명된 대로 정확한 식별자 및 버전 번호로 패키지가 *global-packages* 폴더에 이미 설치되어 있는지 확인합니다.

   - 패키지가 *global-packages* 폴더에 없으면 [구성 파일](Configuring-NuGet-Behavior.md)에 나열된 소스에서 검색하려고 합니다. 온라인 소스의 경우 `-NoCache`가 `nuget.exe` 명령에 지정되거나 `--no-cache`가 `dotnet restore`에 지정된 경우 외에는 먼저 캐시에서 패키지를 검색하려고 합니다. (Visual Studio 및 `dotnet add package`는 항상 캐시를 사용합니다.) 패키지가 캐시에서 사용되는 경우 출력에 “CACHE”가 나타납니다. 캐시의 만료 시간은 30분입니다.

   - 패키지가 캐시에 없으면 구성 파일에 나열된 소스에서 패키지를 다운로드하려고 합니다. 패키지가 다운로드되면 출력에 “GET” 및 “OK”가 나타납니다.

   - 어떤 소스에서도 패키지를 가져올 수 없으면 이제 설치가 실패하고 [NU1103](../reference/errors-and-warnings.md#nu1103)과 같은 오류가 발생합니다. `nuget.exe` 명령의 오류에는 마지막으로 확인된 소스만 표시되지만 어떤 소스에서도 패키지를 사용할 수 없었음을 의미합니다.

   패키지를 가져올 때 다음과 같이 NuGet 구성의 소스 순서가 적용될 수 있습니다.

   - PackageReference 형식을 사용하는 프로젝트의 경우 NuGet은 HTTP 소스를 확인하기 전에 로컬 폴더 및 네트워크 공유를 확인합니다.

   - `packages.config` 관리 형식을 사용하는 프로젝트의 경우 NuGet은 구성의 소스 순서를 사용합니다. 예외적으로 복원 작업의 경우 소스 순서가 무시되고 NuGet은 무엇이든 먼저 응답하는 소스의 패키지를 사용합니다.

   - 일반적으로 특정 식별자 및 버전 번호를 갖는 모든 패키지는 어떤 원본에서 찾든 똑같으므로 NuGet이 원본을 확인하는 순서는 특별히 중요하지는 않습니다.

3. (`nuget.exe`를 제외한 모든 도구) [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md)(전역 패키지 및 캐시 폴더 관리)에 설명된 대로 패키지의 복사본과 기타 정보를 *http-cache* 폴더에 저장합니다.

4. 다운로드되면 패키지를 사용자별 *global-packages* 폴더에 설치합니다. NuGet은 각 패키지 식별자에 대한 하위 폴더를 만든 다음, 설치된 각 패키지 버전에 대한 하위 폴더를 만듭니다.

5. 다른 프로젝트 파일 및 폴더를 업데이트합니다.

    - PackageReference를 사용하는 프로젝트의 경우 `obj/project.assets.json`에 저장된 패키지 종속성 그래프를 업데이트합니다. 패키지 콘텐츠 자체는 프로젝트 폴더에 복사되지 않습니다.
    - `packages.config`를 사용하는 프로젝트의 경우 프로젝트의 대상 프레임워크와 일치하는 확장 패키지의 해당 부분을 프로젝트의 `packages` 폴더로 복사합니다. (`nuget install`을 사용할 경우 `nuget.exe`는 프로젝트 파일을 검사하여 대상 프레임워크를 확인하지 않으므로 확장된 패키지 전체가 복사됩니다.)
    - 패키지에서 [소스 및 구성 파일 변환](../create-packages/source-and-config-file-transformations.md)을 사용하는 경우 `app.config` 및/또는 `web.config`를 업데이트합니다.

6. 하위 수준 종속성이 아직 프로젝트에 없는 경우 모두 설치합니다. [종속성 확인](../consume-packages/dependency-resolution.md)에 설명된 대로 이 프로세스에서 프로세스의 패키지 버전을 업데이트할 수 있습니다.

7. (Visual Studio만 해당) Visual Studio 창에서 사용 가능한 경우 패키지의 추가 정보 파일을 표시합니다.

## <a name="related-articles"></a>관련 문서

- [패키지 사용 개요 및 워크플로](../consume-packages/overview-and-workflow.md)
- [패키지 찾기 및 선택](../consume-packages/finding-and-choosing-packages.md)
- [Managing the NuGet cache and global-packages folders](managing-the-global-packages-and-cache-folders.md)(NuGet 캐시 및 global-packages 폴더 관리)
- [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)
