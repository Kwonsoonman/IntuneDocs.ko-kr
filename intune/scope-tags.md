---
title: Microsoft Intune에서 범위 태그를 사용하여 정책 필터링 - Azure | Microsoft Docs
description: 범위 태그를 사용하여 특정 역할에 대한 구성 프로필을 필터링합니다.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/29/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 080205e601b857d4765eb6b97eeeeeb8f4e6fc1b
ms.sourcegitcommit: 51b763e131917fccd255c346286fa515fcee33f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52187160"
---
# <a name="use-scope-tags-to-filter-policies"></a>범위 태그를 사용하여 정책 필터링

범위 태그를 사용하여 사용자가 만드는 사용자 지정 태그를 사용하여 정책을 필터링할 수 있습니다.

예를 들어 "엔지니어링 부서"라는 범위 태그를 만들고 엔지니어링 부서와 관련된 구성 프로필에 할당합니다. "엔지니어링 관리자" 역할에 동일한 태그를 할당합니다. "엔지니어링 부서" 태그가 있는 정책만 표시됩니다.

## <a name="to-create-a-scope-tag"></a>범위 태그를 만들려면

**역할** > **범위(태그)** > **만들기**를 선택합니다.

## <a name="to-add-a-scope-tag-to-a-configuration-profile"></a>범위 태그를 구성 프로필에 추가하려면

**장치 구성** > **프로필** > 프로필 선택 > **속성** > **범위(태그)** 를 선택합니다.

## <a name="to-assign-a-scope-tag-to-a-role"></a>범위 태그를 역할에 할당하려면

**역할** > **모든 역할** > **정책 및 프로필 관리자** > **할당** > **범위(태그)** 를 선택합니다.

## <a name="next-steps"></a>다음 단계

[역할](role-based-access-control.md) 및 [프로필](device-profile-assign.md)을 관리합니다.

