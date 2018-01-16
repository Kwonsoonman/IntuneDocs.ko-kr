---
title: "Intune을 사용하여 iOS 활성화 잠금 무시"
titlesuffix: Azure portal
description: "Intune을 사용하여 iOS 활성화 잠금을 무시하고 잠긴 장치에 액세스하는 방법을 알아봅니다\""
keywords: 
author: arob98
ms.author: angrobe
manager: angrobe
ms.date: 08/22/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 9ca3b0ba-e41c-45fb-af28-119dff47c59f
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: f976bdcc900accc2955281685c11e33a732909f5
ms.sourcegitcommit: 22ab1c6a6bfeb4fef9850d12b29829c3fecbbeed
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/12/2018
---
# <a name="bypass-activation-lock-on-supervised-ios-devices-with-intune"></a>Intune을 사용하여 감독된 iOS 장치에서 활성화 잠금 무시


[!INCLUDE[azure_portal](./includes/azure_portal.md)]

Microsoft Intune에서는 iOS 8.0 이상 장치용 나의 iPhone 찾기(Find My iPhone) 앱의 기능인 iOS 활성화 잠금을 관리할 수 있습니다. 활성화 잠금은 사용자가 장치에서 나의 iPhone 찾기 앱을 열 때 자동으로 설정됩니다. 활성화 잠금이 설정되면 사용자의 Apple ID와 암호를 입력해야 다음 작업을 수행할 수 있습니다.

- 나의 iPhone 찾기 끄기
- 장치의 콘텐츠 지우기
- 장치 다시 활성화

## <a name="how-activation-lock-affects-you"></a>활성화 잠금 사용 시의 영향

활성화 잠금 기능을 사용하면 iOS 장치를 보호하고, 손실되었거나 도난당한 장치의 복구 가능성을 높일 수는 있지만 IT 관리자의 경우에는 여러 가지 문제를 해결해야 할 수도 있습니다. 예를 들면 다음과 같습니다.

- 사용자가 장치에서 활성화 잠금을 설정합니다. 해당 사용자가 퇴사하게 되어 장치를 반납합니다. 이 경우 해당 사용자의 Apple ID와 암호가 없으면 장치를 다시 활성화할 수 없습니다.
- 활성화 잠금을 설정한 모든 장치의 보고서를 작성해야 합니다.
- 조직에서 장치 새로고침을 진행하는 동안 일부 장치를 다른 부서에 다시 할당해야 하는 경우가 있습니다. 이때 활성화 잠금이 설정되지 않은 장치만 다시 할당할 수 있습니다.

이러한 문제를 해결할 수 있도록 Apple은 iOS 7.1에 활성화 잠금 무시 기능을 도입했습니다. 활성화 잠금 무시 기능을 통해 사용자의 Apple ID와 암호가 없어도 감독된 장치에서 활성화 잠금을 제거할 수 있습니다. 감독된 장치는 장치별 활성화 잠금 무시 코드를 생성할 수 있으며, 이 코드는 Apple 활성화 서버에 저장됩니다.

>[!TIP]
>iOS 장치에 대해 감독 모드를 사용하면 Apple Configurator를 통해 장치를 잠그고 특정 업무용으로 기능을 제한할 수 있습니다. 감독 모드는 회사가 소유한 장치에서만 사용됩니다.

활성화 잠금에 대한 자세한 내용은 [Apple 웹 사이트](https://support.apple.com/HT201365)에서 확인할 수 있습니다.

## <a name="how-intune-helps-you-manage-activation-lock"></a>Intune을 통해 활성화 잠금을 관리하는 방법
Intune에서는 iOS 8.0 이상을 실행하는 감독된 장치의 활성화 잠금 상태를 요청할 수 있습니다. 감독된 장치의 경우에만 Intune은 활성화 잠금 무시 코드를 검색하여 장치에 직접 제공할 수 있습니다. 장치를 초기화한 경우에는 사용자 이름은 비워 두고 코드를 암호로 사용하는 방식으로 장치에 직접 액세스할 수 있습니다.

**Intune을 사용하여 활성화 잠금을 관리하면 다음과 같은 비즈니스 이점이 있습니다.**

- 사용자가 나의 iPhone 찾기 앱의 보안 이점을 활용할 수 있습니다.
- 사용자가 안심하고 장치에서 작업할 수 있게 하며, 이 장치의 용도를 다시 설정해야 하는 경우 장치를 사용 중지하거나 잠금 해제할 수 있습니다.

## <a name="before-you-start"></a>시작하기 전에
장치에서 활성화 잠금을 무시하려면 다음 지침을 따라 사용하도록 설정해야 합니다.

1. [장치 제한 설정을 구성하는 방법](/intune-azure/configure-devices/how-to-configure-device-restrictions)의 정보를 참조하여 iOS용 Intune 장치 제한 프로필을 구성합니다.
2. [iOS에 대한 장치 제한 설정](device-restrictions-ios.md)에서 **일반** 설정 아래의 **활성화 잠금** 옵션을 사용합니다.
3. 프로필을 저장한 다음 활성화 잠금 무시를 관리하려는 장치에 [할당](device-profile-assign.md)합니다.


## <a name="how-to-use-activation-lock-bypass"></a>활성화 잠금 무시 사용 방법

>[!IMPORTANT]
>장치에서 활성화 잠금을 무시하도록 설정한 후 나의 iPhone 찾기 앱을 열면 새 활성화 잠금이 자동으로 적용됩니다. 따라서 **이 절차를 수행하려면 장치를 실제로 보유해야 합니다**.

Intune **활성화 잠금 무시** 원격 장치 작업에서는 사용자의 Apple ID와 암호 없이 iOS 장치에서 활성화 잠금을 제거합니다. 활성화 잠금을 무시한 후 내 iPhone 앱 찾기가 시작되면 장치에서 활성화 잠금이 다시 켜집니다. 장치에 실제로 액세스할 수 있는 경우에만 활성화 잠금을 무시합니다.

1. Azure 포털에 로그인합니다.
2. **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다.
3. **Intune** 블레이드에서 **장치**를 선택합니다.
4. **장치 및 그룹** 블레이드에서 **모든 장치**를 선택합니다.
5. 관리하는 장치 목록에서 감독된 iOS 장치를 선택한 다음 **활성화 잠금 무시** 장치 원격 작업을 선택합니다.

## <a name="next-steps"></a>다음 단계

**장치 관리** 워크로드를 통해 장치 세부 정보 페이지에서 잠금 해제 요청의 상태를 검사할 수 있습니다.
