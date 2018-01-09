---
title: "Intune 장치 등록에 대한 다단계 인증"
titlesuffix: Azure portal
description: "Azure AD에서 장치를 등록하기 위해 다단계 인증을 요구하는 방법입니다."
keywords: 
author: ErikjeMS
ms.author: erikje
manager: angrobe
ms.date: 10/31/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 94280c73-c05c-4e72-b0dd-a7cb997782f9
ROBOTS: 
ms.custom: intune-azure
ms.openlocfilehash: b8fb7745cf7d1d874b890210ef9c75c2a11f12ef
ms.sourcegitcommit: 5004b9564915712b41860df20324f39fac3dc27d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2018
---
# <a name="multi-factor-authentication-for-intune-device-enrollments"></a>Intune 장치 등록에 대한 다단계 인증

[!INCLUDE[azure_portal](./includes/azure_portal.md)]

Intune은 장치 등록에 Azure AD(Active Directory) MFA(다단계 인증)를 사용하여 회사 리소스를 보호하는 데 도움을 줄 수 있습니다.

MFA는 다음과 같은 확인 방법을 두 가지 이상 요구하는 방식으로 작동합니다.

- 사용자가 알고 있는 항목(대개 암호 또는 PIN)
- 사용자가 가지고 있는 항목(휴대폰처럼 쉽게 복제할 수 없으며 신뢰할 수 있는 장치)
- 사용자의 특징을 나타내는 항목(지문과 같은 생체 인식)

MFA는 iOS, Android, Windows 8.1 이상, Windows Phone 8.1 또는 Windows 10 Mobile 이상의 장치에서 지원됩니다.

MFA를 사용하도록 설정하면 최종 사용자가 장치를 등록하기 위해 두 가지 형식의 자격 증명을 제공해야 합니다.

## <a name="configure-intune-to-require-multi-factor-authentication-at-device-enrollment"></a>장치 등록 단계에서 다단계 인증을 요구하도록 Intune 구성

장치를 등록하라 때 MFA를 요구하려면 다음 단계를 따르세요.

>[!Important]
>Microsoft Intune 등록에 대한 **장치 기반 액세스 규칙**을 구성하지 마세요.

1. 자격 증명으로 [Microsoft Azure Portal](https://portal.azure.com)에 로그인합니다.
2. 포털에서 **Azure Active Directory**를 선택합니다.
2. **Azure Active Directory**에서 **관리** > **엔터프라이즈 응용 프로그램**을 선택합니다.
3. **엔터프라이즈 응용 프로그램**에서 **관리** > **모든 응용 프로그램**을 선택합니다. 관리하는 모든 Azure 앱의 목록이 표시됩니다.
3. 목록에서 **Microsoft Intune 등록**을 선택합니다.
4. **Microsoft Intune 등록**에서 **보안** > **조건부 액세스**를 선택합니다.
5. **새 정책**을 선택합니다.
6. **새 정책**에서 정책에 대한 설명이 포함된 이름을 입력합니다.
7. **할당** 섹션에서 **사용자 및 그룹**을 선택합니다.
8. **사용자 및 그룹**에서 이 정책을 수신할 사용자 또는 그룹을 선택한 다음 **완료**를 선택합니다.
9. **할당** 섹션에서 **클라우드 앱**을 선택합니다.
10. **클라우드 앱**의 **포함** 탭에서 **앱 선택**을 선택한 다음 **선택** > **Microsoft Intune 등록**을 선택하고 **완료**를 선택합니다.
11. **할당** 섹션에서 **조건**을 선택합니다.
12. **조건**에서 MFA에 대한 설정을 구성할 필요는 없습니다.
13. **액세스 제어** 섹션에서 **허용**을 선택합니다.
14. **허용**에서 **액세스 권한 부여**를 선택한 다음 **다단계 인증 기능 필요**를 선택합니다.
    장치가 등록될 때까지는 준수 여부를 평가할 수 없으므로 **준수 상태로 표시된 장치 필요**를 선택하지 마세요.
15. **선택**을 선택합니다.
16. **새 정책**에서 **정책 사용** > **켬**을 선택한 다음 **만들기**를 선택합니다.



## <a name="next-steps"></a>다음 단계

최종 사용자가 장치를 등록할 때 이제는 PIN, 전화 또는 생체 인식과 같은 두 번째 식별 형식으로 인증해야 합니다.
