---
title: 拡張保護認証のサンプルの ReadMe
ms.date: 03/30/2017
ms.assetid: 80bf2e97-398d-4db5-9040-d96478a2ccab
ms.openlocfilehash: 9b0a3535282a1fcc1103651f5601459e80d3d8d4
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84601102"
---
# <a name="readme-for-extended-protection-authentication-sample"></a>拡張保護認証のサンプルの ReadMe

拡張保護は、攻撃者 ("man-in-the-middle") がクライアントの資格情報を傍受し、クライアントの目的のサーバー上のセキュリティで保護されたリソースにアクセスするために使用する man-in-the-middle (MITM) 攻撃から保護するためのセキュリティ上の取り組みです。

詳細については、「[認証の拡張保護の概要](extended-protection-for-authentication-overview.md)」を参照してください。

> [!NOTE]
> このサンプルは、IIS でホストされた場合にのみ機能します。 このサンプルは HTTPS をサポートしないので、Visual Studio Development Server 上では機能しません。

## <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップしてビルドし、実行するには

1. [プログラムの追加と削除]-> Windows の機能] から、コンピューターに IIS をインストールします。

2. Windows の機能で Windows 認証を有効にする: インターネットインフォメーションサービス-> World Wide Web サービス-> セキュリティ-> Windows 認証] をオンにします。

3. Windows の機能で HTTP アクティブ化を有効にする: Microsoft .NET Framework 3.5.1-> Windows Communication Foundation HTTP アクティブ化。

4. このサンプルを実行するには、サーバーとの安全なチャネルを確立する必要のあるクライアントが必要なので、インターネット インフォメーション サービス (IIS) マネージャーからインストールすることのできるサーバー証明書が存在する必要があります。

    1. [機能ビュー] タブから、IIS マネージャーの > サーバー証明書を開きます。

    2. このサンプルをテストする目的で、自己署名証明書を作成できます  (インターネット エクスプローラーで証明書の安全性に関するプロンプトが表示されないようにする場合は、信頼されたルート証明機関ストアに証明書をインストールできます)。

5. 既定の Web サイトの操作ウィンドウに移動します。 [サイト > バインドの編集] をクリックします。 存在しない場合は、種類として HTTPS を追加します。ポート番号に 443 を指定し、前の手順で作成した SSL 証明書を割り当てます。

6. サービスをビルドします。 (プロジェクト プロパティで指定されたビルド後のアクションから) IIS に仮想ディレクトリが作成され、サービスを Web ホスト サービスにするために必要な dll、.svc、および構成ファイルがコピーされます。

7. IIS マネージャーを開きます。 前の手順で作成した仮想ディレクトリ (ExtendedProtection) を右クリックして、[アプリケーションへの変換] を選択します。

8. この仮想ディレクトリの認証モジュールを IIS マネージャーで開き、Windows 認証を有効にします。

9. このサンプルでは対応する ExtendedProtection 設定が [常に] に設定されているので、この仮想ディレクトリの Windows 認証の [詳細設定] を開き、[必須] に設定します。

10. ブラウザー ウィンドウから URL にアクセスして、サービスをテストできます。 コンピューター間でこの URL にアクセスする場合は、すべての受信 HTTP および HTTPS 通信に対してファイアウォールが開かれていることを確認してください。

11. クライアント構成ファイルを開き、-address 属性の完全なコンピューター名を指定して \<client>  -  \<endpoint> 置き換え \<full_machine_name> ます。

12. クライアントを実行します。 クライアントがセキュリティで保護されたチャネルを確立し、エンドポイント保護を使用してサービスと通信します。
