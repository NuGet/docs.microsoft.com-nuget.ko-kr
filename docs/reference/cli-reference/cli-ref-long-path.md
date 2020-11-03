---
title: NuGet CLI 긴 경로 지원
description: nuget.exe 긴 경로 지원에 대 한 참조
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 1143da911c80125a9d60e4b98798b11871e9988a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238194"
---
# <a name="long-path-support-nuget-cli"></a>긴 경로 지원 (NuGet CLI)

**적용 대상:** &bullet; **지원 되는 모든 버전:** 4.8 +

NuGet.exe 4.8 이상에서는 파일 경로를 필요로 하는 팩, 복원, 설치 및 기타 대부분의 시나리오에서 파일 및 디렉터리에 대 한 긴 경로를 지원 합니다.

## <a name="required-operating-system"></a>필수 운영 체제

-   Windows 10 (버전 1607 이상)
-   .NET Framework 버전 4.6.2 이상으로 업그레이드 하는 경우에는 Windows 10 (7 월 2015 릴리스 또는 1511 버전)입니다.
-   Windows Server 2016 (모든 버전)

## <a name="enable-win32-long-paths-group-policy"></a>"Win32 긴 경로"를 사용 하도록 설정 그룹 정책

그룹 정책을 설정 하 여 이러한 시스템에서 긴 경로 지원을 사용 하도록 설정 해야 합니다.

단계:
1. **그룹 정책 편집기** 시작 검색 창에서 "그룹 정책 편집"을 입력 하거나 실행 명령 (Windows-R)에서 "gpedit.msc"를 실행 합니다.
2. **로컬 그룹 정책 편집기** 에서 "로컬 컴퓨터 정책/컴퓨터 구성/관리 템플릿/모든 설정/Win32 긴 경로 사용"을 사용 하도록 설정 합니다.

![긴 경로 정책](media/LongPathPolicy.png)


> [!Note]
> 다른 NuGet 도구가 긴 경로를 지원 하도록 설정
>
> -   Dotnet CLI는 운영 체제 또는 버전에 관계 없이 긴 경로를 지원 합니다.
> -   Visual Studio 또는 `msbuild -t:restore` 는 긴 경로를 아직 지원 하지 않습니다.
> -   NuGet 라이브러리를 사용 하 여 복원 및 기타 명령을 실행 하는 소프트웨어는 NuGet.exe 작동 하는 동일한 시스템에서 긴 경로를 지원 합니다. 또한 `longPathAware` windows 매니페스트에서를 설정 하 고 `UseLegacyPathHandling` 를 통해로 구성 하는 경우 `false` [추가 정보를 확인할](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10) App.Config