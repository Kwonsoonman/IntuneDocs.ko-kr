---
title: "Microsoft Intune에서 사용 약관 설정"
titleSuffix: Intune Azure preview
description: "Intune용 회사 포털에서 사용자에게 표시되는 사용 약관을 설정합니다. "
keywords: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.date: 05/05/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 4a3a11a8-9c0c-4334-8c6b-6fea4d0a2efb
ms.reviewer: amyro
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: d53e91e24988d1bc71ff8df425f0d82e0fc43b58
ms.contentlocale: ko-kr
ms.lasthandoff: 05/23/2017

---

# <a name="ensure-users-accept-company-terms-for-access"></a>사용자가 액세스를 위한 회사 약관에 동의하는지 확인

[!INCLUDE[azure_preview](./includes/azure_preview.md)]

Intune 관리자는 사용자가 회사의 사용 약관에 동의해야만 회사 포털을 통해 장치를 등록하고 앱 및 메일 같은 회사 리소스에 액세스할 수 있도록 선택할 수 있습니다. 사용 약관의 구성은 선택 사항입니다.

다양한 언어를 지원하는 경우와 같이 여러 약관 집합을 만들어 다양한 그룹에 할당할 수 있습니다.

## <a name="create-terms-and-conditions"></a>사용 약관 만들기
사용 약관을 만들려면 다음 단계를 완료합니다. 표시 이름 및 설명은 관리용이며 약관 속성은 회사 포털의 사용자에게 표시됩니다.

1. Azure Portal에서 **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다.

2. Intune 블레이드에서 **장치 등록**을 선택한 다음 **사용 약관**을 선택합니다.

3. **만들기**를 선택합니다.
![사용 약관에 사용되는 만들기 단추가 표시된 Intune 포털 스크린샷](media/terms-create-terms.png)

4. 확장된 블레이드에서 다음 정보를 지정합니다.

   - **표시 이름**: Intune 포털의 약관 이름입니다. 사용자에게는 이 이름이 표시되지 않습니다.

   - **설명**: Intune 포털에서 이 용어 집합을 식별하는 데 도움이 되는 선택적 세부 정보입니다.

5. 사용 약관 정의 옆의 화살표를 선택하여 사용 약관 블레이드를 열고 다음 정보를 입력합니다.

   ![최종 사용자 약관 수락 화면 스크린샷과 약관 요약](./media/terms-summary-create.png)

   - **제목**: 회사 포털에 표시되는 제목입니다.

   - **사용 약관 요약**: 사용자가 약관에 동의하는 경우 의미를 설명하는 텍스트입니다. 예를 들어 "장치를 등록하면 Contoso에서 설정한 사용 약관에 동의하게 됩니다. 계속하기 전에 사용 약관을 주의해서 읽어보세요."가 있습니다.

   - **사용 약관**: 사용자에게 표시되며 사용자가 동의하거나 거부해야 하는 사용 약관입니다.

6. **확인**을 선택하고 **만들기**를 선택합니다.

## <a name="assign-terms-and-conditions"></a>사용 약관 할당

회사 포털을 사용하기 전에 사용 약관에 동의해야 하는 사용자의 그룹에 사용 약관을 할당할 수 있습니다.

1. Azure Portal에서 **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다.

2. Intune 블레이드에서 **장치 등록**을 선택한 다음 **사용 약관**을 선택합니다.

3. 사용 약관 목록에서 할당할 약관을 선택하고 **할당 그룹**을 선택합니다.
![사용 약관 할당에 사용되는 그룹 선택 단추와 선택 단추를 보여주는 Intune 포털 그룹 할당 블레이드가 표시된 스크린샷](media/terms-assign-groups.png)

4. **그룹 선택** 블레이드에서 **그룹 선택** 단추를 클릭하고, 약관을 할당할 그룹을 선택하고, **선택**을 클릭합니다.

5. **할당 그룹** 블레이드에서 **저장**을 클릭합니다.  이제 선택한 그룹의 사용자에게 사용 약관이 할당됩니다. 다음번에 사용자가 회사 포털에 액세스할 때 약관에 동의하는지 묻는 메시지가 표시됩니다.

   ![최종 사용자 약관 수락 화면 스크린샷과 약관 요약](./media/terms-summary-accept.png)

## <a name="monitor-a-terms-and-conditions"></a>사용 약관 모니터링

1. Azure Portal에서 **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다. Intune 블레이드에서 **장치 등록**을 선택한 다음 **사용 약관**을 선택합니다.
2. 사용 약관 목록에서 동의를 확인할 약관을 선택하고 **Acceptance Statuses**(승인 상태)를 선택합니다.

## <a name="work-with-multiple-versions-of-terms-and-conditions"></a>여러 버전의 사용 약관 사용
사용 약관을 편집하고 버전을 관리할 수 있습니다. 사용 약관을 크게 변경할 때마다 버전 번호를 높이고 동의를 요구하는 것이 좋습니다. 오타를 수정하거나 서식을 변경하는 등의 경우에는 현재 버전 번호를 유지합니다.

1. Azure Portal에서 **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다.

2. Intune 블레이드에서 **장치 등록**을 선택하고, **사용 약관**을 선택하고, 수정할 사용 약관을 선택한 다음 **속성**을 선택합니다.

4. **속성** 블레이드에서 **사용 약관**을 선택하고 필요에 따라 **제목**, **사용 약관 요약**, **사용 약관**을 수정합니다. 내용을 변경하여 사용자가 약관에 다시 동의해야 하는 경우 **Require users to re-accept, and increment the version number to**(사용자가 다시 동의하고 버전 번호를 증가시켜야 함)를 클릭합니다.

4.  **확인**을 선택하고 **저장**을 선택합니다.
