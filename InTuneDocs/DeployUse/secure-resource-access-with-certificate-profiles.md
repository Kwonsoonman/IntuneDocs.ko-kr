---
title: "リソース アクセス用の証明書プロファイル |Microsoft Intune"
description: "各ユーザーのデバイスにインストールされている証明書で、VPN、Wi-Fi、および電子メール アクセスを保護します。"
keywords: 
author: Nbigman
manager: Arob98
ms.date: 07/21/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 8cbb8499-611d-4217-a7b4-e9b864785dd0
ms.reviewer: kmyrup
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 72288296d966b9b9fae4fd721b4460528213f626
ms.openlocfilehash: c8158b6a54347f6bec1008142eed44daca8946d0


---

# Secure resource access with certificate profiles in Microsoft Intune (Microsoft Intune の証明書プロファイルでリソースへのアクセスを保護する)
VPN、Wi-Fi、または電子メール プロファイルを介して企業リソースへのアクセスを有効にするときは、各ユーザーのデバイスにインストールされている証明書を使用してそのアクセスを保護することもできます。 そのしくみは次のとおりです。

1. 「[SCEP の証明書インフラストラクチャを構成する](configure-certificate-infrastructure-for-scep.md)」または「[PFX の証明書インフラストラクチャを構成する](configure-certificate-infrastructure-for-pfx.md)」の説明に従って、適切な証明書インフラストラクチャを構成します。

2. 各デバイスにルート証明書 (または中間 CA 証明書) をインストールして、デバイスが証明機関の正当性を認識できるようにします。 これを行うには、**信頼された証明書プロファイル**を作成して展開します。 このプロファイルを展開すると、Intune で管理しているデバイスがルート証明書を要求して受け取ります。 プラットフォームごとに別個のプロファイルを作成する必要があります。 **信頼された証明書プロファイル**は、次のプラットフォーム用に使用できます。
 -  iOS 7.1 以降
 -  Mac OS X 10.9 以降
 -  Android 4.0 以降
 -  Windows 8.1 以降
 -  Windows Phone 8.1 以降

3. 「[Intune 証明書プロファイルを構成する](configure-intune-certificate-profiles.md)」の説明に従って、各デバイスが電子メール、VPN、および Wi-Fi アクセスの認証に使用する証明書を要求するようにします。 次のプラットフォーム上のデバイスに対しては、**PKCS #12 (.PFX) 証明書プロファイル**または **SCEP 証明書プロファイル**を作成して展開できます。

-  Android 4.0 以降
-  iOS 7.1 以降
-  Windows 10 (Desktop および Mobile) 以降

次のプラットフォームに対しては、**SCEP 証明書プロファイル**を使用します。
-   Mac OS X 10.9 以降
-   Windows Phone 8.1 以降

プラットフォームごとに別個のプロファイルを作成する必要があります。 プロファイルを作成したら、それを既に作成した**信頼されたルート証明書プロファイル**に関連付けます。

> [!NOTE]           
> -    エンタープライズ証明機関がない場合は、それを作成する必要があります。
>- デバイス プラットフォームに基づいて Simplified Certificate Enrollment Protocol (SCEP) プロファイルを使用することにした場合は、ネットワーク デバイス登録サービス (NDES) サーバーも構成する必要があります。
>-  SCEP プロファイルと .PFX プロファイルのどちらを使用する場合でも、Microsoft Intune 証明書コネクタをダウンロードして構成する必要があります。
> これらすべての構成については、「[SCEP の証明書インフラストラクチャを構成する](configure-certificate-infrastructure-for-scep.md)」と「[PFX の証明書インフラストラクチャを構成する](configure-certificate-infrastructure-for-pfx.md)」で説明されています。

### 次のステップ
- [SCEP の証明書インフラストラクチャを構成する](configure-certificate-infrastructure-for-scep.md)
- [PFX の証明書インフラストラクチャを構成する](configure-certificate-infrastructure-for-pfx.md)
- [Intune 証明書プロファイルを構成する](configure-intune-certificate-profiles.md)



<!--HONumber=Jul16_HO3-->


