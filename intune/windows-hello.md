---
title: "비즈니스용 Windows Hello를 사용하는 방법"
titleSuffix: Azure portal
description: "관리 장치에서 비즈니스용 Windows Hello 사용을 제어하기 위한 정책을 만드는 방법을 알아봅니다.\""
keywords: 
author: vhorne
ms.author: victorh
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 541be8b8-8668-41be-afce-3f3e08c12191
ms.reviewer: 
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: f14120bc6141853177559d4561ea2da866088fb2
ms.sourcegitcommit: 3b397b1dcb780e2f82a3d8fba693773f1a9fcde1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="use-windows-hello-for-business"></a>비즈니스용 Windows Hello 사용


[!INCLUDE[azure_portal](./includes/azure_portal.md)]

Microsoft Intune은 Active Directory 또는 Azure Active Directory 계정을 사용하여 암호, 스마트 카드 또는 가상 스마트 카드를 대신하는 대체 로그인 방법인 비즈니스용 Windows Hello와 통합합니다.

비즈니스용 Hello를 사용하면 암호 대신 *사용자 제스처*를 사용하여 로그인할 수 있습니다. 사용자 제스처는 단순 PIN, 생체 인식 인증(예: Windows Hello) 또는 외부 장치(예: 지문 판독기)일 수 있습니다.

Intune은 다음 두 가지 방법으로 비즈니스용 Hello에 통합됩니다.

-   Intune 정책을 사용하여 사용자가 로그인하는 데 사용할 수 있는 제스처와 사용할 수 없는 제스처를 제어할 수 있습니다.

<!--- -   You can store authentication certificates in the Windows Hello for Business key storage provider (KSP). For more information, see [Secure resource access with certificate profiles in Microsoft Intune](secure-resource-access-with-certificate-profiles.md). --->

> [!IMPORTANT]
> Windows 10 데스크톱 및 1주년 업데이트 전의 모바일 버전에서 리소스에 인증하는 데 사용할 수 있는 두 개의 서로 다른 PIN을 설정할 수 있습니다.
- **장치 PIN**을 장치 잠금을 해제하고 클라우드 리소스에 연결하는 데 사용할 수 있습니다.
- **작업 PIN**은 사용자의 개인 장치(BYOD)에서 Azure AD 리소스에 액세스하는 데 사용되었습니다.

>1주년 업데이트에서 이러한 두 PIN이 하나의 단일 장치 PIN에 병합되었습니다.
이제 장치 PIN을 제어하도록 설정한 Intune 구성 정책뿐 아니라, 구성한 비즈니스용 Windows Hello 정책 둘 다 이러한 새 PIN 값으로 설정되어 있습니다.
PIN을 제어하기 위해 두 정책 유형을 설정한 경우 비즈니스용 Windows Hello 정책이 Windows 10 Desktop 및 모바일 장치에 모두 적용됩니다.
정책 충돌이 해결되어 있고 PIN 정책을 올바르게 적용되었는지 확인하려면 비즈니스용 Windows Hello 정책을 내 구성 정책의 설정에 맞게 업데이트한 다음, 회사 포털 앱에서 장치를 동기화하도록 사용자에게 요청합니다.



## <a name="create-a-windows-hello-for-business-policy"></a>비즈니스용 Windows Hello 정책 만들기

1.  Azure Portal에서 **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다.

2.  Intune 블레이드에서 **장치 등록**을 선택한 다음 **관리** > **비즈니스용 Windows Hello**를 선택합니다.

3.  블레이드가 열리면 **기본값**을 선택합니다.

4.  **모든 사용자** 블레이드에서 **속성**을 클릭하고 비즈니스용 Windows Hello 설정에 대한 **이름** 및 선택적 **설명**을 입력합니다.

5. **모든 사용자** 블레이드에서 **설정**을 클릭하고 **비즈니스용 Windows Hello 구성**에서 다음 중 하나를 선택합니다.

    - **Disabled**. 비즈니스용 Windows Hello를 사용하지 않으려면 이 설정을 선택합니다. 화면의 다른 모든 설정은 사용할 수 없게 됩니다.
    - **Enabled**. 비즈니스용 Windows Hello 설정을 구성하려면 이 설정을 선택합니다.
    - **구성되지 않음**. Intune을 사용하여 비즈니스용 Windows Hello 설정을 제어하지 않으려면 이 설정을 선택합니다. Windows 10 장치에서 기존 비즈니스용 Windows Hello 설정이 변경되지 않습니다. 블레이드의 다른 모든 설정은 사용할 수 없게 됩니다.

6.  이전 단계에서 **사용**을 선택한 경우에는 등록된 모든 Windows 10 및 Windows 10 모바일 장치에 적용될 필요한 설정을 구성합니다.

 - **TPM(신뢰할 수 있는 플랫폼 모듈) 사용**. TPM 칩은 추가적인 데이터 보안 계층을 제공합니다.<br>다음 값 중 하나를 선택합니다.

     - **필수**(기본값). 액세스할 수는 TPM이 있는 장치만 비즈니스용 Windows Hello를 프로비전할 수 있습니다.
     - **기본 설정**. 장치에서 먼저 TPM을 사용하려고 합니다. 사용할 수 없는 경우에는 소프트웨어 암호화를 사용할 수 있습니다.

 - **최소 PIN 길이 필요**/**최대 PIN 길이 필요**. 로그인을 보호하기 위해 지정한 최소 및 최대 PIN 길이를 사용하도록 장치를 구성합니다. 기본 PIN 길이는 6자이지만 최소 길이인 4자를 적용할 수 있습니다. 최대 PIN 길이는 127자입니다.

 - **PIN에 소문자 필요**/**PIN에 대문자 필요**/**PIN에 특수 문자 필요**. PIN에 대문자, 소문자, 특수 문자를 사용하도록 요구하여 강력한 PIN을 적용할 수 있습니다. 다음 중에서 선택합니다.

     - **허용**. 사용자는 해당 PIN에 문자 형식을 사용할 수 있지만 필수는 아닙니다.
    
     - **필수**. 사용자는 PIN에 하나 이상의 문자 형식을 포함해야 합니다. 예를 들어, 일반적으로 하나 이상의 대문자 및 특수 문자가 필요합니다.

     - **허용되지 않음**(기본값). PIN에서 대문자 형식을 사용하지 않아야 합니다. (설정이 구성되지 않은 경우에도 이 동작 수행)<br>특수 문자에는 다음이 포함됩니다. **! " # $ % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] ^ _ &#96; { &#124; } ~**

 - **PIN 만료(일)**. 사용자가 변경해야 하는 기간 이후에 PIN에 대한 만료 기간을 지정하는 것이 좋습니다. 기본값은 41일입니다.

 - **PIN 기록 저장**. 이전에 사용한 PIN의 재사용을 제한합니다. 기본적으로 마지막 5개 PIN을 다시 사용할 수 없습니다.

 - **생체 인식 인증 허용**. 비즈니스용 Windows Hello PIN 대신 안면 인식 또는 지문과 같은 생체 인식 인증을 설정합니다. 사용자는 생체 인식 인증에 실패하는 경우 작업 PIN을 구성해야 합니다. 다음 중에서 선택합니다.

     - **예**. 비즈니스용 Windows Hello에서 생체 인식이 허용됩니다.
     - **아니요**. 비즈니스용 Windows Hello에서 모든 계정 유형에 대해 생체 인식 인증을 금지합니다.

 - **사용 가능한 경우 향상된 스푸핑 방지 사용**. Windows Hello의 스푸핑 방지 기능을 지원하는 장치에서 사용할지 여부를 구성합니다(예: 실제 얼굴 대신 얼굴 사진 검색).<br>**예**로 설정하면 얼굴 인식 기능이 지원되는 경우 모든 사용자는 얼굴 인식 기능에 대해 스푸핑 방지 기능을 사용해야 합니다.

 - **휴대폰 로그인 사용**. 이 옵션이 **예**로 설정되면 원격 Passport를 데스크톱 컴퓨터 인증을 위한 휴대용 포함 장치로 사용할 수 있습니다. 데스크톱 컴퓨터가 Azure Active Directory에 연결되어 있어야 하고 해당 포함 장치는 비즈니스용 Windows Hello PIN으로 구성되어야 합니다.


## <a name="further-information"></a>추가 정보
Microsoft Passport에 대한 자세한 내용은 Windows 10 설명서의 [가이드](https://technet.microsoft.com/library/mt589441.aspx)를 참조하세요.
