---
title: "Intune に iOS デバイスを登録している最中にエラーが表示される | Microsoft Intune"
description: 
keywords: 
author: Staciebarker
manager: angrobe
ms.date: 06/15/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 92a8d06d-0ecb-4912-898b-993e8eaf4e58
ROBOTS: noindex,nofollow
ms.reviewer: esmich
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 618e2abda642c3b9b2e813824dfd4235c9309faa
ms.openlocfilehash: acb8d018b23753ad0a414d0222468caad3284325


---


# Intune に iOS デバイスを登録している最中にエラーが表示される

次の表は、Intune に iOS デバイスを登録している最中に表示される可能性があるエラーの一覧です。 このリンクは IT 管理者と共有してください。 連絡先情報については、[ポータル サイト Web サイト](http://portal.manage.microsoft.com)をご確認ください。

|エラー メッセージ|問題|IT 管理者への通知内容|
|-----------------|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
|NoEnrollmentPolicy|登録ポリシーなし|APNs 証明書などのすべての登録前提条件が構成済みであること、"プラットフォームとしての iOS" が有効であることを確認します。 手順については、「[iOS および Mac のデバイス管理をセットアップする](/intune/deploy-use/set-up-ios-and-mac-management-with-microsoft-intune)」を参照してください。|
|DeviceCapReached|登録済みのモバイル デバイス数が多すぎます。|別のモバイル デバイスを登録する前に、ユーザーは現在登録されているモバイル デバイスの 1 つをポータル サイトから削除する必要があります。 使用しているデバイスの種類ごとの手順 ([Android](unenroll-your-device-from-intune-android.md)、[iOS](unenroll-your-device-from-intune-ios.md)、[Windows](unenroll-your-device-from-intune-windows.md)) を参照してください。|
|APNSCertificateNotValid|モバイル デバイスと会社のネットワークとの通信を可能にする証明書に問題があります。<br /><br />IT 管理者に連絡し、モバイル デバイスの登録時に **APNSCertificateNotValid** というメッセージを受信したことを知らせて、IT 管理者にこの表の解決方法を参照するよう伝えてください。|Apple Push Notification Service (APNS) には、登録済みの iOS デバイスに接続するチャネルが用意されています。 APNS 証明書を取得する手順が実行されていない場合、または APNS 証明書が期限切れの場合、登録は失敗し、このメッセージが表示されます。<br /><br />ユーザー設定の詳細については、「[Active Directory を同期化して Intune にユーザーを追加する](/Intune/Get-Started/start-with-a-paid-subscription-to-microsoft-intune-step-3)」と[ユーザーとデバイスの整理](/Intune/Get-Started/start-with-a-paid-subscription-to-microsoft-intune-step-5)に関するページを確認してください。|
|AccountNotOnboarded|モバイル デバイスと会社のネットワークとの通信を可能にする証明書に問題があります。<br /><br />IT 管理者に連絡し、モバイル デバイスの登録時に **APNSNotOnboarded** というメッセージを受信したことを知らせて、IT 管理者にこの表の解決方法を参照するよう伝えてください。|Apple Push Notification Service (APNS) には、登録済みの iOS デバイスに接続するチャネルが用意されています。 APNS 証明書を取得する手順が実行されていない場合、または APNS 証明書が期限切れの場合、登録は失敗し、このメッセージが表示されます。<br /><br />詳細については、「[Microsoft Intune を使用して iOS および Mac の管理をセットアップする](/Intune/Deploy-use/set-up-ios-and-mac-management-with-microsoft-intune)」を確認してください。|
|DeviceTypeNotSupported|iOS 以外のデバイスを使用して登録を試みた可能性があります。 登録しようとしているモバイル デバイスの種類はサポートされていません。<br /><br />デバイスが iOS バージョン 7.1 以降を実行していることを確認します。<br /><br />IT 管理者に連絡し、モバイル デバイスの登録時に **DeviceTypeNotSupported** というメッセージを受信したことを知らせて、IT 管理者にこの表の解決方法を参照するよう伝えてください。|ユーザーのデバイスが iOS バージョン 7.1 以降を実行していることを確認します。|
|UserLicenseTypeInvalid|ユーザー アカウントがまだ必要なユーザー グループのメンバーではないため、モバイル デバイスを登録できません。<br /><br />IT 管理者に連絡し、モバイル デバイスの登録時に **UserLicenseTypeInvalid** というメッセージを受信したことを知らせて、IT 管理者にこの表の解決方法を参照するよう伝えてください。|ユーザーが自分のデバイスを登録できるようにするには、ユーザーは適切なユーザー グループのメンバーである必要があります。 このメッセージは、指定されたモバイル デバイス管理機関に必要なライセンスの種類をユーザーが持っていないことを示します。 たとえば、モバイル デバイス管理機関として Intune が指定され、ユーザーが System Center 2012 R2 Configuration Manager ライセンスを使用している場合に、このエラーが表示されます。<br /><br />詳細については、以下を確認してください。<br /><br />「[Microsoft Intune を使用して iOS および Mac の管理をセットアップする](/Intune/Deploy-use/set-up-ios-and-mac-management-with-microsoft-intune)」のほか、「[Active Directory を同期化して Intune にユーザーを追加する](/Intune/Get-Started/start-with-a-paid-subscription-to-microsoft-intune-step-3)」と[ユーザーとデバイスの整理](/Intune/Get-Started/start-with-a-paid-subscription-to-microsoft-intune-step-5)に関するページのユーザー設定についての情報を確認してください。|
|MdmAuthorityNotDefined|IT 管理者は社内のモバイル デバイスを管理する方法を構成する必要があります。<br /><br />IT 管理者に連絡し、モバイル デバイスの登録時に **MdmAuthorityNotDefined** というメッセージを受信したことを知らせて、IT 管理者にこの表の解決方法を参照するよう伝えてください。|Intune でモバイル デバイス管理機関が指定されていません。<br /><br />[Microsoft Intune の 30 日間の試用版の使用](/Intune/Understand-explore/get-started-with-a-30-day-trial-of-microsoft-intune)に関するページの「手順 6: モバイル デバイスを登録してアプリをインストールする」セクションの項目 1 を確認してください。|

### 関連項目
[Using your iOS or Mac OS X device with Intune](using-your-ios-or-mac-os-x-device-with-intune.md)



<!--HONumber=Jul16_HO4-->


