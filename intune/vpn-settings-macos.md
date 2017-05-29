---
title: "macOS 장치에 대한 Intune VPN 설정 | Microsoft 문서"
titleSuffix: Intune Azure preview
description: "Intune Azure 미리 보기: macOS 장치에서 VPN 연결을 구성하는 데 사용할 수 있는 Intune 설정을 알아봅니다."
keywords: 
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.date: 05/04/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: d203a70d-37df-4195-85f7-ad5ef14ac2a1
ms.reviewer: karanda
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: 4737fc863e3eda92eafd0536a07abf4100ebe9cc
ms.contentlocale: ko-kr
ms.lasthandoff: 05/23/2017


---

# <a name="vpn-settings-for-macos-devices-in-microsoft-intune"></a>Microsoft Intune의 macOS 장치에 대한 VPN 설정

[!INCLUDE[azure_preview](./includes/azure_preview.md)]

선택한 설정에 따라 아래 목록의 일부 값을 구성할 수 없습니다.

## <a name="base-vpn-settings"></a>**기본 VPN 설정**

**연결 이름** - 이 연결에 대한 이름을 입력합니다. 최종 사용자가 장치에서 사용 가능한 VPN 연결 목록을 찾아볼 때 이 이름이 표시됩니다.
- **IP 주소 또는 FQDN** - 장치를 연결할 VPN 서버의 정규화된 도메인 이름 또는 IP 주소를 입력합니다. 예: **192.168.1.1**, **vpn.contoso.com**.
- **인증 방법** - 장치에서 VPN 서버에 인증할 방법을 선택합니다.
    - **인증서** - **인증 인증서** 아래에서 이전에 연결을 인증하기 위해 만든 SCEP 또는 PKCS 인증서 프로필을 선택합니다. 인증서 프로필에 대한 자세한 내용은 [인증서를 구성하는 방법](certificates-configure.md)을 참조하세요.
    - **사용자 이름 및 암호** - 최종 사용자는 VPN 서버에 로그인하기 위해 사용자 이름 및 암호를 제공해야 합니다.
- **연결 형식** - 다음 공급업체 목록에서 VPN 연결 형식을 선택합니다.
    - **검사점 캡슐 VPN**
    - **Cisco AnyConnect**
    - **Dell SonicWALL Mobile Connect**
    - **F5 Edge Client**
    - **Pulse Secure**
    - **사용자 지정 VPN**
- **분할 터널링** - 장치에서 트래픽에 따라 사용할 연결을 결정할 수 있도록 하는 이 옵션을 **사용**하거나 **사용하지 않도록** 설정합니다. 예를 들어 호텔에 있는 사용자는 VPN 연결을 사용하여 작업 파일에 액세스하지만 일반적인 웹 검색에는 호텔의 표준 네트워크를 사용합니다.

<!--- **Per-app VPN** - Select this option if you want to associate this VPN connection with an iOS or macOS app so that the connection will be opened when the app is run. You can associate the VPN profile with an app when you assign the software. For more information, see [How to assign and monitor apps](apps-deploy.md). --->

## <a name="custom-vpn-settings"></a>사용자 지정 VPN 설정

**사용자 지정 VPN**을 선택한 경우 다음 추가 설정을 구성합니다.

- **VPN 식별자** 사용 중인 VPN 앱의 식별자이며, VPN 공급자가 제공합니다.
- **사용자 지정 VPN 특성에 대한 키 및 값 쌍을 입력합니다.** VPN 연결을 사용자 지정하는 **키** 및 **값**을 추가하거나 가져옵니다. 이러한 값은 일반적으로 VPN 공급자가 제공합니다.


## <a name="proxy-settings"></a>프록시 설정

- **자동 구성 스크립트** - 파일을 사용하여 프록시 서버를 구성합니다. 구성 파일이 포함된 **프록시 서버 URL**(예: **http://proxy.contoso.com**)을 입력합니다.
- **주소** - 프록시 서버 주소를 IP 주소로 입력합니다.
- **포트 번호** - 프록시 서버와 연결된 포트 번호를 입력합니다.

