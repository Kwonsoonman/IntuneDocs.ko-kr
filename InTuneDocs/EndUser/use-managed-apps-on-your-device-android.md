---
title: "Android デバイスで管理対象アプリを使用する | Microsoft Intune"
description: 
keywords: 
author: staciebarker
manager: arob98
ms.date: 05/31/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: ed10a62c-b026-4ad3-ac41-641933522df2
ROBOTS: noindex,nofollow
ms.reviewer: maxles
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 376e6c1ae229187ab8ec73390f091f1d534365dd
ms.openlocfilehash: 84dc834c28ab75c4091d7665e8492ec40ede95f9


---


# Android デバイスで管理対象アプリを使用する

管理対象アプリとは、そのアプリでアクセス可能な会社のデータを保護できるよう IT 管理者が構成可能なアプリです。 管理対象アプリ内の会社のデータに Android デバイスでアクセスする場合、アプリの動作が予期したものとは少し異なる場合があります。 たとえば、保護された会社のデータをコピーして貼り付けできない、またはそのデータを特定の場所に保存できない場合があります。

また、異なる管理対象アプリがデバイス上で連携して動作し、会社のデータを保護しながら、日常のタスクを実行することもできます。 たとえば、1 つの管理対象アプリで会社のファイルを開き、別の管理対象アプリでそのファイルを表示する必要がある場合、ファイルを表示できるようにする管理対象アプリが自動的に開きます。 必要なアプリが使用できない場合、管理されているドキュメント内からドキュメントを開くまたは Web リンクにアクセスするなどの特定の操作が行えない可能性があります。

管理対象アプリで会社のデータにアクセスすると、開こうとしているアプリが管理されていることを通知する以下のようなメッセージが表示されます。

![open-managed-apps-message](./media/managed-apps-message.png)

## 管理対象アプリを取得する方法
管理対象アプリはいくつかの方法で取得できます。

-   デバイスが Microsoft Intune に登録されるときに、会社のポータル アプリまたは会社のポータル Web サイトからアプリをインストールするか、または IT 管理者がアプリをデバイスにインストールする場合があります。 登録については、「[Intune にデバイスを登録する](enroll-your-device-in-Intune-android.md)」をご覧ください。

-   Play ストアからアプリをインストールし、Intune で管理されている会社のユーザー アカウントでサインインします。

## IT 管理者がアプリで管理できるもの
以下は、IT 管理者がアプリで管理でき、デバイス上での会社データとのやり取りに影響するオプションの例です。

-   特定の web サイトへのアクセス

-   アプリケーション間のデータ転送

-   ファイルの保存

-   コピーと貼り付けの操作

-   暗証番号 (pin) のアクセスの要件

-   会社の資格情報を使用したログイン

-   クラウドへのバックアップ機能

-   スクリーン ショットを撮る機能

-   データの暗号化の要件

IT 部門が管理する可能性のある一般的なアプリを以下にいくつか示します。

-   Intune Managed Browser

-   Intune Image Viewer

-   Intune PDF Viewer

-   Intune AV Player

-   Microsoft Word、Excel、PowerPoint

デバイスの管理対象アプリの詳細については、IT 管理者にお問い合わせください。 連絡先情報については、[ポータル サイト Web サイト](http://portal.manage.microsoft.com)をご確認ください。


### 関連項目
[Android デバイスを Intune で使用する](using-your-android-device-with-intune.md)


<!--HONumber=Jul16_HO3-->


