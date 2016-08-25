---
title: "利用規約を拒否した場合に Intune からデバイスの登録を解除する | Microsoft Intune"
description: "使用条件を拒否し、ポータル サイト アプリにサインインできない場合に、Android デバイスを Intune から登録解除する方法について説明します"
keywords: 
author: staciebarker
manager: angrobe
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 4278f000-0258-4de5-93a1-195b48e5061e
ms.reviewer: chrisbal
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 618e2abda642c3b9b2e813824dfd4235c9309faa
ms.openlocfilehash: 82cc94eb37b11251343706d60a45fb78458cab7e


---


# 利用規約を拒否した場合に Intune からデバイスの登録を解除する

Android デバイスの登録を解除する方法として最も良いのは、利用規約を受け入れ、ポータル サイト アプリにサインインしてから、[こちらの手順](unenroll-your-device-from-intune-android.md)を使用して登録を解除する方法です。 ただし、ポータル サイト アプリへのサインインの試行中に利用規約を拒否した場合は、次回以降、ポータル サイト アプリにサインインできなくなるため、デバイスの登録を解除するときは次の "回避策" の手順を実施する必要があります。

会社のポータル アプリをアンインストールする場合は、Intune からもデバイスの登録を解除するため、デバイスから会社のリソースにはアクセスできなくなります。  登録解除した場合の詳細については、「[Intune からデバイスの登録を解除するとどうなるか](what-happens-if-you-unenroll-your-device-from-intune-android.md)」を参照してください。

会社のポータル アプリをアンインストールするには、最初に **[Device administrators]** 設定に進み、**[会社のポータル]** をオフにします。 使用している Android デバイスによっては、手順が多少異なる場合があります。

Intune からデバイスの登録を解除し、会社のポータル アプリをアンインストールするには

1.  **[設定]** &gt; **[セキュリティ &amp; 画面のロック]** &gt;**[デバイス管理者]** の順に進みます。

    この手順は、デバイスの登録を解除したらすぐに実行します。

2.  **[会社のポータル]** の横のチェック ボックスをクリアして、オフにします。

    これで、会社のポータル アプリをアンインストールできます。

サポートが必要な場合は、 IT 管理者に問い合わせるか (連絡先情報については[ポータル サイト Web サイト](http://portal.manage.microsoft.com)をご確認ください)、または Microsoft Android チーム (wintunedroidfbk@microsoft.com) にご連絡ください。


### 関連項目
[Android デバイスを Intune で使用する](using-your-android-device-with-intune.md)



<!--HONumber=Jul16_HO4-->


