---
title: Microsoft Intune-Azure를 사용하여 iOS 분실 모드 활성화 | Microsoft Docs
description: Microsoft Intune을 사용하여 분실되거나 도난당한 iOS 장치의 잠금 화면에서 표시하는 메시지를 사용자 지정하기 위해 분실 모드를 켜거나 시작합니다. 그리고 분실 모드 작업을 사용하는 경우 보안 및 개인 정보 취급 방침에 대한 세부 정보를 가져옵니다.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/25/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 126a7489-fe3e-43fd-a681-defb2fe0bb66
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: b708ed69817ca85dc6648242ceafbdfa25b91fc9
ms.sourcegitcommit: 51b763e131917fccd255c346286fa515fcee33f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52180700"
---
# <a name="enable-lost-mode-on-ios-devices-with-intune"></a>Intune을 사용하여 iOS 장치에서 분실 모드 설정

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

**분실 모드** 장치 작업을 수행하면 분실했거나 도난당한 iOS 장치에 대해 분실 모드를 사용하도록 설정할 수 있습니다. 이 모드를 통해 장치의 잠금 화면에 표시되는 메시지 및 전화 번호를 입력할 수 있습니다. 장치에서 분실 모드를 사용하려면 감독 모드인 회사 소유 iOS 장치여야 합니다.

## <a name="supported-platforms"></a>지원되는 플랫폼

- iOS 9.3 이상

다음에서는 이 기능이 지원되지 않습니다. 
- Windows
- Windows Phone
- macOS
- Android

## <a name="enable-lost-mode"></a>분실 모드 설정

1. [Azure 포털](https://portal.azure.com)에 로그인합니다.
2. **모든 서비스**를 선택하고 **Intune**에서 필터링하고 **Microsoft Intune**을 선택합니다.
3. **장치**를 선택한 다음, **모든 장치**를 선택합니다.
4. 관리하는 장치 목록에서 iOS 장치를 선택하고 **자세히...** 를 선택합니다. 그런 다음, **분실 모드** 원격 작업을 선택합니다.
5. **분실 모드**에서 이 기능을 사용하도록 설정합니다. 그런 다음, 표시할 메시지와 연락처 전화 번호를 입력합니다.
6. **확인**을 선택하여 변경 내용을 저장합니다.

분실 모드를 사용하도록 설정하면 모든 장치 사용이 차단됩니다. 분실 모드를 사용하지 않도록 설정할 때까지 최종 사용자는 장치에 액세스할 수 없습니다. 분실 모드가 설정된 동안 [장치 찾기](device-locate.md) 작업을 사용하여 장치를 찾을 수 있습니다.

## <a name="security-and-privacy-information-for-the-lost-mode-and-locate-device-actions"></a>분실 모드의 보안 및 개인 정보와 장치 찾기 작업
- 이 작업을 켤 때까지 장치 위치 정보는 Intune에 전송되지 않습니다.
- 장치 찾기 작업을 사용하면 장치의 위도/경도 좌표가 Intune으로 전송되고 Azure Portal에 표시됩니다.
- 데이터는 24시간 동안 저장되었다가 제거됩니다. 위치 데이터를 수동으로 제거할 수 없습니다.
- 위치 데이터는 저장된 동안 및 전송되는 동안 모두 암호화됩니다.
- 잠금 화면에 표시하기 위해 입력한 메시지에서 분실 장치를 반환할 특정 세부 정보를 포함해야 합니다.

## <a name="next-steps"></a>다음 단계

분실 모드를 설정한 상태를 보려면 **장치**를 열고 **장치 작업**을 선택합니다.