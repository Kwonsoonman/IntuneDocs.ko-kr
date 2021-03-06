---
title: Windows Autopilot을 사용하여 장치 등록
titleSuffix: Microsoft Intune
description: Windows Autopilot을 사용하여 Windows 10 장치를 등록하는 방법을 알아봅니다.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/5/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: a2dc5594-a373-48dc-ba3d-27aff0c3f944
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.openlocfilehash: 2ef7ebf495511e1d5c04aa8a9c459ba48f3dbb42
ms.sourcegitcommit: 51b763e131917fccd255c346286fa515fcee33f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52180862"
---
# <a name="enroll-windows-devices-by-using-the-windows-autopilot"></a>Windows Autopilot을 사용하여 Windows 장치 등록  
Windows Autopilot이 장치 등록을 간소화합니다. 사용자 지정 운영 체제 이미지 빌드 및 유지 관리는 시간이 오래 걸리는 프로세스입니다. 또한 최종 사용자에게 제공하기 전에 이러한 사용자 지정 운영 체제 이미지를 새 장치에 적용하여 사용 준비를 하는 데에도 시간이 걸릴 수 있습니다. Microsoft Intune 및 Autopilot을 사용하면 사용자 지정 운영 체제 이미지를 빌드 및 유지 관리하고 장치에 적용할 필요 없이 최종 사용자에게 새 장치를 제공할 수 있습니다. Intune을 사용하여 Autopilot 장치를 관리하는 경우 장치를 등록한 후에 정책, 프로필, 앱 등을 관리할 수 있습니다. 이점, 시나리오 및 필수 구성 요소에 대한 개요는 [Windows Autopilot 개요](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot)를 참조하세요.


## <a name="prerequisites"></a>전제 조건
- [Windows 자동 등록 사용](https://docs.microsoft.com/intune-classic/deploy-use/set-up-windows-device-management-with-microsoft-intune#enable-windows-10-automatic-enrollment)
- [Azure Active Directory Premium 구독](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) <!--&#40;[trial subscription](http://go.microsoft.com/fwlink/?LinkID=816845)&#41;-->

## <a name="how-to-get-the-csv-for-import-in-intune"></a>InTune에서 가져올 CSV를 얻는 방법

사용 방법에 대한 자세한 내용은 'PowerShell cmdlet 이해'를 참조하세요.

- [Get-WindowsAutoPilotInfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo/1.3/Content/Get-WindowsAutoPilotInfo.ps1)

## <a name="add-devices"></a>장치 추가

장치 정보가 포함된 CSV 파일을 가져와서 Windows Autopilot 장치를 추가할 수 있습니다.

1. [Azure Portal의 Intune](https://aka.ms/intuneportal)에서 **장치 등록** > **Windows 등록** > **장치** > **가져오기**를 선택합니다.

    ![Windows Autopilot 장치 스크린샷](media/enrollment-autopilot/autopilot-import-device.png)

2. **Windows Autopilot 장치 추가** 에서 추가할 장치를 나열하는 CSV 파일로 이동합니다. 파일에는 일련 번호, Windows 제품 ID, 하드웨어 해시 및 장치의 선택적 주문 ID가 나열되어야 합니다.

    ![Windows AutoPilot 장치 추가 스크린샷](media/enrollment-autopilot/autopilot-import-device2.png)

3. **가져오기**를 선택하여 장치 정보 가져오기를 시작합니다. 가져오기는 몇 분 정도 걸릴 수 있습니다.

4. 가져오기가 완료되면 **장치 등록** > **Windows 등록** > **Windows Autopilot** > **장치** > **동기화**를 선택합니다. 동기화가 진행 중이라는 메시지가 표시됩니다. 동기화되는 장치의 수에 따라 프로세스가 완료되는 데 몇 분 정도 걸릴 수 있습니다.

5. 보기를 새로 고쳐 새 장치를 확인합니다.

## <a name="create-an-autopilot-device-group"></a>Autopilot 장치 그룹 만들기

1. [Azure Portal의 Intune](https://aka.ms/intuneportal)에서 **그룹** > **새 그룹**을 선택합니다.
2. **그룹** 블레이드에서:
    1. **그룹 형식**에서 **보안**을 선택합니다.
    2. **그룹 이름** 및 **그룹 설명**을 입력합니다.
    3. **멤버 자격 형식**에서 **할당** 또는 **동적 장치**를 선택합니다.
3. 이전 단계에서 **멤버 자격 형식**에 대해 **할당됨**을 선택했다면 **그룹** 블레이드에서 **멤버**를 선택하고 Autopilot 장치를 그룹에 추가합니다.
    아직 등록되지 않은 AutoPilot 장치는 장치 이름이 장치의 일련 번호와 동일한 장치입니다.
4. 위의 **멤버 자격 형식**에 대해 **동적 장치**를 선택했다면 **그룹** 블레이드에서 **동적 장치 멤버**를 선택하고 **고급 규칙** 상자에서 다음 코드를 입력합니다.
    - Autopilot 장치를 모두 포함한 그룹을 만들려는 경우 `(device.devicePhysicalIDs -any _ -contains "[ZTDId]")`를 입력합니다.
    - 특별 주문 ID를 사용하여 Autopilot 장치를 모두 포함한 그룹을 만들려는 경우 `(device.devicePhysicalIds -any _ -eq "[OrderID]:179887111881") `를 입력합니다.
    - 특별 구매 주문 ID를 사용하여 Autopilot 장치를 모두 포함한 그룹을 만들려는 경우 `(device.devicePhysicalIds -any _ -eq "[PurchaseOrderId]:76222342342")`를 입력합니다.
    
    **고급 규칙** 코드를 추가한 후에 **저장**을 선택합니다.
5. **만들기**를 선택합니다.  

## <a name="create-an-autopilot-deployment-profile"></a>Autopilot 배포 프로필 만들기
Autopilot 배포 프로필은 Autopilot 장치를 구성하는 데 사용됩니다.
1. [Azure Portal의 Intune](https://aka.ms/intuneportal)에서 **장치 등록** > **Windows 등록** > **배포 프로필** > **프로필 만들기**를 선택합니다.
2. **이름** 및 선택적 **설명**을 입력합니다.
3. 할당된 그룹의 모든 장치가 자동으로 Autopilot으로 변환되도록 하려면 **모든 대상 장치를 다시 Autopilot으로 변환**을 **예**로 설정합니다. 할당된 그룹에서 Autopilot이 아닌 모든 장치는 Autopilot 배포 서비스에 등록됩니다. 등록을 처리하는 데 48시가 가량 걸립니다. 장치 등록을 취소하고 재설정하면 Autopilot이 해당 장치를 등록합니다. 이 방법으로 장치를 등록한 후 이 옵션을 비활성화하거나 프로필 할당을 제거해도 장치가 Autopilot 배포 서비스에서 제거되지 않습니다. 대신 [장치를 직접 제거](enrollment-autopilot.md#delete-autopilot-devices)해야 합니다.
4. **배포 모드**에서 이러한 두 옵션 중 하나를 선택합니다.
    - **사용자 기반**: 이 프로필을 사용하는 장치는 장치를 등록한 사용자와 연결됩니다. 장치를 등록하려면 사용자 자격 증명이 필요합니다.
    - **자체 배포(미리 보기)**: (최신 [Windows 10 Insider Preview 빌드](https://docs.microsoft.com/windows-insider/at-work-pro/) 필요) 이 프로필을 사용하는 장치는 장치를 등록하는 사용자와 연결되지 않습니다. 장치를 등록하는 데 사용자 자격 증명이 필요하지 않습니다.
5. **다음으로 Azure AD에 조인** 상자에서 **Azure AD 조인됨**을 선택합니다.
6. **OOBE(기본 제공 환경)** 를 선택하고, 다음 옵션을 구성한 다음, **저장**을 선택합니다.
    - **언어(지역)***: 장치에 사용할 언어를 선택합니다. 이 옵션은 **배포 모드**에 대해 **자체 배포**를 선택한 경우에만 사용할 수 있습니다.
    - **키보드 자동으로 구성***: **언어(지역)** 을 선택한 경우 **예**를 선택하여 키보드 선택 영역 페이지를 건너뜁니다. 이 옵션은 **배포 모드**에 대해 **자체 배포**를 선택한 경우에만 사용할 수 있습니다.
    - **EULA(최종 사용자 사용권 계약)**: 사용자에게 EULA를 표시할지 여부를 선택합니다(Windows 10 버전 1709 이상).
    - **개인 정보 설정**: 사용자에게 개인 정보 설정을 표시할지 여부를 선택합니다.
    - **계정 변경 옵션 숨기기(Windows 참가자에게만 해당)**: **숨기기**를 선택하여 계정 변경 옵션이 회사 로그인 및 도메인 오류 페이지에서 표시되지 않도록 합니다. 이러한 옵션을 사용하려면 [Azure Active Directory에서 회사 브랜딩을 구성](https://docs.microsoft.com/azure/active-directory/fundamentals/customize-branding)해야 합니다.
    - **사용자 계정 유형**: 사용자 계정 유형(**관리자** 또는 **표준** 사용자)을 선택합니다.
    - **컴퓨터 이름 템플릿 적용(Windows 참가자에게만 해당)**: **예**를 선택하여 등록하는 동안 장치의 이름을 지정할 때 사용할 템플릿을 만듭니다. 이름은 15자 이하여야 하고, 문자, 숫자 및 하이픈만 포함할 수 있습니다. 이름이 모두 숫자일 수는 없습니다. [%SERIAL% 매크로](https://docs.microsoft.com/windows/client-management/mdm/accounts-csp)를 사용하여 하드웨어별 일련 번호를 추가합니다. 또는 [%RAND:x% 매크로](https://docs.microsoft.com/windows/client-management/mdm/accounts-csp)를 사용하여 숫자의 임의 문자열을 추가합니다. 여기서 x는 추가할 자릿수입니다. 

6. **만들기**를 선택하여 프로필을 만듭니다. 이제 Autopilot 배포 프로필을 장치에 할당할 수 있습니다.

***배포 모드**에 대해 **자체 배포(미리 보기)** 를 선택한 경우에만(최신 [Windows 10 Insider Preview 빌드](https://docs.microsoft.com/windows-insider/at-work-pro/) 필요) **언어(지역)** 및 **키보드 자동으로 구성**을 둘 다 사용할 수 있습니다.


## <a name="assign-an-autopilot-deployment-profile-to-a-device-group"></a>장치 그룹에 Autopilot 배포 프로필 할당

1. [Azure Portal의 Intune](https://aka.ms/intuneportal)에서 **장치 등록** > **Windows 등록** > **배포 프로필**을 선택하고 프로필을 선택합니다.
2. 특정 프로필 블레이드에서 **할당**을 선택합니다. 
3. **그룹 선택**을 선택한 다음, **그룹 선택** 블레이드에서 프로필을 할당할 그룹을 선택한 다음, **선택**을 선택합니다.

## <a name="edit-an-autopilot-deployment-profile"></a>Autopilot 배포 프로필 편집
Autopilot 배포 프로필을 만든 후에는 배포 프로필의 특정 부분을 편집할 수 있습니다.   

1. [Azure Portal의 Intune](https://aka.ms/intuneportal)에서 **장치 등록**을 선택합니다.
2. **Windows 등록** 아래의 **Windows Autopilot** 섹션에서 **배포 프로필**을 선택합니다.
3. 편집하려는 프로필을 선택합니다.
4. 왼쪽에 있는 **속성**을 클릭하여 배포 프로필의 이름이나 설명을 변경합니다. 변경한 후에 **저장**을 클릭합니다.
5. OOBE 설정을 변경하려면 **설정**을 클릭합니다. 변경한 후에 **저장**을 클릭합니다.

> [!NOTE]
> 프로필의 변경 내용은 해당 프로필에 할당된 장치에 적용됩니다. 그러나 장치를 다시 설정하고 다시 등록할 때까지는 Intune에 이미 등록되어 있는 장치에 업데이트된 프로필이 적용되지 않습니다.

## <a name="alerts-for-windows-autopilot-unassigned-devices-----163236---"></a>Windows Autopilot 할당되지 않은 장치에 대한 경고 <!-- 163236 -->  

경보에는 Autopilot 배포 프로필이 없는 Autopilot 프로그램 장치 수가 표시됩니다. 경고의 정보를 사용하여 프로필을 만들어서 할당되지 않은 장치에 할당하십시오. 경고를 클릭하면 Windows Autopilot 장치의 전체 목록과 해당 장치에 대한 자세한 정보가 표시됩니다.


할당되지 않은 장치에 대한 경고를 보려면 [Azure Portal의 Intune](https://aka.ms/intuneportal)에서 **장치 등록** > **개요** > **할당되지 않은 장치**를 선택합니다.  


## <a name="assign-a-user-to-a-specific-autopilot-device"></a>특정 Autopilot 장치에 사용자 할당

특정 Autopilot 장치에 사용자를 할당할 수 있습니다. 이렇게 할당하면 Windows를 설정하는 동안 [회사 브랜드](https://docs.microsoft.com/azure/active-directory/fundamentals/customize-branding) 로그인 페이지에 Azure Active Directory의 사용자를 미리 입력합니다. 사용자 지정 인사말 이름을 설정할 수도 있습니다. Windows 로그인을 미리 입력하거나 수정하지 않습니다. 사용이 허가된 Intune 사용자만이 이러한 방식으로 할당될 수 있습니다.

필수 구성 요소: 구성된 Azure Active Directory 회사 포털 및 최신 [Windows 10 Insider Preview 빌드](https://docs.microsoft.com/windows-insider/at-work-pro/).

1. [Azure Portal의 Intune](https://aka.ms/intuneportal)에서 **장치 등록** > **Windows 등록** > **장치** > 장치 선택 > **사용자 할당**을 선택합니다.

    ![사용자 할당 스크린샷](media/enrollment-autopilot/assign-user.png)

2. 사용이 허가된 Azure 사용자를 선택하여 Intune을 사용하고 **선택**을 선택합니다.

    ![사용자 선택 스크린샷](media/enrollment-autopilot/select-user.png)

3. **사용자 이름** 상자에 친숙한 이름을 입력하거나 기본값을 그대로 수락합니다. 이 문자열은 Windows를 설정하는 동안 사용자가 로그인할 경우에 표시하는 친숙한 이름입니다.

    ![친숙한 이름 스크린샷](media/enrollment-autopilot/friendly-name.png)

4. **확인**을 선택합니다.


## <a name="delete-autopilot-devices"></a>Autopilot 장치 삭제

등록되지 않은 Windows Autopilot 장치를 삭제할 수 있습니다.

1. 장치가 Intune에 등록된 경우 먼저 [Azure Active Directory 포털에서 삭제](devices-wipe.md#delete-devices-from-the-azure-active-directory-portal)해야 합니다.

2. [Azure Portal의 Intune](https://aka.ms/intuneportal)에서 **장치 등록** > **Windows 등록** > **장치**를 선택합니다.

3. **Windows AutoPilot 장치**에서 삭제할 장치를 선택한 다음, **삭제**를 선택합니다.

4. **예**를 선택하여 삭제를 확인합니다. 삭제하는 데 몇 분 정도 걸릴 수 있습니다.

## <a name="using-autopilot-in-other-portals"></a>다른 포털에서 Autopilot 사용
모바일 장치 관리에 관심이 없는 경우 다른 포털에서 Autopilot을 사용할 수 있습니다. 다른 포털을 옵션으로 사용할 수 있지만, Intune만 사용하여 Autopilot 배포를 관리하는 것이 좋습니다. Intune과 다른 포털을 사용하는 경우 Intune에서 수행할 수 없는 작업은 다음과 같습니다.  

- Intune에서 만들었지만 다른 포털에서 편집한 프로필에 대한 변경 내용 표시
- 다른 포털에서 만든 프로필 동기화
- 다른 포털에서 수행한 프로필 할당에 대한 변경 내용 표시
- 다른 포털에서 수행한 프로필 할당 동기화
- 다른 포털에서 만든 장치 목록에 대한 변경 내용 표시

## <a name="windows-autopilot-for-existing-devices"></a>기존 장치에 대한 Windows Autopilot

Configuration Manager를 통해 [기존 장치에 대해 Autopilot](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430)을 사용하여 등록할 때 관련자 ID로 Windows 장치를 그룹화할 수 있습니다. 관련자 ID는 Autopilot 구성 파일의 매개 변수입니다. Azure AD 장치 특성인 [enrollmentProfileName](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#using-attributes-to-create-rules-for-device-objects)은 자동으로 "OfflineAutopilotprofile-\<관련자 ID\>"와 동일하게 설정됩니다. 이렇게 하면 enrollmentprofileName 특성을 사용하여 관련자 ID에 따라 임의의 Azure AD 동적 그룹을 만들 수 있습니다.

>[!WARNING] 
> 관련자 ID는 Intune에 미리 나열되지 않으므로 장치에서 원하는 관련자 ID를 보고할 수 있습니다. 사용자가 Autopilot 또는 Apple DEP 프로필 이름과 일치하는 관련자 ID를 만드는 경우 enrollmentProfileName 특성을 기반으로 하는 동적 Azure AD 장치 그룹에 장치가 추가됩니다. 이 충돌을 방지하려면:
> - 항상 ‘전체’ enrollmentProfileName 값과 일치하는 동적 그룹 규칙을 생성합니다.
> - “OfflineAutopilotprofile-”로 시작하는 Autopilot 또는 Apple DEP 프로필은 절대 이름으로 설정하지 마세요.

## <a name="next-steps"></a>다음 단계
등록한 Windows 10 장치에 대해 Windows Autopilot을 구성한 후에는 이러한 장치를 관리하는 방법을 알아봅니다. 자세한 내용은 [Microsoft Intune 장치 관리란?](https://docs.microsoft.com/intune/device-management)을 참조하세요.
