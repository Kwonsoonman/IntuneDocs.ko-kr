---
title: "앱 보호 정책 유효성 검사"
titleSuffix: Intune on Azure
description: "이 항목에서는 앱 보호 정책이 올바르게 설정되어 있으며 정상적으로 작동하는지를 테스트하고 유효성을 검사하는 방법을 설명합니다.\""
keywords: 
author: mattbriggs
ms.author: mabrigg
manager: angerobe
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 15f8a838-0b69-412b-a42e-c6edb61f0cae
ms.reviewer: joglocke
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 28fcd15d2d2e11e4aa2ba6982fc3cb8567e56a31
ms.sourcegitcommit: 2ee1e8248814d74cef80b609a8e43f59fa0b2618
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2017
---
# <a name="how-to-validate-your-app-protection-policy-setup"></a>앱 보호 정책 설정의 유효성을 검사하는 방법

[!INCLUDE[azure_portal](./includes/azure_portal.md)]


이 항목에서는 앱 보호 정책을 설정한 후 문제를 확인하는 방법에 대한 정보를 제공합니다. 이 지침은 Azure Portal의 앱 보호 정책에 적용됩니다.

### <a name="checking-for-symptoms"></a>증상 확인
앱 보호는 데이터 보호 도구이므로 사용자가 문제를 보고할 가능성은 거의 없습니다. 앱 보호 구성에 문제가 있더라도 앱 보호를 사용하지 않을 때와 마찬가지로, 제한 없이 앱 보호 기능에 액세스할 수 있으므로 사용자는 문제가 있음을 알 수 없습니다. 따라서 앱 보호 제한을 의도적으로 테스트할 수 있는 소규모 사용자 그룹에 대해 앱 보호 정책을 파일럿 적용해 앱 보호 구성의 유효성을 검사하는 것이 좋습니다.


### <a name="what-to-check"></a>확인할 사항

테스트 결과 앱 보호 정책 동작이 예상과 다른 경우에는 다음 사항을 확인하는 것이 좋습니다.

- 사용자에게 앱 보호 사용이 허가되었는지 여부
- 사용자에게 O365 사용이 허가되었는지 여부
- 각 사용자의 앱 보호 앱 상태 앱의 가능한 상태는 **체크 인됨** 및 **체크 인되지 않음**입니다.

#### <a name="user-app-protection-status"></a>사용자 앱 보호 상태
1. Azure Portal에서 **앱 관리** > **모니터** >  **앱 보호 사용자 상태** > **사용자**를 선택합니다.

2. 목록에서 사용자를 선택하거나 사용자를 검색하여 선택한 다음 **사용자 선택**을 선택합니다. **앱 보고** 열 맨 위에 사용자에게 앱 보호 사용이 허가되었는지 여부가 표시됩니다. 그 아래에는 사용자에게 O365 사용이 허가되었는지 여부와 해당 사용자의 모든 장치에 대한 앱 상태가 표시됩니다.



### <a name="what-to-do"></a>수행할 작업
사용자 상태에 따라 수행할 작업은 다음과 같습니다.

- 사용자에게 앱 보호 사용이 허가되지 않은 경우 해당 사용자에게 Intune 라이선스를 할당합니다.
- 사용자에게 O365 사용이 허가되지 않은 경우 사용자용 라이선스를 받습니다.
- 사용자의 앱이 목록에서 **체크 인되지 않음**으로 표시되는 경우 해당 앱에 대해 앱 보호 정책을 올바르게 구성했는지 확인합니다.
- 앱 보호 정책을 적용할 모든 사용자에게 이러한 조건이 적용되는지 확인합니다.

### <a name="see-also"></a>참고 항목

[Intune 앱 보호 정책이란?](app-protection-policies.md)
