---
title: Microsoft Intune을 사용한 Check Point SandBlast MTD
titlesuffix: ''
description: 회사 리소스에 대한 모바일 장치 액세스를 제어하기 위해 Intune을 사용하여 CheckPoint SandBlast Mobile Threat Defense(MTD)를 설정하는 방법입니다.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/03/2017
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 1e9b1576-b239-48cc-a672-da6b5fb7be0a
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 6c0c9db9955c8fbf08e5a17d3a1f9fb3fdba2cd5
ms.sourcegitcommit: 51b763e131917fccd255c346286fa515fcee33f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52184525"
---
# <a name="integrate-check-point-sandblast-mobile-with-intune"></a>Intune과 Check Point SandBlast Mobile 통합

## <a name="before-you-begin"></a>시작하기 전에

> [!NOTE] 
> 아래 단계는 [Check Point SandBlast Mobile MTD 콘솔](https://intune-4.eu1.locsec.net/)에서 수행되어야 합니다.

Intune과 Check Point SandBlast Mobile을 통합하는 과정을 시작하기 전에 다음 요소가 있는지 확인해야 합니다.

-   Microsoft Intune 구독

-   다음 권한을 부여할 Azure Active Directory 관리자 자격 증명

    -   로그인 및 사용자 프로필 읽기

    -   로그인한 사용자로 디렉터리에 액세스

    -   디렉터리 데이터 읽기

    -   Intune에 장치 정보 보내기

-   Check Point SandBlast Mobile MTD 콘솔에 액세스할 수 있는 관리자 자격 증명

### <a name="check-point-sandblast-app-authorization"></a>Check Point SandBlast 앱 권한 부여

Check Point SandBlast 앱 권한 부여 프로세스는 다음과 같이 구성되어 있습니다.

-   Check Point SandBlast Mobile 서비스에서 장치 상태와 관련된 정보를 Intune에 다시 전달할 수 있도록 통신을 허용합니다.

-   CheckPoint SandBlast Mobile이 Azure AD 등록 그룹 멤버와 동기화하여 해당 장치의 데이터베이스를 채웁니다.

-   Check Point SandBlast 관리 콘솔에서 Azure AD SSO(Single Sign-On)를 사용하도록 허용합니다.

-   Check Point SandBlast Mobile 앱에서 Azure AD SSO를 사용하여 로그인하도록 허용합니다.

## <a name="to-set-up-check-point-sandblast-mobile-integration"></a>Check Point SandBlast Mobile 통합을 설정하려면

1.  [Check Point SandBlast Mobile MTD 콘솔](https://intune-4.eu1.locsec.net/)로 이동하여 자격 증명으로 로그인합니다.

2.  **설정** 탭을 클릭합니다.

3.  **장치 관리**, **설정** 순으로 선택합니다.

4.  **MDM 서비스** 드롭다운 목록에서 **Microsoft Intune**을 선택합니다.

5.  Microsoft Intune을 MDM 서비스로 설정하면 **Microsoft Intune 구성** 화면이 표시됩니다. iOS, Android, Windows 같은 각 장치 플랫폼에 대해 **내 조직에 추가**를 선택하여 Check Point SandBlast Mobile에 Intune 및 Azure AD와 통신할 권한을 부여합니다.

    ![Check Point MTD Intune 구성을 보여주는 이미지](./media/checkpoint-MTD-1.PNG)

    > [!IMPORTANT]
    > 다음 단계를 계속하려면 모든 장치 플랫폼을 추가해야 합니다.

6.  **수락**을 선택하여 Check Point SandBlast Mobile 앱에 Intune 및 Azure Active Directory와 통신할 권한을 부여합니다.

7.  모든 장치 플랫폼을 사용하도록 설정한 후에는 Azure AD 보안 그룹을 입력해야 합니다.

8.  **확인**을 선택하고, Azure AD 보안 그룹이 성공적으로 확인되면 **저장**을 선택합니다.

## <a name="next-steps"></a>다음 단계

- [Check Point SandBlast Mobile 앱 설정](mtd-apps-ios-app-configuration-policy-add-assign.md)