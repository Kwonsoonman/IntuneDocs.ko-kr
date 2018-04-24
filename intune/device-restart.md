---
title: Microsoft Intune을 사용하여 장치 다시 시작 - Azure | Microsoft Docs
description: 다시 시작 원격 동작을 사용하는 Azure Portal에서 Microsoft Intune을 사용하여 Windows 및 iOS 장치를 다시 시작합니다.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/21/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: c707e0c4-391a-4bad-9dfd-9a7799c48dd5
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 4f8aadebceed9c58717801b374a3a5d776926343
ms.sourcegitcommit: 5eba4bad151be32346aedc7cbb0333d71934f8cf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="remotely-restart-devices-with-intune"></a>Intune을 사용하여 원격으로 장치 다시 시작


[!INCLUDE [azure_portal](./includes/azure_portal.md)]

**다시 시작** 장치 작업을 수행하면 선택한 장치가 다시 시작됩니다. 장치 소유자에게 다시 시작이 자동으로 알려지지 않고 작업을 손실할 수 있습니다.

## <a name="supported-platforms"></a>지원되는 플랫폼

- Windows - Windows 8.1 이상에서 지원됨
- Windows Phone - Windows Phone 8.1 이상에서 지원됨
- iOS - 지원됨

    > [!Note]  
    > 이 명령은 감독되는 장치 및 **장치 잠금** 액세스 권한에 필요합니다. 장치를 즉시 다시 시작합니다. 암호로 잠긴 iOS 장치는 다시 시작한 후에 Wi-Fi 네트워크에 다시 연결되지 않습니다. 장치는 다시 시작한 후에 서버와 통신하지 못할 수 있습니다.
- macOS - 지원되지 않음
- Android - 지원되지 않음

## <a name="restart-a-device"></a>장치 다시 시작

1. [Azure 포털](https://portal.azure.com)에 로그인합니다.
2. **모든 서비스**를 선택하고 **Intune**에서 필터링하고 **Microsoft Intune**을 선택합니다.
3. **장치** > **모든 장치**를 선택합니다.
4. 관리하는 장치 목록에서 장치를 선택하고 **자세히**를 선택한 다음, **다시 시작** 장치 원격 작업을 선택합니다.

## <a name="next-steps"></a>다음 단계

- **다시 시작** 장치 작업의 상태를 보려면 **장치** > **장치 작업**을 선택합니다.
