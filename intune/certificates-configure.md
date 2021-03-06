---
title: Microsoft Intune - Azure에서 인증서 프로필 만들기 | Microsoft Docs
description: 사용자 장치에 대해 SCEP 또는 PKCS 인증서 환경을 구성하여 인증서 프로필을 만들거나 추가하고, 공용 인증서를 내보내고, Azure Portal에서 프로필을 만든 다음, SCEP 또는 PKCS를 Azure Portal의 Microsoft Intune에서 인증서 프로필에 할당합니다
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/23/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 5eccfa11-52ab-49eb-afef-a185b4dccde1
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 1a70e8a5e9ad973f5d2c94a146a9f263f461d0ab
ms.sourcegitcommit: 51b763e131917fccd255c346286fa515fcee33f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52180564"
---
# <a name="configure-a-certificate-profile-for-your-devices-in-microsoft-intune"></a>Microsoft Intune에서 장치에 대한 인증서 프로필 구성

VPN, Wi-Fi 또는 이메일 프로필을 통해 사용자에게 회사 리소스에 대한 액세스 권한을 부여합니다. 인증서를 사용하여 이러한 연결을 인증할 수 있습니다. 인증서를 사용할 때 최종 사용자는 인증을 위해 사용자 이름과 암호를 입력할 필요가 없습니다.

Intune을 사용하여 관리하는 장치에 이러한 인증서를 할당할 수 있습니다. Intune에서는 다음 인증서 유형 할당 및 관리를 지원합니다.

- SCEP(단순 인증서 등록 프로토콜)
- PKCS #12(또는 PFX)

이러한 각 유형의 인증서에는 고유한 필수 구성 요소 및 인프라 요구 사항이 있습니다.

## <a name="overview"></a>개요

1. 올바른 인증서 인프라가 설정되어 있는지 확인합니다. [SCEP 인증서](certificates-scep-configure.md) 및 [PKCS 인증서](certficates-pfx-configure.md)를 사용할 수 있습니다.

2. 각 장치에 루트 인증서 또는 중간 CA(인증 기관) 인증서를 설치하여 장치가 인증 기관의 적법성을 인식할 수 있게 합니다. 이를 수행하려면 **신뢰할 수 있는 인증서 프로필**을 만들고 할당합니다. 이 프로필을 할당하면 Intune 관리 장치가 루트 인증서를 요청하고 받습니다. 각 플랫폼에 대해 별도 프로필을 만들어야 합니다. 신뢰할 수 있는 인증서 프로필을 사용할 수 있는 플랫폼은 다음과 같습니다.

    - iOS 8.0 이상
    - macOS 10.11 이상
    - Android 4.0 이상
    - Android 회사 프로필
    - Windows 8.1 이상
    - Windows Phone 8.1 이상
    - Windows 10 이상

3. 인증서 프로필을 만들어 VPN, Wi-Fi 및 메일 액세스 인증에 사용할 인증서를 장치가 요청할 수 있게 합니다. 다음 플랫폼을 실행하는 장치에 대해 **PKCS** 또는 **SCEP** 인증서 프로필을 만들고 할당할 수 있습니다.

   - iOS 8.0 이상
   - Android 4.0 이상
   - Android 회사 프로필
   - Windows 10(데스크톱 및 모바일) 이상

   다음 플랫폼을 실행하는 장치에 대해서만 **SCEP** 인증서 프로필을 사용할 수 있습니다.

   - macOS 10.9 이상
   - Windows Phone 8.1 이상

각 장치 플랫폼에 대해 별도 프로필을 만들어야 합니다. 프로필을 만들 때 이미 만들어 놓은 신뢰할 수 있는 루트 인증서 프로필과 연결합니다.

### <a name="further-considerations"></a>추가 고려 사항

- 엔터프라이즈 인증 기관이 없는 경우 새로 만들어야 합니다
- SCEP 프로필을 사용하는 경우 NDES(네트워크 장치 등록 서비스) 서버 구성
- SCEP 프로필과 PKCS 프로필 중 무엇을 사용하려고 계획 중이든지 간에 Microsoft Intune 인증서 커넥터의 다운로드 및 구성


## <a name="step-1-configure-your-certificate-infrastructure"></a>1단계: 인증서 인프라 구성

인증서 프로필의 유형별로 인프라를 구성하는 데 도움이 되는 다음 항목을 중 하나를 참조하세요.

- [Intune을 사용하여 SCEP 인증서 구성 및 관리](certificates-scep-configure.md)
- [Intune을 사용하여 PKCS 인증서 구성 및 관리](certficates-pfx-configure.md)


## <a name="step-2-export-your-trusted-root-ca-certificate"></a>2단계: 신뢰할 수 있는 루트 CA 인증서 내보내기

발급 CA(인증 기관) 또는 발급 CA를 신뢰하는 장치에서 신뢰할 수 있는 루트 인증 기관(CA)을 공용 인증서(.cer)로 내보냅니다. 개인 키(.pfx)는 내보내지 마세요.

신뢰할 수 있는 인증서 프로필을 설정할 때 이 인증서를 가져옵니다.

## <a name="step-3-create-trusted-certificate-profiles"></a>3단계: 신뢰할 수 있는 인증서 프로필 만들기
SCEP 또는 PKCS 인증서 프로필을 만들기 전에 신뢰할 수 있는 인증서 프로필을 만듭니다. 각 장치 플랫폼에 신뢰할 수 있는 인증서 프로필 및 SCEP 또는 PKCS 프로필이 필요합니다. 신뢰할 수 있는 인증서를 만들기 위한 단계는 각 장치 플랫폼의 경우와 유사합니다.

1. [Azure 포털](https://portal.azure.com)에 로그인합니다.
2. **모든 서비스**를 선택하고 **Intune**에서 필터링하고 **Microsoft Intune**을 선택합니다.
3. **장치 구성** > **관리** > **프로필** > **프로필 만들기**를 선택합니다.
4. 신뢰할 수 있는 인증서 프로필에 대한 **이름** 및 **설명**을 입력합니다.
5. **플랫폼** 드롭다운 목록에서 이 신뢰할 수 있는 인증서에 대한 장치 플랫폼을 선택합니다. 옵션은 다음과 같습니다.

    - **OWA(Outlook Web Access)**
    - **Android 엔터프라이즈**
    - **iOS**
    - **macOS**
    - **Windows Phone 8.1**
    - **Windows 8.1 이상**
    - **Windows 10 이상**

6. **프로필 유형** 드롭다운 목록에서 **신뢰할 수 있는 인증서**를 선택합니다.
7. 작업 1에서 저장한 인증서를 찾은 다음, **확인**을 선택합니다.
8. Windows 8.1 및 Windows 10 장치에 한해 신뢰할 수 있는 인증서의 **대상 저장소**를 선택합니다.

    - **컴퓨터 인증서 저장소 - 루트**
    - **컴퓨터 인증서 저장소 - 중간**
    - **사용자 인증서 저장소 - 중간**

9. 작업이 완료되면 **확인**을 선택하고 **프로필 만들기** 창으로 돌아와서 **만들기**를 선택합니다.

프로필이 만들어지고 목록에 표시됩니다. 이 프로필을 그룹에 할당하려면 [장치 프로필 할당](device-profile-assign.md)을 참조하세요.

Android 장치에 타사가 신뢰할 수 있는 인증서를 설치했다는 메시지가 표시됩니다.

## <a name="step-4-create-scep-or-pkcs-certificate-profiles"></a>4단계: SCEP 또는 PKCS 인증서 프로필 만들기

인증서 프로필의 각 유형을 구성하고 할당하는 데 도움이 되는 다음 항목을 중 하나를 참조하세요.

- [Intune을 사용하여 SCEP 인증서 구성 및 관리](certificates-scep-configure.md)
- [Intune을 사용하여 PKCS 인증서 구성 및 관리](certficates-pfx-configure.md)

신뢰할 수 있는 인증서 프로필을 만든 후에는 사용하려는 각 플랫폼용으로 SCEP 또는 PKCS 인증서 프로필을 만듭니다. SCEP 인증서 프로필을 만들 때는 같은 플랫폼에 대해 신뢰할 수 있는 인증서 프로필을 입력합니다. 그러면 두 인증서 프로필이 연결되기는 하지만 각 프로필을 개별적으로 할당해야 합니다.

## <a name="next-steps"></a>다음 단계
[장치 프로필 할당](device-profile-assign.md)  
[S/MIME를 사용하여 이메일 서명 및 암호화](certificates-s-mime-encryption-sign.md)  
[타사 인증 기관 사용](certificate-authority-add-scep-overview.md)
