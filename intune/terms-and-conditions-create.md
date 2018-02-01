---
title: "Microsoft Intune에서 사용 약관 설정"
titlesuffix: Azure portal
description: "Intune용 회사 포털에서 사용자에게 표시되는 사용 약관을 설정합니다. "
keywords: 
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/31/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 4a3a11a8-9c0c-4334-8c6b-6fea4d0a2efb
ms.reviewer: amyro
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: df7f91cbdcbafb785d0c4cfb1612d6c2f9e5581e
ms.sourcegitcommit: a41ad9988a8c14e6b15123a9ea9bc29ac437a4ce
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="ensure-users-accept-company-terms-for-access"></a>사용자가 액세스를 위한 회사 약관에 동의하는지 확인

[!INCLUDE[azure_portal](./includes/azure_portal.md)]

Intune 관리자는 사용자가 회사의 사용 약관에 동의해야만 회사 포털을 통해 장치를 등록하고 회사 앱 및 전자 메일 같은 리소스에 액세스하도록 요구할 수 있습니다. 사용 약관의 구성은 선택 사항입니다.

다양한 언어를 지원하는 경우와 같이 여러 약관 집합을 만들어 다양한 그룹에 할당할 수 있습니다.

## <a name="create-terms-and-conditions"></a>사용 약관 만들기
사용 약관을 만들려면 다음 단계를 완료합니다. 표시 이름 및 설명은 관리용이며 약관 속성은 회사 포털의 사용자에게 표시됩니다.

1. Azure Portal에서 **장치 등록**을 선택한 다음 **사용 약관**을 선택합니다.
2. **만들기**를 선택합니다.
![사용 약관에 사용되는 [만들기] 단추가 표시된 Azure Portal 스크린샷](media/terms-create-terms.png)
3. 확장된 블레이드에서 다음 정보를 지정합니다.

   - **표시 이름**: Azure Portal의 약관 이름입니다. 사용자에게는 이 이름이 표시되지 않습니다.

   - **설명**: Azure Portal에서 이 약관 집합을 식별하는 데 도움이 되는 선택적 세부 정보입니다.

4. 사용 약관 정의 옆의 화살표를 선택하여 사용 약관 블레이드를 열고 다음 정보를 입력합니다.

   ![최종 사용자 약관 수락 화면 스크린샷과 약관 요약](./media/terms-summary-create.png)

   - **제목**: 위의 회사 포털에서 사용자에게 표시되는 약관의 이름은 **요약**입니다.
   - **사용 약관 요약**: 사용자가 약관에 동의하는 경우 의미를 설명하는 텍스트입니다. 예를 들어 "장치를 등록하면 Contoso에서 설정한 사용 약관에 동의하게 됩니다. 계속하기 전에 사용 약관을 주의해서 읽어보세요."가 있습니다.
   - **사용 약관**: 사용자에게 표시되며 사용자가 동의하거나 거부해야 하는 사용 약관입니다.

5. **확인**을 선택하고 **만들기**를 선택합니다.

## <a name="see-how-terms-are-displayed-to-your-users"></a>약관이 사용자에게 표시되는 방식 확인
다음 예제에는 관리 콘솔과 회사 포털에 **제목** 및 **사용 약관 요약**이 표시되어 있습니다.

![관리 콘솔과 회사 포털에 표시된 제목 및 사용 약관 요약의 스크린샷](./media/terms-summary-terms.png)

다음 예제에는 관리 콘솔과 회사 포털에 사용 약관이 표시되어 있습니다.

![관리 콘솔과 회사 포털에 표시된 사용 약관의 스크린샷](./media/terms-properties-terms.png)

## <a name="assign-terms-and-conditions"></a>사용 약관 할당

회사 포털을 사용하기 전에 사용 약관에 동의해야 하는 사용자의 그룹에 사용 약관을 할당할 수 있습니다.

1. Azure Portal에서 **장치 등록**을 선택한 다음 **사용 약관**을 선택합니다.
2. 사용 약관 목록에서 할당할 약관을 선택하고 **할당 그룹**을 선택합니다.
![사용 약관 할당에 사용되는 [그룹 선택] 단추와 [선택] 단추를 보여주는 Azure Portal의 [그룹 할당] 블레이드가 표시된 스크린샷](media/terms-assign-groups.png)
3. **그룹 선택** 블레이드에서 **그룹 선택** 단추를 클릭하고, 약관을 할당할 그룹을 선택하고, **선택**을 클릭합니다. 사용 약관에는 동적 그룹을 할당할 수 없습니다.
4. **할당 그룹** 블레이드에서 **저장**을 클릭합니다.  이제 선택한 그룹의 사용자에게 사용 약관이 할당됩니다. 다음번에 사용자가 회사 포털에 액세스할 때 약관에 동의하는지 묻는 메시지가 표시됩니다. 사용 약관은 한 번만 동의하면 됩니다. 즉, 여러 장치를 소유한 사용자가 각 장치에서 사용 약관에 동의할 필요가 없습니다.


## <a name="monitor-terms-and-conditions"></a>사용 약관 모니터링

1. Azure Portal에서 **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다. Intune 블레이드에서 **장치 등록**을 선택한 다음 **사용 약관**을 선택합니다.
2. 사용 약관 목록에서 동의를 확인할 약관을 선택하고 **Acceptance Statuses**(승인 상태)를 선택합니다.

## <a name="work-with-multiple-versions-of-terms-and-conditions"></a>여러 버전의 사용 약관 사용
사용 약관을 편집하고 버전을 관리할 수 있습니다. 사용 약관을 크게 변경할 때마다 버전 번호를 높이고 동의를 요구하는 것이 좋습니다. 오타를 수정하거나 서식을 변경하는 등의 경우에는 현재 버전 번호를 유지합니다.

1. Azure Portal에서 **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다.

2. Intune 블레이드에서 **장치 등록**을 선택하고, **사용 약관**을 선택하고, 수정할 사용 약관을 선택한 다음 **속성**을 선택합니다.

4. **속성** 블레이드에서 **사용 약관**을 선택하고 필요에 따라 **제목**, **사용 약관 요약**, **사용 약관**을 수정합니다. 내용을 변경하여 사용자가 새로운 사용 약관에 다시 동의해야 하는 경우 **사용자가 다시 수락하고 버전 번호를 증가시켜야 합니다.**를 클릭합니다.

4.  **확인**을 선택하고 **저장**을 선택합니다.

사용자는 업데이트된 사용 약관에 한 번만 동의하면 됩니다. 즉, 여러 장치를 소유한 사용자가 각 장치에서 약관에 동의할 필요가 없습니다.
