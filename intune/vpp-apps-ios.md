---
title: "iOS 대량 구매 앱 관리 | Microsoft 문서"
titleSuffix: Intune Azure preview
description: "Intune Azure 미리 보기: iOS 스토어에서 대량 구매한 앱을 Intune에 동기화하고 해당 사용을 추적 및 관리하는 방법을 알아봅니다."
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 05/12/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 51d45ce2-d81b-4584-8bc4-568c8c62653d
ms.reviewer: mghadial
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: 3974145b4c244e251ee91a6216a79a6d8b1ad792
ms.contentlocale: ko-kr
ms.lasthandoff: 05/23/2017

---

# <a name="how-to-manage-ios-apps-you-purchased-through-a-volume-purchase-program-with-microsoft-intune"></a>Microsoft Intune을 사용하여 대량 구매 프로그램을 통해 구매한 iOS 앱을 관리하는 방법


[!INCLUDE[azure_preview](./includes/azure_preview.md)]

iOS 앱 스토어는 회사에서 실행하려는 앱의 라이선스를 여러 개 구매하는 기능을 제공합니다. 이 기능을 사용하면 구입한 앱의 여러 복사본을 추적하는 관리 오버헤드를 줄일 수 있습니다.

Microsoft Intune에서는 앱 스토어에서 라이선스 정보를 가져오고, 사용한 라이선스 수를 추적하며, 소유한 것보다 많은 앱 복사본을 설치할 수 없도록 하여 이러한 프로그램을 통해 구매한 앱의 관리를 지원합니다.

또한 Apple 대량 구매 프로그램 스토어에서 구매한 책을 Intune과 동기화, 관리 및 할당하고 사용자에게 이러한 책을 할당할 수 있습니다. Intune 포털에서 **책** 워크로드를 사용하여 책을 관리합니다. 책 관리 절차는 앱을 관리하는 데 사용하는 절차와 동일합니다.
이 작업을 수행하려면 Apple Volume Purchase Program 토큰을 업로드해야 합니다. 현재 책은 **필수** 설치로만 할당할 수 있습니다.
장치에 책을 할당할 때 해당 장치에는 기본 제공 iBooks 앱이 설치되어 있어야 합니다. 없는 경우 최종 사용자는 이 책을 읽기 위해 앱을 다시 설치해야 합니다. 현재로는 Intune을 사용하여 제거된 기본 제공 앱을 복원할 수 없습니다.


## <a name="manage-volume-purchased-apps-for-ios-devices"></a>iOS 장치용 대량 구매 앱 관리
[Apple 비즈니스용 대량 구매 프로그램](http://www.apple.com/business/vpp/) 또는 [Apple 교육용 대량 구매 프로그램](http://volume.itunes.apple.com/us/store)을 통해 iOS 앱의 라이선스를 여러 개 구입합니다. 이 경우 Apple 웹 사이트에서 Apple VPP 계정을 설정하고 Apple VPP 토큰을 Intune에 업로드해야 합니다.  그런 다음 대량 구매 정보를 Intune과 동기화하고 대량 구매 앱 사용을 추적할 수 있습니다.

## <a name="before-you-start"></a>시작하기 전에
시작하기 전에 Apple에서 VPP 토큰 하나를 가져와 Intune 계정에 업로드해야 합니다. 또한 다음 사항을 이해해야 합니다.

* 여러 대량 구매 프로그램 토큰을 Intune 계정과 연결할 수 있습니다.
* 이전에 VPP 토큰을 다른 제품에 사용한 경우 Intune에 사용할 토큰을 새로 생성해야 합니다.
* 각 토큰은 1년 동안 유효합니다.
* 기본적으로 Intune에서는 하루에 두 번 Apple VPP 서비스와 동기화합니다. 언제든지 수동 동기화를 시작할 수 있습니다.
* VPP 토큰을 Intune으로 가져온 후 같은 토큰을 다른 장치 관리 솔루션으로 가져오지 마세요. 가져오면 라이선스 할당과 사용자 레코드가 손실될 수 있습니다.
* Intune과 함께 iOS VPP를 사용하기 전에 다른 MDM(모바일 장치 관리) 공급업체를 사용하여 만든 기존 VPP 사용자 계정을 제거합니다. Intune은 보안 조치로 해당 사용자 계정을 Intune에 동기화하지 않습니다. Intune은 Intune에서 만든 Apple VPP 서비스의 데이터만 동기화합니다.
* Intune은 최대 256개의 VPP 토큰 추가를 지원합니다.

## <a name="to-get-and-upload-an-apple-vpp-token"></a>Apple VPP 토큰을 가져와 업로드하려면

1. Azure 포털에 로그인합니다.
2. **추가 서비스** > **기타** > **Intune**을 선택합니다.
3. **Intune** 블레이드에서 **Mobile Apps**를 선택합니다.
1.  **모바일 앱** 워크로드에서 **설정** > **iOS VPP 토큰**을 선택합니다.
2.  VPP 토큰 목록 블레이드에서 **추가**를 클릭합니다.
3.  새 VPP 토큰 블레이드에서 다음 정보를 지정합니다.
    - **VPP 토큰 파일** - 아직 없는 경우 비즈니스 또는 교육용 대량 구매 프로그램에 등록합니다. 등록한 후 계정에 대한 Apple VPP 토큰을 다운로드하여 선택합니다.
    - **Apple ID** - 대량 구매 프로그램과 연결된 계정의 Apple ID를 입력합니다.
    - **VPP 계정 유형** - **비즈니스** 또는 **교육**을 선택합니다.
4. 작업이 끝나면 **업로드**를 클릭합니다.

토큰은 토큰 목록 블레이드에 표시됩니다.


언제든지 **지금 동기화**를 선택하여 Apple에 보관된 데이터를 Intune과 동기화할 수 있습니다.

## <a name="to-assign-a-volume-purchased-app"></a>대량 구매 앱을 할당하려면

1. **모바일 앱** 워크로드에서 **관리** > **사용이 허가된 앱**을 선택합니다.
2. 앱 목록 블레이드에서 할당할 앱을 선택한 다음 '**...**' > **그룹 할당**을 선택합니다.
3. <*앱 이름*> - **할당된 그룹** 브레이드에서 **관리** > **할당된 그룹**을 선택합니다.
4. **그룹 할당**을 선택하고 **그룹 선택** 블레이드에서 앱을 할당할 Azure AD 사용자 또는 장치 그룹을 선택합니다.
**필수** 할당 작업을 선택해야 합니다. 또한 2017년 1월 이후에 만든 새 테넌트에도 장치 그룹에 할당하는 기능을 사용할 수 있습니다. 테넌트가 그전에 만들어졌고 VPP 앱을 장치 그룹에 할당할 수 없는 경우 Intune 지원에 문의하세요.
5. 작업이 끝나면 **저장**을 선택합니다.

앱 할당을 모니터링하는 데 유용한 정보는 [앱을 모니터링하는 방법](apps-monitor.md)을 참조하세요.

## <a name="further-information"></a>추가 정보

앱을 **필수** 설치로 할당하는 경우 앱을 설치하는 각 사용자는 라이선스 하나를 사용합니다.

라이선스를 회수하려면 할당 작업을 **제거**로 변경해야 합니다. 앱이 제거된 후에는 라이선스가 회수됩니다.

적합한 장치를 가진 사용자가 VPP 앱을 처음 설치하려고 하면 Apple 대량 구매 프로그램에 가입하라는 메시지가 표시됩니다. 가입해야만 앱 설치가 진행됩니다.

VPP 앱을 사용 가능으로 할당한 경우 앱 콘텐츠 및 라이선스가 앱 스토어에서 직접 할당됩니다.
