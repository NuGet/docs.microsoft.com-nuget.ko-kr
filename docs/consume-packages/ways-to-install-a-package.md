---
title: "NuGet 패키지 설치 방법 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/30/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "디스크 및 적용 가능한 프로젝트 파일에서 수행되는 작업을 포함하여 NuGet 패키지를 프로젝트에 설치하는 프로세스를 설명합니다."
keywords: "NuGet 설치, NuGet 패키지 사용, NuGet 패키지 설치, NuGet 패키지 참조"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e48bbe813168e773bc46b7fe25af29785ff75df
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>NuGet 패키지를 설치하는 다양한 방법

NuGet 패키지는 다음 방법 중 하나를 사용하여 다운로드 및 설치됩니다(아직 설치하지 않은 경우 [NuGet 클라이언트 도구 설치](../install-nuget-client-tools.md) 참조).

| 메서드 | 설명 |
| --- | --- |
| dotnet.exe CLI<br/>`dotnet install <package_name>` | (모든 플랫폼) \<package_name\>으로 식별되는 패키지를 다운로드하고, 해당 콘텐츠를 현재 디렉터리의 폴더로 확장하고, 참조를 프로젝트 파일에 추가합니다. 또한 종속성을 다운로드 및 설치합니다.<ul><li>[패키지 설치 및 사용(dotnet CLI)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[dotnet 명령](../tools/dotnet-commands.md)</li></ul> |
| 패키지 관리자 UI(Visual Studio) | (Windows 및 Mac) 패키지와 종속성을 찾고, 선택하고, 프로젝트에 설치할 수 있는 UI를 제공합니다. 설치된 패키지에 대한 참조를 프로젝트 파일에 추가합니다.<ul><li>[패키지 설치 및 사용(Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[패키지 관리자 UI 참조(Windows)](../tools/package-manager-ui.md)</li><li>[프로젝트에 NuGet 패키지 포함(Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| 패키지 관리자 콘솔(Visual Studio)<br/>`Install-Package <package_name>` | (Windows만) \<package_name\>으로 식별되는 패키지를 다운로드하여 솔루션의 지정된 프로젝트에 설치하고 참조를 프로젝트 파일에 추가합니다. 또한 종속성을 다운로드 및 설치합니다.<ul><li>[패키지 설치 및 사용(Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[패키지 관리자 콘솔 가이드](../tools/package-manager-console.md)</li></ul> |
| nuget.exe CLI<br/>`nuget install <package_name>` | (모든 플랫폼) \<package_name\>으로 식별되는 패키지를 다운로드하고 해당 콘텐츠를 현재 디렉터리의 폴더로 확장합니다. `packages.config` 파일에 나열된 모든 패키지를 다운로드할 수도 있습니다. 또한 종속성을 다운로드하고 설치하지만 프로젝트 파일을 변경하지 않습니다.<ul><li>[install 명령](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a>일반 설치 프로세스

일반적으로 NuGet은 패키지를 설치하기 전에 다음을 수행합니다.

1. 패키지 가져오기:
    - 요청된 패키지가 이미 캐시에 있는지 확인합니다([NuGet 캐시 관리](managing-the-nuget-cache.md) 참조).
    - 패키지가 캐시에 없으면 구성 파일에 나열된 소스에서, 목록의 첫 번째부터 패키지를 다운로드하려고 합니다. 이 동작을 사용하면 nuget.org에서 패키지를 검색하기 전에 전용 패키지 피드를 사용할 수 있습니다([NuGet 동작 구성](configuring-nuget-behavior.md) 참조).
    - 소스 중 하나에서 패키지를 성공적으로 가져오면 NuGet이 패키지를 캐시에 추가합니다. 그렇지 않으면 설치에 실패합니다.

1. 패키지를 프로젝트로 확장합니다.
    - 확장이란 압축된 패키지의 콘텐츠를 적절한 하위 폴더로 푸는 것을 의미합니다. `.nupkg` 자체의 복사본도 하위 폴더에 있습니다.
    - 패키지를 Visual Studio 또는 .NET Core 프로젝트에 설치하는 경우 프로젝트의 대상 프레임워크와 관련된 파일만 확장됩니다. nuget.exe 명령줄을 사용하여 설치하면 모든 어셈블리가 확장됩니다.

1. 패키지가 Visual Studio 또는 dotnet CLI 내에 설치되면 참조가 해당 프로젝트 파일(또는 Visual Studio에 있는 일부 프로젝트 형식의 경우 `packages.config`)에 추가됩니다.

## <a name="related-topics"></a>관련 항목

- [패키지 사용 개요 및 워크플로](../consume-packages/overview-and-workflow.md)
- [패키지 찾기 및 선택](../consume-packages/finding-and-choosing-packages.md)
- [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)
- [NuGet 캐시 관리](managing-the-nuget-cache.md)
