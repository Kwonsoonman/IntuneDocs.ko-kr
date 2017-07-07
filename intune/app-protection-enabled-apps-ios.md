---
title: "앱 보호 정책을 사용하는 iOS 앱"
titleSuffix: Intune on Azure
description: "이 항목에서는 앱 보호 정책을 통해 iOS 앱을 관리할 때 예상되는 상황을 설명합니다.\""
keywords: 
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 586d9440-3813-4dec-b865-8bd319befde0
ms.reviewer: andcerat
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 912bc5230904f5798b2e0026dcf0dd1cecdb811c
ms.sourcegitcommit: 34cfebfc1d8b81032f4d41869d74dda559e677e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2017
---
# <a name="what-to-expect-when-your-ios-app-is-managed-by-app-protection-policies"></a>iOS 앱이 앱 보호 정책으로 관리될 때 예상되는 상황
[!INCLUDE[azure_portal](./includes/azure_portal.md)] 이 항목에서는 앱 보호 정책이 적용되는 앱에 대한 사용자 환경을 설명합니다. 앱 보호 정책은 회사 계정을 사용하여 앱에 액세스하거나 회사의 OneDrive 비즈니스 위치에 저장된 파일에 액세스하는 경우처럼 앱이 업무용으로 사용될 때만 적용됩니다.
##  <a name="accessing-apps"></a>앱 액세스

장치가 **Intune에 등록되지 않은** 경우 최종 사용자는 앱을 처음 사용할 때 앱을 다시 시작하도록 요구됩니다.  앱 보호 정책을 앱에 적용할 수 있도록 앱을 다시 시작해야 합니다. 다음 스크린샷은 Skype 앱을 사용하여 이러한 과정을 보여 줍니다.


![PIN 프롬프트를 보여 주는 iOS 장치의 스크린샷](./media/ios-pin-prompt.png)

**Intune에서 관리를 위해 등록**된 장치의 경우 최종 사용자에게 앱이 현재 관리되고 있다는 메시지가 표시됩니다.

![PIN 프롬프트를 포함하는 회사 메시지에 의해 관리되는 iOS 장치를 보여 주는 스크린샷](./media/ios-managed-devices-pin-prompt.png)

##  <a name="using-apps-with-multi-identity-support"></a>다중 ID가 지원되는 앱 사용

앱 보호 정책은 업무용으로 앱을 사용할 때만 적용되므로 업무용인지 개인용인지에 따라 앱 동작이 달라질 수 있습니다.  

다중 ID를 지원하는 앱의 경우, Intune은 최종 사용자가 업무용으로 앱을 사용할 때만 앱 보호 정책을 적용합니다.  예를 들어 최종 사용자는 업무용 데이터에 액세스할 경우 PIN 프롬프트를 받습니다.  **Outlook 앱**에서는 최종 사용자가 앱을 시작할 때 PIN을 입력하라는 메시지가 표시됩니다. **OneDrive 앱**에서는 최종 사용자가 회사 계정을 입력할 때 PIN을 입력하라는 메시지가 표시됩니다.  Microsoft **Word**, **PowerPoint* 및 **Excel**의 경우에는 최종 사용자가 회사의 비즈니스용 OneDrive 위치에 저장된 문서에 액세스할 때 PIN을 입력하라는 메시지가 표시됩니다.
##  <a name="managing-user-accounts-on-the-device"></a>장치에서 사용자 계정 관리

Intune은 장치 당 하나의 사용자 계정에 앱 보호 정책을 배포하도록 지원합니다.

* 사용 중인 앱에 따라 두 번째 사용자는 장치에서 차단될 수도 있고 차단되지 않을 수도 있습니다. 그러나 어떤 경우이든 앱 보호 정책을 가져오는 첫 번째 사용자만이 정책에 영향을 받습니다.
  * **Microsoft Word**, **Excel** 및 **PowerPoint**는 두 번째 사용자 계정을 차단하지 않지만 두 번째 사용자 계정은 앱 보호 정책의 영향을 받지 않습니다.  

  * **OneDrive 및 Outlook 앱**의 경우 회사 계정을 하나만 사용할 수 있습니다.  해당 앱에서는 여러 회사 계정의 추가가 차단됩니다.  그러나 사용자를 제거하고 장치에 다른 사용자를 추가할 수 있습니다.

* 앱 보호 정책을 배포하기 전에 장치에 기존의 여러 사용자 계정이 있으면 첫 번째 사용자에게 앱 보호 정책을 배포하는 계정은 Intune 앱 보호 정책에 의해 관리됩니다.


여러 사용자 계정이 처리되는 방법을 더 깊게 이해하려면 아래 예제 시나리오를 참고합니다.

사용자 A는 **회사 X** 및 **회사 Y**에서 일합니다. 사용자 A는 각 회사에 회사 계정을 보유하고 둘 다 Intune을 사용하여 앱 보호 정책을 배포합니다. **회사 X**는 **회사 Y**보다 **먼저** 앱 보호 정책을 배포합니다. **회사 X**와 연결된 계정은 앱 보호 정책을 가져오지만 회사 Y와 관련된 계정이 아닙니다. 회사 Y와 관련된 사용자 계정이 앱 보호 정책에 의해 관리되기를 바란다면 회사 X와 관련된 사용자 계정을 제거해야 합니다.
### <a name="adding-a-second-account"></a>두 번째 계정 추가

iOS 장치를 사용하는 경우 동일한 장치에 두 번째 회사 계정을 추가하려고 하면 차단 메시지가 표시될 수 있습니다.  계정이 표시되고 제거하려는 계정을 선택할 수 있습니다.

![메시지 및 예 및 아니요 옵션을 차단하는 대화 상자의 스크린 샷](./media/ios-switch-user.PNG)

## <a name="next-steps"></a>다음 단계
[Android 앱이 앱 보호 정책으로 관리될 때 예상되는 상황](app-protection-enabled-apps-android.md)
### <a name="see-also"></a>참고 항목
[Microsoft Intune으로 앱 보호 정책 만들기 및 배포](app-protection-policies.md)
