---
ms.openlocfilehash: 9c3cb22c8c220a7297eb88db6ff0941e4c11c914
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496053"
---
<span data-ttu-id="c027f-101">nuget.org의 프로필에서 **패키지 관리**를 선택하여 방금 게시한 패키지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c027f-101">From your profile on nuget.org, select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="c027f-102">또한 확인 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c027f-102">You also receive a confirmation email.</span></span> <span data-ttu-id="c027f-103">패키지가 인덱싱되어 다른 사용자가 찾을 수 있는 검색 결과에 표시되는 데 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c027f-103">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="c027f-104">그 동안 아래 메시지가 패키지 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c027f-104">During that time your package page shows the message below:</span></span>

![이 패키지는 아직 인덱싱되지 않았습니다.](../media/QS_Create-03-NotIndexed.png)

<span data-ttu-id="c027f-107">이것으로 끝입니다!</span><span class="sxs-lookup"><span data-stu-id="c027f-107">And that's it!</span></span> <span data-ttu-id="c027f-108">방금 첫 번째 NuGet 패키지를 nuget.org에 게시했으므로 다른 개발자가 자신의 프로젝트에서 이 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c027f-108">You've just published your first NuGet package to nuget.org that other developers can use in their own projects.</span></span>

<span data-ttu-id="c027f-109">이 연습에서 실제로는 유용하지 않은 패키지(예: 빈 클래스 라이브러리를 사용하여 만든 패키지)를 만든 경우 검색 결과에서 패키지를 *나열 취소*해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c027f-109">If in this walkthrough you created a package that isn't actually useful (such as a package created with an empty class library), you should *unlist* the package to hide it from search results:</span></span>

1. <span data-ttu-id="c027f-110">nuget.org에서 사용자 이름(페이지 오른쪽 위)을 선택한 다음 **패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c027f-110">On nuget.org, select your user name (upper right of the page), then select **Manage Packages**.</span></span>

1. <span data-ttu-id="c027f-111">**게시됨** 아래에서 나열 취소할 패키지를 찾고 오른쪽에 있는 휴지통 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c027f-111">Locate the package you want to unlist under **Published** and select the trash can icon on the right:</span></span>

    ![nuget.org의 패키지 목록에 대해 표시된 휴지통 아이콘](../media/qs_create-vs-03-trash-can.png)

1. <span data-ttu-id="c027f-113">후속 페이지에서 **검색 결과에 (패키지 이름) 나열** 상자의 선택을 취소하고 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c027f-113">On the subsequent page, clear the box labeled **List (package-name) in search results** and select **Save**:</span></span>

    ![nuget.org의 패키지에 대한 목록 확인란 선택 취소](../media/qs_create-vs-04-unlist.png)