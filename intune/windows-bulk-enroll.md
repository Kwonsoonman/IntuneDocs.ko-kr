---
title: "Windows 10에 대한 대량 등록"
titlesuffix: Azure portal
description: "Microsoft Intune에 대한 대량 등록 패키지를 만듭니다."
keywords: 
author: Erikje
ms.author: erikje
manager: angrobe
ms.date: 10/23/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 1f39c02a-8d8a-4911-b4e1-e8d014dbce95
ms.reviewer: damionw
ms.custom: intune-azure
ms.openlocfilehash: f24bf5f8767763c3ca56d51127ab1d3f484e51d8
ms.sourcegitcommit: 833b1921ced35be140f0107d0b4205ecacd2753b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/04/2018
---
# <a name="bulk-enrollment-for-windows-devices"></a>Windows 장치에 대한 대량 등록

[!INCLUDE[azure_portal](./includes/azure_portal.md)]

관리자로서 여러 새로운 Windows 장치를 Azure Active Directory 및 Intune에 연결할 수 있습니다. Azure AD 테넌트에 대한 장치를 대량 등록하려면 WCD(Windows 구성 디자이너) 앱을 사용하여 프로비전 패키지를 만듭니다. 회사 소유 장치에 프로비전 패키지를 적용하면 장치가 Azure AD 테넌트에 연결되고 Intune 관리를 위해 등록됩니다. 패키지가 적용되면 Azure AD 사용자가 로그온할 수 있게 됩니다.

Azure AD 사용자는 이러한 장치에서 표준 사용자이며 할당된 Intune 정책 및 필수 앱을 수신합니다. 셀프 서비스 및 회사 포털 시나리오의 경우 이번에는 지원되지 않습니다.

## <a name="prerequisites-for-windows-devices-bulk-enrollment"></a>Windows 장치 대량 등록에 대한 필수 구성 요소

- Windows 10 크리에이터스 업데이트 이상을 실행하는 장치
- [Windows 자동 등록](windows-enroll.md#enable-windows-10-automatic-enrollment)

## <a name="create-a-provisioning-package"></a>프로비전 패키지 만들기

1. Microsoft 스토어에서 [WCD(Windows 구성 디자이너)](https://www.microsoft.com/store/apps/9nblggh4tx22)를 다운로드합니다.
![Windows 구성 디자이너 앱 스토어 스크린샷과 설명이 포함된 스크린샷](media/bulk-enroll-store.png)

2. **Windows 구성 디자이너** 앱을 열고 **데스크톱 장치 프로비전**을 선택합니다.
![Windows 구성 디자이너 앱에서 데스크톱 장치 프로비전을 선택하는 스크린샷](media/bulk-enroll-select.png)

3. **새 프로젝트** 창이 열리며, 여기서 다음 정보를 지정합니다.
  - **이름** - 프로젝트 이름
  - **프로젝트 폴더** - 프로젝트의 저장 위치
  - **설명** - 프로젝트에 대한 설명(옵션) ![Windows 구성 디자이너 앱에서 프로젝트 폴더 이름과 설명을 지정하는 스크린샷](media/bulk-enroll-name.png)

4.  장치에 대한 고유한 이름을 입력합니다. 이름에는 일련 번호(%%SERIAL%%) 또는 임의의 문자 집합이 포함될 수 있습니다. 필요에 따라 Windows 버전을 업그레이드하는 경우 제품 키를 입력하고, 공유용 장치를 구성하고, 사전 설치된 소프트웨어를 제거할 수도 있습니다.
![Windows 구성 디자이너 앱에서 이름, 프로젝트 폴더 및 설명을 지정하는 스크린샷](media/bulk-enroll-device.png)

5.  필요에 따라 장치를 처음 시작할 때 연결할 Wi-Fi 네트워크 장치를 구성할 수 있습니다.  네트워크 장치가 구성되지 않은 경우 장치를 처음 시작할 때 유선 네트워크 연결이 필요합니다.
![Windows 구성 디자이너 앱에서 네트워크 SSID 및 네트워크 유형 옵션을 포함하여 Wi-Fi를 사용하도록 구성하는 스크린샷](media/bulk-enroll-network.png)

6.  **Azure AD에 등록**을 선택하고, **대량 토큰 만료** 날짜를 입력한 다음 **대량 토큰 가져오기**를 선택합니다.
![Windows 구성 디자이너 앱에서 이름, 프로젝트 폴더 및 설명을 지정하는 스크린샷](media/bulk-enroll-account.png)

7. 대량 토큰을 가져올 Azure AD 자격 증명을 제공합니다.
![Windows 구성 디자이너 앱에서 이름, 프로젝트 폴더 및 설명을 지정하는 스크린샷](media/bulk-enroll-cred.png)

8.  **대량 토큰**을 성공적으로 가져오면 **다음**을 클릭합니다.

9. 필요에 따라 **응용 프로그램 추가** 및 **인증서 추가**를 수행할 수 있습니다. 이러한 앱 및 인증서는 장치에서 프로비전됩니다.

10. 경우에 따라 사용자 프로비전 패키지를 암호로 보호할 수 있습니다.  **만들기**를 클릭합니다.
![Windows 구성 디자이너 앱에서 이름, 프로젝트 폴더 및 설명을 지정하는 스크린샷](media/bulk-enroll-create.png)

## <a name="provision-devices"></a>장치 프로비전

1. 앱에서 지정한 **프로젝트 폴더**에 설정된 위치로 프로비전 패키지에 액세스합니다.

2. 장치에 프로비전 패키지를 적용하는 방법을 선택합니다.  다음 방법 중 하나로 장치에 프로비전 패키지를 적용할 수 있습니다.
 - USB 드라이브에 프로비전 패키지를 넣고, 대량 등록할 장치에 USB 드라이브를 삽입한 다음 초기 설정 중 적용
 - 네트워크 폴더에 프로비전 패키지를 넣고, 초기 설정 후 대량 등록할 장치에 삽입하여 적용

 프로비전 패키지 적용에 대한 단계별 지침은 [프로비전 패키지 적용](https://technet.microsoft.com/itpro/windows/configure/provisioning-apply-package)을 참조하세요.

3. 패키지를 적용하면 1분 후에 장치가 자동으로 다시 시작됩니다.
 ![Windows 구성 디자이너 앱에서 이름, 프로젝트 폴더 및 설명을 지정하는 스크린샷](media/bulk-enroll-add.png)

4. 장치가 다시 시작되면 Azure Active Directory에 연결하고 Microsoft Intune에서 등록합니다.

## <a name="troubleshooting-windows-bulk-enrollment"></a>Windows 대량 등록 문제 해결

### <a name="provisioning-issues"></a>프로비전 문제
프로비전은 새로운 Windows 장치에 사용하도록 고안되었습니다. 프로비전 오류가 발생할 경우 부팅 이미지에서 장치를 복구하거나 장치의 공장 기본 설정이 필요할 수도 있습니다. 이 예제에서는 프로비전 오류에 대한 몇 가지 이유에 대해 설명합니다.

- 로컬 계정을 만들지 않는 Active Directory 도메인 또는 Azure Active Directory 테넌트에 연결하려는 프로비전 패키지의 경우 네트워크 연결 중단으로 인해 도메인 연결 프로세스가 실패하는 경우 장치에 연결할 수 없습니다.
- 프로비저닝 패키지에서 실행된 스크립트는 시스템 컨텍스트에서 실행됩니다. 스크립트는 장치 파일 시스템과 구성을 임의로 변경할 수 있습니다. 악의적이거나 잘못된 스크립트는 장치를 이미지로 다시 설치하거나 공장 기본값으로 설정하는 방법으로만 복구할 수 있는 상태를 만듭니다.

### <a name="problems-with-bulk-enrollment-and-company-portal"></a>대량 등록 및 회사 포털 문제
사용자가 회사 포털을 사용하여 이전에 대량 등록된 장치를 등록하려고 하면 해당 장치에 추가 작업(설정 또는 등록)이 필요하다는 경고가 표시됩니다. 장치가 등록되지만 회사 포털 앱 또는 웹 사이트에서 등록이 인식되지 않습니다.

### <a name="bulk-enrollment-with-wi-fi"></a>Wi-Fi를 통한 대량 등록 

대량 등록 장치는 사용자 대상 인증서 및 Wi-Fi 배포를 사용할 수 없습니다. 이러한 연결을 관리하려면 [장치 수준 인증서](certificates-configure.md)를 사용해야 합니다. 

### <a name="conditional-access"></a>조건부 액세스
대량 등록을 사용하여 등록된 Windows 장치에는 조건부 액세스를 사용할 수 없습니다.
