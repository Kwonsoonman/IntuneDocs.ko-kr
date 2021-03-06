---
title: Intune에서 iOS 장치를 등록하는 방법 선택
titlesuffix: Microsoft Intune
description: Microsoft Intune에서 iOS 장치 등록을 설정합니다.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 439c33a6-e80c-4da9-ba09-a51fc36f62ad
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: bc1ae3f545f840f9ebfa1b7b75b56862691d900e
ms.sourcegitcommit: 51b763e131917fccd255c346286fa515fcee33f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52182740"
---
# <a name="enroll-ios-devices-in-intune"></a>Intune에 iOS 장치 등록

Intune은 iPad 및 iPhone의 MDM(모바일 장치 관리)을 가능하게 하고, 사용자가 회사 메일 및 앱에 액세스할 수 있게 해줍니다.

Intune 관리자는 iOS 장치에 대한 등록을 사용하도록 설정할 수 있습니다. 사용자가 개인적으로 소유한 장치를 등록(BYOD("Bring Your Own Device") 등록이라고 함)하도록 허용할 수 있습니다. 회사 소유 장치 등록을 사용하도록 설정할 수도 있습니다.

## <a name="prerequisites-for-ios-enrollment"></a>iOS 등록을 위한 필수 구성 요소
iOS 장치를 사용하도록 설정하기 전에 다음 단계를 완료해야 합니다.
- [Intune 설정](setup-steps.md) - 이러한 단계에서는 Intune 인프라를 설정합니다. 특히 장치를 등록하려면 [MDM 기관을 설정](mdm-authority-set.md)해야 합니다.
- [Apple MDM 푸시 인증서 가져오기](apple-mdm-push-certificate-get.md) - Apple의 경우 iOS 및 macOS 장치 관리를 사용하려면 인증서가 필요합니다.

## <a name="user-owned-ios-devices-byod"></a>사용자 소유 iOS 장치(BYOD)

사용자가 Intune 관리에 대해 개인 장치를 등록하도록 할 수 있습니다. 이를 "Bring Your Own Device" 또는 BYOD라고 합니다. 필수 구성 요소를 완료하고 사용자 라이선스를 할당하면 앱 스토어에서 Intune 회사 포털 앱을 다운로드하고 앱에서 등록 지침을 수행할 수 있습니다.

## <a name="company-owned-ios-devices"></a>회사 소유 iOS 장치
사용자를 위해 장치를 구입하는 조직의 경우, Intune은 다음과 같은 iOS 회사 소유 장치 등록 방법을 지원합니다.

- Apple의 DEP(장치 등록 프로그램)
- Apple School Manager
- Apple Configurator 설치 도우미 등록
- Apple Configurator 직접 등록

[장치 등록 관리자](device-enrollment-manager-enroll.md) 계정을 사용하여 회사 소유 iOS 장치를 등록할 수도 있습니다.

## <a name="device-enrollment-program"></a>장치 등록 프로그램
조직은 Apple의 DEP(장치 등록 프로그램)를 통해 iOS 장치를 구매할 수 있습니다. DEP를 통해 등록 프로필을 "무선"으로 배포하여 장치를 관리할 수 있습니다. [장치 등록 프로그램](device-enrollment-program-enroll-ios.md)에 대해 자세히 알아보세요.

## <a name="apple-school-manager"></a>Apple School Manager
Apple School Manager는 학교용 장치 구매 및 등록 프로그램입니다. DEP처럼 프로필을 배포하여 장치를 관리에 등록할 수 있습니다. [Apple School Manager](apple-school-manager-set-up-ios.md)에 대해 자세히 알아보세요.

## <a name="apple-configurator"></a>Apple Configurator
Mac 컴퓨터에서 실행되는 Apple Configurator를 사용하여 iOS 장치를 등록할 수 있습니다. 장치를 준비하려면 장치를 USB로 연결하고 등록 프로필을 설치합니다. Apple Configurator를 사용하여 다음 두 가지 방법으로 장치를 등록할 수 있습니다.
- 설정 도우미 등록 - 장치를 초기화하고 설정 도우미를 실행할 수 있도록 준비하여 장치의 새 사용자용으로 회사 정책을 설치합니다.
- 직접 등록 - 장치를 초기화하지 않고 미리 정의된 정책을 사용하여 장치를 등록합니다. 이 방법은 사용자 선호도가 없는 장치용입니다.

[Apple Configurator 등록](apple-configurator-setup-assistant-enroll-ios.md)에 대해 자세히 알아보세요.

## <a name="use-the-company-portal-on-dep-enrolled-or-apple-configurator-enrolled-devices"></a>DEP 또는 Apple Configurator에 등록된 장치에서 회사 포털 사용

사용자 선호도로 구성한 장치에서 회사 포털 앱을 설치하고 실행하여 앱을 다운로드하고 장치를 관리할 수 있습니다. 사용자는 장치를 받은 후 몇 가지 추가 단계를 완료하여 설정 도우미를 완료하고 회사 포털 앱을 설치해야 합니다.

사용자 선호도는 다음을 지원하는 데 필요합니다.
  - MAM(모바일 응용 프로그램 관리) 앱
  - 메일 및 회사 데이터에 대한 조건부 액세스
  - 회사 포털 앱

**사용자가 사용자 선호도를 사용하여 회사 소유의 iOS 장치를 등록하는 방법**
1. 사용자가 장치를 켜면 설정 도우미를 완료하라는 메시지가 표시됩니다. 
2. 설정을 완료한 후에 사용자에게는 Apple ID를 묻는 메시지가 표시됩니다. 장치에서 회사 포털을 설치할 수 있도록 Apple ID를 제공해야 합니다. 
3. iOS 장치는 앱 스토어에서 회사 포털 앱을 자동으로 설치합니다.
4. 사용자는 회사 포털 앱을 시작하고 Intune의 구독과 연결된 자격 증명(예: 고유한 개인 이름 또는 UPN)을 사용하여 로그인해야 합니다. 
5. 로그인하면 등록이 완료됩니다. 사용자는 이제 기능의 전체 집합으로 이 장치를 사용할 수 있습니다.

### <a name="about-corporate-owned-managed-devices-with-no-user-affinity"></a>사용자 선호도가 없는, 회사에서 소유하는 관리 장치 정보

사용자 선호도 없음으로 구성된 장치에서는 회사 포털을 지원하지 않으므로 앱을 설치하지 않아야 합니다. 회사 포털은 회사 자격 증명을 갖고 있으며 개인 설정된 회사 리소스(예: 이메일)에 대한 액세스 권한이 필요한 사용자를 위해 설계되었습니다. 사용자 선호도 없음으로 등록된 장치의 경우에는 전용 사용자가 로그인할 필요가 없습니다. 키오스크, POS(Point of Sale), 공유 유틸리티 장치 등이 사용자 선호도 없음으로 등록된 장치의 일반적인 사용 사례입니다.

사용자 선호도가 필요한 경우 장치를 등록하기 전에 장치의 등록 프로필에서 **사용자 선호도**가 선택되어 있어야 합니다. 장치에서 선호도 상태를 변경하려면 장치를 사용 중지한 후 다시 등록해야 합니다.

