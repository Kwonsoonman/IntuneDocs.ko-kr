---
title: "Intune への移行 | Microsoft Intune"
description: 
keywords: 
author: jeffgilb
manager: jeffgilb
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 88936b8a-7453-4410-b6db-29f636ba3e72
ms.reviewer: jeffgilb
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 317b8cc277eb8dffc1cb29739f3f78cfa3241602
ms.openlocfilehash: c6bd34c910f56e7dfad142034ef6fd7a027cd2c4


---

# Intune への移行


以下の一般的な手順に従って、既存のエンタープライズ モビリティ管理ソリューションから Intune に移行できます。

![Intune の移行手順](./media/migrate-intune-steps.png)

## ユーザーに通知する

Intune のパイロット展開が要件を満たすことを確認した後、Intune へのデバイスの移行が近々あることをユーザーに通知します。 メール メッセージ、指示、[ポスター](https://gallery.technet.microsoft.com/Intune-End-User-Enrollment-3a0c9b0c?WT.mc_id=Blog_Intune_General_PCIT)などを使って予告し、会社のリソースおよびアプリケーションへの接続を維持するためにユーザーが実行する必要のある手順での登録の詳細を提供します。 サポート チームが移行プロセスについてユーザーを支援できる状態にしておきます。

## 既存のエンタープライズ モビリティ管理ソリューションを変更する

既存のエンタープライズ モビリティ管理ソリューションと Intune の間の条件付きアクセス ポリシーの処理方法によっては、既存の条件付きアクセス ポリシーを無効にする必要があります。 既存の条件付きアクセス ポリシーを無効にするか、または、Intune に移行する予定のユーザー/デバイスを含まないように既存の条件付きアクセス ポリシーのスコープを設定します。  Intune と既存のエンタープライズ モビリティ管理ソリューションの両方が、同じユーザー/デバイスに条件付きアクセス ポリシーを適用することがないようにしてください。

## Intune の条件付きアクセス ポリシーを有効にする (省略可能)

デバイス移行の猶予期間を設けることなく条件付きアクセス ポリシーをすぐに適用する場合は、以下の手順に従って Intune で条件付きアクセス ポリシーを有効にします。  この決定は、ユーザーおよびヘルプデスク チームとよく相談した上で行ってください。  デバイスが Intune に登録されておらず、Intune のポリシーに準拠していない場合、ユーザーは、Intune に登録してデバイスが Intune のポリシーに準拠するまで、会社のリソースにアクセスできません。

## 既存のエンタープライズ モビリティ管理ソリューションからデバイスを登録解除する

Intune に登録する前に、デバイスを既存のエンタープライズ モビリティ管理ソリューションから登録解除する必要があります。 ユーザー エクスペリエンスを最善にするには、ユーザー自身がデバイスを登録解除できるようにすることをお勧めします。  ソリューション プロバイダーからの登録解除ガイダンスに従って、プラットフォームからユーザーとデバイスを正しく削除し、エンド ユーザーの混乱を最小限にしてください。

## Intune にデバイスを登録する

移行対象のユーザーは、会社のリソース、電子メール、アプリケーションへのアクセスを回復するため、またはアクセスできなくなるのを防ぐため、Intune に直ちに登録する必要があります。 条件付きアクセスを構成してある場合、ユーザーが Intune 登録前に電子メールに接続しようとすると、アクセスはブロックされて、登録メールが送られます。 この電子メールでは、Intune にデバイスを登録する方法が説明されています。  ユーザーは、Intune ポータル サイト アプリで、または Windows 8.1 および Windows 10 Mobile オペレーティング システムでネイティブに、Intune に登録することもできます。 プラットフォームごとの登録手順の詳細については、「[Microsoft Intune の使用に関するエンドユーザーへの通知内容](what-to-tell-your-end-users-about-using-microsoft-intune.md)」を参照してください。

## Intune の条件付きアクセスを構成する (省略可能)

条件付きアクセス適用までの猶予期間を設けてある場合は、エンド ユーザーに通知してある猶予期間が終了したら、Intune で条件付きアクセス ポリシーを有効にして適用を開始します。 これにより、すべてのデバイスは直ちに Intune の条件付きアクセス ポリシーの要件を満たすことが必要になります。

## 残りのデバイスとユーザーを登録する

条件付きアクセスを有効にすると、すべてのユーザーは、会社のリソースにアクセスするために、Intune に登録して組織のコンプライアンス ポリシーを満たすことが必要になります。 ユーザーを一括ではなく段階的に登録して移行する場合は、すべてのデバイスとユーザーが登録され、Intune によって管理されるようになるまで、前記の手順を繰り返します。

## 以前のエンタープライズ モビリティ管理ソリューションの使用を終了する

すべてのユーザーとデバイスを Intune に移行し、Intune への移行が成功したことを検証した後は、以前のエンタープライズ モビリティ管理ソリューションの使用を終了し、サービスのサブスクリプションを解除できます。 ソリューション プロバイダーからの指示に従って、不要になったインフラストラクチャ要件を正しく削除し、すべてのサブスクリプション/ライセンスを取り消してください。

## 移行に関するその他の情報

Intune への移行に関してさらに支援が必要な場合は、 問題なく移行を行うための専門的な支援オプションが提供されています。

<!--- - [Microsoft Intune Onboarding](/em/solutions/fasttrack-center-benefit-for-enterprise-mobility-suite-ems)--->
- [マイクロソフト コンサルティング サービス](https://www.microsoft.com/en-us/microsoftservices/default.aspx)
- [Intune の技術的および非技術的サポート](/intune/troubleshoot/how-to-get-support-for-microsoft-intune)
- [Microsoft Intune TechNet フォーラム](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod)

## このガイドのダウンロード可能なコピーを入手する

このガイド全体のダウンロード可能なコピーを入手する場合は、[TechNet ギャラリー](https://gallery.technet.microsoft.com/Migrating-to-Intune-ea439387)にアクセスしてください。



<!--HONumber=Aug16_HO1-->


