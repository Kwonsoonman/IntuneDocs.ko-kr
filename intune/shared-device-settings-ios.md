---
title: "iOS용 Intune 공유 장치 구성 설정"
titleSuffix: Intune Azure preview
description: "Intune Azure 미리 보기: iOS 장치 잠금 화면에서 정보를 표시하는 데 사용할 수 있는 Intune 설정을 알아봅니다."
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 04/12/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: f122e4ee-90e7-4b42-b801-8c1c7c0a5bf7
ms.reviewer: heenamac
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: 6a2aba8b2f062a3e06d517a572992b84fd977514
ms.contentlocale: ko-kr
ms.lasthandoff: 05/23/2017


---

# <a name="shared-device-configuration-settings-to-display-messages-on-the-ios-device-lock-screen"></a>iOS 장치 잠금 화면에서 메시지를 표시하기 위한 공유 장치 구성 설정

[!INCLUDE[azure_preview](./includes/azure_preview.md)]

공유 장치 구성 설정을 사용하여 로그인 창 및 잠금 화면에 표시되는 선택적 텍스트를 지정할 수 있습니다(예: "분실 시, 돌려주기" 메시지 및 자산 태그 정보). 

>[!IMPORTANT]
> 이 기능은 iOS 9.3 이상을 실행하는 감독 모드 장치에서 지원됩니다.

1. **장치 기능** 블레이드에서 **공유 장치 구성(감독 모드인 경우에만)**을 선택합니다.
2. **공유 장치 구성(감독 모드인 경우에만)** 블레이드에서 다음을 구성합니다.
    - **자산 태그 정보** - 장치의 자산 태그에 대한 정보를 입력합니다. 예를 들면 **Contoso Corp에서 소유함**입니다. 입력한 정보는 이 프로필을 할당하는 모든 장치에 적용됩니다.
    - **잠금 화면 각주** - 장치를 분실했거나 도난당한 경우 반환하는 데 도움이 되는 정보를 입력합니다. 예를 들면 **발견하는 경우 ‘번호’로 연락해주세요**입니다.
3. 작업이 완료되면 **프로필 만들기** 블레이드로 돌아갈 때까지 **확인**을 선택한 다음 **만들기**를 선택합니다. 
