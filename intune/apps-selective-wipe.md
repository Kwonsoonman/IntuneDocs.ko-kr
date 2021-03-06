---
title: 앱에서 회사 데이터만 초기화하는 방법
titleSuffix: Microsoft Intune
description: Microsoft Intune을 사용하여 앱을 선택적으로 초기화하는 방법을 알아봅니다.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 10/09/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 42605e6e-5b84-44ff-b86e-346ea123b53e
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 19d173cabda71b4e6a24008eb94f9665c54ba924
ms.sourcegitcommit: 51b763e131917fccd255c346286fa515fcee33f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52184355"
---
# <a name="how-to-wipe-only-corporate-data-from-intune-managed-apps"></a>Intune 관리 앱에서 회사 데이터만 초기화하는 방법

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

장치를 분실하거나 도난당한 경우, 또는 직원이 퇴사하는 경우, 장치에서 업무용 앱 데이터가 확실히 제거되도록 해야 합니다. 하지만 장치에서 개인 데이터(특히, 직원 소유의 장치인 경우)를 제거하지 말아야 하는 경우가 있습니다.

>[!NOTE]
> iOS 및 Android 플랫폼은 현재 Intune 관리 앱에서 회사 데이터 초기화가 지원되는 두 개의 플랫폼입니다.

회사 앱 데이터를 선택적으로 제거하려면 이 항목의 단계를 사용하여 초기화 요청을 만듭니다. 요청이 완료되고 나면, 다음 번에 장치에서 앱을 실행할 때 회사 데이터가 앱에서 제거됩니다. 삭제 요청을 만드는 것 외에도 APP(응용 프로그램 보호 정책) 액세스 설정 조건이 충족되지 않으면 조직의 데이터를 선택적으로 지우는 작업을 새 작업으로 구성할 수 있습니다. 이 기능을 사용하면 미리 구성된 기준에 따라 응용 프로그램에서 중요한 조직 데이터를 자동으로 보호하고 제거할 수 있습니다.

>[!IMPORTANT]
> 앱에서 기본 주소록에 직접 동기화된 연락처가 제거됩니다. 기본 주소록에서 다른 외부 소스에 동기화된 연락처는 초기화할 수 없습니다. 현재 Microsoft Outlook 앱에만 적용됩니다.

## <a name="create-a-wipe-request"></a>초기화 요청 만들기

1.  [Azure 포털](https://portal.azure.com)에 로그인합니다.

2.  **모든 서비스**를 선택하고 필터 텍스트 상자에 **Intune**을 입력하고 **Intune**을 선택합니다. Intune 창이 열리면 **클라이언트 앱** 창을 선택합니다.

    ![Microsoft Intune 창 스크린샷](./media/apps-selective-wipe01.png)

3.  **클라이언트 앱 창**에서 **앱 선택적 초기화**를 선택합니다.

4.  **새 초기화 요청**을 선택합니다. **새 초기화 요청** 창이 열립니다.

    ![새 초기화 요청 창의 스크린샷](./media/AzurePortal_MAM_NewWipeRequest.png)

5.  사용자를 선택한 다음, **선택**을 선택하여 초기화할 앱 데이터의 사용자를 선택합니다.

6.  다음으로 **새 초기화 요청** 창에서 **장치**를 선택합니다. 선택한 사용자와 연결된 모든 장치를 나열하고 장치 이름(사용자가 정의한 이름) 및 장치 유형, 장치 플랫폼의 두 열도 제공하는 **장치 선택** 창이 열립니다. 초기화하려는 장치를 선택합니다.

7.  이제 **새 초기화 요청** 창으로 다시 전환됩니다. 초기화 요청을 수행하려면 **확인**을 클릭합니다.

서비스에서 장치의 각 보호된 앱 및 초기화 요청과 연결된 사용자에 대해 별도의 초기화 요청을 만들고 추적합니다.

## <a name="monitor-your-wipe-requests"></a>초기화 요청 모니터링

초기화 요청의 전반적인 상태를 표시하고, 보류 중인 요청 및 오류의 수가 포함된 요약된 보고서를 생성할 수 있습니다. 세부 정보를 확인하려면 다음 단계를 따릅니다.

1.  **클라이언트 앱 - 앱 선택적 초기화** 창에서 사용자별로 그룹화된 요청 목록을 확인할 수 있습니다. 시스템에서는 장치에서 실행 중인 각각의 보호된 앱에 대해 초기화 요청을 생성하므로 한 사용자에 대해 여러 요청이 표시될 수 있습니다. 상태를 통해 초기화 요청이 **보류 중**인지, **실패**했는지 아니면 **성공**했는지 확인할 수 있습니다.

    ![앱 선택적 초기화 창의 초기화 요청 상태 스크린샷](./media/wipe-request-status-1.png)

또한 장치 이름과 장치 유형을 볼 수 있습니다. 이는 보고서를 읽을 때 유용합니다.

>[!IMPORTANT]
> 초기화하려면 사용자가 앱을 열어야 하며 초기화에는 요청 후 최대 30분 걸릴 수 있습니다.

## <a name="delete-a-wipe-request"></a>초기화 요청 삭제

보류 중 상태의 초기화는 수동으로 삭제할 때까지 표시됩니다. 초기화 요청을 수동으로 삭제하려면

1.  **클라이언트 앱 - 앱 선택적 초기화** 창에서 다음을 수행합니다.

2.  목록에서 삭제하려는 초기화 요청을 마우스 오른쪽 단추로 클릭하고 **초기화 요청 삭제**를 선택합니다.

    ![앱 선택적 초기화 창의 초기화 요청 목록 스크린샷](./media/delete-wipe-request.png)

3.  삭제를 확인하라는 메시지가 표시되면 **예** 또는 **아니요**를 선택하고 **확인**을 클릭합니다.

### <a name="see-also"></a>참고 항목
[앱 보호 정책이란?](app-protection-policy.md)

[앱 관리란?](app-management.md)
