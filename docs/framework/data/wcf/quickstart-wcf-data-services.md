---
title: クイック スタート (WCF Data Services)
ms.date: 08/24/2018
helpviewer_keywords:
- WCF Data Services, quick-start example
- WCF Data Services, Entity Data Model (EDM) service
ms.assetid: 7b18ca1e-d4d6-4c7a-afb9-ce3cebb98a8d
ms.openlocfilehash: f945d33a4fc789b3c73c1c80040fc8527301758b
ms.sourcegitcommit: 43cbde34970f5f38f30c43cd63b9c7e2e83717ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81121224"
---
# <a name="quickstart-wcf-data-services"></a>クイック スタート (WCF Data Services)

このクイックスタートでは、「[はじめに](getting-started-with-wcf-data-services.md)」のトピックをサポートする一連のタスクを通して WCF Data Services と Open Data Protocol (OData) を学習することができます。

## <a name="what-youll-learn"></a>学習内容

このクイックスタートの最初のタスクでは、データ サービスを作成し、Northwind サンプル データベースの OData フィードを公開する方法を示します。 後半のトピックでは、Web ブラウザーを使用して OData フィードにアクセスします。また、クライアント ライブラリを使用して OData フィードを使用する Windows Presentation Foundation (WPF) クライアント アプリケーションも作成します。

## <a name="prerequisites"></a>必須コンポーネント

このクイックスタートを最後まで行うには、次のコンポーネントをインストールします。

- Visual Studio

- SQL Server のインスタンス。 これには SQL Server Express が含まれます。これは、Visual Studio 2015 の既定のインストールに含まれているか、または Visual Studio 2017 以降の**データ ストレージおよび処理**ワークロードの一部として含まれています。

- Northwind サンプル データベース。 データベースをインストールするには、[Microsoft SQL Serverの Northwind および pubs サンプル データベース](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs)から Transact-SQL スクリプトを実行します。

## <a name="wcf-data-services-quickstart-tasks"></a>WCF Data Services クイックスタートのタスク

 [データ サービスを作成する](creating-the-data-service.md)

 ASP.NET アプリケーションの定義、データ モデルの定義、データ サービスの作成、およびリソースへのアクセスの有効化を行います。

 [Web ブラウザーからサービスにアクセスする](accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md)

 Visual Studio からサービスを開始し、公開されているフィードに対して Web ブラウザーから HTTP GET 要求を送信してサービスにアクセスします。

 [.NET Framework クライアント アプリケーションを作成する](creating-the-dotnet-client-application-wcf-data-services-quickstart.md)

 WPF アプリを作成して、OData フィードの使用、Windows コントロールへのデータのバインド、バインドされたコントロールのデータの変更、およびデータ サービスへの変更内容の送信を行います。

> [!NOTE]
> クイックスタートの完了バージョンからのプロジェクト ファイルは、[GitHub](https://github.com/microsoftarchive/msdn-code-gallery-community-s-z/tree/master/WCF%20Data%20Services%20Quickstart%20(OData%20Service%20and%20WPF%20Client)) からダウンロードできます。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [クイックスタートの開始](creating-the-data-service.md)

## <a name="see-also"></a>関連項目

- [ADO.NET Entity Framework](../adonet/ef/index.md)
