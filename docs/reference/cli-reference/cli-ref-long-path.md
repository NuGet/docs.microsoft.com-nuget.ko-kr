---
title: NuGet CLI 긴 경로 지원
description: Nuget.exe 긴 경로 지원에 대 한 참조
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327680"
---
# <a name="long-path-support-nuget-cli"></a>긴 경로 지원 (NuGet CLI)

**적용 대상:** 지원 &bullet; 되는 모든 **버전:** 4.8 +

NuGet .exe 4.8 이상에서는 파일 경로를 필요로 하는 팩, 복원, 설치 및 기타 대부분의 시나리오에서 파일 및 디렉터리에 대 한 긴 경로를 지원 합니다.

## <a name="required-operating-system"></a>필수 운영 체제

-   Windows 10 (버전 1607 이상)
-   .NET Framework 버전 4.6.2 이상으로 업그레이드 하는 경우에는 Windows 10 (7 월 2015 릴리스 또는 1511 버전)입니다.
-   Windows Server 2016 (모든 버전)

## <a name="enable-win32-long-paths-group-policy"></a>"Win32 긴 경로"를 사용 하도록 설정 그룹 정책

그룹 정책을 설정 하 여 이러한 시스템에서 긴 경로 지원을 사용 하도록 설정 해야 합니다.

위한
1. **그룹 정책 편집기** 시작 검색 창에서 "그룹 정책 편집"을 입력 하거나 실행 명령 (Windows-R)에서 "gpedit.msc"를 실행 합니다.
2. **로컬 그룹 정책 편집기**에서 "로컬 컴퓨터 정책/컴퓨터 구성/관리 템플릿/모든 설정/Win32 긴 경로 사용"을 사용 하도록 설정 합니다.

![긴 경로 정책](media/LongPathPolicy.png)


> [!Note]
> 다른 NuGet 도구가 긴 경로를 지원 하도록 설정
>
> -   Dotnet CLI는 운영 체제 또는 버전에 관계 없이 긴 경로를 지원 합니다.
> -   Visual Studio 또는 msbuild t:restore는 긴 경로를 아직 지원 하지 않습니다.
> -   NuGet 라이브러리를 사용 하 여 복원 및 기타 명령을 실행 하는 소프트웨어는 windows 매니페스트에서 UseLegacyPathHandling를 설정 하 고 App.config [를 통해 false로 구성 하는 경우 nuget.exe가 작동 하는 동일한 시스템에서 긴 경로를 지원 합니다. 자세한 정보 보기](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

