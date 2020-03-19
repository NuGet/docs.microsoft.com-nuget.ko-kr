---
title: NuGet에서 전역 패키지, 캐시, 임시 폴더를 관리하는 방법
description: 패키지를 설치, 복원 및 업데이트할 때 사용되는 컴퓨터에 있는 전역 패키지 설치 폴더, 패키지 캐시 및 임시 폴더를 관리하는 방법입니다.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428590"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>전역 패키지, 캐시 및 임시 폴더 관리

패키지를 설치, 업데이트 또는 복원할 때마다 NuGet은 프로젝트 구조 외부의 여러 폴더에서 패키지 및 패키지 정보를 관리합니다.

| 이름 | 설명 및 위치(사용자별)|
| --- | --- |
| global&#8209;packages | *global-packages* 폴더는 NuGet이 다운로드한 패키지를 설치하는 위치입니다. 각 패키지는 패키지 식별자 및 버전 번호와 일치하는 하위 폴더로 완전히 확장됩니다. [PackageReference](package-references-in-project-files.md) 형식을 사용하는 프로젝트는 항상 이 폴더의 직접 패키지를 직접 사용합니다. [packages.config](../reference/packages-config.md)를 사용할 경우 패키지가 *global-packages* 폴더에 설치된 다음, 프로젝트의 `packages` 폴더에 복사됩니다.<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>NUGET_PACKAGES 환경 변수 `globalPackagesFolder` 또는 `repositoryPath`[구성 설정](../reference/nuget-config-file.md#config-section)(각각 PackageReference 및 `packages.config`를 사용할 경우) 또는 `RestorePackagesPath` MSBuild 속성(MSBuild에만 해당)을 사용하여 재정의합니다. 환경 변수가 구성 설정보다 우선 합니다.</li></ul> |
| http&#8209;cache | Visual Studio 패키지 관리자(NuGet 3.x 이상) 및 `dotnet` 도구는 다운로드한 패키지의 복사본을 이 캐시에 `.dat` 파일로 저장하고, 각 패키지 소스에 대해 하위 폴더를 구성합니다. 패키지는 확장되지 않으며 캐시의 만료 시간은 30분입니다.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>NUGET_HTTP_CACHE_PATH 환경 변수를 사용하여 재정의합니다.</li></ul> |
| temp | NuGet이 다양한 작업을 수행하는 중 임시 파일을 저장하는 폴더입니다.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |
| plugins-cache **4.8+** | NuGet이 작업 클레임 요청의 결과를 저장하는 폴더입니다.<br/><ul><li>Windows: `%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/plugins-cache`</li><li>NUGET_PLUGINS_CACHE_PATH 환경 변수를 사용하여 재정의합니다.</li></ul> |

> [!Note]
> NuGet 3.5 이전에서는 `%localappdata%\NuGet\Cache`에 있는 *http-cache* 대신 *packages-cache*를 사용합니다.

NuGet은 캐시 및 *global-packages* 폴더를 사용하여 일반적으로 컴퓨터에 있는 이미 있는 패키지 다운로드를 방지하여 설치, 업데이트 및 복원 작업의 성능을 개선합니다. PackageReference를 사용하는 경우 *global-packages* 폴더는 다운로드한 패키지를 프로젝트 폴더 내에 보관하는 것도 막아 이러한 패키지가 소스 제어에 실수로 추가될 수 있는 문제를 방지하고 NuGet이 컴퓨터 스토리지에 미치는 전반적인 영향도 줄입니다.

패키지를 검색하라는 요청을 받으면 NuGet은 먼저 *global-packages* 폴더를 찾습니다. 정확한 버전의 패키지가 없는 경우 NuGet은 모든 비 HTTP 패키지 소스를 확인합니다. 그래도 패키지를 못 찾으면 NuGet은 `dotnet.exe` 명령에 `--no-cache` 또는 `nuget.exe` 명령에 `-NoCache`를 지정하지 않은 경우 *http-cache*에서 패키지를 찾습니다. 패키지가 캐시에 없거나 캐시가 사용되지 않는 경우에는 NuGet은 HTTP를 통해 패키지를 검색합니다.

자세한 내용은 [패키지를 설치하면 어떻게 되나요?](../concepts/package-installation-process.md)를 참조하세요.

## <a name="viewing-folder-locations"></a>폴더 위치 보기

[nuget locals 명령](../reference/cli-reference/cli-ref-locals.md)을 사용하여 위치를 확인할 수 있습니다.

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

일반적인 출력(Windows. “user1”은 현재 사용자 이름):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

(`package-cache`는 NuGet 2.x에서 사용되며 NuGet 3.5 이전 버전에서 표시됩니다. )

[dotnet nuget locals 명령](/dotnet/core/tools/dotnet-nuget-locals)을 사용하여 폴더 위치를 확인할 수도 있습니다.

```dotnetcli
dotnet nuget locals all --list
```

일반적인 출력(Mac/Linux. “user1”은 현재 사용자 이름):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

단일 폴더의 위치를 표시하려면 `all` 대신`http-cache`, `global-packages`, `temp` 또는 `plugins-cache`를 사용합니다.

## <a name="clearing-local-folders"></a>로컬 폴더 지우기

패키지 설치 문제가 발생하는 경우 또는 원격 갤러리의 패키지를 설치하려는 경우 `locals --clear`(dotnet.exe) 또는 `locals -clear`(nuget.exe) 옵션을 사용하여 지울 폴더를 지정하거나 `all`을 사용하여 모든 폴더를 지웁니다.

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

현재 Visual Studio에서 열려 있는 프로젝트에서 사용되는 모든 패키지는 *global-packages* 폴더에서 지워지지 않습니다.

Visual Studio 2017부터 **도구 > NuGet 패키지 관리자 > 패키지 관리자 설정** 메뉴 명령을 사용한 다음, **모든 NuGet 캐시 지우기**를 선택합니다. 캐시 관리는 현재 패키지 관리자 콘솔을 통해 사용할 수 없습니다. Visual Studio 2015에서 CLI 명령을 대신 사용합니다.

![캐시를 지우기 위한 NuGet 옵션 명령](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>오류 문제 해결

`nuget locals` 또는 `dotnet nuget locals`를 사용하는 경우 다음과 같은 오류가 발생할 수 있습니다.

- ‘오류: *이 프로세스는 <package>다른 프로세스에서 사용 중* 또는 *로컬 리소스 지우기 실패: 하나 이상의 파일을 삭제할 수 없음*으로 인해 파일에 액세스할 수 없습니다.

    폴더에 있는 하나 이상의 파일이 다른 프로세스에서 사용 중입니다. 예를 들어 *global-packages* 폴더의 패키지를 참조하는 Visual Studio 프로젝트가 열려 있습니다. 해당 프로세스를 닫고 다시 시도합니다.

- ‘오류: *<path>* 경로에 대한 액세스가 거부되었습니다 또는 *디렉터리가 비어 있지 않습니다’* .

    캐시에서 파일을 삭제할 수 있는 권한이 없습니다. 가능한 경우 폴더 권한을 변경하고 다시 시도합니다. 또는 시스템 관리자에게 문의하세요.

- ‘오류: *지정된 경로, 파일 이름 중 하나 또는 둘 다가 너무 깁니다. 정규화된 파일 이름은 260자 미만이어야 하며 디렉터리 이름은 248자 미만이어야 합니다.*

    폴더 이름을 줄이고 다시 시도하세요.
