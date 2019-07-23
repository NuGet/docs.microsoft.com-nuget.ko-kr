---
ms.openlocfilehash: 5acdc54726e4cb07794f8ee07d5e0d357ff622a3
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842044"
---
1. <span data-ttu-id="b1dc3-101">[nuget.org 계정에 로그인](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)하거나 아직 계정이 없는 경우 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1dc3-101">[Sign into your nuget.org account](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) or create an account if you don't have one already.</span></span>

1. <span data-ttu-id="b1dc3-102">사용자 이름(오른쪽 위)을 선택한 다음 **API 키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dc3-102">Select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="b1dc3-103">**만들기**를 선택하고, 키 이름을 지정하고, **범위 선택 > 푸시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dc3-103">Select **Create**, provide a name for your key, select **Select Scopes > Push**.</span></span> <span data-ttu-id="b1dc3-104">**GLOB 패턴**에 \*를 입력한 후 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dc3-104">Enter \* for **Glob pattern**, then select **Create**.</span></span> <span data-ttu-id="b1dc3-105">(범위에 대한 자세한 내용은 아래를 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="b1dc3-105">(See below for more about scopes.)</span></span>

1. <span data-ttu-id="b1dc3-106">키가 만들어지면 **복사**를 선택하여 CLI에서 필요한 액세스 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dc3-106">Once the key is created, select **Copy** to retrieve the access key you need in the CLI:</span></span>

    ![클립보드에 API 키 복사](../media/QS_Create-02-APIKey.png)

1. <span data-ttu-id="b1dc3-108">**중요**: 나중에 키를 다시 복사할 수 없으므로 키를 안전한 위치에 저장하세요.</span><span class="sxs-lookup"><span data-stu-id="b1dc3-108">**Important**: Save your key in a secure location because you cannot copy the key again later on.</span></span> <span data-ttu-id="b1dc3-109">API 키 페이지로 돌아갈 경우 키를 복사하려면 키를 다시 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1dc3-109">If you return to the API key page, you need to regenerate the key to copy it.</span></span> <span data-ttu-id="b1dc3-110">CLI를 통해 더 이상 패키지를 푸시하지 않으려는 경우 API 키를 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1dc3-110">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

<span data-ttu-id="b1dc3-111">범위 지정을 사용하면 다른 용도의 API 키를 별도로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1dc3-111">Scoping allows you to create separate API keys for different purposes.</span></span> <span data-ttu-id="b1dc3-112">각 키는 만기 시간이 있으며 범위를 특정 패키지(또는 GLOB 패턴)로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1dc3-112">Each key has its expiration timeframe and can be scoped to specific packages (or glob patterns).</span></span> <span data-ttu-id="b1dc3-113">각 키의 범위를 새 패키지 및 업데이트 푸시, 업데이트만 푸시 또는 목록 해제와 같은 특정 작업으로 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1dc3-113">Each key is also scoped to specific operations: push of new packages and updates, push of updates only, or delisting.</span></span> <span data-ttu-id="b1dc3-114">범위 지정을 통해 조직의 패키지를 관리하는 여러 사용자의 API 키를 만들어 필요한 권한만 가지도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1dc3-114">Through scoping, you can create API keys for different people who manage packages for your organization such that they have only the permissions they need.</span></span> <span data-ttu-id="b1dc3-115">자세한 내용은 [Introducing scoped API keys](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html) (범위 지정된 API 키 소개)(blogs.nuget.org)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1dc3-115">For more information, see [Introducing scoped API keys](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html) (blogs.nuget.org).</span></span>