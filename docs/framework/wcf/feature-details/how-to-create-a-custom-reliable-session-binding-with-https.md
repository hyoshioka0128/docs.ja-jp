---
title: '方法: カスタムの信頼できるセッションによる HTTPS を使用したバインディングを作成する'
ms.date: 03/30/2017
ms.assetid: fa772232-da1f-4c66-8c94-e36c0584b549
ms.openlocfilehash: 70f8f4f33626ab0d1705e03750bfd9baa324e60a
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598997"
---
# <a name="how-to-create-a-custom-reliable-session-binding-with-https"></a>方法: カスタムの信頼できるセッションによる HTTPS を使用したバインディングを作成する

ここでは、信頼できるセッションを使用した SSL (Secure Sockets Layer) トランスポート セキュリティの使用方法について説明します。 HTTPS 上で信頼できるセッションを使用するには、信頼できるセッションと HTTPS トランスポートを使用するカスタム バインドを作成する必要があります。 信頼できるセッションは、コードを使用するか、構成ファイルで宣言によって、強制的に有効にします。 この手順では、クライアントとサービスの構成ファイルを使用して、信頼できるセッションと要素を有効にし [**\<httpsTransport>**](../../configure-apps/file-schema/wcf/httpstransport.md) ます。

この手順の重要な部分は、 **\<endpoint>** 構成要素に `bindingConfiguration` という名前のカスタムバインディング構成を参照する属性が含まれていることです `reliableSessionOverHttps` 。 [**\<binding>**](../../configure-apps/file-schema/wcf/bindings.md)構成要素は、この名前を参照して、信頼できるセッションと HTTPS トランスポートを使用して **\<reliableSession>** 、要素と要素を含めることを指定し **\<httpsTransport>** ます。

この例のソースコピーについては、「HTTPS を使用した[カスタムバインディングの信頼できるセッション](../samples/custom-binding-reliable-session-over-https.md)」を参照してください。

### <a name="configure-the-service-with-a-custombinding-to-use-a-reliable-session-with-https"></a>HTTPS で信頼できるセッションを使用するための CustomBinding でサービスを構成する

1. サービスの種類にサービス コントラクトを定義します。

   [!code-csharp[c_HowTo_CreateReliableSessionHTTPS#1121](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/service.cs#1121)]

1. サービス クラスにサービス コントラクトを実装します。 サービスの実装内では、アドレスまたはバインド情報が指定されていないことに注意してください。 構成ファイルからアドレスやバインド情報を取得するためのコードを記述する必要はありません。

   [!code-csharp[c_HowTo_CreateReliableSessionHTTPS#1122](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/service.cs#1122)]

1. *Web.config ファイルを*作成して、 `CalculatorService` `reliableSessionOverHttps` 信頼できるセッションと HTTPS トランスポートを使用するという名前のカスタムバインドを持つのエンドポイントを構成します。

   [!code-xml[c_HowTo_CreateReliableSessionHTTPS#2111](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/common/web.config#2111)]

1. 次の行を含む .svc ファイルを作成*し*ます。

   `<%@ServiceHost language=c# Service="CalculatorService" %>`

1. サービスの *.svc*ファイルをインターネットインフォメーションサービス (IIS) 仮想ディレクトリに配置します。

### <a name="configure-the-client-with-a-custombinding-to-use-a-reliable-session-with-https"></a>HTTPS で信頼できるセッションを使用するようにクライアントを構成する (CustomBinding)

1. コマンドラインから[ServiceModel メタデータユーティリティツール (*svcutil.exe*)](../servicemodel-metadata-utility-tool-svcutil-exe.md)を使用して、サービスメタデータからコードを生成します。

   ```console
   Svcutil.exe <Metadata Exchange (MEX) address or HTTP GET address>
   ```

1. 生成されるクライアントには、 `ICalculator` クライアント実装が満たす必要のあるサービスコントラクトを定義するインターフェイスが含まれています。

   [!code-csharp[C_HowTo_CreateReliableSessionHTTPS#1221](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/client.cs#1221)]

1. 生成されたクライアント アプリケーションは `ClientCalculator` も実装します。 サービスの実装内でアドレスとバインディング情報が指定されていないことに注意してください。 構成ファイルからアドレスおよびバインド情報を取得するコードを記述する必要はありません。

   [!code-csharp[C_HowTo_CreateReliableSessionHTTPS#1222](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/client.cs#1222)]

1. `reliableSessionOverHttps`HTTPS トランスポートと信頼できるセッションを使用するように、という名前のカスタムバインディングを構成します。

   [!code-xml[C_HowTo_CreateReliableSessionHTTPS#2211](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/common/app.config#2211)]

1. アプリケーションで `ClientCalculator` のインスタンスを作成し、サービス操作を呼び出します。

   [!code-csharp[C_HowTo_CreateReliableSessionHTTPS#1223](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/client.cs#1223)]

1. クライアントをコンパイルして実行します。  

## <a name="net-framework-security"></a>.NET Framework のセキュリティ

このサンプルで使用される証明書は、 *Makecert*で作成されたテスト証明書であるため、ブラウザーからなどの HTTPS アドレスにアクセスしようとすると、セキュリティの警告が表示されます `https://localhost/servicemodelsamples/service.svc` 。

## <a name="see-also"></a>関連項目

- [信頼できるセッション](reliable-sessions.md)
