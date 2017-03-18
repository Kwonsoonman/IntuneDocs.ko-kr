---
title: "Exchange 온-프레미스 조건부 액세스 정책"
titleSuffix: Intune Azure preview
description: "Intune Azure 미리 보기: Intune에서 Exchange 온-프레미스 조건부 액세스 및 기존 Exchange Online Dedicated를 구성하는 방법"
keywords: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 127dafcb-3f30-4745-a561-f62c9f095907
ms.suite: ems
ms.custom: intune-azure
translationtype: Human Translation
ms.sourcegitcommit: 153cce3809e24303b8f88a833e2fc7bdd9428a4a
ms.openlocfilehash: a9edd882e2cf0fb7abf50002e9f1e8dfd5634fe1
ms.lasthandoff: 02/18/2017


---

# <a name="how-to-create-a-conditional-access-policy-for-exchange-on-premises-and-legacy-exchange-online-dedicated-in-microsoft-intune-azure-preview"></a>Microsoft Intune Azure 미리 보기에서 Exchange 온-프레미스 및 기존 Exchange Online Dedicated에 대한 조건부 액세스 정책을 만드는 방법


[!INCLUDE[azure_preview](../includes/azure_preview.md)]

이 항목에서는 장치 준수를 기반으로 Exchange 온-프레미스에 대한 조건부 액세스를 구성하는 프로세스를 안내합니다.

Exchange Online Dedicated 환경이 있고 신규 또는 기존 구성 상태인지를 확인해야 하는 경우 계정 관리자에게 문의하세요. Exchange 온-프레미스 또는 레거시 Exchange Online Dedicated 환경에 대한 메일 액세스를 제어하려면 Intune에서 Exchange 온-프레미스에 대한 조건부 액세스를 구성합니다.

## <a name="prerequisites"></a>전제 조건

조건부 액세스를 구성하기 **전에** 다음을 확인합니다.

- Exchange 버전은 **Exchange 2010 이상**이어야 합니다. Exchange Server CAS(클라이언트 액세스 서버) 배열이 지원됩니다.
- Intune을 Microsoft Exchange 온-프레미스에 연결하는 **Exchange Active Sync 온-프레미스 Exchange 커넥터**를 사용해야 합니다. 커넥터에 대한 자세한 내용은 다음을 참조하세요. <link>

  - Intune 콘솔에서 사용할 수 있는 온-프레미스 Exchange Connector는 Intune 테넌트에 고유하며 다른 테넌트에 사용할 수 없습니다. 또한 테넌트용 Exchange Connector가 **한 대의 컴퓨터**에만 설치되어 있는지 확인해야 합니다.

이 커넥터는 Intune 관리 콘솔에서 다운로드해야 합니다. 온-프레미스 Exchange 커넥터를 구성하는 방법에 대한 연습은 다음을 참조하세요. <link to new topic>

Exchange 서버와 통신할 수 있기만 하면 모든 컴퓨터에 커넥터를 설치할 수 있습니다.

- 이 커넥터는 **Exchange CAS 환경**을 지원합니다. 원할 경우 Exchange CAS 서버에 직접 커넥터를 설치하는 것도 기술적으로 가능하지만 서버의 부하가 증가하므로 권장되지 않습니다. 커넥터를 구성할 때는 커넥터가 Exchange CAS 서버 중 하나와 통신하도록 설정해야 합니다.
- **Exchange ActiveSync**는 인증서 기반 인증 또는 사용자 자격 증명 항목으로 구성되어야 합니다.

조건부 액세스 정책이 구성되고 사용자를 대상으로 지정한 경우 사용자가 자신의 전자 메일에 연결하기 전에 사용하는 **장치**는 다음과 같아야 합니다.

- Intune에 **등록**되어 있거나 도메인에 가입된 PC여야 합니다.
- **Azure Active Directory에 등록**되어야 합니다. 또한 클라이언트 Exchange ActiveSync ID가 Azure Active Directory에 등록되어 있어야 합니다.

Intune 및 Office 365 고객의 경우에는 AAD DRS가 자동으로 활성화됩니다. ADFS 장치 등록 서비스를 이미 배포한 고객의 온-프레미스 Active Directory에는 등록된 장치가 표시되지 않습니다. **Windows PC 및 Windows Phone 장치에는 적용되지 않습니다**.

- 장치가 해당 장치에 배포된 Intune 준수 정책을 **준수해야** 합니다.

장치가 조건부 액세스 설정을 충족되지 않으면 사용자가 로그인할 때 다음 메시지 중 하나가 표시됩니다.

- 장치를 Intune에 등록하지 않았거나 Azure Active Directory에 등록하지 않은 경우, 회사 포털 앱을 설치하고 장치를 등록하며 메일을 활성화하는 방법에 대한 지침이 포함된 메시지가 표시됩니다. 이 프로세스는 또한 장치의 Exchange ActiveSync ID를 Azure Active Directory의 장치 레코드와 연결합니다.
- 장치가 정책을 준수하지 않으면 사용자가 문제에 관한 정보를 찾을 수 있는 Intune 웹 포털 또는 회사 포털 앱과 문제를 해결하는 방법을 알려주는 메시지가 표시됩니다.

## <a name="support-for-mobile-devices"></a>모바일 장치에 대한 지원

- Windows Phone 8.1 이상
- iOS의 기본 메일 앱
- EAS 메일 클라이언트(예: Android 4 이상의 Gmail).
- EAS 메일 클라이언트 **Android for Work 장치**: **업무용 프로필**에서 **Gmail** 및 **Nine Work** 앱만 Android for Work에 대해 지원됩니다. 조건부 액세스가 Android for Work에서 작동하려면 Gmail 또는 Nine Work 앱에 대한 메일 프로필을 배포하며, 이러한 앱을 필수 설치로 배포해야 합니다.

>[!NOTE]
>Android 및 iOS용 Microsoft Outlook 앱은 지원되지 않습니다.

> Android for Work는 향후 몇 개월에 걸쳐 Intune 테넌트에서 출시됩니다.

Android for Work의 지원 상태에 대한 자세한 내용은 [Microsoft Intune의 새로운 기능](https://docs.microsoft.com/en-us/intune/whats-new/whats-new-archive#october-2016)의 2016년 10월 에디션에서 Android for Work 게시물을 참조하세요.

## <a name="support-for-pcs"></a>PC 지원

Windows 8.1 이상에 설치된 **메일** 응용 프로그램(Intune에 등록된 경우)


## <a name="configure-exchange-on-premises-access"></a>Exchange 온-프레미스 액세스 구성

1. Azure Portal에서 **조건부 액세스** 워크로드를 선택하여 온-프레미스 블레이드를 엽니다.
2. **온-프레미스** 블레이드에 조건부 액세스 정책의 상태 및 그 영향을 받는 장치가 표시됩니다.
3. **관리** 아래에서 **Exchange 온-프레미스 액세스**를 선택합니다.
4. **Exchange 온-프레미스 액세스** 블레이드에서 **예**를 선택하여 Exchange 온-프레미스 액세스 제어를 사용하도록 설정합니다.

  >[!NOTE]
  >Exchange Active Sync 온-프레미스 커넥터를 구성하지 않은 경우에는 이 옵션을 사용할 수 없습니다.  Exchange 온-프레미스에 대한 조건부 액세스를 설정하려면 먼저 이 커넥터를 설치하고 구성해야 합니다. 자세한 내용은 [Intune 온-프레미스 Exchange Connector 설치](install-intune-on-premises-exchange-connector.md)를 참조하세요.

5. **할당** 아래에서 **그룹 포함됨**을 선택합니다.  조건부 액세스를 적용해야 하는 보안 사용자 그룹을 사용합니다.  그러려면 사용자가 Intune에 장치를 등록하고 준수 프로필을 준수해야 합니다.
6. 특정 사용자 그룹을 제외하려면 **그룹 제외됨**을 선택한 다음 장치 등록 및 준수 대상에서 제외할 사용자 그룹을 선택하면 됩니다.
7. **설정** 아래에서 **사용자 알림**을 선택하여 기본 메일 메시지를 수정합니다. 이 메시지는 해당 장치가 준수되지 않으며 Exchange 온-프레미스에 액세스하려는 사용자에게 전송됩니다. 메시지 템플릿에는 마크업 언어가 사용됩니다.  입력할 때 메시지 모양에 대한 미리 보기도 표시됩니다. 마크업 언어에 대한 자세한 내용은 이 Wikipedia [문서](https://en.wikipedia.org/wiki/Markup_language)를 참조하세요.
8. **고급 Exchange Active Sync 액세스 설정** 블레이드에서 다음 두 단계에 설명된 대로 Intune을 통해 관리되지 않는 장치의 액세스에 대한 전역 기본 규칙 및 플랫폼 수준 규칙을 설정합니다.
9. 조건부 액세스 또는 다른 규칙의 영향을 받지 않는 장치의 경우 Exchange에 대한 액세스를 허용하거나 차단하도록 선택할 수 있습니다.
  - 액세스를 허용하도록 설정하면 모든 장치에서 Exchange 온-프레미스에 즉시 액세스할 수 있습니다.  **그룹 포함됨**의 사용자에게 속한 장치는 이후에 준수 정책을 준수하지 않거나 Intune에 등록되지 않은 것으로 평가되는 경우 차단됩니다.
  - 액세스를 차단하도록 설정하면 모든 장치에서 초기에 Exchange 온-프레미스에 대한 액세스가 즉시 차단됩니다.  **그룹 포함됨**의 사용자에게 속한 장치는 Intune에 등록되고 준수하는 것으로 평가되는 경우 액세스 권한이 부여됩니다. Samsung KNOX Standard를 실행하지 않는 Android 장치는 이 설정을 지원하지 않으므로 항상 차단됩니다.
10. **장치 플랫폼 예외** 아래에서 **추가**를 선택하여 플랫폼을 지정합니다. **관리되지 않는 장치 액세스** 설정이 **차단됨**으로 설정된 경우 등록 및 호환되는 장치는 차단에 대한 플랫폼 예외가 있는 경우에도 허용됩니다. **확인**을 선택하여 설정을 저장합니다.
11. **온-프레미스** 블레이드에서 **저장**을 클릭하여 조건부 액세스 정책을 저장합니다.
