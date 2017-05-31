---
title: "모바일 장치 관리를 위한 Intune 준비 | Microsoft 문서"
description: "이 문서의 목적은 독자가 Intune으로 마이그레이션하기 전에 비즈니스 및 기술 요구 사항을 평가할 수 있도록 돕는 것입니다."
keywords: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 03/24/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 58591442-6606-4f39-a06b-f17a1f25af25
ms.reviewer: dagerrit
ms.suite: ems
ms.custom: intune-classic
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: 9108fbc615baea5896c0c323566a0c092ed68da0
ms.contentlocale: ko-kr
ms.lasthandoff: 05/23/2017


---

# <a name="phase-1-prepare-intune-for-mobile-device-management-mdm"></a>1단계: MDM(모바일 장치 관리)을 위한 Intune 준비

[!INCLUDE[note for both-portals](../includes/note-for-both-portals.md)]

Intune 설정의 세부 정보를 살펴보기 전에 조직의 모바일 장치 관리 요구 사항을 검토해 보겠습니다. 현재 MDM 공급자의 활성 사용자에 대한 보고서를 실행하여 중요한 사용자 그룹을 확인하는 것이 유용할 수 있습니다. 그러면 아래 [MDM 요구 사항 평가 섹션](/intune-classic/plan-design/migration-phase1-prepare-intune-for-mobile-device-management#assess-mdm-requirements)의 질문 검토를 시작할 수 있습니다.

## <a name="assess-mdm-requirements"></a>MDM 요구 사항 평가

### <a name="what-kinds-of-devices-do-you-need-to-manage"></a>어떤 종류의 장치를 관리해야 하나요?

-   어떤 [플랫폼](/intune-classic/get-started/supported-mobile-devices-and-computers)을 지원해야 하나요?

-   회사 장치 또는 BYOD를 지원하는 데 필요한 장치인가요?

-   어떤 종류의 연결을 사용하나요? Wi-Fi, 셀룰러 또는 VPN인가요?

### <a name="what-do-your-users-need-to-do-on-managed-devices"></a>관리되는 장치에서 사용자가 무엇을 해야 하나요?

-   앱을 최종 사용자에게 프로비전해야 하나요?

-   사용자 지정 LOB(기간 업무) 앱을 사용하나요? 아니면 공용 스토어 앱만 필요한가요?

-   메일 계정을 프로비전해야 하나요?

### <a name="what-kinds-of-users"></a>사용자의 종류는 어떤가요?

-   얼마나 많은 사용자가 단일 장치를 사용하나요?

-   어떤 사용 약관이 필요한가요?

    -   법률 부서가 조기에 이 문제에 관여하도록 해야 합니다.

    -   필요한 지역화는 무엇인가요?

-   일반적으로 사용자가 기술 및 IT에 익숙한가요?

### <a name="what-is-your-device-security-policy"></a>장치 보안 정책은 어떻게 되나요?

-   장치 수준 암호화가 필요한가요?

-   장치 암호/PIN 코드 길이는 어떤가요?

-   장치 기능을 사용하지 않도록 설정하거나 특정 장치 동작을 제한해야 하나요?

    -   카메라 사용 안 함, 단일 앱 모드 잠금 등의 장치 구성 프로필을 사용하여 다양한 플랫폼 관련 설정을 제어할 수 있습니다.
<br></br>
-   어떤 종류의 인증을 지원해야 하나요?

    -   인증서 기반 인증이 필요한 경우 어떤 종류의 인증서를 프로비전해야 하나요?

        -   Intune에서는 등록된 장치에 대한 리소스 액세스 프로필을 사용하여 인증서를 프로비전할 수 있습니다.
<br></br>
    -   어떤 종류의 PKI(공개 키 인프라) 인프라를 지원해야 하나요?
<br></br>
-   장치 또는 앱 수준에서 VPN(가상 사설망)을 지원해야 하나요?

    -   Intune에서는 타사 VPN 공급자에 대한 VPN 구성을 프로비전할 수 있습니다.
<br></br>
-   가동 중지 시간을 방지하기 위해 특정 요구 사항에 대한 임시 예외를 만들 수 있나요? 또는 액세스 권한이 있는 장치가 항상 모든 보안 요구 사항을 준수해야 하나요?

## <a name="additional-information"></a>추가 정보

-   다양한 산업 분야의 [사례 연구](https://customers.microsoft.com/story/mwh-global-now-part-of-stantec-secures-mobile-devices-with-intune)를 검토하여 여러 조직이 모바일 장치 관리에 대한 요구 사항을 평가한 방법을 통해 자세한 예제를 알아보세요.

## <a name="next-steps"></a>다음 단계

[1단계: 기본 설정](/intune-classic/plan-design/migration-phase1-basic-setup)
