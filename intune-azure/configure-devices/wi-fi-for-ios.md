---
title: "iOS 장치에 대한 Intune Wi-Fi 설정 | Intune Azure 미리 보기 | Microsoft Docs"
description: "Intune Azure 미리 보기: iOS 장치에서 Wi-Fi 연결을 구성하는 데 사용할 수 있는 Intune 설정을 알아봅니다."
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 02/15/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 89229a5e-3421-4221-a62f-fa800620cc0d
ms.reviewer: heenamac
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4d095506215b775d56d172e9aabae1737757310
ms.openlocfilehash: 85224b2758eeb1f9c7745b9f18f250a7d1292e0f
ms.lasthandoff: 02/16/2017


---

# <a name="wi-fi-settings-for-ios-devices-in-microsoft-intune"></a>Microsoft Intune의 iOS 장치에 대한 Wi-Fi 설정

[!INCLUDE[azure_preview](../includes/azure_preview.md)]



## <a name="wi-fi-settings-for-basic-and-enterprise-profiles"></a>기본 및 엔터프라이즈 프로필에 대한 Wi-Fi 설정

- **네트워크 이름** - 이 Wi-Fi 네트워크 설정에 대한 이름을 입력합니다. 사용자가 장치에서 사용 가능한 연결 목록을 찾아볼 때 표시되는 이름입니다.
- **SSID** - Service Set Identifier(서비스 집합 ID)의 약어입니다. 장치에 연결할 무선 네트워크의 실제 이름입니다. 그러나 사용자에게는 연결을 선택할 때 위에서 만든 네트워크 이름만 표시됩니다.
- **자동으로 연결** - 이 네트워크 범위에 있을 때마다 장치를 연결합니다.
- **숨겨진 네트워크** - 이 네트워크가 장치의 사용 가능한 네트워크 목록에 표시되지 않도록 합니다.
- **프록시 설정** - 다음에서 선택합니다.
    - **없음** - 프록시 설정을 구성하지 않습니다.
    - **수동** - **프록시 서버 주소**(IP 주소) 및 연결된 **포트 번호**를 입력합니다.
    - **자동** – 파일을 사용하여 프록시 서버를 구성합니다. 구성 파일이 포함된 **프록시 서버 URL**(예: **http://proxy.contoso.com**)을 입력합니다.

## <a name="wi-fi-settings-for-basic-profiles-only"></a>기본 프로필에만 적용되는 Wi-Fi 설정

- **보안 유형** - Wi-Fi 네트워크에 인증하는 데 사용할 보안 프로토콜을 선택합니다.
    - **열기(인증 없음)** - 네트워크가 안전하지 않은 경우에만 옵션을 사용합니다.
    - **WPA/WPA2 - 개인**
    - **4**

## <a name="wi-fi-settings-for-enterprise-profiles-only"></a>엔터프라이즈 프로필에만 적용되는 Wi-Fi 설정

- **EAP 유형** -보안 무선 연결을 인증하는 데 사용되는 EAP(확장할 수 있는 인증 프로토콜) 유형을 선택합니다.
    - **EAP-FAST**
    - **EAP-SIM**
    - **EAP-TLS**
    - **EAP-TTLS**
    - **LEAP**
    - **PEAP**

### <a name="further-options-when-you-choose-an-eap-type"></a>EAP 유형을 선택할 때의 추가 옵션


|설정 이름|추가 정보|사용하는 경우|
|--------------|-------------|----------|
|**PAC(보호된 액세스 자격 증명) 설정**|인증 서버와 클라이언트 간의 인증된 터널을 설정하기 위해 보호된 액세스 자격 증명을 사용하려는 경우 선택합니다. 다음 중 하나 선택:<br>- **PAC 사용** - 기존 PAC 파일(있는 경우)을 사용합니다.<br>- **PAC 사용 및 프로비전** - PAC 파일을 장치에 프로비전합니다.<br>- **익명으로 PAC 사용 및 프로비전** - PAC 파일을 장치에 프로비전하며, 서버를 인증하지 않아도 PAC 파일이 프로비전되도록 합니다.|EAP 유형이 **EAP-FAST**인 경우|

#### <a name="server-trust"></a>서버 트러스트


|설정 이름|추가 정보|사용하는 경우|
|--------------|-------------|----------|
|**인증서 서버 이름**|신뢰할 수 있는 CA(인증 기관)에서 발급하는 인증서에 사용되는 일반적인 이름입니다. 이 정보를 제공하는 경우 Wi-Fi 네트워크에 연결할 때 최종 사용자 장치에 표시되는 동적 트러스트 대화 상자를 무시할 수 있습니다.|EAP 유형이 **EAP-TLS**, **EAP-TTLS** 또는 **PEAP**인 경우|
|**서버 유효성 검사에 대한 루트 인증서**|연결을 인증하는 데 사용되는 신뢰할 수 있는 루트 인증서 프로필을 선택합니다. |EAP 유형이 **EAP-TLS**, **EAP-TTLS** 또는 **PEAP**인 경우|
|**ID 개인 정보 사용(외부 ID)**|EAP ID 요청에 대한 응답으로 전송되는 텍스트를 지정합니다. 이 텍스트에는 원하는 값을 사용할 수 있습니다. 인증하는 동안 이 익명 ID가 먼저 전송된 다음 실제 ID가 보안 채널을 통해 전송됩니다.|EAP 유형이 **PEAP**인 경우|


#### <a name="client-authentication"></a>클라이언트 인증


|설정 이름|추가 정보|사용하는 경우|
|--------------|-------------|----------|
|**클라이언트 인증에 사용할 클라이언트 인증서(ID 인증서)**|연결을 인증하는 데 사용되는 SCEP 또는 PKCS 인증서 프로필을 선택합니다.|EAP 유형이 **EAP-TLS**인 경우|
|**인증 방법**|연결에 대한 인증 방법을 선택합니다.<br>- **인증서** - 서버에 제공되는 ID 인증서인 SCEP 또는 PKCS 클라이언트 인증서를 선택하려는 경우<br><br>- **사용자 이름 및 암호** - 다른 인증 방법을 지정하려는 경우 <br><br>**사용자 이름 및 암호**를 선택한 경우<br><br>-  **EAP 이외의 방법(내부 ID)**을 구성한 후 연결을 인증할 방법으로 다음 중 하나를 선택합니다.<br>- **없음**<br>- **암호화되지 않은 암호(PAP)**<br>- **CHAP(Challenge Handshake 인증 프로토콜)**<br>- **MS-CHAP(Microsoft CHAP)**<br>- **MS-CHAP v2(Microsoft CHAP 버전 2)**<br>사용 가능한 옵션은 선택한 EAP 종류에 따라 달라집니다.<br><br>**및**<br><br>- **ID 개인 정보(외부 ID)** - EAP ID 요청에 대한 응답으로 전송되는 텍스트를 지정하려는 경우 이 텍스트에는 원하는 값을 사용할 수 있습니다. 인증하는 동안 이 익명 ID가 먼저 전송된 다음 실제 ID가 보안 채널을 통해 전송됩니다.|EAP 유형이 **EAP-TTLS** 또는 *인 경우

