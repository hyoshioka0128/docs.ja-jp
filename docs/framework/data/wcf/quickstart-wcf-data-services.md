---
title: クイック スタート (WCF Data Services)
ms.date: 08/24/2018
helpviewer_keywords:
- WCF Data Services, quick-start example
- WCF Data Services, Entity Data Model (EDM) service
ms.assetid: 7b18ca1e-d4d6-4c7a-afb9-ce3cebb98a8d
ms.openlocfilehash: d0002182c5ae519c36348acdd2587bca499fe72e
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73975136"
---
# <a name="quickstart-wcf-data-services"></a>クイック スタート (WCF Data Services)

このクイックスタートでは、[はじめに](getting-started-with-wcf-data-services.md)のトピックをサポートする一連のタスクを通じて、WCF Data Services と Open Data Protocol (OData) について理解することができます。

## <a name="what-youll-learn"></a>学習する内容

このクイックスタートの最初のタスクでは、データサービスを作成して、Northwind サンプルデータベースから OData フィードを公開する方法を示します。 後のトピックでは、Web ブラウザーを使用して OData フィードにアクセスします。また、クライアントライブラリを使用して OData フィードを使用する Windows Presentation Foundation (WPF) クライアントアプリケーションを作成します。

## <a name="prerequisites"></a>必要条件

このクイック スタートを最後まで行うには、次のコンポーネントがインストールされている必要があります。

- Visual Studio

- SQL Server のインスタンス。 これには、visual Studio 2015 の既定のインストールに含まれる SQL Server Express、または Visual Studio 2017 の**データストレージと処理**ワークロードの一部として含まれるが含まれます。

- Northwind サンプル データベース。 このサンプル データベースをダウンロードするには、ダウンロード ページ「 [SQL Server 用サンプル データベース](https://go.microsoft.com/fwlink/?linkid=24758)」を参照してください。

## <a name="wcf-data-services-quickstart-tasks"></a>WCF data services クイックスタートのタスク

 [データサービスを作成する](creating-the-data-service.md)

 ASP.NET アプリケーションの定義、データ モデルの定義、データ サービスの作成、およびリソースへのアクセスの有効化を行います。

 [Web ブラウザーからサービスにアクセスする](accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md)

 Visual Studio からサービスを開始し、公開されているフィードに対して Web ブラウザーから HTTP GET 要求を送信してサービスにアクセスします。

 [.NET Framework クライアントアプリケーションを作成する](creating-the-dotnet-client-application-wcf-data-services-quickstart.md)

 OData フィードを使用する WPF アプリを作成し、データを Windows コントロールにバインドして、バインドされたコントロールのデータを変更した後、変更内容をデータサービスに送り返します。

> [!NOTE]
> クイック スタートを完了したプロジェクト ファイルは、「 [WCF Data Services ドキュメントのサンプル](https://go.microsoft.com/fwlink/?LinkId=179994) 」ページからダウンロードできます。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [クイックスタートを開始する](creating-the-data-service.md)

## <a name="see-also"></a>関連項目

- [ADO.NET Entity Framework](../adonet/ef/index.md)
