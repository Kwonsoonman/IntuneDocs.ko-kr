---
title: "iOS 앱 보호 정책 설정"
titlesuffix: Microsoft Intune
description: "이 항목에서는 iOS 장치에 대한 앱 보호 정책 설정을 설명합니다."
keywords: 
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/20/2018
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 0f8b08f2-504c-4b38-bea2-b8a4ef0526b8
ms.reviewer: andcerat
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 6225afab71d1f47793ea295553dfcaf169374a06
ms.sourcegitcommit: 7e5c4d43cbd757342cb731bf691ef3891b0792b5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2018
---
#  <a name="ios-app-protection-policy-settings"></a>iOS 앱 보호 정책 설정
[!INCLUDE[azure_portal](./includes/azure_portal.md)]

이 항목에서 설명하는 정책 설정은 Azure Portal의 **정책 추가** > **설정** 블레이드에서 앱 보호 정책에 대해 [구성](app-protection-policies.md)될 수 있습니다.

데이터 재배치 설정 및 액세스 설정의 두 가지 정책 설정 범주가 있습니다. 이 항목에서 ***정책 관리 앱***이라는 용어는 앱 보호 정책을 사용하여 구성된 앱을 나타냅니다.

##  <a name="data-relocation-settings"></a>데이터 재배치 설정

| Setting | 사용 방법 | 기본값 |
|------|------|------|
| **iTunes 및 iCloud 백업 차단** | 이 앱이 회사 또는 학교 데이터를 iTunes 및 iCloud로 백업하는 것을 방지하려면 **예**를 선택합니다. 이 앱이 회사 또는 학교 데이터를 iTunes 및 iCloud로 백업하도록 허용하려면 **아니요**를 선택합니다.| 예 |
| **앱이 다른 앱으로 데이터를 전송하도록 허용** | 이 앱에서 데이터를 받을 수 있는 앱을 지정합니다. <ul><li> **정책 관리 앱**: 다른 정책 관리 앱으로만 데이터를 전송하도록 허용합니다.</li> <li>**모든 앱**: 모든 앱으로의 전송을 허용합니다. </li> <li>**없음**: 다른 정책 관리 앱을 포함한 모든 앱에 대한 데이터 전송을 허용하지 않습니다.</li></ul> 또한 이 옵션을 **정책 관리 앱** 또는 **없음**으로 설정하는 경우 스포트라이트 검색을 통해 앱 내의 데이터를 검색할 수 있는 iOS 9 기능이 차단됩니다. <br><br> Intune에서 기본적으로 데이터를 전송할 수 있는 몇 가지 예외적인 앱 및 서비스가 있습니다. 또한, Intune APP을 지원하지 않는 앱에 전송될 데이터를 허용해야 하는 경우 사용자만의 예외를 만들 수 있습니다. 자세한 내용은 [데이터 전송 예외](#data-transfer-exemptions)를 참조합니다. | 모든 앱 |
| **앱이 다른 앱의 데이터를 받도록 허용** | 이 앱에 데이터를 전송할 수 있는 앱을 지정합니다. <ul><li>**정책 관리 앱**: 다른 정책으로 관리된 앱에서만 데이터를 전송하도록 허용합니다.</li><li>**모든 앱**: 모든 앱의 데이터 전송을 허용합니다.</li><li>**없음**: 다른 정책 관리 앱을 포함한 모든 앱에서의 데이터 전송을 허용하지 않습니다.</li></ul> 예외적으로 intune이 데이터를 전송받을 수 있는 몇 가지 앱과 서비스가 있습니다. 전체 앱 및 서비스 목록은 [데이터 전송 예외](#data-transfer-exemptions)를 참조하세요. 등록되지 않은 iOS 장치의 다중 ID MAM 지원 응용 프로그램은 이 정책을 무시하고 모든 수신 데이터를 허용합니다. | 모든 앱 |
| **"다른 이름으로 저장" 차단** | 이 앱에서 다른 이름으로 저장 옵션을 사용할 수 없도록 설정하려면 **예**를 선택합니다. 다른 이름으로 저장을 사용할 수 있도록 설정하려면 **아니요**를 선택합니다. | 아니요 |
| **다른 앱에서 잘라내기, 복사 및 붙여넣기 제한** | 이 앱에서 잘라내기, 복사 및 붙여넣기 동작을 사용할 수 있는 경우를 지정합니다. 다음 중에서 선택합니다. <ul><li>**차단됨**: 이 앱과 다른 앱 간에 잘라내기, 복사 및 붙여넣기 작업을 허용하지 않습니다.</li><li>**정책 관리 앱**: 이 앱과 다른 정책 관리 앱 간에만 잘라내기, 복사 및 붙여넣기 작업을 허용합니다.</li><li>**정책 관리 앱에 붙여넣기**: 이 앱과 다른 정책 관리 앱 간에 잘라내기 또는 복사를 허용합니다. 모든 앱의 데이터를 이 앱에 붙여넣을 수 있습니다.</li><li>**모든 앱**: 이 앱과 다른 앱 간의 잘라내기, 복사 및 붙여넣기에 대한 제한이 없습니다. | 모든 앱 |
|**Managed Browser에서 표시할 수 있는 웹 콘텐츠 제한** | 앱의 웹 링크를 Managed Browser 앱에서 열 수 있도록 적용하려면 **예**를 선택합니다. <br><br> Intune에 등록되지 않은 장치의 경우 Managed Browser 앱에서만 정책 관리 앱의 웹 링크를 열 수 있습니다. <br><br> Intune을 사용하여 장치를 관리하는 경우 [Microsoft Intune에서 Managed Browser 정책을 사용하여 인터넷 액세스 관리](app-configuration-managed-browser.md)를 참조하세요. | 아니요 |
| **앱 데이터 암호화** | 정책 관리 앱의 경우 iOS에서 제공하는 장치 수준 암호화 체계를 사용하여 데이터가 저장 시 암호화됩니다. PIN이 필요한 경우에는 앱 보호 정책의 설정에 따라 데이터가 암호화됩니다. <br><br> FIPS 140-2로 인증되었거나 FIPS 140-2 인증이 보류 중인 iOS 암호화 모듈을 알아보려면 [여기](https://support.apple.com/HT202739)의 공식 Apple 설명서로 이동하세요. <br><br> 이 앱의 회사 또는 학교 데이터를 암호화하는 경우를 지정합니다. 다음 중에서 선택합니다. <ul><li>**장치가 잠긴 경우**: 장치가 잠겨 있는 동안 이 정책과 연결된 모든 앱 데이터가 암호화됩니다.</li><li>**장치가 잠길 때 열린 파일이 있음**: 장치가 잠겨 있는 동안 앱에서 현재 열려 있는 파일의 데이터를 제외하고 이 정책과 연결된 모든 앱 데이터가 암호화됩니다.</li><li>**장치를 다시 시작한 후**: 장치를 다시 시작할 때 이 정책과 연결된 모든 앱 데이터가 암호화되며 처음으로 장치 잠금을 해제할 때까지 유지됩니다.</li><li>**장치 설정 사용**: 장치의 기본 설정에 따라 앱 데이터가 암호화됩니다. </li></ul> 이 설정을 사용하도록 설정할 경우 사용자가 PIN을 설정하고 해당 장치에 액세스할 때 사용해야 할 수 있습니다.  PIN이 없고 암호화가 필수인 경우 앱이 열리지 않으며 "Your organization has required you to first enable a device PIN to access this app."(조직 요구에 맞게 이 앱에 액세스하려면 먼저 장치 PIN을 사용할 수 있도록 해야 합니다.)라는 메시지와 함께 PIN을 설정하라는 메시지가 사용자에게 표시됩니다.  | 장치가 잠길 때 |
| **연락처 동기화 사용 안 함** | 앱에서 장치의 네이티브 연락처 앱에 데이터를 저장하는 것을 방지하려면 **예**를 선택합니다. **아니요**를 선택하면 앱에서 장치의 네이티브 연락처 앱에 데이터를 저장할 수 있습니다. <br><br>선택적 초기화를 수행하여 앱에서 회사 또는 학교 데이터를 제거할 경우 앱에서 네이티브 연락처 앱으로 직접 동기화된 연락처가 제거됩니다. 기본 주소록에서 다른 외부 소스에 동기화된 연락처는 초기화할 수 없습니다. 현재 Microsoft Outlook 앱에만 적용됩니다. | 아니요 |
| **인쇄를 사용하지 않도록 설정** | 앱에서 회사 또는 학교 데이터를 인쇄하는 것을 방지하려면 **예**를 선택합니다. | 아니요 |
| **회사 데이터를 저장할 저장소 서비스 선택** | 사용자는 비즈니스용 OneDrive, SharePoint, 로컬 저장소 등의 선택한 서비스에 데이터를 저장할 수 있습니다. 기타 서비스는 모두 차단됩니다. | 0개 선택됨 |

> [!NOTE]
> 데이터 재배치 설정으로는 iOS 장치에서 Apple의 관리되는 여는 위치 기능을 제어할 수 없습니다. Apple의 관리되는 여는 위치를 관리하려면[Microsoft Intune으로 iOS 앱 간의 데이터 전송 관리](data-transfer-between-apps-manage-ios.md)를 참조하세요.

## <a name="data-transfer-exemptions"></a>데이터 전송 예외

Intune 앱 보호 정책에서 특정 시나리오의 데이터 송수신을 허용할 수 있는 예외적인 앱 및 플랫폼 서비스가 일부 있습니다. 이 목록은 변경될 수 있으며 생산성 보장에 유용한 서비스 및 앱을 나타냅니다.

| 앱/서비스 이름 | 설명 |
| ---- | --- |
|<code>tel; telprompt</code> | 네이티브 휴대폰 앱 |
|<code>skype</code> | Skype |
|<code>app-settings</code> | 장치 설정 |
|<code>itms; itmss; itms-apps; itms-appss; itms-services</code> | 앱 스토어 |
|<code>calshow</code> | 네이티브 달력 |

자세한 내용은 [앱에 대한 데이터 전송 정책 예외](app-protection-policies-exception.md)를 참조합니다. 

## <a name="access-settings"></a>액세스 설정

| Setting | 사용 방법 | 기본값 |
|------|------|------|
| **액세스하려면 PIN 필요** | 이 앱을 사용하는 데 PIN을 요구하려면 **예**를 선택합니다. 회사 또는 학교 컨텍스트에서 앱을 처음으로 실행할 때 이 PIN을 설정하라는 메시지가 표시됩니다. PIN은 온라인 또는 오프라인으로 작업할 때 적용됩니다. 기본값은 **예**입니다.<br><br> PIN 강도에 대한 다음 설정을 구성합니다. <ul><li>**유형 선택**: 앱 보호 정책이 적용된 앱에 액세스하기 전에 숫자 또는 암호 유형 PIN의 요구 사항을 설정합니다. 숫자 요구 사항에는 숫자만 포함되고, 암호는 1자 이상의 알파벳 문자 **또는** 1자 이상의 특수 문자로 정의할 수 있습니다. 기본값은 **숫자**입니다.</li><li>**PIN 초기화 전 시도 횟수**: 초기화하기 전까지 PIN을 성공적으로 입력하기 위해 시도할 수 있는 횟수를 지정합니다. 기본값 = **5**. <br> 이 정책 설정 형식은 양의 정수를 지원합니다.</li><li> **단순한 PIN 허용**: 사용자가 1234, 1111, abcd 또는 aaaa와 같은 단순한 PIN 시퀀스를 사용할 수 있도록 허용하려면 **예**를 선택합니다. 단순한 순서를 사용하는 것을 방지하려면 **아니요**를 선택합니다. <br>**참고**: iOS에서 암호 형식 PIN을 구성하고, 단순 PIN 허용을 예로 설정한 경우 1자 이상의 문자 **또는** 1자 이상의 특수 문자여야 합니다. 암호 형식 PIN을 구성하고, 단순 PIN 허용을 아니요로 설정한 경우 1자 이상의 문자 **및** 1자 이상의 특수 문자여야 합니다.  기본값은 **예**입니다. </li><li> **PIN 길이**: PIN 시퀀스의 최소 자릿수를 지정합니다. 기본값은 **4**입니다. </li><li> **PIN 대신 지문 허용(iOS 8.0 이상)**: 사용자가 앱 액세스를 위해 PIN 대신 [Touch ID](https://support.apple.com/HT201371)를 사용하도록 허용하려면 **예**를 선택합니다. 기본값은 **예**입니다.</li><li> **PIN 대신 안면 인식 허용(iOS 11 이상)**: 사용자가 앱 액세스를 위해 PIN 대신 [Face ID](https://support.apple.com/HT208109)를 사용하도록 허용하려면 **예**를 선택합니다. 기본값은 **예**입니다. 사용자가 회사 계정으로 앱에 액세스하는 경우 안면 식별을 제공하라는 메시지가 표시됩니다.</li><li> **장치 PIN을 관리하는 경우 앱 PIN 사용 안 함**: 등록된 장치에서 장치 잠금이 검색되는 경우 앱 PIN을 사용하지 않도록 설정하려면 **예**를 선택합니다. <br> **참고:** 앱에 Intune SDK 버전 7.0.1 이상이 있어야 합니다. 기본값은 **아니요**입니다.</li></ul> iOS 장치에서 사용자가 PIN 대신 [Touch ID](https://support.apple.com/HT201371) 또는 [Face ID](https://support.apple.com/HT208109)를 사용하여 자신의 ID를 증명하도록 허용할 수 있습니다. Intune은 [LocalAuthentication](https://developer.apple.com/documentation/localauthentication/) API를 사용하여 Touch ID 및 Face ID를 통해 사용자를 인증합니다. Touch ID 및 Face ID에 대한 자세한 내용은 [iOS 보안 가이드](https://www.apple.com/business/docs/iOS_Security_Guide.pdf)를 참조하세요. 회사 또는 학교 계정으로 이 앱을 열려고 하면 PIN을 입력하는 대신 해당 지문 ID 또는 안면 ID를 제공하라는 메시지가 표시됩니다. 이 설정을 사용하는 경우 회사 또는 학교 계정을 사용하는 동안 최근 실행 앱 미리 보기 이미지가 흐리게 표시됩니다. </li></ul><!-- <br><br>You can require a PIN expiration for targeted iOS apps. You can configure the PIN requirement and expiration date in days through the Azure portal. When required, a user will be required to set and use a new PIN before getting access to an iOS app. Only iOS apps that have app protection enabled with the Intune App SDK will support this feature.-->| 액세스하려면 PIN 필요: 예 <br><br> 유형 선택: 숫자 <br><br> PIN 초기화 시도 횟수: 5 <br><br> 단순한 PIN 허용: 예 <br><br> PIN 길이: 4 <br><br> 지문 허용: 예 <br><br> 안면 인식 허용: 예 <br><br> 앱 PIN 사용 안 함: 아니요 |
| **액세스 시 회사 자격 증명 필요** | 앱 액세스에 PIN을 입력하는 대신 해당 회사 또는 학교 계정으로 로그인하도록 요구하려면 **예**를 선택합니다. 이 옵션을 **예**로 설정하면 PIN 또는 터치 ID에 대한 요구 사항이 재정의됩니다.  | 아니요 |
| **관리되는 앱이 무단 해제 또는 루팅된 장치를 실행할 수 없도록 차단** |  이 앱이 무단 해제 또는 루팅된 장치에서 실행되는 것을 차단하려면 **예**를 선택합니다. 개인적인 작업에 이 앱을 계속 사용할 수 있지만 이 앱의 회사 또는 학교 데이터에 액세스하려면 다른 장치를 사용해야 합니다. | 예 |
| **액세스 요구 사항을 다시 확인할 시간(분)** | 다음 설정을 구성합니다. <ul><li>**제한 시간**: 이전에 정책에서 정의된 액세스 요구 사항이 다시 확인되기까지 걸리는 시간(분)입니다. 예를 들어 관리자가 정책에서 장치에 루팅된 PIN 및 블록을 설정하고, 사용자가 Intune 관리 앱을 열 때, PIN을 입력해야 하고 루팅되지 않은 장치에서 앱을 사용해야 합니다. 이 설정을 사용하는 경우 사용자가 **30분**(기본값) 동안은 Intune 관리 앱에서 PIN을 다시 입력하거나 또 다른 root-detection 확인을 할 필요가 없습니다.  <br><br>**참고:** iOS의 경우 PIN은 **같은 게시자**의 모든 Intune 관리 앱 간에서 공유됩니다. 앱이 장치에서 포그라운드를 나가면 특정 PIN에 대한 PIN 타이머가 재설정됩니다. 사용자는 이 설정에서 정의한 시간 동안 PIN을 공유하는 Intune 관리 앱에 PIN을 입력할 필요가 없습니다. <br><br> 이 정책 설정 형식은 양의 정수를 지원합니다.</li><li>**오프라인 유예 기간**: MAM 앱이 오프라인 상태로 실행될 수 있는 시간(분)으로, 앱의 액세스 요구 사항이 다시 확인되기까지 걸리는 시간(분)을 지정합니다. 기본값 = **720**분(12시간). 이 기간이 만료되면 앱을 계속 실행하기 위해 AAD에 사용자 인증이 필요합니다.<br><br> 이 정책 설정 형식은 양의 정수를 지원합니다.</li></ul>| 시간 제한: 30 <br><br> 오프라인: 720 |
| **앱 데이터를 초기화하기 전의 오프라인 간격(일)** | 이 오랜 기간(관리자가 정의) 동안 오프라인으로 실행되고 나면 앱에서 사용자가 네트워크에 연결하고 다시 인증해야 합니다. 성공적으로 인증하고 나면 데이터에 계속 액세스할 수 있으며 오프라인 간격이 재설정됩니다.  사용자가 인증에 실패하면 앱에서 사용자 계정과 데이터를 선택적으로 초기화합니다.  선택적 초기화로 제거되는 데이터에 대한 자세한 내용은 [Intune-관리 앱에서 회사 데이터만 초기화하는 방법](https://docs.microsoft.com/intune/apps-selective-wipe)을 참조하세요. <br><br> 이 정책 설정 형식은 양의 정수를 지원합니다. | 90일 |
| **Require minimum iOS operating system**(최소 iOS 운영 체제 필요) | 이 앱을 사용하기 위한 최소 iOS 운영 체제를 요구하려면 **예**를 선택합니다. 장치의 iOS 버전이 요구 사항을 충족하지 않으면 사용자 액세스가 차단됩니다. <br> **참고:** 앱에 Intune SDK 버전 7.0.1 이상이 있어야 합니다. | 아니요 |
| **Require minimum iOS operating system (Warning only)**(최소 iOS 운영 체제 필요(경고)) | 이 앱을 사용하기 위한 최소 iOS 운영 체제를 요구하려면 **예**를 선택합니다. 장치의 iOS 버전이 요구 사항을 충족하지 않으면 사용자에게 알림이 표시됩니다. 이 알림은 무시할 수 있습니다. <br> **참고:** 앱에 Intune SDK 버전 7.0.1 이상이 있어야 합니다. | 아니요 |
| **Require minimum app version**(최소 앱 버전 필요) | 앱을 사용할 최소 앱 버전을 요구하려면 **예**를 선택합니다. 장치의 앱 버전이 요구 사항을 충족하지 않으면 사용자 액세스가 차단됩니다.<br><br>응용 프로그램 간에 서로 다른 버전 지정 체계를 종종 있는 하나의 앱 (예를 들어 "Outlook 버전 정책")을 대상으로 하는 하나의 최소 응용 프로그램 버전으로는 정책을 만듭니다. <br><br> 이 정책 설정 형식은 major.minor, major.minor.build, major.minor.build.revision을 지원합니다. <br><br> **참고:** 앱에 Intune SDK 버전 7.0.1 이상이 있어야 합니다. | 아니요 | 
| **Require minimum app version (Warning only)**(최소 앱 버전 필요(경고)) | 이 앱을 사용하기 위한 최소 앱 버전을 권장하려면 **예**를 선택합니다. 장치의 앱 버전이 요구 사항을 충족하지 않으면 사용자에게 알림이 표시됩니다. 이 알림은 무시할 수 있습니다.<br><br>응용 프로그램 간에 서로 다른 버전 지정 체계를 종종 있는 하나의 앱 (예를 들어 "Outlook 버전 정책")을 대상으로 하는 하나의 최소 응용 프로그램 버전으로는 정책을 만듭니다. <br><br> 이 정책 설정 형식은 major.minor, major.minor.build, major.minor.build.revision을 지원합니다. <br><br> **참고:** 앱에 Intune SDK 버전 7.0.1 이상이 있어야 합니다. | 아니요 | 
| **Require minimum Intune app protection policy SDK version**(최소 Intune 앱 보호 정책 SDK 버전 필요) | 사용할 앱에 대한 최소 Intune 앱 보호 정책 SDK를 요구하려면 **예**를 선택합니다. 앱의 Intune 앱 보호 정책 SDK 버전이 요구 사항을 충족하지 않으면 사용자 액세스가 차단됩니다. <br> <br> Intune 앱 보호 정책 SDK에 대한 자세한 내용은 [Intune 앱 SDK 개요](app-sdk.md)를 참조하세요. <br><br> 이 정책 설정 형식은 major.minor, major.minor.build, major.minor.build.revision을 지원합니다. <br><br> **참고:** 앱에 Intune SDK 버전 7.0.1 이상이 있어야 합니다. | 아니요 |


##  <a name="add-ins-for-outlook-app"></a>Outlook 앱용 추가 기능

최근에 iOS용 Outlook에 인기 있는 앱을 메일 클라이언트와 통합할 수 있는 추가 기능이 적용되었습니다. Outlook용 추가 기능은 웹, Windows, Mac 및 iOS용 Outlook에서 사용할 수 있습니다. 추가 기능은 Microsoft Exchange를 통해 관리되기 때문에 사용자는 Outlook 및 관리되지 않는 추가 기능 응용 프로그램에서 데이터와 메시지를 공유할 수 있습니다(Exchange에서 사용자에 대해 추가 기능을 해제하지 않은 경우).

최종 사용자가 Outlook 추가 기능에 액세스하고 설치하는 것을 중지하려면(이는 모든 Outlook 클라이언트에 영향을 줌) Exchange 관리 센터에서 역할을 다음과 같이 변경해야 합니다.

- 사용자가 Office 스토어 추가 기능을 설치하지 못하도록 하려면 내 마켓플레이스 역할을 제거합니다.
- 사용자가 추가 기능을 테스트용으로 로드하지 못하도록 하려면 내 사용자 지정 앱 역할을 제거합니다.
- 사용자가 모든 추가 기능을 설치하지 못하도록 하려면 내 사용자 지정 앱 및 내 마켓플레이스 역할을 둘 다 제거합니다.

이러한 지침은 웹, Windows, Mac 및 모바일의 Outlook에서 Office 365, Exchange 2016 및 Exchange 2013에 적용됩니다.

- [Outlook용 추가 기능](https://technet.microsoft.com/library/jj943753(v=exchg.150).aspx)에 대해 자세히 알아보세요.
- [Outlook 앱용 추가 기능을 설치하고 관리할 수 있는 관리자 및 사용자를 지정하는 방법](https://technet.microsoft.com/library/jj943754(v=exchg.150).aspx)에 대해 자세히 알아보세요.
