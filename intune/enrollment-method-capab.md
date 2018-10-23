---
title: Windows 장치의 등록 방법에 따른 Intune 기능
titlesuffix: Microsoft Intune
description: 각 등록 방법이 Windows 장치에 대해 지원하는 기능을 참조하세요.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/21/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: c9e440aef7f434cbe675506fd6f22a9bd26b2c31
ms.sourcegitcommit: 528d2bc70bfd25803a2d9f0fe9372c8a5f5e7dad
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446823"
---
# <a name="capabilities-by-enrollment-method-for-windows-devices"></a>Windows 장치의 등록 방법에 따른 기능
[!INCLUDE[azure_portal](./includes/azure_portal.md)]

Intune을 사용하여 직원의 장치 및 앱을 관리하고 회사 데이터에 액세스하는 방법을 관리할 수 있습니다. 장치는 먼저 Intune 서비스에서 등록되어야 합니다. 작업자의 장치를 등록하는 몇 가지 방법이 있습니다. 아래 표에 나와 있는 것처럼 각 메서드에는 다른 모범 사례 및 기능이 포함됩니다.

## <a name="best-practices-by-enrollment-method"></a>등록 메서드별 모범 사례
| **Best practices**(최선의 구현 방법) | **[Azure AD 조인됨](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Autopilot을 사용하여 Azure AD 조인됨](enrollment-autopilot.md)** |**[대량](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#bring-your-own-device)** | **GPO** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|EDU에 일반적으로 사용됨|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|
|장치를 공유 장치로 사용 가능|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|
|개인 장치는 회사 리소스에 액세스해야 함|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|
|앱의 셀프 서비스|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|

## <a name="capabilities-by-enrollment-method"></a>등록 메서드별 기능

| **기능** | **[Azure AD 조인됨](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Autopilot을 사용하여 Azure AD 조인됨](enrollment-autopilot.md)** |**[대량](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#bring-your-own-device)** | **GPO** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|조건부 액세스                                      |![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|
|장치와 연결된 사용자                    |![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|
|Azure AD Premium 필요                               |![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|
|장치는 CA에서 보호되는 리소스를 평가할 수 있음             |![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|
|사용자는 해당 장치에서 관리자가 아니어야 함               |![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|
|장치 설치 환경을 구성하는 기능        |![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|
|사용자 개입 없이 장치를 등록하는 기능      |![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|
|PowerShell 스크립트를 실행하는 기능                       |![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)| 
|AD 도메인 조인 후 자동 등록 지원      |![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|
|하이브리드 Azure AD 조인 후 자동 등록 지원|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|
|Azure AD 조인 후 자동 등록 지원       |![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|

## <a name="next-steps"></a>다음 단계

[등록 옵션](enrollment-options.md)
