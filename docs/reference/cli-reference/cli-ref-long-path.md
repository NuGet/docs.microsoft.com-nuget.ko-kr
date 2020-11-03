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
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="72ad9-103">긴 경로 지원 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="72ad9-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="72ad9-104">**적용 대상:** &bullet; **지원 되는 모든 버전:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="72ad9-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="72ad9-105">NuGet.exe 4.8 이상에서는 파일 경로를 필요로 하는 팩, 복원, 설치 및 기타 대부분의 시나리오에서 파일 및 디렉터리에 대 한 긴 경로를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="72ad9-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="72ad9-106">필수 운영 체제</span><span class="sxs-lookup"><span data-stu-id="72ad9-106">Required Operating System</span></span>

-   <span data-ttu-id="72ad9-107">Windows 10 (버전 1607 이상)</span><span class="sxs-lookup"><span data-stu-id="72ad9-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="72ad9-108">.NET Framework 버전 4.6.2 이상으로 업그레이드 하는 경우에는 Windows 10 (7 월 2015 릴리스 또는 1511 버전)입니다.</span><span class="sxs-lookup"><span data-stu-id="72ad9-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="72ad9-109">Windows Server 2016 (모든 버전)</span><span class="sxs-lookup"><span data-stu-id="72ad9-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="72ad9-110">"Win32 긴 경로"를 사용 하도록 설정 그룹 정책</span><span class="sxs-lookup"><span data-stu-id="72ad9-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="72ad9-111">그룹 정책을 설정 하 여 이러한 시스템에서 긴 경로 지원을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72ad9-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="72ad9-112">단계:</span><span class="sxs-lookup"><span data-stu-id="72ad9-112">Steps:</span></span>
1. <span data-ttu-id="72ad9-113">**그룹 정책 편집기** 시작 검색 창에서 "그룹 정책 편집"을 입력 하거나 실행 명령 (Windows-R)에서 "gpedit.msc"를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="72ad9-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="72ad9-114">**로컬 그룹 정책 편집기** 에서 "로컬 컴퓨터 정책/컴퓨터 구성/관리 템플릿/모든 설정/Win32 긴 경로 사용"을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="72ad9-114">In the **Local Group Policy Editor** , enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![긴 경로 정책](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="72ad9-116">다른 NuGet 도구가 긴 경로를 지원 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="72ad9-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="72ad9-117">Dotnet CLI는 운영 체제 또는 버전에 관계 없이 긴 경로를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="72ad9-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="72ad9-118">Visual Studio 또는 `msbuild -t:restore` 는 긴 경로를 아직 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72ad9-118">Visual Studio or `msbuild -t:restore` does not yet support long paths.</span></span>
> -   <span data-ttu-id="72ad9-119">NuGet 라이브러리를 사용 하 여 복원 및 기타 명령을 실행 하는 소프트웨어는 NuGet.exe 작동 하는 동일한 시스템에서 긴 경로를 지원 합니다. 또한 `longPathAware` windows 매니페스트에서를 설정 하 고 `UseLegacyPathHandling` 를 통해로 구성 하는 경우 `false` [추가 정보를 확인할](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10) App.Config</span><span class="sxs-lookup"><span data-stu-id="72ad9-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set `longPathAware` in their windows manifest and configure `UseLegacyPathHandling` to `false` via App.Config [See more information](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)</span></span>