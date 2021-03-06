---
title: Microsoft Intune으로 장치 보호
titleSuffix: Microsoft Intune
description: Intune이 무단 액세스 및 기타 위협으로부터 장치를 보호하는 데 어떤 도움을 줄 수 있는지 알아봅니다.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/19/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.openlocfilehash: 06f14b0ba1edcde28c7f2c732ab286e80f186bf2
ms.sourcegitcommit: 51b763e131917fccd255c346286fa515fcee33f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52188265"
---
# <a name="protect-devices-with-microsoft-intune"></a>Microsoft Intune으로 장치 보호

Microsoft Intune을 사용하면 관리하는 장치와 해당 장치에 저장된 데이터를 보호할 수 있습니다.

## <a name="device-configuration"></a>장치 구성
Intune [구성 정책](device-profiles.md)을 사용하면 폭넓은 설정 및 기능을 제어하여 장치를 쉽게 보호하고 구성할 수 있습니다. 예를 들면 다음과 같습니다.
- 카메라, Bluetooth 등의 장치에서 하드웨어 기능 사용을 제한할 수 있습니다.
- 규격 및 비규격 앱을 구성할 수 있습니다. 비규격 앱 설치 시 경고가 표시되며 플랫폼에 따라서는 설치가 실제로 차단될 수도 있습니다.

## <a name="reset-passcodes-when-users-are-locked-out-of-their-devices"></a>사용자가 자신의 장치를 잠글 때 암호 재설정
모바일 장치의 회사 데이터를 보호하는 첫 번째 단계는 장치를 사용할 때 암호를 입력하도록 하는 것입니다. 때로는 암호를 제거하거나 원격으로 임시 암호를 설정하여 [암호를 재설정](device-passcode-reset.md)하거나 직원이 그렇게 하도록 해야 합니다. 장치를 분실하거나 도난당한 경우 [원격으로 장치를 잠글](device-remote-lock.md) 수도 있습니다.

## <a name="retire-devices-and-remove-data"></a>장치 사용 중지 및 데이터 제거
사용자가 퇴사하거나 장치를 분실/도난당한 경우 등 장치를 [Intune 관리 대상에서 제거](devices-wipe.md)해야 할 때는 해당 장치에서 데이터도 제거해야 하는 경우가 많습니다. Intune은 회사 데이터의 보안을 유지할 수 있는 다양한 방법을 제공합니다.

## <a name="require-devices-to-be-compliant"></a>장치가 규칙을 준수해야 하도록 지정
Intune 기능에서는 지정한 규칙을 준수하지 않는 장치를 평가하고 경우에 따라 수정하는 데 사용할 수 있는 [장치 준수 정책](device-compliance-get-started.md)을 제공합니다. 예를 들어 다음에 대한 보고서를 가져올 수 있습니다.
- 탈옥 iOS 장치
- 암호화된 장치 또는 암호화되지 않은 장치
- Windows 10 장치 상태(상태 증명 서비스에 의해 결정됨)

## <a name="protect-apps-and-the-data-they-use"></a>앱 및 앱에서 사용하는 데이터 보호
Intune에서는 앱과 해당 데이터를 보호하는 데 사용할 수 있는 다양한 기능을 제공합니다. 예를 들어 MAM(모바일 응용 프로그램 관리) 정책은 다음과 같이 할 수 있습니다.
- 보호된 앱에서 데이터가 백업되지 않도록 함
- 다른 앱에 복사 및 붙여넣기 제한
- 앱에 액세스하려면 PIN 필요. 자세한 내용은 [Microsoft Intune을 사용하여 앱 및 데이터 보호](app-protection-policy.md)를 참조하세요.

## <a name="add-an-additional-layer-of-protection-to-devices"></a>장치에 추가 보호 계층 추가
[MFA(다단계 인증)](multi-factor-authentication.md)는 네트워크에서 장치 사용자를 인증하는 더욱 안전한 방식입니다.  MFA를 사용하는 경우에는 사용자가 사용자 이름과 암호 외에 전화 통화나 문자 메시지를 통해 신원을 확인해야 합니다.

## <a name="control-windows-hello-for-business-settings-on-windows-devices"></a>Windows 장치에서 비즈니스용 Windows Hello 설정 제어
Active Directory를 사용하는 Windows 10 이상 버전 또는 Azure Active Directory 계정에서 암호, 스마트 카드 또는 가상 스마트 카드를 대신하는 로그인 방법인 [비즈니스용 Windows Hello](windows-hello.md)와 Intune을 통합할 수 있습니다.

## <a name="bypass-activation-lock-on-ios-devices"></a>iOS 장치에서 활성화 잠금 무시
활성화 잠금은 사용자 장치를 보호하는 데 도움이 되는 기능입니다. 이 기능은 누군가가 장치를 초기화하거나 다시 활성화하기 전에 사용자가 Apple ID와 암호를 입력하도록 요구합니다. 그러나 이 기능은 사용자가 잠금을 제거하지 않고 퇴사하는 경우 등에 문제가 발생할 수 있습니다. [iOS 활성화 잠금 무시]( device-activation-lock-bypass.md)는 감독 되는 iOS 장치에서 잠금을 제거하여 장치를 다시 할당하거나 지울 수 있도록 합니다.

## <a name="next-steps"></a>다음 단계

[Mobile Threat Defense](mobile-threat-defense.md)에 대해 알아보기


