---
title: "Windows용 회사 포털 앱 설치 | Microsoft 문서"
description: 
keywords: 
author: barlanmsft
ms.author: barlan
manager: angrobe
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: d65e3452-5bbf-4d26-a06e-401ddcc47f39
searchScope:
- User help
ROBOTS: 
ms.reviewer: priyar
ms.suite: ems
ms.custom: intune-enduser
ms.translationtype: Human Translation
ms.sourcegitcommit: 5ed0e84c16ea540c08e97cb55ef8a09cbc7339f6
ms.openlocfilehash: 052de47e19f4e171428ee22b4701ed516461231f
ms.contentlocale: ko-kr
ms.lasthandoff: 05/25/2017


---


# <a name="what-happens-if-you-install-the-company-portal-app-and-enroll-your-windows-device-in-intune"></a>Intune에서 회사 포털 앱을 설치하고 Windows 장치를 등록하면 어떻게 되나요?

회사 포털 앱을 설치한 후 사용하여 Windows 또는 Windows Phone 장치를 등록할 때 IT 관리자가 회사 또는 학교 데이터를 안전하게 보호하기 위해 장치를 관리하도록 할 수 있습니다. 이 항목에서는 Windows 10 이전 장치에서 발생하는 결과를 설명합니다. Windows 10 장치의 경우 [관련 항목](what-happens-if-you-install-the-company-portal-app-and-enroll-your-device-in-intune-windows10.md)을 참조하세요.

## <a name="what-happens-to-all-windows-devices-after-enrollment"></a>등록 후 모든 Windows 장치에서 발생하는 결과
Intune에서 Windows 또는 Windows Phone 장치를 등록하면 다음을 수행할 수 있습니다.

-   회사 네트워크, 메일 및 작업 파일 액세스

-   회사 포털 웹 사이트에서 회사 앱을 다운로드합니다. __참고__: Windows 7 및 Windows Vista의 경우 회사 포털 웹 사이트에서만 회사 앱을 다운로드할 수 있습니다.

-   회사 또는 학교 메일 계정을 자동으로 설정

-   분실하거나 도난당한 경우 전화를 공장 설정으로 다시 설정

장치를 등록할 경우 다음과 같은 작업을 수행할 수 있는 권한을 IT 관리자에게 부여합니다.

-   사용자 장치를 장치 제조업체의 기본 설정으로 복원합니다. 장치를 분실하거나 도난당한 경우 유용한 조치입니다.

-   회사 관련 파일 및 비즈니스 앱만 제거합니다. *개인 데이터 및 설정은 제거되지 않습니다.*

-   IT 관리자는 사용자가 개인적으로 설치한 소프트웨어를 비롯하여 장치에 설치되어 있는 소프트웨어를 볼 수 있습니다.

-   장치에서 회사 데이터를 보호하도록 도와주려면 장치 암호나 PIN이 있어야 하는 등과 같은 요구 사항을 설정합니다. IT 관리자는 잘못된 암호를 입력할 수 있는 횟수를 제한할 수도 있고 너무 많이 시도하는 경우 장치를 잠글 수 있습니다.

-   장치를 분실하거나 도난당하는 경우 회사 데이터를 보호하기 위해 장치에서 데이터를 암호화해야 합니다.

-   사용 약관에 조건에 동의해야 합니다.

-   회사 관련 데이터의 사진을 찍을 수 없게 합니다.

## <a name="what-happens-to-all-windows-pcs-after-enrollment"></a>등록 후 모든 Windows PC에서 발생하는 결과

-  IT 관리자가 컴퓨터를 관리할 수 있도록 하고, 사용자가 앱 및 지원 정보 같은 회사 리소스에 액세스할 수 있도록, 사용자의 컴퓨터에 소프트웨어가 설치됩니다. IT 관리자가 이 소프트웨어를 자동으로 업데이트할 수 있습니다.

-  Intune Endpoint Protection이 사용자의 컴퓨터에 설치될 수 있습니다. 이것은 바이러스 및 맬웨어를 검사하는 소프트웨어입니다.

-  IT 관리자가 사용자 컴퓨터의 하드 드라이브에서 데이터를 수집하거나 삭제할 수 있습니다.

-  IT 관리자가 사용자 컴퓨터에 앱 및 업데이트를 설치할 수 있습니다.

## <a name="what-happens-every-eight-hours-after-device-enrollment"></a>장치 등록 후 8시간마다 발생되는 작업

등록된 장치에서 8시간마다 다음 작업이 수행됩니다.

-   IT 관리자가 사용하도록 설정한 임의의 정책 또는 앱 업데이트를 다운로드합니다.

-   하드웨어 인벤토리 업데이트를 보냅니다.

-   임의의 회사 앱 인벤토리 업데이트를 보냅니다.

의문 사항이 있으면 IT 관리자에게 문의하세요. 연락처 정보는 [회사 포털 웹 사이트](https://portal.manage.microsoft.com)를 참조하세요.

