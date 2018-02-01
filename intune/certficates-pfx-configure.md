---
title: "Intune을 사용하여 PKCS 인증서 구성 및 관리"
titleSuffix: Intune on Azure
description: "Intune을 사용하여 PKCS 인증서를 구성 및 관리합니다.”"
keywords: 
author: MicrosoftGuyJFlo
ms.author: joflore
manager: dougeby
ms.date: 12/09/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 
ms.reviewer: 
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: d877a1de8e66372d36641dd863a517fecf176d69
ms.sourcegitcommit: a41ad9988a8c14e6b15123a9ea9bc29ac437a4ce
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="configure-and-manage-pkcs-certificates-with-intune"></a>Intune을 사용하여 PKCS 인증서 구성 및 관리

[!INCLUDE[azure_portal](./includes/azure_portal.md)]

## <a name="requirements"></a>요구 사항

Intune에서 PKCS 인증서를 사용하려면 다음 인프라가 있어야 합니다.

* 기존 AD DS(Active Directory Domain Services) 도메인이 구성됨.
 
  AD DS를 설치 및 구성하는 방법에 대한 자세한 내용은 [AD DS 디자인 및 계획](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/ad-ds-design-and-planning) 문서를 참조하세요.

* 기존 엔터프라이즈 CA(인증 기관)가 구성됨.

  AD CS(Active Directory 인증서 서비스)를 설치 및 구성하는 방법에 대한 자세한 내용은 [Active Directory 인증서 서비스 단계별 가이드](https://technet.microsoft.com/library/cc772393)를 참조하세요.

  > [!WARNING]
  > Intune에서는 독립 실행형 CA가 아닌 엔터프라이즈 CA(인증 기관)를 사용하여 AD CS를 실행해야 합니다.

* 엔터프라이즈 CA에 연결되어 있는 클라이언트.
* 엔터프라이즈 CA에서 내보낸 루트 인증서 복사본입니다.
* Intune 포털에서 다운로드한 Microsoft Intune Certificate Connector(NDESConnectorSetup.exe)입니다.
* Microsoft Intune Certificate Connector(NDESConnectorSetup.exe)를 호스트할 수 있는 Windows Server입니다.

## <a name="export-the-root-certificate-from-the-enterprise-ca"></a>엔터프라이즈 CA에서 루트 인증서 내보내기

VPN, WiFi 및 기타 리소스를 통해 인증하려면 각 장치에서 루트 또는 중간 CA 인증서가 필요합니다. 다음 단계에서는 엔터프라이즈 CA에서 필요한 인증서를 가져오는 방법을 설명합니다.

1. 관리 권한이 있는 계정으로 엔터프라이즈 CA에 로그인합니다.
2. 관리자 권한으로 명령 프롬프트를 엽니다.
3. 루트 CA 인증서를 나중에 액세스할 수 있는 위치로 내보냅니다.

   예를 들면 다음과 같습니다.

4.  마법사를 완료한 후 마법사를 닫기 전에 **인증서 커넥터 UI 시작**을 클릭합니다.

   `certutil -ca.cert certnew.cer`

   자세한 내용은 [인증서 관리를 위한 Certutil 작업](https://technet.microsoft.com/library/cc772898.aspx#BKMK_ret_sign)을 참조하세요.

## <a name="configure-certificate-templates-on-the-certification-authority"></a>인증 기관에서 인증서 템플릿 구성

1. 관리 권한이 있는 계정으로 엔터프라이즈 CA에 로그인합니다.
2. **인증 기관** 콘솔을 엽니다.
3. **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **관리**를 선택합니다.
4. **사용자** 인증서 템플릿을 찾아서 마우스 오른쪽 단추로 클릭한 다음 **템플릿 복제**를 선택합니다. 창이 열리고 **새 템플릿의 속성**이 표시됩니다.
5. **호환성** 탭에서 다음을 수행합니다.
   * **인증 기관**을 **Windows Server 2008 R2**로 설정
   * **인증서 받는 사람**을 **Windows 7/Server 2008 R2**로 설정
6. **일반** 탭에서 다음을 수행합니다.
   * **템플릿 표시 이름**을 의미 있는 이름으로 설정합니다.

   > [!WARNING]
   > 기본적으로 **템플릿 이름**은 *공백 없이* **템플릿 표시 이름**과 동일합니다. 나중에 사용할 수 있도록 템플릿 이름을 기록합니다.

7. **요청 처리** 탭에서 **개인 키를 내보낼 수 있음** 상자를 선택합니다.
8. **암호화** 탭에서 **최소 키 크기**가 2048로 설정되었는지 확인합니다.
9. **주체 이름** 탭에서 **요청 시 제공** 라디오 단추를 선택합니다.
10. **확장** 탭에서 **응용 프로그램 정책** 아래에 파일 시스템 암호화, 메일 보안 및 클라이언트 인증이 표시되는지 확인합니다.
    
      > [!IMPORTANT]
      > iOS 및 macOS 인증서 템플릿의 경우 **확장** 탭에서 **키 사용**을 편집하고 **서명이 원본 증명임**이 선택되어 있지 않음을 확인합니다.

11. **보안** 탭에서 Microsoft Intune Certificate Connector를 설치할 서버의 컴퓨터 계정을 추가합니다.
    * 이 계정에 **읽기** 및 **등록** 권한을 허용합니다.
12. **적용**을 클릭한 다음 **확인**을 클릭하여 인증서 템플릿을 저장합니다.
13. **인증서 템플릿 콘솔**을 닫습니다.
14. **인증 기관** 콘솔에서 **인증서 템플릿**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**, **발급할 인증서 템플릿**을 차례로 클릭합니다.
    * 이전 단계에서 만든 템플릿을 선택하고 **확인**을 클릭합니다.
15. 서버에서 Intune 등록 장치 및 사용자를 대신하여 인증서를 관리하려면 아래 단계를 따릅니다.

    a. 인증 기관을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.

    b. [보안] 탭에서 Microsoft Intune Certificate Connector를 실행할 서버의 컴퓨터 계정을 추가합니다.
      * **인증서 발급 및 관리** 및 **인증서 요청** 허용 권한을 컴퓨터 계정에 부여합니다.
16. 엔터프라이즈 CA에서 로그아웃합니다.

## <a name="download-install-and-configure-the-microsoft-intune-certificate-connector"></a>Microsoft Intune Certificate Connector 다운로드, 설치 및 구성

![ConnectorDownload][ConnectorDownload]

1. Azure Portal에서 **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다.
2. **Intune** 블레이드에서 **장치 구성**을 선택합니다. 
3. **장치 구성** 블레이드에서 **인증 기관**을 선택합니다. 
4. **추가**를 클릭하고 **커넥터 파일 다운로드**를 선택합니다. 설치할 서버에서 액세스할 수 있는 위치에 다운로드를 저장합니다. 
5.  Microsoft Intune Certificate Connector를 설치할 서버에 로그인합니다.
6.  설치 프로그램을 실행하고 기본 위치를 적용합니다. 커넥터를 C:\Program Files\Microsoft Intune\NDESConnectorUI\NDESConnectorUI.exe에 설치합니다.
    1. 설치 프로그램 옵션 페이지에서 **PFX 배포**를 선택하고 **다음**을 클릭합니다.
    2. **설치**를 클릭하고 설치가 완료될 때까지 기다립니다.
    3. 완료 페이지에서 **Intune Connector 시작** 확인란을 선택하고 **마침**을 클릭합니다.
7.  [NDES Connector] 창이 **등록** 탭으로 열립니다. Intune에 대한 연결을 사용하려면 **로그인**을 클릭하고 관리자 권한이 있는 계정을 제공합니다.
8.  **고급** 탭에서 **이 컴퓨터의 시스템 계정 사용(기본값)** 라디오 단추를 선택한 상태로 둡니다.
9.  **적용**을 클릭한 다음 **닫기**를 클릭합니다.
10. 이제 Azure Portal에서 다시 이동합니다. 몇 분 후에 **Intune** > **장치 구성** > **인증 기관**의 **연결 상태** 아래에 녹색 확인 표시와 **활성** 단어가 표시됩니다. 이 확인을 통해 커넥터 서버가 Intune과 통신할 수 있음을 알 수 있습니다.


## <a name="create-a-device-configuration-profile"></a>장치 구성 프로필 만들기

1. [Azure 포털](https://portal.azure.com)에 로그인합니다.
2. **Intune**, **장치 구성**, **프로필**로 이동하고 **프로필 만들기**를 클릭합니다.

   ![NavigateIntune][NavigateIntune]

3. 다음 정보를 채웁니다.
   * 프로필의 **이름**
   * 선택적으로 설명 설정
   * 프로필을 배포할 **플랫폼**
   * **프로필 형식**을 **신뢰할 수 있는 인증서**로 설정
4. **설정**으로 이동하여 이전에 내보낸 .cer 파일 루트 CA 인증서를 제공합니다.

   > [!NOTE]
   > **3단계**에서 선택한 플랫폼에 따라 인증서의 **대상 저장소**를 선택하는 옵션이 제공되거나 제공되지 않을 수 있습니다.

   ![ProfileSettings][ProfileSettings]

5. **확인**, **만들기**를 차례로 클릭하여 프로필을 저장합니다.
6. 하나 이상의 장치에 새 프로필을 할당하려면 [Microsoft Intune 장치 프로필을 할당하는 방법](device-profile-assign.md)을 참조하세요.

## <a name="create-a-pkcs-certificate-profile"></a>PKCS 인증서 프로필 만들기

1. [Azure 포털](https://portal.azure.com)에 로그인합니다.
2. **Intune**, **장치 구성**, **프로필**로 이동하고 **프로필 만들기**를 클릭합니다.
3. 다음 정보를 채웁니다.
   * 프로필의 **이름**
   * 선택적으로 설명 설정
   * 프로필을 배포할 **플랫폼**
   * **프로필 형식**을 **PKCS 인증서**로 설정
4. **설정**으로 이동하여 다음 정보를 제공합니다.
   * **갱신 임계값(%)** - 권장 값은 20%입니다.
   * **인증서 유효 기간** - 인증서 템플릿을 변경하지 않은 경우 이 옵션을 1년으로 설정해야 합니다.
   * **인증 기관** - 이 옵션은 엔터프라이즈 CA의 내부 FQDN(정규화된 도메인 이름)입니다.
   * **인증 기관 이름** - 이 옵션은 엔터프라이즈 CA의 이름이며 이전 항목과 다를 수 있습니다.
   * **인증서 템플릿 이름** - 이 옵션은 이전에 생성된 템플릿의 이름입니다. 기본적으로 **템플릿 이름**은 *공백 없이* **템플릿 표시 이름**과 동일합니다.
   * **주체 이름 형식** - 별도로 필요한 경우가 아니면 이 옵션을 **일반 이름**으로 설정합니다.
   * **주체 대체 이름** - 별도로 필요한 경우가 아니면 이 옵션을 **UPN(사용자 계정 이름)**으로 설정합니다.
   * **확장된 키 사용** - 이전 섹션 **인증 기관에서 인증서 템플릿 구성**의 10단계에서 기본 설정을 사용한 경우에는 선택 상자에서 다음 **미리 정의된 값**을 추가합니다.
      * **모든 용도**
      * **클라이언트 인증**
      * **메일 보안**
   * **루트 인증서** - (Android 프로필의 경우) 이 옵션은 이전 섹션 [엔터프라이즈 CA에서 루트 인증서 내보내기](#export-the-root-certificate-from-the-enterprise-ca)의 3단계에서 내보낸 .cer 파일입니다.

5. **확인**, **만들기**를 차례로 클릭하여 프로필을 저장합니다.
6. 하나 이상의 장치에 새 프로필을 할당하려면 [Microsoft Intune 장치 프로필을 할당하는 방법](device-profile-assign.md) 문서를 참조하세요.


[NavigateIntune]: ./media/certificates-pfx-configure-profile-new.png "Azure Portal에서 Intune으로 이동하여 신뢰할 수 있는 인증서에 대한 새 프로필을 만듭니다."
[ProfileSettings]: ./media/certificates-pfx-configure-profile-fill.png "프로필을 만들고 신뢰할 수 있는 인증서를 업로드합니다."
[ConnectorDownload]: ./media/certificates-download-connector.png "Azure Portal에서 인증서 커넥터 다운로드"  
