---
title: NuGet 오류 및 경고 참조
description: 경고 및 다양 한 NuGet 작업 중 NuGet에서 발급 한 오류에 대 한 참조를 완료 합니다.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 4d9ef92c006a0d3051a73ec8ebbb0f72bb2b2355
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59509089"
---
# <a name="errors-and-warnings"></a>오류 및 경고

NuGet 4.3.0 오류 및 경고가이 항목에 설명 된 대로 번호가 매겨집니다에 관련 된 문제를 해결 하는 데 대 한 자세한 정보를 제공 합니다.

오류 및 경고 여기에 나열 된는 함께만 사용할 수 있습니다 [PackageReference 기반](../consume-packages/package-references-in-project-files.md) 프로젝트 및 NuGet 4.3.0입니다. 또한 NuGet 경고를 표시 하지 않거나 오류로 상승할 MSBuild 속성을 따릅니다. 자세한 내용은 [방법: 컴파일러 경고 표시 안 함](/visualstudio/ide/how-to-suppress-compiler-warnings) Visual Studio 설명서에서.

## <a name="errors"></a>오류

| 그룹화 | 오류 번호 |
| --- | --- |
| 잘못 된 입력된 오류 | [NU1001](./errors-and-warnings/NU1001.md), [NU1002](./errors-and-warnings/NU1002.md), [NU1003](./errors-and-warnings/NU1003.md) |
| 누락 된 패키지 및 프로젝트 오류 | [NU1100](./errors-and-warnings/NU1100.md), [NU1101](./errors-and-warnings/NU1101.md), [NU1102](./errors-and-warnings/NU1102.md), [NU1103](./errors-and-warnings/NU1103.md), [NU1104](./errors-and-warnings/NU1104.md), [NU1105](./errors-and-warnings/NU1105.md), [NU1106](./errors-and-warnings/NU1106.md), [NU1107](./errors-and-warnings/NU1107.md), [NU1108](./errors-and-warnings/NU1108.md) |
| 호환성 오류 | [NU1201](./errors-and-warnings/NU1201.md), [NU1202](./errors-and-warnings/NU1202.md), [NU1203](./errors-and-warnings/NU1203.md), [NU1401](./errors-and-warnings/NU1401.md) |
| NuGet 내부 오류 | [NU1000](./errors-and-warnings/NU1000.md) |
| 서명 된 패키지 오류 (예: 생성 및 확인) | [NU3001](./errors-and-warnings/NU3001.md), [NU3004](./errors-and-warnings/NU3004.md), [NU3005](./errors-and-warnings/NU3005.md), [NU3008](./errors-and-warnings/NU3008.md), [NU3034](./errors-and-warnings/NU3034.md)|
| 팩 오류 | [NU5000](./errors-and-warnings/NU5000.md), [NU5001](./errors-and-warnings/NU5001.md)를 [NU5002](./errors-and-warnings/NU5002.md)를 [NU5003](./errors-and-warnings/NU5003.md)를 [NU5004](./errors-and-warnings/NU5004.md)를 [NU5005](./errors-and-warnings/NU5005.md)를 [NU5007](./errors-and-warnings/NU5007.md), [NU5008](./errors-and-warnings/NU5008.md)를 [NU5009](./errors-and-warnings/NU5009.md)합니다 [NU5010](./errors-and-warnings/NU5010.md)를 [NU5011](./errors-and-warnings/NU5011.md), [NU5012](./errors-and-warnings/NU5012.md), [NU5013](./errors-and-warnings/NU5013.md)를 [NU5014](./errors-and-warnings/NU5014.md)를 [NU5015](./errors-and-warnings/NU5015.md)를 [NU5016](./errors-and-warnings/NU5016.md)를 [NU5017](./errors-and-warnings/NU5017.md), [ NU5018](./errors-and-warnings/NU5018.md), [NU5019](./errors-and-warnings/NU5019.md)합니다 [NU5020](./errors-and-warnings/NU5020.md)를 [NU5021](./errors-and-warnings/NU5021.md)를 [NU5022](./errors-and-warnings/NU5022.md), [NU5023](./errors-and-warnings/NU5023.md), [NU5024](./errors-and-warnings/NU5024.md)합니다 [NU5025](./errors-and-warnings/NU5025.md)를 [NU5026](./errors-and-warnings/NU5026.md)를 [NU5027](./errors-and-warnings/NU5027.md), [NU5028](./errors-and-warnings/NU5028.md)하십시오 [NU5029](./errors-and-warnings/NU5029.md), [NU5036](./errors-and-warnings/NU5036.md)
| 라이선스 특정 팩 오류 | [NU5030](./errors-and-warnings/NU5030.md), [NU5031](./errors-and-warnings/NU5031.md), [NU5032](./errors-and-warnings/NU5032.md), [NU5033](./errors-and-warnings/NU5033.md), [NU5034](./errors-and-warnings/NU5034.md), [NU5035](./errors-and-warnings/NU5035.md)

## <a name="warnings"></a>경고

| 그룹화 | 경고 번호 |
| --- | --- |
| 잘못 된 입력된 경고 | [NU1501](./errors-and-warnings/NU1501.md), [NU1502](./errors-and-warnings/NU1502.md), [NU1503](./errors-and-warnings/NU1503.md) |
| 예기치 않은 패키지 버전 경고 | [NU1601](./errors-and-warnings/NU1601.md), [NU1602](./errors-and-warnings/NU1602.md), [NU1603](./errors-and-warnings/NU1603.md), [NU1604](./errors-and-warnings/NU1604.md), [NU1605](./errors-and-warnings/NU1605.md), [NU1606](./errors-and-warnings/NU1108.md), [NU1607](./errors-and-warnings/NU1107.md) |
| 확인자 충돌 경고 | [NU1608](./errors-and-warnings/NU1608.md) |
| 패키지 대체 경고 | [NU1701](./errors-and-warnings/NU1701.md) |
| 경고를 피드 합니다. | [NU1801](./errors-and-warnings/NU1801.md) |
| NuGet 내부 경고 | [NU1500](./errors-and-warnings/NU1500.md) |
| 서명 된 패키지 경고 (생성 및 확인) | [NU3000](./errors-and-warnings/NU3000.md), [NU3002](./errors-and-warnings/NU3002.md)를 [NU3003](./errors-and-warnings/NU3003.md)를 [NU3006](./errors-and-warnings/NU3006.md)를 [NU3007](./errors-and-warnings/NU3007.md)를 [NU3009](./errors-and-warnings/NU3009.md)를 [NU3010](./errors-and-warnings/NU3010.md), [NU3011](./errors-and-warnings/NU3011.md)를 [NU3012](./errors-and-warnings/NU3012.md)합니다 [NU3013](./errors-and-warnings/NU3013.md)를 [NU3014](./errors-and-warnings/NU3014.md), [NU3015](./errors-and-warnings/NU3015.md), [NU3016](./errors-and-warnings/NU3016.md)를 [NU3017](./errors-and-warnings/NU3017.md)를 [NU3018](./errors-and-warnings/NU3018.md)를 [NU3019](./errors-and-warnings/NU3019.md)를 [NU3020](./errors-and-warnings/NU3020.md), [ NU3021](./errors-and-warnings/NU3021.md), [NU3022](./errors-and-warnings/NU3022.md)합니다 [NU3023](./errors-and-warnings/NU3023.md)를 [NU3024](./errors-and-warnings/NU3024.md)를 [NU3025](./errors-and-warnings/NU3025.md), [NU3026](./errors-and-warnings/NU3026.md), [NU3027](./errors-and-warnings/NU3027.md)합니다 [NU3028](./errors-and-warnings/NU3028.md)를 [NU3029](./errors-and-warnings/NU3029.md)를 [NU3030](./errors-and-warnings/NU3030.md), [NU3031](./errors-and-warnings/NU3031.md), [NU3032](./errors-and-warnings/NU3032.md)합니다 [NU3033](./errors-and-warnings/NU3033.md)를 [NU3035](./errors-and-warnings/NU3035.md)를 [NU3036](./errors-and-warnings/NU3036.md), [NU3037 ](./errors-and-warnings/NU3037.md)하십시오 [NU3038](./errors-and-warnings/NU3038.md), [NU3040](./errors-and-warnings/NU3040.md) |
| 팩 경고 | [NU5100](./errors-and-warnings/NU5100.md), [NU5101](./errors-and-warnings/NU5101.md)를 [NU5102](./errors-and-warnings/NU5102.md)를 [NU5103](./errors-and-warnings/NU5103.md)를 [NU5104](./errors-and-warnings/NU5104.md)를 [NU5105](./errors-and-warnings/NU5105.md)를 [NU5106](./errors-and-warnings/NU5106.md), [NU5107](./errors-and-warnings/NU5107.md)를 [NU5108](./errors-and-warnings/NU5108.md)합니다 [NU5109](./errors-and-warnings/NU5109.md)를 [NU5110](./errors-and-warnings/NU5110.md), [NU5111](./errors-and-warnings/NU5111.md), [NU5112](./errors-and-warnings/NU5112.md)를 [NU5114](./errors-and-warnings/NU5114.md)를 [NU5115](./errors-and-warnings/NU5115.md)를 [NU5116](./errors-and-warnings/NU5116.md)를 [NU5117](./errors-and-warnings/NU5117.md), [ NU5118](./errors-and-warnings/NU5118.md), [NU5119](./errors-and-warnings/NU5119.md)합니다 [NU5120](./errors-and-warnings/NU5120.md)를 [NU5121](./errors-and-warnings/NU5121.md)를 [NU5122](./errors-and-warnings/NU5122.md), [NU5123](./errors-and-warnings/NU5123.md), [NU5500](./errors-and-warnings/NU5500.md)
| 라이선스 특정 팩 경고 | [NU5124](./errors-and-warnings/NU5124.md), [NU5125](./errors-and-warnings/NU5125.md)