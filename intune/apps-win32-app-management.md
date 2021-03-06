---
title: Microsoft Intune에 Win32 앱 추가
titlesuffix: ''
description: Microsoft Intune으로 Win32 앱을 추가, 제공 및 관리하는 방법을 알아보세요. 이 항목에서는 Intune Win32 앱 제공 및 관리 기능에 대한 개요와 Win32 앱 문제 해결 정보를 제공합니다.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/15/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 0dc1974a57e5a5aa6808936c37e02fd31a7cac7b
ms.sourcegitcommit: 51b763e131917fccd255c346286fa515fcee33f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52187297"
---
# <a name="intune-standalone---win32-app-management-public-preview"></a>Intune 독립 실행형 - Win32 앱 관(공개 미리 보기)

Intune 독립 실행형은 보다 나은 Win32 앱 관리 기능을 제공합니다. 클라우드로 연결된 고객은 Win32 앱 관리를 위한 Configuration Manager를 사용할 수 있지만, Intune 전용 고객은 Win32 LOB(사업 부문) 앱에 대한 보다 나은 관리 기능을 사용할 수 있습니다. 이 항목에서는 Intune Win32 앱 관리 기능과 문제 해결 정보에 대한 개요를 제공합니다.

## <a name="prerequisites-for-public-preview"></a>공개 미리 보기의 필수 구성 요소

- Windows 10 버전 1607 이상(Enterprise)
- Windows 10 클라이언트의 필수 요건은 다음과 같습니다. 
    - AAD(Azure Active Directory) 또는 Hybrid Azure Active Directory에 가입해야 합니다.
    - Intune(MDM-managed)에 등록되어 있어야 합니다.
- Windows 응용 프로그램 크기는 공개 미리 보기 상태에서 앱당 8GB로 제한됩니다. 

> [!NOTE]
> 현재 Windows 10 버전 1607의 Pro 및 Education 버전에 대한 테스트를 진행하고 있으며, 고객의 피드백을 기다립니다.


## <a name="prepare-the-win32-app-content-for-upload"></a>업로드할 Win32 앱 콘텐츠 준비

[Microsoft Intune Win32 앱 업로드 준비 도구](https://github.com/Microsoft/Intune-Win32-App-Packaging-Tool)를 사용하여 Win32 앱을 전처리합니다. 패키징 도구는 응용 프로그램 설치 파일을 *.intunewin* 형식으로 변환합니다. 또한 패키지 도구는 Intune에서 요구하는 일부 특성을 검색하여 응용 프로그램 설치 상태를 확인합니다. 앱 설치 프로그램 폴더에서 이 도구를 사용하면 Intune 콘솔에서 Win32 앱을 만들 수 있습니다.

GitHub에서 [Microsoft Intune Win32 앱 업로드 준비 도구](https://github.com/Microsoft/Intune-Win32-App-Packaging-Tool)를 다운로드할 수 있습니다.

### <a name="available-command-line-parameters"></a>사용 가능한 명령줄 매개 변수 

|    **명령줄 매개 변수**    |    **설명**    |
|:------------------------------:|:----------------------------------------------------------:|
|    `-h`     |    도움말    |
|    `-c <setup_folder>`     |    모든 설치 파일에 대한 설정 폴더    |
|   ` -s <setup_file>`     |    설치 파일(예: *setup.exe* 또는 *setup.msi*)    |
|    `-o <output_folder>`     |    생성된 *.intunewin* 파일의 출력 폴더    |
|    `-q`       |    자동 모드    |

### <a name="example-commands"></a>예제 명령

|    **명령 예**    |    **설명**    |
|:-----------------------------------------------------------------------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|    `IntuneWinAppUtil -h`    |    이 명령은 도구에 대한 사용 정보를 보여줍니다.    |
|    `IntuneWinAppUtil -c <setup_folder> -s <source_setup_file> -o <output_folder> <-q>`    |    이 명령은 지정된 원본 폴더 및 설치 파일에서 `.intunewin` 파일을 생성합니다. MSI 설치 파일의 경우 이 도구는 Intune에 필요한 정보를 검색합니다. `-q`가 지정되면 명령이 자동 모드로 실행되고, 출력 파일이 이미 있으면 덮어씁니다. 또한 출력 폴더가 없으면 자동으로 생성됩니다.    |

*.intunewin* 파일을 생성하는 경우 참조해야 하는 모든 파일을 설치 폴더의 하위 폴더에 추가합니다. 그런 후, 상대 경로를 사용하여 필요한 특정 파일을 참조합니다. 예를 들면 다음과 같습니다.

**설치 원본 폴더:** *c:\testapp\v1.0*<br>
**라이선스 파일:** *c:\testapp\v1.0\licenses\license.txt*

상대 경로 *licenses\license.txt*를 사용하여 *license.txt* 파일을 참조하세요.

## <a name="create-assign-and-monitor-a-win32-app"></a>Win32 앱 만들기, 할당 및 모니터링

LOB(사업 부문) 앱과 마찬가지로 Win32 앱을 Microsoft Intune에 추가할 수 있습니다. 이 유형의 앱은 일반적으로 사내 또는 타사에서 작성됩니다. 다음 단계는 Windows 앱을 Intune에 추가할 수 있도록 지침을 제공합니다.

### <a name="step-1-specify-the-software-setup-file"></a>1단계: 소프트웨어 설치 파일 지정

1.  [Azure 포털](https://portal.azure.com/)에 로그인합니다.
2.  **모든 서비스** > **Intune**을 선택합니다. Intune은 **모니터링 + 관리** 섹션에 있습니다.
3.  **Intune** 창에서 **클라이언트 앱** > **앱** > **추가**을 선택합니다.
4.  **앱 추가** 창에 제공된 드롭다운 목록에서 **Windows 앱(Win32) - 미리 보기**를 선택합니다.

    ![스크린샷 추가 앱 - 추가 유형 드롭다운 상자](./media/apps-win32-app-01.png)

### <a name="step-2-upload-the-app-package-file"></a>2단계: 앱 패키지 파일 업로드

1.  **앱 추가** 창에서 **앱 패키지 파일**을 선택하여 파일을 선택합니다. 앱 패키지 파일 창이 표시됩니다.

    ![스크린샷 앱 패키지 파일](./media/apps-win32-app-02.png)

2.  **앱 패키지 파일** 창에서 찾아보기 단추를 선택합니다. 그런 다음 확장명이 *.intunewin*인 Windows 설치 파일을 선택합니다.
3.  작업을 마쳤으면 **확인**을 선택합니다.

### <a name="step-3-configure-app-information"></a>3단계: 앱 정보 구성

1.  **앱 추가** 창에서 **앱 정보**를 선택해 앱을 구성합니다.
2.  **앱 정보** 창에서 다음 정보를 구성합니다. 이 창의 일부 값은 자동으로 채워질 수 있습니다.
    - **이름**: 회사 포털에 표시되는 앱 이름을 입력합니다. 동일한 앱 이름을 두 번 사용하는 경우 각 앱이 회사 포털에 표시됩니다.
    - **설명**: 앱에 대한 설명을 입력합니다. 설명은 회사 포털에 표시됩니다.
    - **게시자**: 앱의 게시자 이름을 입력합니다.
    - **범주**: 기본 제공 앱 범주를 하나 이상 선택하거나 직접 만든 범주를 선택합니다. 범주를 사용하면 사용자가 회사 포털을 탐색할 때 앱을 더 쉽게 찾을 수 있습니다.
    - **회사 포털에서 이 항목을 추천 앱으로 표시**: 사용자가 앱을 찾을 때 회사 포털의 기본 페이지에서 앱이 눈에 잘 띄게 표시됩니다.
    - **정보 URL**: 선택적으로, 앱에 대한 정보가 포함된 웹 사이트의 URL을 입력합니다. URL은 회사 포털에 표시됩니다.
    - **개인 정보 URL**: 선택적으로, 앱에 대한 개인 정보 관련 정보가 포함된 웹 사이트의 URL을 입력합니다. URL은 회사 포털에 표시됩니다.
    - **개발자**: 선택적으로, 앱 개발자의 이름을 입력합니다.
    - **소유자**: 선택적으로, 이 앱의 소유자 이름을 입력합니다. 예를 들어 **HR 부서** 등을 입력합니다.
    - **메모**: 이 앱과 연결할 모든 메모를 입력합니다.
    - **로고**: 앱과 연결된 아이콘을 업로드합니다. 사용자가 회사 포털을 탐색할 때 이 아이콘이 앱과 함께 표시됩니다.
3.  작업을 마쳤으면 **확인**을 선택합니다.

### <a name="step-4-configure-app-installation-details"></a>4단계: 앱 설치 정보 구성
1.  **앱 추가** 창에서 **프로그램**을 선택하여 앱에 대한 설치 및 제거 명령을 구성합니다.
2.  전체 설치 명령줄을 추가하여 앱을 설치합니다. 

    예를 들어 앱 파일 이름이 **MyApp123**인 경우 `msiexec /i “MyApp123.msi”`를 추가합니다.

3.  앱의 GUID를 기반으로 앱을 제거하려면 전체 제거 명령줄을 추가합니다. 

    예를 들어 `msiexec /x “{12345A67-89B0-1234-5678-000001000000}”`를 구성할 수 있습니다.

    > [!NOTE]
    > **사용자** 또는 **시스템** 컨텍스트에 설치되도록 Win32 앱을 구성할 수 있습니다. **사용자** 컨텍스트는 지정된 사용자만을 가리킵니다. **시스템** 컨텍스트는 Windows 10 장치의 모든 사용자를 가리킵니다.
    >
    > 최종 사용자는 Win32 앱을 설치할 장치에 로그인할 필요가 없습니다.

4.  작업을 마쳤으면 **확인**을 선택합니다.

### <a name="step-5-configure-app-requirements"></a>5단계: 앱 요구 사항 구성

1.  **앱 추가** 창에서 **요구 사항**을 선택하여 앱 설치 전에 장치가 충족시켜야 할 요구 사항을 구성합니다.
2.  **요구 사항** 창에서 다음 정보를 구성합니다. 이 창의 일부 값은 자동으로 채워질 수 있습니다.
    - **운영 체제 아키텍처**: 앱을 설치하는 데 필요한 아키텍처를 선택합니다.
    - **최소 운영 체제**: 앱을 설치하는 데 필요한 최소 운영 체제를 선택합니다.
    - **필요한 디스크 공간(MB)**: 앱을 설치할 시스템 드라이브에 필요한 사용 가능한 디스크 공간을 선택적으로 추가합니다.
    - **필요한 실제 메모리(MB)**: 앱을 설치하는 데 필요한 실제 메모리(RAM)를 선택적으로 추가합니다.
    - **필요한 최소 논리 프로세서 수**: 앱을 설치하는 데 필요한 최소 논리 프로세서 수를 선택적으로 추가합니다.
    - **필요한 최소 CPU 속도(MHz)**: 앱을 설치하는 데 필요한 최소 CPU 속도를 선택적으로 추가합니다.
3.  작업을 마쳤으면 **확인**을 선택합니다.

### <a name="step-6-configure-app-detection-rules"></a>6단계: 앱 검색 규칙 구성

1.  **앱 추가** 창에서 **검색 규칙**을 선택하여 앱의 존재를 검색하기 위한 규칙을 구성합니다.
2.  **규칙 형식** 필드에서 앱의 존재를 검색하는 방법을 선택합니다. 검색 규칙을 수동으로 구성할 수도 있고, 사용자 정의 스크립트를 사용하여 앱의 존재를 검색할 수도 있습니다. 하나 이상의 검색 규칙을 선택해야 합니다. 

    > [!NOTE]
    > **검색 규칙** 창에서 여러 규칙을 추가하도록 선택할 수 있습니다. **모든** 규칙의 조건이 충족되어야 앱을 검색할 수 있습니다.

    - **검색 규칙을 수동으로 구성** - 다음 규칙 유형 중 하나를 선택할 수 있습니다.
        1.  **MSI** - MSI 버전 확인을 기반으로 확인합니다. 이 옵션은 한 번만 추가할 수 있습니다. 이 규칙 유형을 선택하면 다음 두 가지 설정이 가능합니다.
            - **MSI 제품 코드** - 앱에 유효한 MSI 제품 코드를 추가합니다.
            - **MSI 제품 버전 확인** - MSI 제품 코드 외에 MSI 제품 버전을 확인하려면 **예**를 선택합니다.
        2.  **파일** - 파일 또는 폴더 검색, 날짜, 버전 또는 크기를 기준으로 확인합니다.
            - **경로** - 검색할 파일 또는 폴더가 포함된 폴더의 전체 경로입니다.
            - **파일 또는 폴더** - 검색할 파일 또는 폴더입니다.
            - **검색 방법** - 앱의 존재를 확인하는 데 사용되는 검색 방법 유형을 선택합니다.
            - **64비트 클라이언트에서 32비트 앱과 연결됨** - 64비트 클라이언트의 32비트 컨텍스트에서 경로 환경 변수를 확장하려면 **예**를 선택합니다. 64비트 클라이언트의 64비트 컨텍스트에서 경로 변수를 확장하려면 **아니요**(기본값)를 선택합니다. 32비트 클라이언트는 항상 32비트 컨텍스트를 사용합니다.
            
            **파일 기반 검색 예**
            1.  파일 존재 여부를 확인합니다.
         
                ![검색 규칙 창의 스크린샷 - 파일 존재](./media/apps-win32-app-03.png)
        
            2.  폴더 존재 여부를 확인합니다.
         
                ![검색 규칙 창의 스크린샷 - 폴더 존재](./media/apps-win32-app-04.png)
        
        3. **레지스트리** - 값, 문자열, 정수 또는 버전을 기반으로 확인합니다.
            - **키 경로** - 검색할 값을 포함하는 레지스트리 항목의 전체 경로입니다.
            - **값 이름** - 검색할 레지스트리 값의 이름입니다. 이 값이 비어 있으면 키에서 검색이 수행됩니다. 검색 방법이 파일 또는 폴더 존재 검색이 아닌 경우에는 키의 값(기본값)이 검색 값으로 사용됩니다.
            - **검색 방법** - 앱의 존재를 확인하는 데 사용되는 검색 방법 유형을 선택합니다.
            - **64비트 클라이언트에서 32비트 앱과 연결됨** - 64비트 클라이언트에서 32비트 레지스트리를 검색하려면 **예**를 선택하세요. 64비트 클라이언트에서 64비트 레지스트리를 검색하려면 **아니요**(기본값)를 선택하세요. 32비트 클라이언트는 항상 32비트 레지스트리를 검색합니다.
            
            **레지스트리 기반 검색 예**
            1.  레지스트리 키가 존재하는지 확인합니다.
            
                ![검색 규칙 창의 스크린샷 - 레지스트리 키가 존재함](./media/apps-win32-app-05.png)    
            
            2.  레지스트리 값이 존재하는지 확인합니다(**미리 보기에서는 사용할 수 없음**).
        
                ![검색 규칙 창의 스크린샷 - 레지스트리 값이 존재함](./media/apps-win32-app-06.png)    
        
            3.  레지스트리 값 문자열이 일치하는지 확인합니다.
        
                ![검색 규칙 창의 스크린샷 - 레지스트리 값 문자열이 일치함](./media/apps-win32-app-07.png)    
     
    - **사용자 지정 검색 스크립트 사용** - 이 앱을 검색하는 데 사용할 PowerShell 스크립트를 지정합니다. 
    
        1.  **스크립트 파일** - 클라이언트에 앱이 있는지 검색하는 PowerShell 스크립트를 선택합니다. 스크립트가 모두 0 값 종료 코드를 반환하고 문자열 값을 STDOUT에 작성하면 앱이 검색됩니다.
        2.  **64비트 클라이언트에서 32비트 프로세스로 스크립트 실행** - 로그온한 최종 사용자의 자격 증명을 사용하여 스크립트를 실행하려면 **예**를 선택합니다. 시스템 컨텍스트에서 스크립트를 실행하려면 **아니요**(기본값)를 선택합니다.
        3.  **스크립트 서명 확인 강제 적용** - 스크립트가 신뢰할 수 있는 게시자에 의해 서명되었는지 확인하려면 **예**를 선택합니다. 그러면 경고 또는 프롬프트가 표시되지 않고 스크립트가 실행되도록 할 수 있습니다. 스크립트가 차단 해제된 상태로 실행됩니다. 서명 확인 없이 최종 사용자 확인으로 스크립트를 실행하려면 **아니요**(기본값)를 선택합니다.
    
        Intune Sidecar는 스크립트에서 결과를 확인합니다. 스크립트에 의해 표준 출력(STDOUT) 스트림, 표준 오류(STDERR) 스트림 및 종료 코드에 기록된 값을 읽습니다. 스크립트가 0이 아닌 값으로 끝나는 경우 스크립트는 실패하고 응용 프로그램 검색 상태는 설치되지 않음 상태입니다. 종료 코드가 0이고 STDOUT에 데이터가 포함되어 있으면 응용 프로그램 검색 상태는 설치됨 상태인 것입니다. 
    
        > [!NOTE]
        > 스크립트가 0 값으로 종료되면 스크립트 실행이 성공한 것입니다. 두 번째 출력 채널은 앱이 검색되었음을 나타냅니다. STDOUT 데이터는 앱이 클라이언트에서 발견되었음을 나타냅니다. STDOUT에서 특정 문자열을 찾지 않습니다.
    
3.  규칙을 추가한 후 **추가** > **확인**을 선택합니다.

### <a name="step-7-configure-app-return-codes"></a>7단계: 앱 반환 코드 구성

1.  **앱 추가** 창에서 **반환 코드**를 선택하여 앱 설치 재시도 동작 또는 설치 후 동작을 지정하는 데 사용되는 반환 코드를 추가합니다. 기본적으로 앱을 만드는 동안 반환 코드 항목이 추가됩니다. 그러나 추가 반환 코드를 추가하거나 기존 반환 코드를 변경할 수 있습니다. 
2.  **반환 코드** 창에서 반환 코드를 추가하거나 기존 반환 코드를 수정합니다.
    - **실패** - 앱 설치 실패를 나타내는 반환 값입니다.
    - **하드 재부팅** - 하드 재부팅 반환 코드는 재부팅 없이 클라이언트에 다음 Win32 앱 설치를 허용하지 않습니다. 
    - **소프트 재부팅** - 소프트 재부팅 반환 코드는 클라이언트 재부팅을 요구하지 않고 다음 Win32 앱 설치를 허용합니다. 현재 응용 프로그램의 설치를 완료하려면 재부팅해야 합니다.
    - **재시도** - 재시도 반환 코드 에이전트가 3회에 걸쳐 앱 설치를 시도합니다. 각 시도 사이의 대기 시간은 5분입니다. 
    - **성공** - 앱이 성공적으로 설치되었음을 나타내는 반환 값입니다.
3.  반환 코드 목록을 추가 또는 수정했으면 **확인**을 선택합니다.

### <a name="step-8-add-the-app"></a>8단계: 앱 추가

1.  **앱 추가** 창에서 앱 정보를 올바르게 구성했는지 확인합니다.
2.  **추가**를 선택하여 Intune에 앱을 업로드합니다.

### <a name="step-9-assign-the-app"></a>9단계: 앱 할당

1.  앱 창에서 **할당**을 선택합니다.
2.  **그룹 추가**를 선택하여 앱과 관련된 **그룹 추가** 창을 엽니다.
3.  특정 앱의 경우 **할당 유형**을 선택합니다.
    - **등록 장치에 대해 사용 가능**: 사용자가 회사 포털 앱 또는 회사 포털 웹 사이트에서 앱을 설치합니다.
    - **필수**: 앱이 선택한 그룹의 장치에 설치됩니다.
    - **제거**: 앱이 선택한 그룹의 장치에서 제거됩니다.
4.  **포함된 그룹**을 선택하고 이 앱을 사용할 그룹을 할당합니다.
5.  **할당** 창에서 **확인**을 선택하여 포함된 그룹 선택을 완료합니다.
6.  이 앱 할당에서 영향을 주지 않도록 사용자 그룹을 제외하려면 **그룹 제외**를 선택합니다.
7.  **그룹 추가** 창에서 **확인**을 선택합니다.
8.  앱 **할당** 창에서 **저장**을 선택합니다.

현재 Intune에 Win32 앱을 추가하는 단계를 완료한 상태입니다. 앱 할당 및 모니터링에 대한 자세한 내용은 [Microsoft Intune으로 그룹에 앱 할당](https://docs.microsoft.com/intune/apps-deploy) 및 [Microsoft Intune으로 앱 정보 및 할당 모니터링](https://docs.microsoft.com/intune/apps-monitor)을 참조하세요.

## <a name="install-required-and-available-apps-on-devices"></a>장치에 사용 가능한 필수 앱 설치

최종 사용자는 사용 가능한 필수 앱 설치에 대한 Windows 알림 메시지를 받게 됩니다. 다음 이미지는 장치가 다시 시작될 때까지 앱 설치가 완료되지 않았다는 알림 메시지를 나타낸 것입니다. 

![앱 설치에 대한 Windows 알림 메시지 스크린샷 예](./media/apps-win32-app-08.png)    

다음은 장치에 앱 변경이 적용되고 있음을 최종 사용자에게 알리는 이미지입니다.

![장치에 앱 변경이 적용되고 있음을 최종 사용자에게 알리는 스크린샷 예](./media/apps-win32-app-09.png)    

## <a name="troubleshoot-win32-app-issues"></a>Win32 앱 문제 해결
클라이언트 컴퓨터에 대한 에이전트 로그는 일반적으로 `C:\ProgramData\Microsoft\IntuneManagementExtension\Logs`에 있습니다. `CMTrace.exe`를 이용하여 이러한 로그 파일을 볼 수 있습니다. [SCCM 클라이언트 도구](https://docs.microsoft.com/sccm/core/support/tools)에서 *CMTrace.exe*를 다운로드할 수 있습니다. 

![에이전트 로그 스크린샷](./media/apps-win32-app-10.png)    

### <a name="troubleshooting-areas-to-consider"></a>고려할 문제 해결 영역
- 대상을 확인하여 에이전트가 장치에 설치되어 있는지 확인합니다. 그룹을 대상으로 하는 Win32 앱 또는 그룹을 대상으로 하는 PowerShell 스크립트는 보안 그룹에 대한 에이전트 설치 정책을 만듭니다.
- OS 버전 확인 – Windows 10 1607 이상.  
- Windows 10 SKU 확인 - Windows 10 S 또는 S-mode가 사용으로 설정된 Windows 버전은 MSI 설치를 지원하지 않습니다.

## <a name="next-steps"></a>다음 단계

- Intune의 앱을 추가하는 방법에 대한 자세한 내용은 [Microsoft Intune에 앱 추가](apps-add.md)를 참조하세요.
