---
title: "모바일 장치를 등록하는 방법 선택 | Microsoft Intune"
description: "몇 가지 간단한 질문에 응답하여 Intune에서 모바일 장치를 등록 하는 방법 결정"
keywords: 
author: NathBarn
manager: angrobe
ms.date: 07/25/2016
ms.topic: article
ms.prod: 
ms.service: 
ms.technology: 
ms.assetid: ed9250aa-e894-4eac-92b8-5f1a3748e255
ROBOTS: NOINDEX,NOFOLLOW
ms.reviewer: dagerrit
translationtype: Human Translation
ms.sourcegitcommit: e1fe6b167b7d46f03472833bc1c3c19030f47bce
ms.openlocfilehash: 825392d060229a6b3f3bd3e84ad4be127118aa21


---
# 모바일 장치를 등록하는 방법 선택

이러한 일련의 질문에 답변하면 관리하는 장치에 대한 최상의 등록 방법을 결정하는 데 도움이 됩니다.


## **공유 iOS 장치는 어떻게 관리해야 하나요?**

  > [!div class="button"]
  [iOS DEP 등록 >](/intune/deploy-use/ios-device-enrollment-program-in-microsoft-intune) [iOS 직접 등록 >](/intune/deploy-use/ios-direct-enrollment-in-microsoft-intune)  [DEM 등록 >](/intune/deploy-use/enroll-corporate-owned-devices-with-the-device-enrollment-manager-in-microsoft-intune)

  - **Apple의 DEP(장치 등록 프로그램)** - DEP로 구입되고 관리되는 iOS 장치는 등록 프로필을 사용하여 대상으로 지정될 수 있습니다. 사용자가 처음으로 장치를 켤 때 장치는 DEP 프로필을 다운로드하고 프로필 DEP를 사용하여 등록됩니다.

  - **Mac의 Apple Configurator** - Apple Configurator는 Mac PC에서 실행되는 Apple 응용 프로그램입니다. USB 케이블로 iOS 장치를 Mac에 연결하여 장치에 등록 프로필을 설치할 수 있습니다. 장치를 공장 기본 설정으로 복원하여 등록할 수 있는 경우 설정 도우미 등록을 사용합니다. 장치를 공장 기본 설정으로 복원하지 않으려는 경우에는 직접 등록을 사용합니다.

  - **장치 등록 관리자** -Intune의 DEM(장치 등록 관리자)을 사용하면 관리자가 단일 사용자 계정으로 여러 모바일 장치를 등록할 수 있습니다. 이러한 장치에는 사용자 선호도(예: 전용 사용자)가 있을 수 없으며 회사 포털 앱을 설치하고 로그인하여 장치를 등록해야합니다.

  > [!div class="button"]
  [< 뒤로](choose-how-to-enroll-devices3.md)



<!--HONumber=Aug16_HO2-->

