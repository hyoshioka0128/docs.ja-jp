---
title: Web ブラウザーからサービスへのアクセス (WCF Data Services クイックスタート)
description: Visual Studio で WCF Data Services を開始し、ブラウザーでフィード読み取りを無効にする方法について説明します。 サービス定義ドキュメントを取得し、データ サービス リソースにアクセスします。
ms.date: 03/30/2017
ms.assetid: 5a6fa180-3094-4e6e-ba2b-8c80975d18d1
ms.openlocfilehash: 713436c31bc3f622c4f44a83e33fff3fcbba1c1c
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247779"
---
# <a name="accessing-the-service-from-a-web-browser-wcf-data-services-quickstart"></a>Web ブラウザーからサービスへのアクセス (WCF Data Services クイックスタート)

これは、WCF Data Services クイックスタートの 2 番目のタスクです。 このタスクでは、Visual Studio から WCF Data Services を開始し、必要に応じて Web ブラウザーでのフィード読み取りを無効にします。 次に、公開されているリソースに対して Web ブラウザーから HTTP GET 要求を送信し、サービス定義ドキュメントを取得して、データ サービス リソースにアクセスします。

> [!NOTE]
> 既定では、Visual Studio によって、コンピューター上の `localhost` URI にポート番号が自動的に割り当てられます。 このタスクでは、URI の例でポート番号 `12345` を使用しています。 Visual Studio プロジェクトで特定のポート番号を設定する方法については、「[データ サービスの作成](creating-the-data-service.md)」を参照してください。

## <a name="to-request-the-default-service-document-by-using-internet-explorer"></a>Internet Explorer を使用して既定のサービス ドキュメントを要求するには

1. Internet Explorer の **[ツール]** メニューの **[インターネット オプション]** をクリックし、 **[コンテンツ]** タブの **[設定]** をクリックして **[フィードの読み取りビューを有効にする]** をオフにします。

     フィードの読み取りが無効になります。 この機能が無効でなければ、Web ブラウザーは、AtomPub エンコードのドキュメントが返されると生の XML データを表示せずに XML フィードとして処理します。

    > [!NOTE]
    > ブラウザーでフィードを生の XML データとして表示できない場合は、そのままでフィードをページのソース コードとして表示できます。

2. Visual Studio で **F5** キーを押してアプリケーションのデバッグを開始します。

3. ローカル コンピューターで Web ブラウザーを開きます。 アドレス バーに次の URI を入力します。

    ```http
    http://localhost:12345/northwind.svc
    ```

     既定のサービス ドキュメントが返されます。このドキュメントには、このデータ サービスによって公開されているエンティティ セットの一覧が含まれています。

## <a name="to-access-entity-set-resources-from-a-web-browser"></a>Web ブラウザーからエンティティ セット リソースにアクセスするには

1. Web ブラウザーのアドレス バーに次の URI を入力します。

    ```http
    http://localhost:12345/northwind.svc/Customers
    ```

     Northwind サンプル データベース内のすべての顧客のセットが返されます。

2. Web ブラウザーのアドレス バーに次の URI を入力します。

    ```http
    http://localhost:12345/northwind.svc/Customers('ALFKI')
    ```

     特定の顧客 `ALFKI` のエンティティ インスタンスが返されます。

3. Web ブラウザーのアドレス バーに次の URI を入力します。

    ```http
    http://localhost:12345/northwind.svc/Customers('ALFKI')/Orders
    ```

     顧客と注文の間のリレーションシップがスキャンされ、特定の顧客 `ALFKI` のすべての注文のセットが返されます。

4. Web ブラウザーのアドレス バーに次の URI を入力します。

    ```http
    http://localhost:12345/northwind.svc/Customers('ALFKI')/Orders?$filter=OrderID eq 10643
    ```

     特定の顧客 `ALFKI` に属する注文がフィルターされ、指定した `OrderID` 値に基づいた特定の注文だけが返されます。

## <a name="next-steps"></a>次の手順

ここでは、Web ブラウザーから特定のリソースに対して HTTP GET 要求を発行して、WCF Data Services に正常にアクセスしました。 Web ブラウザーを使用すると、リクエストのアドレス構文を試したり、結果を表示したりすることが簡単にできます。 しかし、一般的に、この方法では運用データ サービスにはアクセスできません。 通常、アプリケーションでは、アプリケーション コードまたはスクリプト言語を使用してデータ サービスと対話します。 次に、クライアント ライブラリを使用して共通言語ランタイム (CLR) オブジェクトと同様にデータ サービス リソースにアクセスするクライアント アプリケーションを作成します。

> [!div class="nextstepaction"]
> [.NET Framework クライアント アプリケーションの作成](creating-the-dotnet-client-application-wcf-data-services-quickstart.md)

## <a name="see-also"></a>関連項目

- [データ サービス リソースへのアクセス](accessing-data-service-resources-wcf-data-services.md)
