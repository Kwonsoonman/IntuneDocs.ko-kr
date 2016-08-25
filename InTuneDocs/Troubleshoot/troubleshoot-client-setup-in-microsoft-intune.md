---
title: "クライアント セットアップのトラブルシューティング | Microsoft Intune"
description: "一般的なクライアント セットアップに関する問題のトラブルシューティングを行います。"
keywords: 
author: Nbigman
manager: angrobe
ms.date: 08/02/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: e46d292b-1d16-46db-a87f-d53eefa4d22a
ms.reviewer: tscott
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: eeb0aeac2f94dfde50d9398b09c6b21c7ae40624
ms.openlocfilehash: 3f7e5752780d7159ce3081ec7a194f4e81e4cd16


---

# Microsoft Intune でのクライアント セットアップのトラブルシューティング
クライアントのセットアップで生じる一般的な問題のトラブルシューティングについては、以下の情報を参照してください。 この情報で問題が解決しない場合、さらに役立つ方法を探すには、「[Microsoft Intune のサポートを受ける方法](how-to-get-support-for-microsoft-intune.md)」を参照してください。

## クライアントのインストールが失敗する

-   [Microsoft Intune 管理コンソール](https://manage.microsoft.com/)に、コンピューターへのクライアント ソフトウェアの展開に関するアラートが何も表示されていない場合は、まず、クライアント コンピューターがインターネットに接続可能かどうかと、プロキシの構成を確認します。次に、コンピューターがサービスの URL ([ https://manage.microsoft.com](https://manage.microsoft.com/)) と通信できることを確かめてから、 クライアント ソフトウェアのインストールを再試行してください。

-   "クライアント ソフトウェアの展開エラー" アラートが発生した場合に、特定のユーザーに電子メールが送信されるようにすることができます。このためには、[ **管理** ] ワークスペースで通知規則を構成します。 詳しくは、「[Microsoft Intune のアラートによる通知](/intune/deploy-use/get-notified-by-alerts)」を参照してください。

-   Intune では、クライアント ソフトウェアの展開に失敗すると、重大なアラートとして **"クライアント ソフトウェアの展開エラー"** を表示します。 これは、[Microsoft Intune 管理コンソール](https://manage.microsoft.com/)の **[システムの概要]** ページと **[アラート]** ページで確認できます。 アラートを確認する方法を次に示します。

1.  [Microsoft Intune 管理コンソール](https://manage.microsoft.com/)で、**[アラート]** &gt; **[概要]** の順に選択します。

2.   **[アラートの概要]** ページで次の情報を確認できます。

    -   上位 3 件のアラート。日付、カテゴリ、または重要度を基準に並べ替えることができます。

    -   アクティブなアラートの合計数

3.  **[すべてのアラート]** を選択すると、次の情報が **[アラート]** ページに表示されます。 重要なアラートが一番上に表示されます。

    -   **名前** – 生成されたアラートの種類の名前。

    -   **ソース** – アラートの発生元へのリンク。  アラートの種類の表示のしきい値を **[すべて]**に設定している場合は、影響を受けた単一のデバイスが表示されます。  アラートの種類の表示のしきい値を特定の値に設定している場合は、そのアラートによって影響を受けたすべてのデバイスの一覧が表示されます。

    -   **最終更新日時** – アラートが最後に変更された日時を示します。 アラートが閉じている場合は、アラートが閉じた日時を表示します。

    -   **重要度** – アラートの重要度を示します。

## コンピューターの登録パッケージがダウンロードされない
**問題:** コンピューターを登録しようとすると、次の問題が発生します。
-  登録パッケージをダウンロードできない
-  ダウンロードのダイアログが表示されるが、タイムアウトになる

**解決方法:** ダウンロードに使用するブラウザーで、ダウンロードが実行される間、ダウンロードを有効にすると共に、暗号化されたファイルをローカル ディスクに保存できるようにします。

## クライアントのインストールがハングし、エラー コード 0x80040154 が返される
**問題:**

-  登録時にクライアントのインストールがハングする

-  デバイスを登録できない

-  WindowsUpdate.log にエラー 0x80040154 が記録される

この問題は、PC に重要なソフトウェア更新プログラムが適用されていない場合に発生することがあります。

**解決方法:** 「[Microsoft Intune でソフトウェア更新プログラムを使用して Windows PC を最新の状態に保つ](/intune/deploy-use/keep-windows-pcs-up-to-date-with-software-updates-in-microsoft-intune)」の説明に従って、重要な更新プログラムがインストールされるようにソフトウェア更新ポリシーを設定してください。


## policyplatform.log に記録される Microsoft Intune ポリシー関連エラー
MDM Windows デバイス以外のデバイスでは、policyplatform.log ファイルに記録されるポリシー エラーは、デバイスの Windows ユーザー アカウント制御 (UAC) の設定が既定値以外であることが原因である場合があります。 いくつかの既定値以外の UAC 設定は、Microsoft Intune クライアントのインストールやポリシーの実行に影響を与えます。

### UAC の問題を解決するには

1.  「[Microsoft Intune の管理からデータおよびデバイスを削除する](/intune/deploy-use/retire-devices-from-microsoft-intune-management)」の説明に従って、コンピューターを削除します。

2.  クライアント ソフトウェアが削除されるまで、20 分間待ちます。

    > [!NOTE]
    > [プログラムと機能] からクライアントを削除しないでください。

3.  スタート メニューで「**UAC**」と入力して、[ユーザー アカウント制御の設定] を開きます。

4.  通知のスライダーを既定の設定に移動します。

## Microsoft Intune 管理コンソールからクライアントをアンインストールできなかった場合の対処

### Microsoft Intune コマンド ライン ツールを使用して、クライアント ソフトウェアを削除するには

1.  管理者モードでコマンド プロンプトを開きます。

2.  *%programfiles%\Microsoft\OnlineManagement\Common* フォルダーに移動します。

3.  次のコマンドを実行します。 ``ProvisioningUtil.exe /UninstallAgents /MicrosoftIntune``

## クライアント インストール エラー コード
次の表で、クライアント ソフトウェアのインストールが失敗した場合に、 **[アラート]** に表示されるエラー コードについて説明します。 エラー コードごとに、問題を解決する上での推奨事項が記載されています。

|エラー コード|問題|推奨される解決策|
|--------------|--------------------|------------------------|
|**0x80CF0437**|クライアント コンピューターのクロックが正しい時刻に設定されていません。|クライアント コンピューターのクロックおよびタイム ゾーンが正しく設定されていることを確認してください。|
|**0x80240438**、 **0x80CF0438**、 **0x80CF401B**|Intune サービスに接続できません。 クライアントのプロキシ設定を確認してください。|クライアント コンピューターのプロキシの構成が Intune でサポートされていることと、クライアント コンピューターがインターネットにアクセスできることを確認してください。 サポートされるプロキシ構成について詳しくは、「[Microsoft Intune の Endpoint Protection を使用して Windows PC を保護する](/intune/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)」を参照してください。|
|**0x80CF402C**|Intune サービスに接続できません。 ネットワーク接続を確認します。|コンピューターのネットワーク接続を確認します。 ネットワーク ケーブルが接続されていること、またはワイヤレス接続がオンになっていることを確認してください。|
|**0x80240438、0x80CF0438**|Internet Explorer とローカル システムのプロキシ設定が構成されていません。|クライアントのプロキシ設定をチェックし、クライアント コンピューターのプロキシの構成が Intune でサポートされていることと、クライアント コンピューターがインターネットにアクセス可能であることを確認してください。 サポートされるプロキシ構成について詳しくは、「[Microsoft Intune の Endpoint Protection を使用して Windows PC を保護する](/intune/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)」を参照してください。|
|**0x80043001**|登録パッケージが最新ではありません。|[ **管理** ] ワークスペースを使用して、最新のクライアント ソフトウェア パッケージをダウンロードしてインストールしてください。 その方法については、トピック「[Microsoft Intune を使用して Windows PC クライアントをインストールする](/intune/deploy-use/install-the-windows-pc-client-with-microsoft-intune)」をご覧ください。|
|**0x80043004**|サブスクリプションが存在しないか、無効になっています。|Intune のアカウントとサブスクリプションがアクティブであることを確認します。 自分のアカウントの設定を見るには、[Office 365 管理センター](http://go.microsoft.com/fwlink/?LinkId=698854%20)でアカウントにサインインしてください。|
|**0x80043002**|アカウントがメンテナンス モードです。|アカウントがメンテナンス モードになっている場合は、新しいクライアント コンピューターを登録することはできません。 自分のアカウントの設定を見るには、[Office 365 管理センター](http://go.microsoft.com/fwlink/?LinkId=698854%20)でアカウントにサインインしてください。|
|**0x80043003**|アカウントが削除されています。|Intune のアカウントとサブスクリプションがアクティブであることを確認します。 自分のアカウントの設定を見るには、アカウントにサインインしてください。|
|**0x80043005**|クライアント コンピューターがインベントリから削除されています。|数時間待ってから、コンピューターにある古いバージョンのクライアント ソフトウェアをすべて削除し、クライアント ソフトウェアをもう一度インストールしてください。 そのための指示については、前述の「**Microsoft Intune 管理コンソールからクライアントをアンインストールできなかった場合の対処**」をご覧ください。|
|**0x80043006**|アカウントで許可されている接続クライアントの最大数に達しています。|サービスにさらにコンピューターを登録する前に、接続クライアント ライセンスを追加購入する必要があります。|
|**0x80043007**|インストーラーと同じフォルダーに証明書ファイルが見つかりませんでした。|インストールを開始する前にすべてのファイルを抽出してください。 抽出したファイルの名前や場所を変更しないでください。すべてのファイルが同じフォルダー内にないと、インストールが失敗します。 詳しくは、「[Microsoft Intune を使用して Windows PC クライアントをインストールする](/intune/deploy-use/install-the-windows-pc-client-with-microsoft-intune)」を参照してください。|
|**0x8024D015**、 **0x00240005**、 **0x80070BC2**、 **0x80070BC9**、 **0x80CFD015**|クライアント コンピューターの再起動が保留中になっているため、ソフトウェアをインストールできません。|コンピューターを再起動してから、クライアント ソフトウェアをもう一度インストールしてください。|
|**0x80070032**|クライアント コンピューターが、クライアント ソフトウェアのインストールに必要な前提条件を満たしていません。|必要なすべての更新プログラムがクライアント コンピューターにインストールされていることを確認してから、クライアント ソフトウェアをもう一度インストールしてください。 クライアント ソフトウェアをインストールするための前提条件の詳細については、「[Microsoft Intune に使用するネットワーク インフラストラクチャの要件](/intune/get-started/network-infrastructure-requirements-for-microsoft-intune)」を参照してください。|
|**0x80043008**|Microsoft Online Management 更新ービスを開始できませんでした。|「[Microsoft Intune のサポートを受ける方法](how-to-get-support-for-microsoft-intune.md)」の説明に従って、サポートにお問い合わせください。|
|**0x80043009**|クライアント コンピューターは、既にサービスに登録されています。|サービスを再登録する前に、クライアント コンピューターを削除する必要があります。 その方法については、「[Retire devices from Intune management](/intune/deploy-use/retire-devices-from-microsoft-intune-management)」 (Microsoft Intune の管理からデバイスを削除する) を参照してください。|
|**0x8004300B**|クライアントで実行されている Windows のバージョンがサポートされていないため、クライアント ソフトウェア インストール パッケージを実行できません。|Intune が、クライアント コンピューターで実行されている Windows のバージョンをサポートしていません。 サポートされるオペレーティング システムの一覧は、「[Microsoft Intune に使用するネットワーク インフラストラクチャの要件](/intune/get-started/network-infrastructure-requirements-for-microsoft-intune)」を参照してください。|
|**0xAB2**|Windows インストーラーが、カスタム動作に必要な VBScript ランタイムにアクセスできませんでした。|このエラーは、ダイナミック リンク ライブラリ (DLL) に基づくカスタム動作が原因で発生します。 DLL のトラブルシューティング時に、場合によっては「 [Microsoft Support KB198038: Useful Tools for Package and Deployment Issues (Microsoft サポート技術情報 198038: パッケージと展開の問題に役立つツール)](http://go.microsoft.com/fwlink/?LinkID=234255)」に記載されているツールを使用する必要があります。|
|**0x8004300f**|System Center Configuration Manager クライアントが既にインストールされているため、ソフトウェアをインストールすることはできません。|Configuration Manager クライアントを削除してから、クライアント ソフトウェアをもう一度インストールしてください。|
|**0x80043010**|Open Mobile Alliance Device Management (OMADM) が既にインストールされているため、このソフトウェアはインストールできません。|OMADM クライアントの登録を解除してから、クライアント ソフトウェアをもう一度インストールしてください。|
インストールの問題が解決しない場合は、「[Microsoft Intune のサポートを受ける方法](how-to-get-support-for-microsoft-intune.md)」の説明に従って、サポートにお問い合わせください。 このとき、クライアント コンピューターの登録ログ (%*programfiles*%\Microsoft\OnlineManagement\Logs\Enrollment.log と %*userprofile*%\AppData\Local\Microsoft\OnlineManagement\Logs\Enrollement.log)、および Windows Update ログ (%*windir*%\windowsupdate.log) を手元に用意してください。

### 次のステップ
このトラブルシューティング情報を使っても問題が解決しない場合は、「[Microsoft Intune のサポートを受ける方法](how-to-get-support-for-microsoft-intune.md)」の説明に従って Microsoft サポートにお問い合わせください。



<!--HONumber=Aug16_HO1-->


