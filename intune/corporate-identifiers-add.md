---
title: "Intune에 회사 식별자 추가"
titlesuffix: Azure portal
description: "Microsoft Intune에 회사 식별자(등록 방법, IMEI 및 일련 번호)를 추가하는 방법을 알아봅니다. \""
keywords: 
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.date: 08/23/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 566ed16d-8030-42ee-bac9-5f8252a83012
ms.reviewer: dagerrit
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 58dac14dcc38329cfa0a98746e667bf6e5438170
ms.sourcegitcommit: b8987b8dfb009ea55678d7f640ac5f18a6ab167e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2017
---
# <a name="identify-devices-as-corporate-owned"></a>회사 소유의 장치 식별

[!INCLUDE[azure_portal](./includes/azure_portal.md)]

Intune 관리자로서 사용자는 장치를 회사 소유로 식별하여 관리 및 식별을 구체화할 수 있습니다. Intune은 추가 관리 작업을 수행하고 회사 소유 장치에서 전체 전화 번호와 앱의 인벤토리와 같은 추가 정보를 수집할 수 있습니다. 회사 소유가 아닌 장치에서 등록하지 못하도록 차단하는 장치 제한을 설정할 수도 있습니다.

다음 조건 중 충족되는 것이 있으면 장치가 회사 소유로 식별됩니다.

- [장치 등록 관리자](device-enrollment-manager-enroll.md) 계정을 사용하여 등록됨(모든 플랫폼)
- Apple [장비 등록 프로그램](device-enrollment-program-enroll-ios.md), [Apple School Manager](apple-school-manager-set-up-ios.md) 또는 [Apple Configurator](apple-configurator-enroll-ios.md)를 사용하여 등록됨(iOS만 해당)
- IMEI(International Mobile Equipment Identifier) 번호(IMEI 번호가 있는 모든 플랫폼) 또는 일련 번호(iOS 및 Android)를 사용하여 [등록 전에 회사 소유로 식별됨](#identify-corporate-owned-devices-with-imei-or-serial-number)
- Azure Active Directory 또는 Enterprise Mobility + Security에 Windows 10 Enterprise 장치로 등록됨
- 장치 속성에 [장치 소유권이 회사](#change-device-ownership)인 것으로 나열됨

## <a name="identify-corporate-owned-devices-with-imei-or-serial-number"></a>IMEI 또는 일련 번호로 회사 소유 장치 식별

Intune 관리자는 IMEI 번호 또는 일련 번호가 나열된 쉼표로 구분된 값(.csv) 파일을 만들고 가져올 수 있습니다. Intune에서는 장치 등록 중에 이러한 식별자를 사용하여 장치 소유권을 회사로 지정합니다. 모든 지원되는 플랫폼에 대해서 IMEI 번호를 선언할 수 있습니다. iOS 및 Android 장치에 대한 일련 번호만 선언할 수 있습니다. 각 IMEI 또는 일련 번호에는 관리 용도로 목록에 지정된 세부 정보를 포함할 수 있습니다.

<!-- When you upload serial numbers for company-owned iOS devices, they must be paired with a corporate enrollment profile. Devices must then be enrolled using either Apple’s device enrollment program (DEP) or Apple Configurator to have them appear as company-owned. -->

[Apple 장치 일련 번호를 확인하는 방법을 알아봅니다](https://support.apple.com/HT204308).<br>
[Android 장치 일련 번호를 확인하는 방법을 알아봅니다](https://support.google.com/store/answer/3333000).

## <a name="add-corporate-identifiers"></a>회사 식별자 추가
목록을 만들려면 헤더 없이 2열로 구성된 쉼표로 구분된 값(.csv) 목록을 만듭니다. 왼쪽 열에 IMEI 또는 일련 번호를 추가하고, 오른쪽 열에 세부 정보를 추가합니다. ID, IMEI 또는 일련 번호 중 한 가지 유형만 단일 .csv 파일로 가져올 수 있습니다. 세부 정보는 128자로 제한되며 관리 용도로만 사용됩니다. 세부 정보는 장치에 표시되지 않습니다. 현재는 .csv 파일당 500개의 행으로 제한됩니다.

**일련 번호가 포함된 .csv 파일 업로드** – 머리글 없이 두 열로 이루어진 쉼표로 구분된 값(.csv) 목록을 만들고 목록을 .csv 파일당 장치 5,000대 또는 용량 5MB로 제한합니다.

|||
|-|-|
|&lt;ID #1&gt;|&lt;장치 #1 세부 정보&gt;|
|&lt;ID #2&gt;|&lt;장치 #2 세부 정보&gt;|

이.csv 파일을 텍스트 편집기에서 보면 다음과 같이 표시됩니다.

```
01234567890123,device details
02234567890123,device details
```

> [!IMPORTANT]
> 일부 Android 장치는 IMEI 번호가 여러 개 있습니다. Intune은 등록된 장치당 하나의 IMEI 번호만 읽습니다. IMEI 번호를 가져오지만 Intune에서 인벤토리에 배정한 IMEI가 아닌 경우 장치는 회사 소유 장치가 아니라 개인 장치로 분류됩니다. 한 장치에 대해 여러 IMEI 번호를 가져오면 인벤토리에 배정되지 않은 번호는 등록 상태가 **알 수 없음**으로 표시됩니다.<br>
>참고: Android 일련 번호는 고유함이나 존재가 보장되지 않습니다. 일련 번호가 신뢰할 수 있는 장치 ID인지는 해당 장치 공급자에게 확인하세요.
>장치에서 Intune으로 보고된 일련 번호는 장치의 Android 설정/정보 메뉴에 표시되는 ID와 일치하지 않을 수 있습니다. 장치 제조업체에 보고된 일련 번호 형식을 확인하세요.

### <a name="add-a-csv-list-of-corporate-identifiers"></a>회사 식별자의 .csv 목록 추가

1. Azure Portal의 Intune에서 **장치 등록** > **회사 장치 식별자**를 선택한 다음 **추가**를 클릭합니다.

 ![추가 단추가 강조 표시된 회사 장치 식별자 작업 영역 스크린샷](./media/add-corp-id.png)

2. **식별자 추가** 블레이드에서 식별자 형식 **IMEI** 또는 **일련**을 지정합니다. 이전에 가져온 숫자가 **기존 식별자 세부 정보를 덮어쓸지**를 지정할 수 있습니다.

3. 폴더 아이콘을 클릭하고 가져오려는 목록의 경로를 지정하세요. IMEI .csv 파일로 이동하여 **추가**를 선택합니다. **새로 고침**을 클릭하면 새로운 장치 식별자를 확인할 수 있습니다.

가져온 장치가 반드시 등록되지는 않습니다. 장치는 **등록됨** 또는 **연결되지 않음** 중 하나의 상태일 수 있습니다. **연결되지 않음**은 장치가 Intune 서비스와 통신된 적이 없음을 의미합니다.

### <a name="delete-corporate-identifiers"></a>회사 식별자 삭제

1. Azure Portal의 Intune에서 **장치 등록** > **회사 장치 식별자**를 선택합니다.
2. 삭제할 장치 식별자를 선택하고 **삭제**를 선택합니다.
3. 삭제를 확인 합니다.

등록된 장치의 회사 식별자를 삭제해도 장치의 소유권이 변경되지는 않습니다. 장치의 소유권을 변경하려면 **장치** > **모든 장치**로 이동하고 장치를 선택한 다음 **속성**을 선택하고 **장치 소유권**을 변경합니다.

### <a name="imei-specifications"></a>IMEI 사양
International Mobile Equipment Identifiers에 대한 자세한 사양은 [3GGPP TS 23.003](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=729)을 참조하세요.

## <a name="change-device-ownership"></a>장치 소유권 변경

장치 속성은 Intune의 각 장치 레코드에 대한 **소유권**을 표시합니다. 관리자는 장치를 **개인** 또는 **회사**로 지정할 수 있습니다.

**장치 소유권을 변경하려면 다음과 같이 합니다.**
1. Azure Portal의 Intune에서 **장치** > **모든 장치**로 이동하고 장치를 선택합니다.
3. **속성**을 선택합니다.
4. **장치 소유권**을 **개인** 또는 **회사**로 지정합니다.

  ![장치 범주 및 장치 소유권 옵션을 보여 주는 장치 속성의 스크린 샷입니다.](./media/device-properties.png)
