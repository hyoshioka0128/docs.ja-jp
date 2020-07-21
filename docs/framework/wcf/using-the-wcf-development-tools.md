---
title: WCF 開発ツールの使用
ms.date: 03/30/2017
ms.assetid: 054adb87-c244-4d5a-83d1-0b2b44bd454b
ms.openlocfilehash: 82bb7e225492bcdba4d2e611de405a09571355c0
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79183077"
---
# <a name="using-the-wcf-development-tools"></a>WCF 開発ツールの使用
このセクションでは、WCF サービスの開発に役立つ Visual Studio 開発ツールについて説明します。  
  
 Visual Studio テンプレートを基盤として使用して、独自のサービスをすばやく構築し、WCF サービスの自動ホストと WCF テスト クライアントを使用してサービスをデバッグおよびテストできます。 これらのツールによって、高速でシームレスなデバッグとテストのサイクルが実現し、初期の段階でホスト モデルにコミットする必要がなくなります。  

 > [!NOTE]
 > Visual Studio 2017 以降では、WCF 開発ツールは既定ではインストールされません。 これらの機能を使用するには、Visual Studio インストーラーで Windows コミュニケーションファウンデーション コンポーネントが選択されていることを確認する必要があります。
  
## <a name="the-wcf-developer-tools"></a>WCF の開発者用ツール  
 [WCF Visual Studio テンプレート](wcf-vs-templates.md)  
  
 定義済みの Visual Studio プロジェクトテンプレートと項目テンプレートを使用して、WCF サービスと周辺アプリケーションをすばやく構築できます。  
  
 [WCF サービス ホスト (WcfSvcHost.exe)](wcf-service-host-wcfsvchost-exe.md)  
  
 WCF サービスの自動ホスト (WcfSvcHost.exe) を使用すると、Visual Studio デバッガー (F5) を起動して、実装したサービスを自動的にホストおよびテストできます。 その後、WCF テスト クライアント (wcfTestClient.exe) または独自のクライアントを使用してサービスをテストし、潜在的なエラーを見つけて修正できます。  
  
 [WCF のテスト用クライアント (WcfTestClient.exe)](wcf-test-client-wcftestclient-exe.md)  
  
 WCF テスト クライアント (WcfTestClient.exe) は、任意の型のパラメーターを入力し、その入力をサービスに送信し、サービスが返送する応答を表示できるようにする GUI ツールです。 WCF サービスの自動ホストと組み合わせた場合、シームレスなサービス テスト エクスペリエンスを提供します。  
  
 [XML からのデータ型クラスの生成](generating-data-type-classes-from-xml.md)  
  
 クリップボードに格納されている XML データは、コード ページに貼り付けることができます。 データで定義されているクラスは、コード型に変換されます。  
  
## <a name="using-the-tools-without-administrator-privilege"></a>管理特権を必要としないツールの使用  
 管理者特権を持たないユーザーが WCF サービスを開発できるようにするには、Visual Studio のインストール中に名前空間http://+:8731/Design_Time_Addresses"" に対して ACL (アクセス制御リスト) が作成されます。 この ACL は (UI) に設定され、コンピューターにログオンしているすべての対話ユーザーが含まれます。 管理者は、この ACL にユーザーを追加または削除したり、追加のポートを開いたりできます。この ACL によって、既定の構成で、WCF テンプレートまたは WF テンプレートでデータを送受信できるようになります。 また、ユーザーは、管理者特権を付与せずに、WCF サービスの自動ホスト (wcfSvcHost.exe) を使用できます。  
  
 管理者特権の管理者アカウントで Windows Vista の Netsh.exe ツールを使用してアクセスを変更できます。 Netsh.exe の使用例を次に示します。  
  
```console  
netsh http add urlacl url=http://+:8001/MyService user=<domain>\<user>  
```  
  
 Netsh.exe の詳細については、「 [Netsh.exe ツールおよびコマンド ライン スイッチの使用方法](https://docs.microsoft.com/previous-versions/tn-archive/bb490939(v=technet.10))」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [WCF Visual Studio テンプレート](wcf-vs-templates.md)
- [WCF サービス ホスト (WcfSvcHost.exe)](wcf-service-host-wcfsvchost-exe.md)
- [WCF のテスト用クライアント (WcfTestClient.exe)](wcf-test-client-wcftestclient-exe.md)
