---
title: "Microsoft Intune-Azure와 장치 동기화 | Micrososft Docs"
description: "Microsoft Intune으로 등록되거나 관리되는 장치를 동기화하여 최신 정책과 작업을 가져옵니다. Azure Portal을 사용하여 동기화하는 단계를 포함하고 다시 시도할 수 있는 오류 코드를 나열합니다."
keywords: 
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/22/2018
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 02ad249e-f098-421f-861f-6b2ff733ac7c
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: d2d13ce2ed06549a6cd09fd766a0072b15fcd067
ms.sourcegitcommit: 4db0498342364f8a7c28995b15ce32759e920b99
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="sync-devices-to-get-the-latest-policies-and-actions---intune"></a>장치를 동기화하여 최신 정책과 작업 가져오기 - Intune


[!INCLUDE[azure_portal](./includes/azure_portal.md)]

장치 **동기화** 작업은 선택한 장치가 Intune을 사용하여 즉시 체크 인하도록 강제합니다. 장치가 체크 인하면 장치에 할당된 보류 중인 작업 또는 정책을 즉시 받게 됩니다. 이 기능을 통해 예약된 다음 체크 인을 기다리지 않고 즉시 할당한 정책의 유효성을 검사하고 문제를 해결할 수 있습니다.

## <a name="supported-platforms"></a>지원되는 플랫폼

- Windows
- Windows Phone
- iOS
- macOS
- Android

## <a name="sync-a-device"></a>장치 동기화

1. 로그인은 [Azure 포털](https://portal.azure.com)합니다.
2. **모든 서비스**를 선택하고 **Intune**에서 필터링하고 **Microsoft Intune**을 선택합니다. 
3. **Intune**에서 **장치**를 선택하고 **모든 장치**를 선택합니다.
4. 관리하는 장치 목록에서 장치를 선택하고 **자세히...**를 선택한 다음, **동기화** 작업을 선택합니다.
5. **예**를 선택하여 확인합니다.


## <a name="retryable-error-codes"></a>다시 시도 가능 오류 코드

관리자가 **동기화** 장치 작업을 실행하는 경우 실패하고 다시 시도 가능 오류 코드가 발생한 iOS 및 Android 앱이 장치에 제공됩니다. 그러나 다시 시도 가능이 아닌 오류 코드가 발생한 앱은 장치에서 제공되기 전에 7일 동안 기다려야 합니다.


| 오류 코드  | 제안되는 설명 | 다시 시도 가능 |
|---|---|---|
| 2016330898 | 알 수 없는 오류가 발생했습니다. | 아니요 |
| 2016330897 | Intune 연결 시간이 초과되었습니다. 연결을 다시 설정하십시오. | 예 |
| 2016330896 | 인터넷 연결이 끊어졌습니다. 연결을 다시 설정하십시오. | 예 |
| 2016330895 | 인터넷 연결이 끊어졌습니다. 연결을 다시 설정하십시오. | 예 |
| 2016330894 | 인터넷 연결이 끊어졌습니다. 연결을 다시 설정하십시오. | 예 |
| 2016330893 | 인터넷 연결이 끊어졌습니다. 연결을 다시 설정하십시오. | 예|
| 2016330892 | 국제 로밍을 사용하지 않습니다. | 아니요|
| 2016330891 | 전화 통화 중에는 이 장치의 셀룰러 데이터 연결에 액세스할 수 없습니다. 전화 통화가 완료될 때까지 기다리십시오. | 예|
| 2016330890 | 이 장치의 셀룰러 네트워크입니다. 이러한 장치는 이 시간에 사용하지 못했습니다. | 아니요|
| 2016330889 | 보안 연결에 실패했습니다. 연결을 다시 설정하십시오. | 예|
| 2016330888 | 서버 신뢰 평가에 실패했습니다. | 아니요|

## <a name="next-step"></a>다음 단계

**장치 작업**을 선택하여 동기화 작업의 상태를 확인합니다. 
