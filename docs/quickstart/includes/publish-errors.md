---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496022"
---
<span data-ttu-id="3b515-101">`push` 명령의 오류는 일반적으로 문제를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b515-101">Errors from the `push` command typically indicate the problem.</span></span> <span data-ttu-id="3b515-102">예를 들어 프로젝트에서 버전 번호를 업데이트하는 것을 잊었을 수 있고 이미 존재하는 패키지를 게시하려고 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b515-102">For example, you may have forgotten to update the version number in your project and are therefore trying to publish a package that already exists.</span></span>

<span data-ttu-id="3b515-103">또한 호스트에 이미 존재하는 식별자를 사용하여 패키지를 게시하려고 하면 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b515-103">You also see errors when trying to publish a package using an identifier that already exists on the host.</span></span> <span data-ttu-id="3b515-104">예를 들어 이름 “AppLogger”가 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b515-104">The name "AppLogger", for example, already exists.</span></span> <span data-ttu-id="3b515-105">이러한 경우 `push` 명령은 다음 오류를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b515-105">In such a case, the `push` command gives the following error:</span></span>

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

<span data-ttu-id="3b515-106">방금 만든 유효한 API 키를 사용하는 경우 이 메시지는 오류의 “사용 권한” 부분에서 완전히 지워지지 않은 명명 충돌을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b515-106">If you're using a valid API key that you just created, then this message indicates a naming conflict, which isn't entirely clear from the "permission" part of the error.</span></span> <span data-ttu-id="3b515-107">패키지 식별자를 변경하고, 프로젝트를 다시 빌드하고, `.nupkg` 파일을 다시 만들고, `push` 명령을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="3b515-107">Change the package identifier, rebuild the project, recreate the `.nupkg` file, and retry the `push` command.</span></span>