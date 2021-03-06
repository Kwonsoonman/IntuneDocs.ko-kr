---
title: Microsoft Intune-Azure를 사용한 Windows 10 장치 다시 설정 | Microsoft Docs
description: Microsoft Intune을 사용하여 Windows 10 PC에서 앱을 제거하기 위해 새로 시작을 사용합니다.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/09/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 5aa5cfa3-c483-4099-b40f-578ff8dca425
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: cd2320e4c3935c4865d785bbb2461bba20afffdb
ms.sourcegitcommit: 51b763e131917fccd255c346286fa515fcee33f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52188741"
---
# <a name="use-fresh-start-to-reset-windows-10-devices-with-intune"></a>Intune을 통해 새로 시작 기능을 사용하여 Windows 10 장치 다시 설정


[!INCLUDE [azure_portal](./includes/azure_portal.md)]

**새로 시작** 장치 작업은 Windows 10 버전 1703 이상을 실행하는 PC에 설치된 모든 앱을 제거합니다. 새로 시작을 통해 일반적으로 새로운 PC에 설치되는 사전 설치된(OEM) 앱을 제거할 수 있습니다.  

1. [Azure Portal](https://portal.azure.com)에 로그인하고 **Microsoft Intune** > **장치** > **모든 장치**로 이동합니다.
2. 관리하는 장치 목록에서 Windows 10 데스크톱 장치를 선택합니다.
3. **새로 시작**을 클릭합니다. 
4. **이 장치에 사용자 데이터 유지**를 선택합니다. 이렇게 하면
   * 장치의 Azure Active Directory를 조인된 상태로 유지할 수 있습니다.
    * 모바일 장치 관리에 장치가 등록된 상태로 유지할 수 있습니다. 
    * 장치 사용자의 홈 폴더에 있는 콘텐츠를 유지하고 앱과 설정을 제거할 수 있습니다.  
  > [!IMPORTANT]
 > 사용자 데이터를 유지하지 않으면 장치가 초기 상태로 복원되고 Azure Active Directory 및 모바일 장치 관리에서 등록이 취소됩니다. 
 
5. **확인**을 클릭합니다.   
6. 이 작업의 상태를 보려면 **장치**로 돌아가서 **장치 작업**을 클릭합니다.  
