---
title: Microsoft Intune에 MTD 앱 추가 및 할당
titleSuffix: ''
description: Intune을 사용하여 Azure Portal에서 MTD 앱, Microsoft Authenticator 앱 및 iOS 구성 정책을 추가합니다.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/25/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 00356258-76a8-4a84-9cf5-64ceedb58e72
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: afc5028e4ed57757832844637298caf1656d610c
ms.sourcegitcommit: 51b763e131917fccd255c346286fa515fcee33f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52181176"
---
# <a name="add-and-assign-mobile-threat-defense-mtd-apps-with-intune"></a>Intune을 사용하여 MTD(Mobile Threat Defense) 앱 추가 및 할당

> [!NOTE] 
> 이 항목은 모든 Mobile Threat Defense 파트너에게 적용됩니다.

Intune을 사용하면 최종 사용자가 모바일 장치에서 위협이 식별될 때 알림을 받을 수 있도록 MTD 앱을 추가 및 배포하고 위협을 해결하기 위한 지침을 받을 수 있습니다.


## <a name="before-you-begin"></a>시작하기 전에

[Azure Portal](https://portal.azure.com/)에서 아래 단계를 완료해야 합니다. 다음 프로세스에 대해 잘 알고 있어야 합니다.

  -   [Intune에 앱 추가](apps-add.md)
  -   [Intune에 iOS 앱 구성 정책 추가](https://docs.microsoft.com/intune/deploy-use/configure-ios-apps-with-mobile-app-configuration-policies-in-microsoft-intune)
  -   [Intune을 사용하여 앱 할당](https://docs.microsoft.com/intune/deploy-use/deploy-apps-in-microsoft-intune)
  -   [iOS 앱 구성 정책 추가](https://docs.microsoft.com/intune/deploy-use/configure-ios-apps-with-mobile-app-configuration-policies-in-microsoft-intune)

> [!TIP]
> Intune 회사 포털은 사용자의 ID가 Azure AD에서 확인될 수 있도록 Android 장치에서 브로커로 작동합니다.

## <a name="configure-microsoft-authenticator-for-ios"></a>iOS용 Microsoft Authenticator 구성
iOS 장치의 경우 사용자의 ID가 Azure AD에서 확인될 수 있도록 [Microsoft Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to)가 필요합니다. 또한 Intune에서 사용할 MTD iOS 앱에 신호를 보내는 iOS 앱 구성 정책이 필요합니다.

[Microsoft Intune에 iOS 스토어 앱 추가](store-apps-ios.md) 지침을 참조하세요. **앱 정보 구성** 섹션의 **12단계**에서 이 [Microsoft Authenticator 앱 스토어 URL](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8)을 사용합니다.

## <a name="configure-mtd-applications"></a>MTD 응용 프로그램 구성

MTD 공급자에 해당하는 섹션을 선택합니다.

  - [Lookout for Work](#configure-lookout-for-work-apps)
  - [SEP Mobile(Symantec Endpoint Protection Mobile)](#configure-symantec-endpoint-protection-mobile-apps)
  - [Check Point SandBlast Mobile](#configure-check-point-sandblast-mobile-apps)
  - [Zimperium](#configure-zimperium-apps)
  - [Pradeo](#configure-pradeo-apps)
  - [더 향상된 모바일](#configure-better-mobile-apps)

### <a name="configure-lookout-for-work-apps"></a>Lookout for Work 앱 구성

- **OWA(Outlook Web Access)**
  - [Microsoft Intune에 Android 스토어 앱 추가](store-apps-android.md) 지침을 참조하세요. **7단계**에서 이 [Lookout for work Google 앱 스토어 URL](https://play.google.com/store/apps/details?id=com.lookout.enterprise)을 사용합니다.

- **iOS**

  - [Microsoft Intune에 iOS 스토어 앱 추가](store-apps-ios.md) 지침을 참조하세요. **앱 정보 구성** 섹션의 **12단계**에서 이 [Lookout for Work iOS 앱 스토어 URL](https://itunes.apple.com/us/app/lookout-for-work/id997193468?mt=8)을 사용합니다.

-   **Apple 스토어 외부의 Lookout for Work 앱**
    - Lookout for Work iOS 앱에 다시 서명해야 합니다. Lookout에서는 iOS App Store 외부에 Lookout for Work iOS 앱을 배포합니다. 앱을 배포하기 전에 iOS 엔터프라이즈 개발자 인증서를 사용하여 앱에 다시 서명해야 합니다.
    - Lookout for Work iOS 앱에 다시 서명하는 방법에 대한 자세한 내용은 Lookout 웹 사이트에서 [Lookout for Work iOS 앱 다시 서명 프로세스](https://personal.support.lookout.com/hc/articles/114094038714)를 참조하세요.

    - **Lookout for Work iOS 앱 사용자에 대해 Azure AD 인증을 사용합니다.**

        1. [Azure Portal](https://portal.azure.com)로 이동해서 자격 증명으로 로그인한 다음 응용 프로그램 페이지를 탐색합니다.

        2. **Lookout for Work iOS 앱**을 **네이티브 클라이언트 응용 프로그램**으로 추가합니다.

        3. **com.lookout.enterprise.yourcompanyname**을 IPA에 서명할 때 선택한 고객 번들 ID로 바꿉니다.

        4.  원래 리디렉션 URI의 URL 인코드된 버전을 뒤에 추가하여 다른 리디렉션 URI(**&lt;companyportal://code/>**)를 추가합니다.

        5.  **위임된 권한**을 앱에 추가합니다.

        > [!NOTE] 
        > 자세한 내용은 [Azure AD를 사용하여 네이티브 클라이언트 응용 프로그램 구성](https://azure.microsoft.com/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application)을 참조하세요.

     - **Lookout for Work ipa 파일을 추가합니다.**

        - [Intune을 사용하여 iOS LOB 앱 추가](lob-apps-ios.md) 항목에 설명된 대로 다시 서명된 .ipa 파일을 업로드합니다. 또한 최소 OS 버전을 iOS 8.0 이상으로 설정해야 합니다.

### <a name="configure-symantec-endpoint-protection-mobile-apps"></a>Symantec Endpoint Protection Mobile 앱 구성

 - **OWA(Outlook Web Access)**

    - [Microsoft Intune에 Android 스토어 앱 추가](store-apps-android.md) 지침을 참조하세요. **7단계**에서 이 [SEP Mobile 앱 스토어 URL](https://play.google.com/store/apps/details?id=com.skycure.skycure)을 사용합니다.  **최소 운영 체제**의 경우 **Android 4.0(Ice Cream Sandwich)** 을 선택합니다.

 - **iOS**

    - [Microsoft Intune에 iOS 스토어 앱 추가](store-apps-ios.md) 지침을 참조하세요. **12**단계에서 **앱 구성 정보** 섹션 아래에 있는 이 [SEP Mobile 앱 상점 URL](https://itunes.apple.com/us/app/skycure/id695620821?mt=8)을 사용합니다.

### <a name="configure-check-point-sandblast-mobile-apps"></a>Check Point SandBlast Mobile 앱 구성

 - **OWA(Outlook Web Access)**

    - [Microsoft Intune에 Android 스토어 앱 추가](store-apps-android.md) 지침을 참조하세요. **7단계**에서 이 [Check Point SandBlast Mobile 앱 스토어 URL](https://play.google.com/store/apps/details?id=com.lacoon.security.fox)을 사용합니다.

 - **iOS**

    - [Check Point SandBlast Mobile](https://www.checkpoint.com/products/sandblast-mobile/)에 문의하여 iOS 앱을 다운로드합니다. [Microsoft Intune에 iOS 스토어 앱 추가](store-apps-ios.md) 지침을 참조한 다음, **앱 정보 구성** 섹션의 **12단계**에서 Apple 스토어 URL을 사용합니다.

### <a name="configure-zimperium-apps"></a>Zimperium 앱 구성

 - **OWA(Outlook Web Access)**

    - [Microsoft Intune에 Android 스토어 앱 추가](store-apps-android.md) 지침을 참조하세요. **7단계**에서 이 [Zimperium 앱 스토어 URL](https://play.google.com/store/apps/details?id=com.zimperium.zips&hl=en)을 사용합니다.

 - **iOS**

    - [Microsoft Intune에 iOS 스토어 앱 추가](store-apps-ios.md) 지침을 참조하세요. **앱 정보 구성** 섹션의 **12단계**에서 이 [Zimperium 앱 스토어 URL](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8)을 사용합니다.

### <a name="configure-pradeo-apps"></a>Pradeo 앱 구성

 - **OWA(Outlook Web Access)**

    - [Microsoft Intune에 Android 스토어 앱 추가](store-apps-android.md) 지침을 참조하세요. **7단계**에서 이 [Pradeo 앱 스토어 URL](https://play.google.com/store/apps/details?id=net.pradeo.service&hl=en_US)을 사용합니다.

 - **iOS**

    - [Microsoft Intune에 iOS 스토어 앱 추가](store-apps-ios.md) 지침을 참조하세요. **앱 정보 구성** 섹션의 **12단계**에서 이 [Pradeo 앱 스토어 URL](https://itunes.apple.com/us/app/pradeo-agent/id547979360?mt=8)을 사용합니다.

### <a name="configure-better-mobile-apps"></a>Better Mobile 앱 구성

 - **OWA(Outlook Web Access)**

    - [Microsoft Intune에 Android 스토어 앱 추가](store-apps-android.md) 지침을 참조하세요. **7단계**에서 이 [Active Shield 앱 스토어 URL](https://play.google.com/store/apps/details?id=com.better.active.shield.enterprise)을 사용합니다.

 - **iOS**

    - [Microsoft Intune에 iOS 스토어 앱 추가](store-apps-ios.md) 지침을 참조하세요. **앱 정보 구성** 섹션의 **12단계**에서 이 [ActiveShield 앱 스토어 URL](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4)을 사용합니다.

## <a name="configure-your-mtd-apps-with-an-ios-app-configuration-policy"></a>iOS 앱 구성 정책으로 MTD 앱 구성

### <a name="lookout-for-work-app-configuration-policy"></a>Lookout for Work 앱 구성 정책

- [iOS 앱 구성 정책 사용](app-configuration-policies-use-ios.md) 항목에 설명된 대로 iOS 앱 구성 정책을 만듭니다.

### <a name="sep-mobile-app-configuration-policy"></a>SEP Mobile 앱 구성 정책

-   [Symantec Endpoint Protection 관리 콘솔](https://aad.skycure.com)에서 이전에 구성된 Azure AD 계정, 즉 Intune 클래식 포털에 로그인하는 데 사용되는 계정과 같은 계정을 사용해야 합니다.

-   iOS 앱 구성 정책 파일을 **다운로드**해야 합니다. 
    -   [Symantec Endpoint Protection 관리 콘솔](https://aad.skycure.com)로 이동하고 관리자 자격 증명을 사용하여 로그인합니다.

    -   **설정**으로 이동하여 **통합** 아래에서 **Intune**을 선택합니다. **EMM 통합 선택**을 선택합니다. **Microsoft**를 선택한 다음, 선택 항목을 저장합니다.

    -   **통합 설치 파일** 링크를 클릭하고 생성된 \*.zip 파일을 저장합니다. .zip 파일에는 ***.plist** 파일이 포함되어 있으며 이 파일은 Intune에서 iOS 앱 구성 정책을 만드는 데 사용됩니다.

    -   SEP Mobile iOS 앱 구성 정책을 추가하려면 [iOS에 대해 Microsoft Intune 앱 구성 정책 사용](app-configuration-policies-use-ios.md) 지침을 참조하세요.

    - **8단계**에서 **XML 데이터 입력** 옵션을 사용하고 ***.plist** 파일 콘텐츠를 복사하여 구성 정책 본문에 붙여넣습니다.

> [!NOTE]
> 파일을 검색할 수 없는 경우 [Symantec Endpoint Protection Mobile Enterprise 지원](https://support.symantec.com/en_US/contact-support.html)에 문의하세요.

### <a name="check-point-sandblast-mobile-app-configuration-policy"></a>Check Point SandBlast Mobile 앱 구성 정책

- Check Point SandBlast Mobile iOS 앱 구성 정책을 추가하려면 [iOS에 대해 Microsoft Intune 앱 구성 정책 사용](app-configuration-policies-use-ios.md) 지침을 참조하세요.
    - **8단계**에서 **XML 데이터 입력** 옵션을 사용하고 아래 콘텐츠를 복사하여 구성 정책 본문에 붙여넣습니다.

```
<dict><key>MDM</key><string>INTUNE</string></dict>
```

### <a name="zimperium-app-configuration-policy"></a>Zimperium 앱 구성 정책

- Zimperium iOS 앱 구성 정책을 추가하려면 [iOS에 대해 Microsoft Intune 앱 구성 정책 사용](app-configuration-policies-use-ios.md) 지침을 참조하세요.
    - **8단계**에서 **XML 데이터 입력** 옵션을 사용하고 아래 콘텐츠를 복사하여 구성 정책 본문에 붙여넣습니다.

```
<dict>
<key>provider</key><string>Intune</string>
<key>userprincipalname</key><string>{{userprincipalname}}</string>
<key>deviceid</key>
<string>{{deviceid}}</string>
<key>serialnumber</key>
<string>{{serialnumber}}</string>
<key>udidlast4digits</key>
<string>{{udidlast4digits}}</string>
</dict>
```

### <a name="better-mobile-app-configuration-policy"></a>Better Mobile 앱 구성 정책

- Better Mobile iOS 앱 구성 정책을 추가하려면 [iOS에 대해 Microsoft Intune 앱 구성 정책 사용](app-configuration-policies-use-ios.md) 지침을 참조하세요.
    - **8단계**에서 **XML 데이터 입력** 옵션을 사용하고 아래 콘텐츠를 복사하여 구성 정책 본문에 붙여넣습니다. `https://client.bmobi.net` URL을 적절한 콘솔 URL로 바꿉니다.

```
<dict>
<key>better_server_url</key>
<string>https://client.bmobi.net</string>
<key>better_udid</key>
<string>{{aaddeviceid}}</string>
<key>better_user</key>
<string>{{userprincipalname}}</string>
</dict>
```

## <a name="assign-apps-to-groups"></a>그룹에 앱 할당

- 이 단계는 모든 MTD 파트너에게 적용됩니다. [Intune을 사용하여 그룹에 앱 할당](apps-deploy.md) 지침을 참조하세요.

## <a name="next-steps"></a>다음 단계

- [MTD 장치 준수 정책 구성](mtd-device-compliance-policy-create.md)
