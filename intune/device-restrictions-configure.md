---
title: Microsoft Intune - Azure에서 장치 제한 설정 구성 | Microsoft Docs
description: Microsoft Intune에서 Android, macOS, iOS, Windows Phone 및 Windows 10 장치에서 기능을 제한하는 장치 프로필 추가
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/27/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 9b84877d37d26dababda2987801fc7267cb3c2e6
ms.sourcegitcommit: 51b763e131917fccd255c346286fa515fcee33f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52181210"
---
# <a name="configure-device-restriction-settings-in-microsoft-intune"></a>Microsoft Intune에서 장치 제한 설정 구성

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

장치 제한을 통해 다음과 같은 다양한 범주에 걸쳐 관리하는 광범위한 설정 및 기능을 제어할 수 있습니다.
- 보안
- 브라우저
- 하드웨어
- 데이터 공유 설정

예를 들어 iOS 장치의 사용자가 장치 카메라에 액세스하지 못하도록 하는 장치 제한 프로필을 만들 수 있습니다.

장치 제한 프로필 기본 사항을 학습한 다음, 각 플랫폼에 대한 더 많은 아티클을 읽어 장치 세부 사항을 알아봅니다.

## <a name="create-a-device-profile-containing-device-restriction-settings"></a>장치 제한 설정을 포함하는 장치 프로필 만들기

1. [Azure 포털](https://portal.azure.com)에 로그인합니다.
2. **모든 서비스**를 선택하고 **Intune**에서 필터링하고 **Microsoft Intune**을 선택합니다.
3. **장치 구성** > **프로필** > **프로필 만들기**를 선택합니다.
4. 장치 제한 프로필의 **이름** 및 **설명**을 입력합니다.
5. **플랫폼** 드롭다운 목록에서 사용자 지정 설정을 적용할 장치 플랫폼을 선택합니다. 현재 장치 제한 설정에 대해 다음 플랫폼 중 하나를 선택할 수 있습니다.
    - **OWA(Outlook Web Access)**
    - **iOS**
    - **macOS**
    - **Windows Phone 8.1**
    - **Windows 8.1 이상**
    - **Windows 10 이상**
6. **프로필** 유형 드롭다운 목록에서 **장치 제한**을 선택합니다. Surface Hub와 같은 Windows 10 Team 장치에 대한 장치 제한 프로필을 만들려면 **장치 제한(Windows 10 Team)** 을 선택합니다.
7. 선택한 플랫폼에 따라 구성할 수 있는 설정이 다릅니다. 각 플랫폼에 대한 자세한 설정을 보려면 다음 항목 중 하나로 이동하세요.
    - [Android 설정](device-restrictions-android.md)
    - [iOS 설정](device-restrictions-ios.md)
    - [macOS 설정](device-restrictions-macos.md)
    - [Windows Phone 8.1 설정](device-restrictions-windows-phone-8-1.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10 설정](device-restrictions-windows-10.md)
    - [Windows 10 Team 설정](device-restrictions-windows-10-teams.md)
    - [Windows Holographic for Business 설정](device-restrictions-windows-holographic.md)
    - [Android 회사 프로필 설정](device-restrictions-android-for-work.md)
8. 완료되면 **프로필 만들기** 페이지로 돌아와서 **만들기**를 클릭합니다.

프로필이 만들어지고 프로필 목록 페이지에 표시됩니다.
계속해서 이 프로필을 그룹에 할당하려면 [장치 프로필을 할당하는 방법](device-profile-assign.md)을 참조하세요.

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/disable-android-camera.png)

-->
