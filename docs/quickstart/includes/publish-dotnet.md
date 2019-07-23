---
ms.openlocfilehash: bb39e1056ea97ecf1ac70d7fd8e79e65dc04655c
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842132"
---
1. <span data-ttu-id="6a306-101">`.nupkg` 파일을 포함하는 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6a306-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="6a306-102">다음 명령을 실행하여 패키지 이름(고유한 패키지 ID)을 지정하고 키 값을 API 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6a306-102">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="6a306-103">dotnet은 게시 프로세스의 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6a306-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="6a306-104">[dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a306-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>