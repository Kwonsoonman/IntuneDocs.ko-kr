---
title: "iOS 장치에 대한 Intune VPN 설정"
titlesuffix: Azure portal
description: "iOS 장치에서 VPN 연결을 구성하는 데 사용할 수 있는 Intune 설정을 알아봅니다.\""
keywords: 
author: vhorne
ms.author: victorh
manager: angrobe
ms.date: 12/15/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 1447c123-ea33-4ea0-aab4-69577cdb8d00
ms.reviewer: karanda
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: fe6878601f84ccf6c7296a039060b4049a17e22d
ms.sourcegitcommit: a3a744ea55f38a360ca9f788c77a5b3018d1add5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/30/2017
---
# <a name="vpn-settings-for-ios-devices-in-microsoft-intune"></a>Microsoft Intune의 iOS 장치에 대한 VPN 설정

[!INCLUDE[azure_portal](./includes/azure_portal.md)]

선택한 설정에 따라 다음 목록의 일부 값을 구성할 수 없습니다.

## <a name="base-vpn-settings"></a>기본 VPN 설정


**연결 이름** - 이 연결에 대한 이름을 입력합니다. 최종 사용자가 장치에서 사용 가능한 VPN 연결 목록을 찾아볼 때 이 이름이 표시됩니다.
- **IP 주소 또는 FQDN** - 장치가 연결되는 VPN 서버의 IP 주소 또는 정규화된 도메인 이름을 입력합니다. 예: **192.168.1.1**, **vpn.contoso.com**.
- **인증 방법** - 장치에서 VPN 서버에 인증하는 방법을 선택합니다.
    - **인증서** - **인증 인증서** 아래에서 이전에 연결을 인증하기 위해 만든 SCEP 또는 PKCS 인증서 프로필을 선택합니다. 인증서 프로필에 대한 자세한 내용은 [인증서를 구성하는 방법](certificates-configure.md)을 참조하세요.
    - **사용자 이름 및 암호** - 최종 사용자는 VPN 서버에 로그인하기 위해 사용자 이름 및 암호를 제공해야 합니다.
- **연결 형식** - 다음 공급업체 목록에서 VPN 연결 형식을 선택합니다.
    - **검사점 캡슐 VPN**
    - **Cisco AnyConnect**
    - **Dell SonicWALL Mobile Connect**
    - **F5 Edge Client**
    - **Pulse Secure**
    - **Cisco(IPSec)**
    - **Citrix**
    - **사용자 지정 VPN**
- **분할 터널링** - 장치에서 트래픽에 따라 사용할 연결을 결정할 수 있도록 하는 이 옵션을 **사용** 또는 **사용 안 함**으로 설정합니다. 예를 들어 호텔에 있는 사용자는 VPN 연결을 사용하여 작업 파일에 액세스하지만, 일반적인 웹 검색에는 호텔의 표준 네트워크를 사용합니다.


## <a name="custom-vpn-settings"></a>사용자 지정 VPN 설정

**사용자 지정 VPN**을 연결 형식으로 선택한 경우 다음 추가 설정을 구성합니다.

- **VPN 식별자** 사용 중인 VPN 앱의 식별자이며, VPN 공급자가 제공합니다.
- **사용자 지정 VPN 특성에 대한 키 및 값 쌍을 입력합니다.** VPN 연결을 사용자 지정하는 **키** 및 **값**을 추가하거나 가져옵니다. 이러한 값은 일반적으로 VPN 공급자가 제공합니다.

## <a name="apps-per-app-vpn-settings"></a>앱(앱별 VPN) 설정

- **앱별 VPN** - Safari 브라우저에서 방문할 때 URL에서 VPN 연결을 사용하려면 이 옵션을 사용하도록 설정합니다. 이를 구성하려면 기본 VPN 설정에서 **인증서**를 인증 방법으로 선택해야 합니다.
- **Safari 브라우저를 사용하는 동안 VPN 연결을 사용하도록 설정할 URL** - [추가]를 클릭하여 하나 이상의 웹 사이트 URL을 추가합니다. 이러한 URL을 방문하는 경우 VPN 연결이 사용하도록 설정됩니다.

- **주문형 규칙** - VPN 연결이 시작되는 경우를 제어하는 조건부 규칙을 구성할 수 있습니다. 예를 들어 장치가 회사 Wi-Fi 네트워크 중 하나에 연결되지 않은 경우에만 VPN 연결이 사용되는 조건을 만들 수 있습니다. 또는 장치에서 지정한 DNS 검색 도메인에 액세스할 수 없는 경우 VPN 연결이 시작되지 않는 조건을 만들 수 있습니다.

    - **SSID 또는 DNS 검색 도메인** - 이 조건에서 무선 네트워크 **SSID** 또는 **DNS 검색 도메인**을 사용할지를 선택합니다. 하나 이상의 SSID 또는 검색 도메인을 구성하려면 추가를 선택합니다.
    - **URL 문자열 프로브** - 선택적으로 규칙에서 테스트로 사용하는 URL을 제공합니다. 이 프로필이 설치된 장치에서 리디렉션 없이 이 URL에 액세스할 수 있는 경우 VPN 연결이 시작되고 장치가 대상 URL에 연결됩니다. 사용자에게 URL 문자열 프로브 사이트가 표시되지 않습니다. URL 문자열 프로브의 예는 VPN을 연결하기 전에 장치 준수를 확인하는 감사 웹 서버의 주소입니다. 또는 VPN을 통해 장치를 대상 URL에 연결하기 전에 URL에서 VPN이 사이트에 연결할 수 있는지 테스트할 수도 있습니다.
    - **도메인 작업** - 다음 항목 중 하나를 선택합니다.
        - 필요한 경우 연결 - 
        - 연결 안 함 - 
    - **작업** - 다음 항목 중 하나를 선택합니다.
        - 연결 - 
        - 연결 평가 - 
        - 무시 - 
        - 연결 끊기 - 


## <a name="proxy-settings"></a>프록시 설정

- **자동 구성 스크립트** - 파일을 사용하여 프록시 서버를 구성합니다. 구성 파일이 포함된 **프록시 서버 URL**(예: **http://proxy.contoso.com**)을 입력합니다.
- **주소** - 프록시 서버 주소를 IP 주소로 입력합니다.
- **포트 번호** - 프록시 서버와 연결된 포트 번호를 입력합니다.