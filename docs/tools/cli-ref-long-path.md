---
title: NuGet CLI 긴 경로 지원
description: Nuget.exe 긴 경로 지원에 대 한 참조
author: zhili1208
ms.author: lzhi
manager: rob
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 0119be3fd8fd6c2e06e0135de5e498e0730bb0cc
ms.sourcegitcommit: a76ecc58f41c2c5b3536ff4a3f3fcbdf5258177c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39072734"
---
# <a name="long-path-support-nuget-cli"></a>긴 경로 지원 (NuGet CLI)

**적용 대상:** 모든 &bullet; **지원 되는 버전:** 4.8 이상

팩, 복원, 설치 및 파일 경로 해야 하는 대부분의 시나리오를 같은 파일에 대 한 NuGet.exe 4.8 이상을 지원 긴 경로 및 시나리오에 대 한 디렉터리입니다.

## <a name="required-operating-system"></a>필수 운영 체제

-   Windows 10 (버전 1607 이상)
-   Windows 10 (2015 년 7 월 릴리스 또는 버전 1511).NET Framework 버전 4.6.2로 업그레이드 하는 경우 이상.
-   Windows Server 2016 (모든 버전)

## <a name="enable-win32-long-paths-group-policy"></a>"Win32 긴 경로" 그룹 정책을 사용 하도록 설정

그룹 정책을 설정 하 여 해당 시스템에 긴 경로 지원을 사용 하도록 설정 해야 합니다.

단계:
1. 시작할 **그룹 정책 편집기** -시작 검색 표시줄에서 "그룹 정책 편집"을 입력 하거나 실행 명령 (Windows-R)에서 "gpedit.msc"를 실행 합니다.
2. 에 **로컬 그룹 정책 편집기**, 사용 "로컬 컴퓨터 정책/컴퓨터 구성/관리 템플릿/모든 책갈피 사용 설정/Win32 긴 경로"입니다.

![긴 경로 정책](media/LongPathPolicy.png)


> [!Note]
> 긴 경로 지원 하기 위해 다른 NuGet 도구를 사용 하도록 설정
>
> -   Dotnet CLI 버전 또는 운영 체제에 관계 없이 긴 경로 지원합니다.
> -   Visual Studio 또는 msbuild /t: restore가 긴 경로 아직 지원 하지 않습니다.
> -   NuGet 라이브러리를 사용 하 여 복원 및 다른 명령을 실행 하는 소프트웨어는 지원 긴 경로 동일한 시스템에서 NuGet.exe에서 작동 하는 설정 하는 경우 창에 longPathAware 매니페스트 하 고 UseLegacyPathHandling App.Config통해false로구성[ 자세한 내용은 참조 하세요.](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

