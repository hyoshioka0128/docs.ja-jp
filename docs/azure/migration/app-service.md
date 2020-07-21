---
title: .NET Web アプリまたはサービスを Azure App Service に移行する
description: .NET Web アプリまたはサービスをオンプレミスから Azure App Service に移行する方法について説明します。
ms.topic: conceptual
ms.date: 07/08/2020
ms.openlocfilehash: d208865942b49ae2d5437b8f2fcff294933af21b
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174310"
---
# <a name="migrate-your-net-web-app-or-service-to-azure-app-service"></a>.NET Web アプリまたはサービスを Azure App Service に移行する

[App Service](/azure/app-service/overview) は、スケーラブルな Web サイトと Web アプリケーションをホストするために最適化された、フル マネージドのコンピューティング プラットフォーム サービスです。 この記事では、既存のアプリケーションを Azure App Service にリフトアンドシフトする方法、考慮すべき変更、および[クラウドへの移行](https://azure.microsoft.com/migration/web-applications/)に関するその他のリソースについて説明します。 ほとんどの ASP.NET Web サイト (WebForms、MVC) とサービス (Web API、WCF) は、変更なしで Azure App Service に直接移行できます。 若干の変更が必要なものもあれば、リファクタリングが必要なものもあります。

開始するには、 [ASP.NET および SQL アプリケーションを Azure App Service に発行](https://tutorials.visualstudio.com/azure-webapp-migrate/intro)します。

## <a name="considerations"></a>注意事項

### <a name="on-premises-resources-including-sql-server"></a>オンプレミスのリソース (SQL Server を含む)

移行または変更が必要になる可能性のあるオンプレミスのリソースへのアクセスを確認します。 オンプレミスのリソースへのアクセスを軽減するには、次のような方法があります。

* [Azure Virtual Network](/azure/app-service/web-sites-integrate-with-vnet) を使用して、App Service をオンプレミスのリソースに接続する VPN を作成します。
* [Azure Relay](/azure/service-bus-relay/relay-what-is-it) を使用して、ファイアウォールを変更せずに、オンプレミス サービスをクラウドに安全に公開します。
* [SQL データベース](https://go.microsoft.com/fwlink/?linkid=863217)などの依存関係を Azure に移行します。
* クラウドのサービスとしてのプラットフォーム サービスを使用して依存関係を減らします。 たとえば、オンプレミスのメール サーバーに接続するのではなく、[SendGrid](/azure/sendgrid-dotnet-how-to-send-email) を使用することを検討します。

### <a name="port-bindings"></a>ポートのバインド

Azure App Service では、HTTP トラフィック用のポート 80 と、HTTPS トラフィック用のポート 443 がサポートされています。

WCF では、次のバインドがサポートされています。

| バインド | メモ |
|--|--|
| `BasicHttp` |  |
| `WSHttp` |  |
| `WSDualHttpBinding` | [Web ソケットのサポート](https://docs.microsoft.com/azure/app-service/web-sites-configure)を有効にする必要があります。 | [Web ソケットのサポート](/azure/app-service/web-sites-configure)を有効にする必要があります。 |
| `NetHttpBinding` | 双方向コントラクトに対して、[Web ソケットのサポート](https://docs.microsoft.com/azure/app-service/web-sites-configure)を有効にする必要があります。 | 双方向コントラクトに対して、[Web ソケットのサポート](/azure/app-service/web-sites-configure)を有効にする必要があります。 |
| `NetHttpsBinding` | 双方向コントラクトに対して、[Web ソケットのサポート](https://docs.microsoft.com/azure/app-service/web-sites-configure)を有効にする必要があります。 | 双方向コントラクトに対して、[Web ソケットのサポート](/azure/app-service/web-sites-configure)を有効にする必要があります。 |
| `BasicHttpContextBinding` |  |
| `WebHttpBinding` |  |
| `WSHttpContextBinding` |  |

### <a name="authentication"></a>認証

Azure App Service では既定で匿名認証がサポートされており、意図した場合はフォーム認証がサポートされます。 Windows 認証は、Azure Active Directory および ADFS と統合する場合にのみ使用できます。 オンプレミスのディレクトリを Azure Active Directory と統合する方法の詳細については、[こちら](/azure/active-directory/connect/active-directory-aadconnect)をご覧ください。

### <a name="assemblies-in-the-gac-global-assembly-cache"></a>GAC (グローバル アセンブリ キャッシュ) 内のアセンブリ

これはサポートされていません。 アプリの *\bin* フォルダーに必要なアセンブリをコピーすることを検討してください。 サーバーにインストールされているカスタム *.msi* ファイル (PDF ジェネレーターなど) は使用できません。

### <a name="iis-settings"></a>IIS 設定

従来、アプリケーションの applicationHost.config で構成していたあらゆるものを、Azure Portal で構成できるようになりました。 AppPool のビット、WebSocket の有効化/無効化、マネージド パイプライン バージョン、.NET Framework バージョン (2.0/4.0) などがこれに該当します。 [アプリケーション設定](/azure/app-service/web-sites-configure)を変更するには、[Azure Portal](https://portal.azure.com) に移動し、Web アプリのブレードを開いて、 **[アプリケーションの設定]** タブを選択します。

#### <a name="iis5-compatibility-mode"></a>IIS5 互換モード

IIS5 互換モードはサポートされていません。 Azure App Service では、各 Web App とその下のすべてのアプリケーションが、[アプリケーション プール](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc735247(v=ws.10))の特定のセットを使用して同じワーカー プロセスで実行されます。

#### <a name="iis7-schema-compliance"></a>IIS7+ スキーマ準拠

Azure App Service IIS スキーマで定義されていない要素と属性があります。 問題が発生した場合は、[XDT 変換](https://azure.microsoft.com/documentation/articles/web-sites-transform-extend/)を使用することを検討してください。

#### <a name="single-application-pool-per-site"></a>サイトごとに 1 つのアプリケーション プール

Azure App Service では、各 Web アプリとその下のすべてのアプリケーションが、同じアプリケーション プールで実行されます。 一般的な設定で単一のアプリケーション プールを確立するか、アプリケーションごとに個別の Web アプリを作成することを検討してください。

### <a name="com-and-com-components"></a>COM および COM+ コンポーネント

Azure App Service では、プラットフォーム上で COM コンポーネントを登録することはできません。 アプリで COM コンポーネントを使用する場合は、それらのコンポーネントをマネージド コードで書き換えて、サイトまたはアプリケーショントと共にデプロイする必要があります。

### <a name="physical-directories"></a>物理ディレクトリ

Azure App Service では、物理ドライブへのアクセスは許可されていません。 [Azure Files](/azure/storage/files/storage-files-introduction) を使用して、SMB 経由でファイルにアクセスすることが必要な場合があります。 HTTPS 経由でアクセスする場合は、[Azure Blob Storage](/azure/storage/blobs/storage-blobs-introduction) にファイルを格納できます。

### <a name="isapi-filters"></a>ISAPI フィルター

Azure App Service では、ISAPI フィルターの使用をサポートできます。ただし、ISAPI DLL をサイトと共に配置し、web.config を使用して登録する必要があります。

### <a name="https-bindings-and-ssl"></a>HTTPS バインドと SSL

HTTPS バインドは移行されず、SSL 証明書も Web サイトに関連付けられません。 ただし、サイトの移行が完了したら、[SSL 証明書を手動でアップロード](/azure/app-service/app-service-web-tutorial-custom-ssl)できます。

### <a name="sharepoint-and-frontpage"></a>SharePoint と FrontPage

SharePoint と FrontPage Server Extensions (FPSE) はサポートされていません。

### <a name="web-site-size"></a>Web サイトのサイズ

無料サイトのコンテンツのサイズは 1 GB に制限されています。 サイトが 1 GB を超える場合は、有料の SKU にアップグレードする必要があります。 「[App Service の価格](https://azure.microsoft.com/pricing/details/app-service/windows/)」をご覧ください。

### <a name="database-size"></a>データベース サイズ

SQL Server データベースについては、現在の [SQL Database の価格](https://azure.microsoft.com/pricing/details/sql-database)を確認してください。

### <a name="azure-active-directory-aad-integration"></a>Azure Active Directory (AAD) の統合

AAD は無料のアプリでは機能しません。 AAD を使用するには、アプリの SKU をアップグレードする必要があります。 「[App Service の価格](https://azure.microsoft.com/pricing/details/app-service/windows/)」をご覧ください。

### <a name="monitoring-and-diagnostics"></a>監視と診断

監視と診断に現在使用しているオンプレミスのソリューションは、クラウドでは機能しない可能性があります。 ただし、Web アプリでの問題を特定し、デバッグできるように、Azure には、ログ記録、監視、診断用のツールが用意されています。 Web アプリの診断は、アプリの構成で簡単に有効にすることができます。また、記録されたログは、Azure Application Insights で表示できます。 Web アプリの診断ログの有効化の詳細については、[こちら](/azure/app-service/web-sites-enable-diagnostic-log)をご覧ください。

### <a name="connection-strings-and-application-settings"></a>接続文字列とアプリケーション設定

[Azure KeyVault](/azure/key-vault/) を使用することを検討してください。これは、アプリケーションで使用される機密情報を安全に格納するサービスです。 また、このデータを App Service 設定として保存することもできます。

### <a name="dns"></a>DNS

アプリケーションの要件に基づいて、DNS 構成を更新することが必要な場合があります。 これらの DNS 設定は、App Service の[カスタム ドメイン設定](/azure/app-service/app-service-web-tutorial-custom-domain)で構成できます。

## <a name="azure-app-service-with-windows-containers"></a>Windows コンテナーを使用した Azure App Service

アプリを App Service に直接移行できない場合は、Windows コンテナーを使用した App Service を検討します。これにより、GAC、COM コンポーネント、MSI、.NET FX API へのフル アクセス、DirectX などを使用できるようになります。

## <a name="see-also"></a>関連項目

* [アプリが App Service に適しているかどうかを判断する方法](https://appmigration.microsoft.com/)
* [クラウドへのデータベースの移行](sql.md)
* [Azure Web アプリのサンドボックスの詳細と制限事項](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)
