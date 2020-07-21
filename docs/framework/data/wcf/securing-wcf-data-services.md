---
title: WCF Data Services のセキュリティ保護
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- securing application [WCF Data Services]
- WCF Data Services, security
ms.assetid: 99fc2baa-a040-4549-bc4d-f683d60298af
ms.openlocfilehash: 4dbfe286099ebd0da269ca7ec6e4587d0d8b2e03
ms.sourcegitcommit: 5988e9a29cedb8757320817deda3c08c6f44a6aa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82200068"
---
# <a name="securing-wcf-data-services"></a>WCF Data Services のセキュリティ保護

この記事では、WCF Data Services と、Open Data Protocol (OData) をサポートするサービスにアクセスするアプリケーションの開発、配置、および実行に特有のセキュリティの注意点について説明します。 安全な .NET Framework アプリケーションの作成に関する推奨事項にも従う必要があります。  
  
WCF Data Services ベースの OData サービスをセキュリティで保護する方法を計画するときには、認証 (プリンシパルの ID を発見および確認するプロセス) と承認 (認証されたプリンシパルが要求されたリソースにアクセスできるかどうかを判断するプロセス) の両方を解決する必要があります。 また、SSL を使用してメッセージを暗号化するかどうかを検討します。  
  
## <a name="authenticating-client-requests"></a>クライアント要求の認証  
WCF Data Services は、認証を独自に実装する代わりにデータ サービス ホストに依存しています。 したがって、ネットワーク ホストによって受信要求が既に認証されていること、WCF Data Services によって提供されるインターフェイスを使用して要求のプリンシパルが正しく識別されていることが前提とされます。 これらの認証オプションと方法の詳細については、[OData と認証に関する複数パートの記事](https://devblogs.microsoft.com/odata/?s=%22OData+and+authentication%22)を参照してください。  
  
### <a name="authentication-options-for-a-wcf-data-service"></a>WCF Data Service の認証オプション  
 次の表に、WCF Data Service への要求を認証するために使用できる認証メカニズムを示します。  
  
|認証オプション|説明|  
|----------------------------|-----------------|  
|匿名認証|匿名 HTTP 認証が有効になっている場合は、すべてのプリンシパルがデータ サービスに接続できます。 匿名アクセスには資格情報は必要ありません。 このオプションは、だれでもデータ サービスにアクセスできるようにする場合にのみ使用します。|  
|基本認証とダイジェスト認証|ユーザー名とパスワードで構成される資格情報が認証に必要です。 Windows 以外のクライアントの認証がサポートされます。 **セキュリティに関するメモ:** 基本認証の資格情報 (ユーザー名とパスワード) はクリア テキストで送信されるので、傍受される可能性があります。 ダイジェスト認証では、指定された資格情報に基づくハッシュが送信されるため、基本認証に比べて安全です。 ただし、どちらの方法も man-in-the-middle 攻撃を受ける可能性があります。 これらの認証方法を使用する場合は、SSL (Secure Sockets Layer) を使用してクライアントとデータ サービスの間の通信を暗号化することを検討してください。 <br /><br /> Microsoft インターネット インフォメーション サービス (IIS) には、ASP.NET アプリケーションの HTTP 要求に対する基本認証とダイジェスト認証の実装が用意されています。 この Windows 認証プロバイダーの実装を使用すると、.NET Framework クライアント アプリケーションで、資格情報を要求の HTTP ヘッダーでデータ サービスに渡して Windows ユーザーの認証をシームレスにネゴシエートできます。 詳細については、「[ダイジェスト認証のテクニカル リファレンス](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc782794(v=ws.10))」を参照してください。<br /><br /> データ サービスで Windows 資格情報以外のカスタム認証サービスに基づく基本認証を使用する場合は、認証用のカスタム ADP.NET HTTP モジュールを実装する必要があります。<br /><br /> WCF Data Services でカスタム基本認証スキームを使用する方法の例については、ブログ記事「[OData と認証の – パート 6 – カスタム基本認証](https://devblogs.microsoft.com/odata/odata-and-authentication-part-6-custom-basic-authentication/)」を参照してください。|  
|Windows 認証|Windows ベースの資格情報の交換には、NTLM または Kerberos が使用されます。 このメカニズムは基本認証やダイジェスト認証より安全ですが、クライアントが Windows ベースのアプリケーションである必要があります。 IIS には、ASP.NET アプリケーションの HTTP 要求に対する Windows 認証の実装も用意されています。 詳細については、「 [ASP.NET フォーム認証の概要](https://docs.microsoft.com/previous-versions/aspnet/7t6b43z4(v=vs.100))」を参照してください。<br /><br /> WCF Data Services で Windows 認証スキームを使用する方法の例については、ブログ記事「[OData と認証の – パート 2 – Windows 認証](https://devblogs.microsoft.com/odata/odata-and-authentication-part-2-windows-authentication/)」を参照してください。|  
|ASP.NET フォーム認証|フォーム認証では、独自のコードを使用してユーザーを認証し、認証トークンをクッキーまたはページ URL に保存できます。 作成したログイン フォームを使用してユーザーのユーザー名とパスワードを認証します。 認証されない要求はログイン ページにリダイレクトされ、ここでユーザーが資格情報を入力してフォームを送信します。 アプリケーションで要求を認証する場合、後続の要求で使用する ID を再確立するためのキーが含まれたチケットをシステムが発行します。 詳細については、「[フォーム認証プロバイダー](https://docs.microsoft.com/previous-versions/aspnet/9wff0kyh(v=vs.100))」を参照してください。 **セキュリティに関するメモ:** ASP.NET Web アプリケーションでフォーム認証を使用する場合、既定では、フォーム認証チケットを含むクッキーはセキュリティで保護されません。 認証チケットと最初のログイン資格情報の両方を保護するには、SSL を要求することを検討してください。 <br /><br /> WCF Data Services でフォーム認証を使用する方法の例については、ブログ記事「[OData と認証の – パート 7 – フォーム認証](https://devblogs.microsoft.com/odata/odata-and-authentication-part-7-forms-authentication/)」を参照してください。|  
|クレーム ベースの認証|クレーム ベースの認証では、データ サービスはユーザー認証を "サードパーティ" の信頼された ID プロバイダー サービスに依存します。 ID プロバイダーは、データ サービス リソースへのアクセスを要求しているユーザーを確実に認証し、要求されたリソースへのアクセスを許可するトークンを発行します。 このトークンがデータ サービスに提示され、そのアクセス トークンを発行した識別情報サービスとの信頼関係に基づいてユーザーのアクセスが許可されます。<br /><br /> クレーム ベースの認証プロバイダーの利点は、信頼ドメイン間でさまざまな種類のクライアントの認証に使用できることです。 このようなサードパーティ プロバイダーを使用することにより、ユーザーの管理と認証の要件をデータ サービスからオフロードできます。 OAuth 2.0 は、サービスとしてのフェデレーション認証のために Azure AppFabric アクセス制御によってサポートされているクレーム ベースの認証プロトコルであり、 REST ベースのサービスをサポートします。 WCF Data Services で OAuth 2.0 を使用する方法の例については、ブログ記事「[OData と認証の – パート 8 – OAuth WRAP](https://devblogs.microsoft.com/odata/odata-and-authentication-part-8-oauth-wrap/)」を参照してください。|  
  
<a name="clientAuthentication"></a>
### <a name="authentication-in-the-client-library"></a>クライアント ライブラリの認証  
 既定では、OData サービスに要求を送信する際、WCF Data Services クライアント ライブラリから資格情報は提供されません。 データ サービスでユーザー認証のためにログイン資格情報が要求されている場合は、<xref:System.Net.NetworkCredential> の <xref:System.Data.Services.Client.DataServiceContext.Credentials%2A> プロパティからアクセスできる <xref:System.Data.Services.Client.DataServiceContext> で資格情報を渡すことができます。以下に例を示します。  
  
```csharp  
// Set the client authentication credentials.  
context.Credentials =  
    new NetworkCredential(userName, password, domain);  
```  
  
```vb  
' Set the client authentication credentials.  
context.Credentials = _  
    New NetworkCredential(userName, password, domain)  
```  
  
 詳細については、[データ サービス要求のクライアント資格情報の指定](specify-client-creds-for-a-data-service-request-wcf.md)」を参照してください。  
  
 クレーム ベースのトークンやクッキーなど、<xref:System.Net.NetworkCredential> オブジェクトでは指定できないログイン資格情報がデータ サービスで要求されている場合は、手動で HTTP 要求のヘッダー (通常は `Authorization` と `Cookie`) を設定する必要があります。 このような認証シナリオの詳細については、ブログ記事「[OData と認証の – パート 3 – クライアント側フック](https://devblogs.microsoft.com/odata/odata-and-authentication-part-3-clientside-hooks/)」を参照してください。 要求メッセージの HTTP ヘッダーを設定する方法の例については、「[方法: クライアント要求のヘッダーを設定する](how-to-set-headers-in-the-client-request-wcf-data-services.md)」を参照してください。  
  
## <a name="impersonation"></a>偽装  
 データ サービスは通常、データ サービスをホストしているワーカー プロセスの資格情報を使用して、要求されたリソース (サーバー上のファイル、データベースなど) にアクセスします。 偽装を使用しているときは、要求を出しているユーザーの Window ID (ユーザー アカウント) で ASP.NET アプリケーションを実行できます。 偽装は、IIS を使用してユーザーを認証するアプリケーションで使用されるのが一般的です。この場合、要求されたリソースへのアクセスにそのプリンシパルの資格情報が使用されます。 詳細については、「[ASP.NET の偽装](https://docs.microsoft.com/previous-versions/aspnet/xh507fc5(v=vs.100))」参照してください。  
  
## <a name="configuring-data-service-authorization"></a>データ サービスの承認の構成  
 承認とは、事前に行われた認証に基づいて識別されるプリンシパルまたはプロセスにアプリケーション リソースへのアクセスを許可することです。 一般に、データ サービスのユーザーには、クライアント アプリケーションで必要とされている操作を実行するのに十分な権限のみを与えるようにします。  
  
### <a name="restrict-access-to-data-service-resources"></a>データ サービス リソースへのアクセスの制限  
 WCF Data Services では、データ サービスにアクセスできるすべてのユーザーにデータ サービス リソース (エンティティ セットおよびサービス操作) に対する共通の読み取りおよび書き込みのアクセス権が既定で付与されます。 読み取りおよび書き込みのアクセスを定義する規則は、データ サービスによって公開される各エンティティ セットおよびサービス操作に対して個別に定義できます。 読み取りおよび書き込みの両方のアクセスを、クライアント アプリケーションで必要なリソースのみに制限することをお勧めします。 詳細については、「[最小限のリソース アクセス要件](configuring-the-data-service-wcf-data-services.md#accessRequirements)」を参照してください。  
  
### <a name="implement-role-based-interceptors"></a>ロール ベースのインターセプターの実装  
 インターセプターを使用すると、データ サービス リソースに対する要求を、データ サービスによって処理される前にインターセプトすることができます。 詳細については、「[インターセプター](interceptors-wcf-data-services.md)」を参照してください。 インターセプターを使用すると、要求を行っている認証されたユーザーに基づいて承認決定を行うことができます。 認証されたユーザーの ID に基づいてデータ サービス リソースへのアクセスを制限する方法の例については、「[方法: データ サービス メッセージを先に取得する](how-to-intercept-data-service-messages-wcf-data-services.md)」を参照してください。  
  
### <a name="restrict-access-to-the-persisted-data-store-and-local-resources"></a>永続化データ ストアとローカル リソースへのアクセスの制限  
 永続化ストアにアクセスするためのアカウントには、データベースまたはファイル システムでデータ サービスの要件をサポートするのに十分な権限のみを与えるようにしてください。 匿名認証が使用されている場合は、そのアカウントがホスト アプリケーションの実行に使用されます。 詳細については、[IIS 上で実行する WCF Data Service を開発する](how-to-develop-a-wcf-data-service-running-on-iis.md)」を参照してください。 偽装を使用する場合は、認証されたユーザーにそれらのリソースへのアクセスを (通常は Windows グループの一部として) 許可する必要があります。  
  
## <a name="other-security-considerations"></a>その他のセキュリティの考慮事項  
  
### <a name="secure-the-data-in-the-payload"></a>ペイロードのデータの保護  
OData は HTTP プロトコルに基づいています。 データ サービスで実装されている認証によっては、HTTP メッセージのヘッダーに重要なユーザー資格情報が含まれている場合があります。 メッセージの本文にも、保護する必要がある貴重な顧客データが含まれている場合があります。 いずれの場合も、SSL を使用してその情報をネットワークで保護することをお勧めします。  
  
### <a name="ignored-message-headers-and-cookies"></a>無視されるメッセージ ヘッダーとクッキー  
 HTTP 要求のヘッダーは、コンテンツ タイプとリソースの場所を宣言するもの以外は無視されます。また、データ サービスによって設定されることはありません。  
  
 Cookie は、認証方式の一部としては使用できます (ASP.NET フォーム認証など)。 一方、受信要求で設定された HTTP Cookie は、WCF Data Service によって無視されます。 データ サービスのホストによって処理されることはありますが、WCF Data Services ランタイムによって分析されたり返されたりすることはありません。 応答で送信された Cookie が WCF Data Services クライアント ライブラリで処理されることもありません。  
  
### <a name="custom-hosting-requirements"></a>カスタム ホストの要件  
 既定では、WCF Data Services は IIS でホストされる ASP.NET アプリケーションとして作成されます。 そのため、データ サービスでこのプラットフォームのセキュリティ動作を活用できます。 カスタム ホストによってホストされる WCF Data Services を定義することもできます。 詳細については、「[データ サービスのホスティング](hosting-the-data-service-wcf-data-services.md)」を参照してください。 データ サービスをホストするコンポーネントとプラットフォームでは、データ サービスへの攻撃を防ぐために次のセキュリティ動作を確保する必要があります。  
  
- 可能なすべての操作について、データ サービス要求で受け入れる URI の長さを制限します。  
  
- 着信および発信の両方の HTTP メッセージのサイズを制限します。  
  
- 任意の時点の未処理の要求の総数を制限します。  
  
- HTTP ヘッダーとその値のサイズを制限し、WCF Data Services でヘッダーのデータにアクセスできるようにします。  
  
- TCP SYN 攻撃やメッセージ リプレイ攻撃などの既知の攻撃を検出して阻止します。  
  
### <a name="values-are-not-further-encoded"></a>値のさらなるエンコード  
 データ サービスに送信されたプロパティ値が WCF Data Services ランタイムによってさらにエンコードされることはありません。 たとえば、書式設定された HTML コンテンツがエンティティの文字列プロパティに含まれていた場合、データ サービスによってタグが HTML エンコードされることはありません。 応答のプロパティ値についても、データ サービスによってさらなるエンコードが行われることはありません。 クライアント ライブラリで追加のエンコードが行われることもありません。  
  
### <a name="considerations-for-client-applications"></a>クライアント アプリケーションに関する注意点  
 以下のセキュリティの注意点は、WCF Data Services クライアントを使用して OData サービスにアクセスするアプリケーションに当てはまります。  
  
- クライアント ライブラリは、データ サービスへのアクセスに使用されるプロトコルで十分なレベルのセキュリティが確保されていることを前提としています。  
  
- クライアント ライブラリは、基になるプラットフォームによって提供されるトランスポート スタックのタイムアウトや解析のすべてのオプションに対して既定値を使用します。  
  
- クライアント ライブラリはアプリケーション構成ファイルの設定を読み取りません。  
  
- クライアント ライブラリにはドメイン間アクセスのメカニズムは実装されていません。 基になる HTTP スタックによって提供されるメカニズムが使用されます。  
  
- クライアント ライブラリにはユーザー インターフェイス要素はありません。送受信されるデータの表示は行われません。  
  
- クライアント アプリケーションで常にユーザー入力と信頼されていないサービスからのデータを検証することをお勧めします。  
  
## <a name="see-also"></a>関連項目

- [WCF Data Services の定義](defining-wcf-data-services.md)
- [WCF Data Services クライアント ライブラリ](wcf-data-services-client-library.md)
