---
title: Microsoft Intune - Azur에서 VPN 설정 보기 | Microsoft Docs
description: 트래픽 규칙, 조건부 액세스, Windows 10 장치에 대한 DNS 및 프록시 설정, Windows Holographic for Business 장치를 포함해 Microsoft Intune에서 사용할 수 있는 VPN 설정, 사용 목적 및 수행 작업에 대해 읽고 알아봅니다.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/8/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.suite: ems
ms.reviewer: tycast
ms.custom: intune-azure
ms.openlocfilehash: 9464b73acc43b9625560156617359c374d7100fb
ms.sourcegitcommit: 5eba4bad151be32346aedc7cbb0333d71934f8cf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="read-about-the-vpn-settings-in-intune"></a>Intune에서 VPN 설정에 대해 읽기

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

Intune을 사용하여 VPN 연결을 구성할 수 있습니다. 이 아티클에서는 이러한 설정, 트래픽 규칙, 조건부 액세스, DNS 및 프록시 설정을 설명합니다.

이러한 설정은 다음에 적용됩니다.

- Windows 10을 실행하는 장치
- Windows Holographic for Business를 실행하는 장치

선택하는 설정에 따라 일부 값은 구성할 수 없습니다.

## <a name="base-vpn-settings"></a>기본 VPN 설정

- **연결 이름**: 이 연결에 대한 이름을 입력합니다. 최종 사용자가 장치에서 사용 가능한 VPN 연결 목록을 찾아볼 때 이 이름이 표시됩니다.
- **서버**: 장치를 연결할 한 대 이상의 VPN 서버를 추가합니다.
  - **추가**: 다음 정보를 입력하는 **행 추가**를 엽니다.
    - **설명**: 서버의 설명이 포함된 이름(예: **Contoso VPN 서버**) 입력
    - **IP 주소 또는 FQDN**: 장치가 연결되는 VPN 서버(예: **192.168.1.1** 또는 **vpn.contoso.com**)의 IP 주소 또는 정규화된 도메인 이름 입력
    - **기본 서버**: 이 서버를 장치에서 연결을 설정하는 데 사용할 기본 서버로 사용합니다. 기본적으로 하나의 서버만 설정합니다.
  - **가져오기**: 설명, IP 주소 또는 FQDN, 기본 서버 형식의 서버 목록을 포함하는 쉼표로 구분된 파일로 이동합니다. **확인**을 선택하여 이러한 서버를 **서버** 목록으로 가져옵니다.
  - **내보내기**: 서버 목록을 쉼표로 구분된 값(csv) 파일로 내보내기

**연결 형식**: 다음 공급업체 목록에서 VPN 연결 형식을 선택합니다.

- **자동**
- **검사점 캡슐 VPN**
- **Citrix VPN**
- **SonicWall Mobile Connect**
- **F5 Edge Client**
- **IKEv2**
- **L2TP**
- **PPTP**
- **Pulse Secure**

**로그인 그룹 또는 도메인**(SonicWALL Mobile Connect만 해당): VPN 프로필에 이 속성을 설정할 수 없습니다. 대신, Mobile Connect는 사용자 이름 및 도메인을 `username@domain` 또는 `DOMAIN\username` 형식으로 입력할 경우 이 값을 구문 분석합니다.

**사용자 지정 XML**/**EAP XML**: VPN 연결을 구성하는 사용자 지정 XML 명령을 입력합니다.

**Pulse Secure의 예:**

```
<pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
```

**CheckPoint 모바일 VPN의 예:**

```
<CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
```

**SonicWall Mobile Connect의 예:**

```
<MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
```

**F5 Edge Client의 예:**

```
<f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
```

사용자 지정 XML 명령을 작성하는 방법에 대한 자세한 내용은 각 제조업체의 VPN 설명서를 참조하세요.

사용자 지정 EAP XML을 만드는 방법에 대한 자세한 내용은 [EAP 구성](https://docs.microsoft.com/windows/client-management/mdm/eap-configuration)을 참조하세요.

**분할 터널링**: 장치에서 트래픽에 따라 사용할 연결을 결정할 수 있도록 **사용** 또는 **사용 안 함**으로 설정합니다. 예를 들어 호텔에 있는 사용자는 VPN 연결을 사용하여 작업 파일에 액세스하지만, 일반적인 웹 검색에는 호텔의 표준 네트워크를 사용합니다.
- **이 VPN 연결에 대한 분할 터널링 경로**: 타사 VPN 공급자에 대한 선택적 경로를 추가합니다. 대상 접두사 및 각각의 접두사 크기를 입력합니다.

## <a name="apps-and-traffic-rules"></a>앱 및 트래픽 규칙

**이러한 앱에 VPN 연결을 사용하도록 제한**: 일부 앱에서 이 VPN 연결을 사용하게 하려면 이 설정을 사용합니다.
**연결된 앱**: 자동으로 VPN 연결을 사용하는 앱 목록을 입력합니다. 앱의 유형에 따라 앱 식별자가 결정됩니다. 유니버설 앱의 경우 패키지 패밀리 이름을 입력합니다. 데스크톱 앱의 경우에는 앱의 파일 경로를 입력합니다.

>[!IMPORTANT]
>앱당 VPN에 대해 만든 모든 앱 목록을 보호하는 것이 좋습니다. 권한이 없는 사용자가 이 목록을 변경한 경우 해당 목록을 앱별 VPN 앱 목록으로 가져오는 경우 액세스 권한이 부여되면 안 되는 앱에 VPN 액세스 권한을 잠재적으로 부여하게 됩니다. 앱 목록을 보호할 수 있는 한 가지 방법은 ACL(액세스 제어 목록)을 사용하는 것입니다.

**이 VPN 연결에 대한 네트워크 트래픽 규칙**: VPN 연결을 위해 사용할 프로토콜, 로컬 및 원격 포트와 주소 범위를 선택합니다. 네트워크 트래픽 규칙을 만들지 않으면 모든 프로토콜, 포트 및 주소 범위를 사용할 수 있습니다. 규칙을 만들고 나면 해당 규칙에 입력하는 프로토콜, 포트 및 주소 범위만 VPN 연결에 사용됩니다.

## <a name="conditional-access"></a>조건부 액세스

**이 VPN 연결에 대한 조건부 액세스**: 클라이언트에서 장치 준수 흐름이 가능하게 합니다. 사용하도록 설정하면, VPN 클라이언트가 인증에 사용할 인증서를 가져오기 위해 Azure Active Directory와 통신하려고 합니다. 인증서 인증을 사용하려면 VPN을 설정해야 하고, VPN 서버가 Azure Active Directory에서 반환된 서버를 신뢰해야 합니다.

**대체 인증서를 사용한 SSO(Single Sign-On)**: 장치 준수에 대해 Kerberos 인증을 위한 VPN 인증 인증서와 다른 인증서를 사용합니다. 다음 설정으로 인증서를 입력합니다.

- **확장 키 사용**: EKU(확장 키 사용)의 이름
- **개체 식별자**: EKU의 개체 식별자
- **발급자 해시**: SSO 인증서의 지문

## <a name="dns-settings"></a>DNS 설정

**이 VPN 연결의 DNS 이름 및 서버**: 연결이 설정된 후 VPN 연결에 사용할 DNS 서버를 선택합니다.
각 서버에 대해 다음을 입력합니다.
- **DNS 이름**
- **DNS 서버**
- **프록시**

## <a name="proxy-settings"></a>프록시 설정

- **자동으로 프록시 설정 검색**: VPN 서버에 연결을 위한 프록시 서버가 필요한 경우 장치가 연결 설정을 자동으로 검색할지 여부를 선택합니다.
- **자동 구성 스크립트**: 파일을 사용하여 프록시 서버를 구성합니다. 구성 파일을 포함하는 `http://proxy.contoso.com`과 같은 **프록시 서버 URL**을 입력합니다.
- **프록시 서버 사용**: 프록시 서버 설정을 수동으로 입력하려면 이 옵션을 사용합니다.
  - **주소**: 프록시 서버 주소를 IP 주소로 입력
  - **포트 번호**: 프록시 서버와 연결된 포트 번호 입력
- **로컬 주소에 프록시 사용 안 함**: VPN 서버에 연결을 위한 프록시 서버가 필요한 경우 입력하는 로컬 주소에 대해 프록시 서버를 사용하지 않으려면 이 설정을 선택합니다.
