---
title: "Intune 설계 만들기 | Microsoft 문서"
description: "이 문서의 정보를 활용하여 Microsoft Intune 클라우드 전용 설계 및 구현을 위한 설계를 만들 수 있습니다."
keywords: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 12/28/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: a8e38e29-f5e3-4a71-a170-d3b1a06e37c6
ms.reviewer: jeffbu, cgerth
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: fa33bd3833f7f7198eed3f4f486c27bae3ba47d7
ms.openlocfilehash: 5f05aa4a27be14a05663aa9de82af63291699403


---

# <a name="create-an-intune-design"></a>Intune 설계 만들기

[!INCLUDE[note for both-portals](../includes/note-for-both-portals.md)]

가이드의 섹션은 섹션 2의 다른 항목과 함께 사용해야 합니다. 이 설계는 이 가이드의 이전 섹션을 완료하면서 수집하는 정보 및 결정할 사항에 따라 달라집니다. 이 설계 섹션에서는 클라우드에 상주하는 Microsoft 클라우드 기반 서비스인 Intune 독립 실행형에 집중합니다.

온-프레미스 인프라 요구 사항이 매우 적긴 하지만 여전히 설계 계획 작업을 하여 목적 및 목표에 부합되고 요구 사항을 충족하는 적절한 모바일 장치 관리 솔루션을 보유하는 것이 좋습니다.

또한 구현 및 테스트 단계 도중에 설계를 변경하는 일은 일반적이며, 이러한 변경 내용 및 변경이 발생한 근거를 모두 문서화해야 합니다. 다음과 같은 영역을 살펴보겠습니다.

-   현재 환경

-   Intune 배포 옵션

-   외부 종속성에 대한 ID 요구 사항

-   장치 플랫폼 고려 사항

-   배달하기 위한 요구 사항  

이러한 각 영역에 대해 더 자세히 살펴보겠습니다. 

## <a name="record-your-environment"></a>사용자 환경 기록

설계를 만들기 전에 먼저 수행할 첫 번째 단계는 현재 환경을 기록하는 것입니다. 현재 환경은 설계 결정에 영향을 줄 수 있으므로 다른 Intune 설계 결정을 내릴 때 현재 환경을 문서화하고 참조해야 합니다. 다음은 현재 환경을 기록하는 방법의 몇 가지 예입니다.

-   **클라우드의 ID**

    -   DirSync 또는 AAD(Azure Active Directory) Connect를 사용하나요?

    -   환경이 페더레이션되었나요?

    -   다단계 인증을 사용하나요?

-   **메일 환경**

    -   Exchange를 사용 중인가요? 그렇다면 온-프레미스 또는 클라우드에서 사용하고 있나요?

    -   프로젝트 도중에 Exchange를 클라우드로 마이그레이션하나요?

-   **현재 MDM 솔루션**

    -   현재 다른 MDM 솔루션을 사용하고 있나요?

    -   회사 및 BYOD 사용 사례 시나리오에 사용하고 있는 MDM 솔루션은 무엇인가요?

    -   사용하고 있는 기능은 무엇인가요(예: 앱 장치 설정, Wi-Fi 구성 등)?

    -   어떤 장치 플랫폼이 지원되나요?

    -   어떤 그룹이 MDM 솔루션을 사용하고 있으며 그 사용자 수는 어떻게 되나요?

-   **인증서 솔루션**

    -   인증서 솔루션을 구현했나요?

    -   어떤 유형의 인증서를 사용하나요?

-   **시스템 관리**

    -   PC 및 서버 환경을 어떻게 관리하고 있나요?

    -   System Center Configuration Manager를 사용하고 있나요? 타사 시스템 관리 플랫폼을 사용하고 있나요?

-   **VPN 솔루션**

    -   사용 중인 VPN 솔루션은 무엇인가요?

    -   그 솔루션을 회사 및 BYOD 사용 사례 시나리오 둘 다에 사용하나요?

현재 MDM 환경을 기록할 때 사용자 환경을 변경할 수 있도록 모든 프로젝트 또는 다른 모든 계획이 적절히 준비되었는지 확인해야 합니다. 다음은 Intune 설계를 만들 때 도움이 되도록 현재 환경을 기록하는 방법의 예입니다.

| **솔루션 영역** | **현재 환경** | **설명** |
|:---:|:---:|:---:|
| **ID** | Azure AD, Azure AD Connect, 페더레이션되지 않음, MFA 없음 | 연말까지 MFA를 사용할 수 있도록 프로젝트 준비 |                 
| **메일 환경** | Exchange 온-프레미스, Exchange Online | 현재 Exchange 온-프레미스에서 Exchange Online으로 마이그레이션 중입니다. 사서함의 75%가 마이그레이션되었습니다. Intune 파일럿이 시작되기 전에 나머지 25%가 마이그레이션됩니다. |                
| **SharePoint** | SharePoint 온-프레미스 | SharePoint Online으로 이동할 계획 없음 |  
| **현재 MDM** | Exchange ActiveSync |  |
| **인증서 솔루션** | Microsoft Server 2012 R2, AD 인증서 서비스 | 웹 사이트 서버에 PKI만 사용 |
| **시스템 관리** | System Center Configuration Manager CB 1606 | Intune 하이브리드 솔루션을 조사하려 함 |
| **VPN 솔루션** | Cisco AnyConnect |  |

## <a name="choose-an-intune-deployment-option"></a>Intune 배포 옵션 선택

Intune은 두 가지 배포 옵션 즉, 독립 실행형 및 하이브리드를 제공합니다. 따라서 어떤 옵션이 비즈니스 요구 사항에 적합한지 결정해야 합니다. 독립 실행형은 클라우드에서 실행되는 Intune 서비스를 나타내며, 하이브리드는 Intune과 System Center Configuration Manager의 통합을 나타냅니다.

- [Microsoft Intune 독립 실행형 및 System Center Configuration Manager에서 하이브리드 모바일 장치 관리 선택](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)에 대해 자세히 알아보세요.

## <a name="intune-tenant-location"></a>Intune 테넌트 위치

조직이 글로벌 서비스를 제공하는 경우 서비스를 구독할 때 테넌트가 상주할 위치를 계획해야 합니다. 처음으로 Intune 구독을 등록하고 아래에 나와 있는 전 세계의 지역에 매핑할 때 국가가 정의됩니다.

-   북아메리카

-   유럽, 중동 및 아프리카

-   아시아 및 태평양

>[!IMPORTANT]
> 나중에 국가/테넌트 위치를 변경할 수 없습니다.

## <a name="external-dependencies"></a>외부 종속성

외부 종속성은 Intune과 분리되어 있지만 Intune의 요구 사항이거나 Intune과 통합될 수 있는 서비스 및 제품입니다. 모든 외부 종속성과 그 구성 방식에 대한 요구 사항을 파악하는 것이 중요합니다. 일반적인 외부 종속성의 몇 가지 예가 아래에 나와 있습니다.

-   ID

-   사용자 및 장치 그룹

-   PKI

아래에서 이러한 일반적인 외부 종속성을 더 자세히 살펴보겠습니다.

### <a name="identity"></a>ID

ID는 조직에 속해 있으며 장치를 등록하는 사용자를 식별하는 방법입니다. Intune은 사용자 ID 공급자로 Azure AD(Azure Active Directory)가 필요합니다. 이 서비스를 이미 사용하고 있는 경우 클라우드에서 기존 ID를 이미 활용 중일 수 있습니다. 또한 Azure AD Connect는 Microsoft 클라우드 서비스와 온-프레미스 사용자 ID를 동기화하기 위한 추천 도구입니다. 조직이 이미 Office 365를 사용하고 있는 경우 Intune에서 동일한 Azure Active Directory 환경을 사용하는 것이 중요합니다.

Intune의 ID 요구 사항에 대한 자세한 내용은 아래에서 찾아볼 수 있습니다.

-   [ID 요구 사항](https://docs.microsoft.com/active-directory/active-directory-hybrid-identity-design-considerations-overview#design-considerations-overview)에 대해 자세히 알아보세요.

-   [디렉터리 동기화 요구 사항](https://docs.microsoft.com/active-directory/active-directory-hybrid-identity-design-considerations-directory-sync-requirements)에 대해 자세히 알아보세요.

-   [다단계 인증 요구 사항](https://docs.microsoft.com/active-directory/active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements)에 대해 자세히 알아보세요.

### <a name="user-and-device-groups"></a>사용자 및 장치 그룹

사용자 및 장치 그룹은 배포의 대상을 결정합니다. 여기에는 정책, 응용 프로그램 및 프로필에 대한 배포 대상이 포함될 수 있습니다. Intune 클라우드는 사용자 및 장치 그룹만 지원합니다. 따라서 어떤 사용자 및 장치 그룹이 필요할지 결정해야 합니다. 모든 그룹을 온-프레미스 Active Directory에 생성한 후 Azure Active Directory로 동기화하는 것이 좋습니다. 사용자 및 장치 그룹 계획 및 만들기에 대한 자세한 내용은 아래에서 찾아볼 수 있습니다.

-   [사용자 및 장치 그룹 계획](https://docs.microsoft.com/intune/deploy-use/plan-your-user-and-device-groups)에 대해 자세히 알아보세요.

-   [사용자 및 장치 그룹을 만드는 방법](https://docs.microsoft.com/en-us/intune/deploy-use/use-groups-to-manage-users-and-devices-with-microsoft-intune)에 대해 알아보세요.

### <a name="public-key-infrastructure-pki"></a>PKI(공개 키 인프라)

공개 키 인프라는 장치 또는 사용자에 인증서를 제공하여 서비스에 안전하게 인증해 줍니다. Intune은 Microsoft PKI 인프라를 지원합니다. 모바일 장치에 장치 및 사용자 인증서를 발급하여 인증서 기반 인증 요구 사항을 충족할 수 있습니다. 인증서를 구현하기 전에 먼저, 인증서가 필요한지, 네트워크 인프라가 인증서 기반 인증을 지원할 수 있는지 그리고 인증서가 기존 환경에서 현재 사용되는지 확인해야 합니다.

Intune에서 VPN, Wi-Fi 또는 메일 프로필과 함께 인증서를 사용할 계획인 경우 지원되는 [PKI 인프라를 구축](https://docs.microsoft.com/intune/deploy-use/secure-resource-access-with-certificate-profiles)하고 인증서 프로필을 만들고 배포할 준비를 했는지 확인해야 합니다.

또한 SCEP 인증서가 발급될 경우 NDES(네트워크 장치 등록 서비스) 기능을 호스트할 서버 및 통신 수행 방식을 결정해야 합니다.

Intune에서 인증서를 구성하는 방법에 대한 자세한 내용은 다음을 참조하세요.

-   [How to configure the certificate infrastructure for SCEP](https://docs.microsoft.com/intune/deploy-use/configure-certificate-infrastructure-for-scep)(SCEP 인증서 인프라 구성 방법)

-   [PFX 인증서 인프라 구성](https://docs.microsoft.com/intune/deploy-use/configure-certificate-infrastructure-for-pfx)

-   [Intune 인증서 프로필 구성](https://docs.microsoft.com/intune/deploy-use/configure-intune-certificate-profiles)

-   [Microsoft Intune을 사용하여 회사 리소스에 대한 액세스 허용](https://docs.microsoft.com/intune/deploy-use/enable-access-to-company-resources-with-microsoft-intune)

## <a name="device-platform-considerations"></a>장치 플랫폼 고려 사항

장치가 올바르게 작동하는 방법을 이해하려면 해당 장치를 주의 깊게 살펴보아야 합니다.

-   지원되는 장치 플랫폼 확인

-   장치

-   장치 소유권

-   대량 등록

이러한 영역에 대해 더 자세히 살펴보겠습니다.

### <a name="determine-supported-device-platforms"></a>지원되는 장치 플랫폼 확인

환경에서 사용할 장치를 알아야 하며, 설계를 만들 때 Intune에서 해당 장치를 지원하는지 여부를 확인해야 합니다. Intune은 iOS, Android 및 Windows 플랫폼을 지원합니다.

-   [Intune에서 지원되는 장치](https://docs.microsoft.com/intune/get-started/supported-mobile-devices-and-computers)에 대해 자세히 알아보세요.

### <a name="devices"></a>장치

Intune에서 모바일 장치를 관리하여 회사 데이터를 보호하고 최종 사용자가 더 많은 위치에서 작업할 수 있습니다. Intune이 여러 장치 플랫폼을 지원하므로 조직의 설계에서 지원할 장치 및 OS 플랫폼을 문서화하는 것이 좋습니다. 이는 사용 사례 요구 사항 섹션에 따라 만든 장치 및 플랫폼에서 확장됩니다.

또한 OS 플랫폼 및 버전을 기준으로 장치 기능을 확인할 때 목록을 참조할 버전을 알고 있는 것이 좋습니다. 예는 다음과 같습니다.

| **장치 플랫폼** | **OS 버전** |
|:---:|:---:|
| iOS - iPhone | 9.0+ |                
| iOS - iPad | 8.0+ |               
| Android - Samsung Knox Standard | 4.0+ |
| Windows 10 태블릿 | 10+ |

### <a name="device-ownership"></a>장치 소유권

Intune은 회사 소유 및 BYOD 소유권을 둘 다 지원합니다. 장치가 장치 등록 관리자 또는 장치 등록 프로그램을 통해 등록된 경우 회사 소유로 간주됩니다. 예를 들어 Apple DEP를 통해 장치를 등록하고 회사 소유로 표시하고 대상 회사 정책 및 앱을 수신하는 장치 그룹에 배치할 수 있습니다.

회사 및 BYOD 사용 사례에 대한 자세한 내용은 [섹션 3: 사용 사례 시나리오 요구 사항 확인](section-3-determine-use-case-requirements.md)을 참조하세요.

### <a name="bulk-enrollment"></a>대량 등록

회사 포털을 통한 셀프 서비스 등록을 보완하기 위해 Intune에서 장치를 등록하는 데 사용할 수 있는 여러 등록 옵션이 있습니다. 대량 등록은 플랫폼에 따라 다양한 방법으로 수행할 수 있습니다. 대량 등록이 필요할 경우 먼저, 대량 등록 방법을 결정하고 설계에 통합해야 합니다. 대량 등록의 다양한 방법에 대한 자세한 내용은 아래에서 찾아보세요.

-   [대량 등록](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)에 대해 자세히 알아보세요.

## <a name="feature-requirements"></a>기능 요구 사항

다음 섹션에서는 다음 기능 및 사용 사례 시나리오 요구 사항에 부합되는 기능을 살펴보겠습니다.

-   사용 약관 정책

-   정책

-   리소스 프로필

-   앱

-   준수 정책

-   조건부 액세스

이러한 각 영역에 대해 더 자세히 살펴보겠습니다.

### <a name="terms-and-conditions-policies"></a>사용 약관 정책

사용 약관은 최종 사용자가 등록하기 전에 수락해야 하는 정책 또는 조건을 설명하는 데 사용할 수 있습니다. Intune은 여러 사용 약관 정책을 사용자 그룹에 추가하고 배포하는 기능을 지원합니다. 사용 약관 정책이 필요한지 여부를 확인해야 합니다. 사용 약관 정책이 필요한 경우 조직에서 이 정보를 제공하는 담당자를 확인해야 합니다.

-   [사용 약관 정책을 만드는 방법](https://docs.microsoft.com/intune/deploy-use/terms-and-condition-policy-settings-in-microsoft-intune)에 대해 알아보세요. 다음은 사용 약관 정책을 문서화하는 방법의 예입니다.

| **사용 약관 이름** | **사용 사례** | **대상 그룹** |
|:---:|:---:|:---:|
| 회사 T&C | 회사 | 회사 사용자 |                 
| BYOD T&C | BYOD | BYOD 사용자 |                

### <a name="configuration-policies"></a>구성 정책

구성 정책은 장치에 대한 보안 설정 및 기능을 관리하는 데 사용됩니다. 구성 정책을 설계할 때 Intune 장치에 필요한 구성을 확인하려면 사용 사례 요구 사항 섹션을 참조하세요. 구성해야 할 설정과 그 방법을 문서화하고, 대상으로 지정할 사용자 또는 장치 그룹도 문서화하세요.

플랫폼별 구성 정책을 하나 이상 만들어야 합니다. 필요한 경우 플랫폼별로 여러 구성 정책을 만들 수 있습니다. 다음은 서로 다른 플랫폼 및 사용 사례 시나리오에 대한 네 가지의 다른 구성 정책을 설계하는 예입니다.

| **정책 이름** | **장치 플랫폼** | **설정** | **대상 그룹** |   
|:---:|:---:|:---:|:---:|
| 회사 - iOS | iOS | PIN은 필수, 길이는 6자, 클라우드 백업 제한 | 회사 장치 |                                                           
| 회사 - Android | Android | PIN은 필수, 길이는 6자, 클라우드 백업 제한 | 회사 장치 |                                                           
| BYOD - iOS  | iOS | PIN은 필수, 길이는 4자 | BYOD 장치 |
| BYOD - Android  | Android | PIN은 필수, 길이는 4자 | BYOD 장치 |

### <a name="profiles"></a>프로필

프로필은 최종 사용자가 회사 데이터에 연결하는 데 사용됩니다. Intune은 여러 유형의 프로필을 지원합니다. [프로필](https://docs.microsoft.com/intune/deploy-use/enable-access-to-company-resources-with-microsoft-intune)을 구성할 시기를 결정하려면 사용 사례 및 요구 사항을 참조하세요. 모든 장치 프로필은 플랫폼 유형에 따라 분류되며, 설계 설명서에 포함되어야 합니다.

-   인증서 프로필

-   Wi-Fi 프로필

-   VPN 프로필

-   전자 메일 프로필

각 유형의 프로필을 더 자세히 살펴보겠습니다.

##### <a name="certificate-profiles"></a>인증서 프로필

인증서 프로필을 통해 Intune이 사용자 또는 장치에 인증서를 발급할 수 있습니다. Intune에서는 다음을 지원합니다.

-   SCEP(단순 인증서 등록 프로토콜)

-   신뢰할 수 있는 루트 인증서

-   PFX 인증서

인증서가 필요한 사용자 그룹, 필요한 인증서 프로필의 수 및 인증서 프로필의 배포 대상이 되는 사용자 그룹을 문서화하는 것이 좋습니다.

>[!NOTE]
> 신뢰할 수 있는 루트 인증서는 SCEP 인증서에 필요하므로 SCEP 인증서 대상으로 지정된 모든 사용자가 신뢰할 수 있는 루트 인증서도 받을 수 있는지 확인해야 합니다. SCEP 인증서가 필요한 경우 어떤 SCEP 인증서 템플릿이 필요할지 설계하고 문서화하세요.

다음은 설계하는 동안 인증서를 문서화할 수 있는 방법의 예입니다.

| **유형** | **프로필 이름** | **장치 플랫폼** | **사용 사례** |   
|:---:|:---:|:---:|:---:|
| 루트 CA | 회사 루트 CA | Android, iOS, Windows Mobile | 회사, BYOD  |                                                           
| SCEP | 사용자 인증서 | Android, iOS, Windows Mobile | 회사, BYOD |                                                           

##### <a name="wi-fi-profile"></a>Wi-Fi 프로필

Wi-Fi 프로필은 모바일 장치를 무선 네트워크에 자동으로 연결하는 데 사용됩니다. Intune은 지원되는 모든 플랫폼에 대한 Wi-Fi 프로필 배포를 지원합니다.

-   [Intune에서 Wi-Fi 프로필을 지원하는 방법](https://docs.microsoft.com/intune/deploy-use/wi-fi-connections-in-microsoft-intune)에 대해 자세히 알아보세요.

다음은 Wi-Fi 프로필에 대한 설계의 예입니다.

| **유형** | **프로필 이름** | **장치 플랫폼** | **사용 사례** |   
|:---:|:---:|:---:|:---:|
| Wi-Fi | 아시아 Wi-Fi 프로필 | Android | 회사, BYOD 아시아 지역|                                                           
| Wi-Fi | 북아메리카 Wi-Fi 프로필 | Android, iOS, Windows 10 Mobile | 회사, BYOD 북아메리카 지역 |                                                           

##### <a name="vpn-profile"></a>VPN 프로필

VPN 프로필을 통해 사용자가 원격 위치에서 네트워크에 안전하게 액세스할 수 있습니다. Intune은 네이티브 모바일 VPN 연결 및 타사 공급업체의 VPN 프로필을 지원합니다.

-   [Intune에서 지원하는 VPN 프로필 및 공급업체](https://docs.microsoft.com/intune/deploy-use/vpn-connections-in-microsoft-intune)에 대해 자세히 알아보세요.

다음은 VPN 프로필의 설계를 문서화하는 예입니다.

| **유형** | **프로필 이름** | **장치 플랫폼** | **사용 사례** |   
|:---:|:---:|:---:|:---:|
| VPN | VPN Cisco의 모든 연결 프로필 | Android, iOS, Windows 10 Mobile | 회사, BYOD 북아메리카 및 독일|                                                           
| VPN | Pulse Secure | Android | 회사, BYOD 아시아 지역 |                                                           

##### <a name="email-profile"></a>전자 메일 프로필

메일 프로필을 통해 메일 클라이언트가 연결 정보를 사용하여 자동으로 설정되고 메일 구성을 설정할 수 있습니다. Intune은 일부 장치에서 메일 프로필을 지원합니다.

-   [메일 프로필](https://docs.microsoft.com/en-us/intune/deploy-use/configure-access-to-corporate-email-using-email-profiles-with-microsoft-intune)에 대해 자세히 알아보세요.

다음은 메일 프로필의 설계를 문서화하는 예입니다.

| **유형** | **프로필 이름** | **장치 플랫폼** | **사용 사례** |   
|:---:|:---:|:---:|:---:|
| 전자 메일 프로필 | iOS 메일 프로필 | iOS | 회사 - 정보 근로자 BYOD |                                                           
| 전자 메일 프로필 | Android Knox 메일 프로필 | Android Knox | BYOD |

### <a name="apps"></a>앱

Intune은 여러 가지 방법으로 사용자 또는 장치에 대한 앱 배달을 지원합니다. 배달된 응용 프로그램의 유형은 소프트웨어 설치 관리자 앱, 공용 앱 스토어의 앱, 외부 링크 또는 관리되는 iOS 앱일 수 있습니다. 개별 앱 배포 외에도 대량 구매 앱은 iOS 및 Windows의 대량 구매 프로그램을 통해 관리하고 배포할 수 있습니다. Intune에서 앱 및 대량 구매 프로그램을 지원하는 방법에 대한 자세한 내용이 아래에 나와 있습니다.

-   [앱 유형](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)에 대해 자세히 알아보세요.

-   [비즈니스용 iOS VPP(대량 구매 프로그램)](https://docs.microsoft.com/intune/deploy-use/manage-ios-apps-you-purchased-through-a-volume-purchase-program-with-microsoft-intune)에 대해 자세히 알아보세요.

-   [비즈니스용 Windows 스토어](https://docs.microsoft.com/intune/deploy-use/manage-apps-you-purchased-from-the-windows-store-for-business-with-microsoft-intune)에 대해 자세히 알아보세요.

#### <a name="app-type-requirements"></a>앱 유형 요구 사항

앱을 사용자 및 장치에 배포할 수 있으므로 Intune에서 관리할 응용 프로그램을 결정하는 것이 좋습니다. 목록을 수집하는 동안 다음 질문에 대답해 보세요.

-   앱이 클라우드 서비스와 통합되어야 합니까?

-   BYOD 사용자가 모든 앱을 사용할 수 있나요?

-   이러한 앱에 사용할 수 있는 배포 옵션은 무엇인가요?

-   회사가 파트너에 대해 SaaS(Software as a Service) 앱 데이터 액세스를 제공해야 하나요?

-   앱이 사용자 장치에서 인터넷에 액세스해야 하나요?

-   앱 스토어에서 앱을 공개적으로 사용할 수 있나요 아니면 앱이 사용자 지정 LOB(기간 업무) 앱인가요?


>[!TIP]
> [Microsoft Intune을 사용하여 앱 추가](https://docs.microsoft.com/intune/deploy-use/add-apps)를 확인해 보세요.

#### <a name="app-protection-policies"></a>앱 보호 정책

앱 보호 정책은 응용 프로그램에서 회사 데이터를 관리하는 방법을 정의하여 데이터 손실을 최소화합니다. Intune은 모바일 앱 관리와 함께 작동하도록 빌드된 응용 프로그램에 대해 앱 보호 정책을 지원합니다. 앱 보호 정책을 설계할 때 지정된 앱에서 회사 데이터에 지정할 제한 사항을 결정해야 합니다. [앱 데이터 보호](https://docs.microsoft.com/intune/deploy-use/protect-app-data-using-mobile-app-management-policies-with-microsoft-intune)가 작동하는 방식을 검토하는 것이 좋습니다. 다음은 기존 응용 프로그램을 문서화하는 방법 및 필요한 보호의 예입니다.

| **응용 프로그램** | **용도** | **플랫폼** | **사용 사례** | **앱 보호 정책** |
|:---:|:---:|:---:|:---:|:---:|
| Outlook Mobile  | 사용 가능 | iOS | 회사 - 임원 | 무단 해제할 수 없음, 파일 암호화 |                                                         
| Word | 사용 가능 | iOS, Android - Samsung Knox, 비 Knox, Windows 10 Mobile | 회사, BYOD | 무단 해제할 수 없음, 파일 암호화 |                                                         

#### <a name="compliance-policies"></a>규정 준수 정책

준수 정책은 장치가 특정 요구 사항을 준수하는지 여부를 결정합니다. Intune은 준수 정책을 사용하여 장치를 규격으로 간주할지, 비규격으로 간주할지 여부를 결정합니다. 그런 다음 회사 리소스에 대한 액세스를 제한하는 데 준수 상태를 사용할 수 있습니다. 조건부 액세스가 필요한 경우 [장치 준수 정책](https://docs.microsoft.com/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune)을 설계하는 것이 좋습니다. 얼마나 많은 장치 준수 정책이 필요한지 그리고 어떤 사용자 그룹이 대상 사용자 그룹인지 판단하려면 요구 사항 및 사용 사례를 참조하세요. 또한 비규격으로 간주되기 전까지 체크 인하지 않고 장치가 얼마나 오랫동안 오프라인으로 있을 수 있는지를 결정해야 합니다.

다음은 준수 정책을 설계하는 방법의 예입니다.

| **정책 이름** | **장치 플랫폼** | **설정** | **대상 그룹** |   
|:---:|:---:|:---:|:---:|
| 준수 정책 | iOS, Android - Samsung Knox, 비 Knox, Windows 10 Mobile | PIN - 필수, 무단 해제할 수 없음 | 회사, BYOD |

#### <a name="conditional-access-policies"></a>조건부 액세스 정책

조건부 액세스는 규격 장치만 회사 리소스에 액세스하도록 허용하는 데 사용됩니다. Intune은 전체 EMS(Enterprise Mobility + Security)에서 작동하여 회사 리소스에 대한 액세스를 제어합니다. 사용자는 조건부 액세스가 필요한지와 보호해야 하는 대상을 결정해야 합니다.

-   [조건부 액세스](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-email-and-o365-services-with-microsoft-intune)에 대해 자세히 알아보세요.

온라인 액세스의 경우 조건부 액세스 정책에서 대상으로 지정할 플랫폼 및 사용자 그룹을 결정하세요.

또한 Exchange Online 또는 Exchange 온-프레미스용 Intune Service-to-Service Connector를 설치/구성해야 하는지 여부를 결정해야 합니다.

다음에서 Intune Service-to-Service Connector를 설치하고 구성하는 방법을 자세히 알아보세요.

-   [Exchange Online](https://docs.microsoft.com/intune/deploy-use/intune-service-to-service-exchange-connector)

-   [Exchange 온-프레미스](https://docs.microsoft.com/intune/deploy-use/intune-on-premises-exchange-connector)

다음은 조건부 액세스 정책을 문서화하는 방법의 예입니다.

| **서비스** | **최신 인증용 플랫폼** | **기본 인증** | **사용 사례** |   
|:---:|:---:|:---:|:---:|
| Exchange Online | iOS, Android | Intune에서 지원하는 플랫폼에서 비규격 장치 차단 | 회사, BYOD |
| SharePoint Online | iOS, Android |  | 회사, BYOD |

## <a name="next-section"></a>다음 섹션

다음 섹션에서는 [Intune 구현 프로세스](section-8-onboarding-process.md)에 대한 지침을 제공합니다.



<!--HONumber=Dec16_HO5-->

