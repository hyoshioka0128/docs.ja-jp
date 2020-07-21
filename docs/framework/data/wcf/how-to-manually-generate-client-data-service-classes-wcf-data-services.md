---
title: '方法: クライアント データ サービス クラスを手動で生成する (WCF Data Services)'
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, configuring
- WCF Data Services, client library
ms.assetid: b98cb1d6-956a-4e50-add6-67e4f2587346
ms.openlocfilehash: f8d99213a1ef98c48855ba9f561f87a800768c89
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894299"
---
# <a name="how-to-manually-generate-client-data-service-classes-wcf-data-services"></a>方法: クライアント データ サービス クラスを手動で生成する (WCF Data Services)
WCF Data Services を Visual Studio に統合すると、 **[サービス参照の追加]** ダイアログ ボックスを使用して参照を Visual Studio プロジェクト内のデータ サービスに追加するときに、クライアント データ サービス クラスを自動的に生成することが可能になります。 詳細については、[データ サービス参照を追加する](how-to-add-a-data-service-reference-wcf-data-services.md)」を参照してください。 コード生成ツールの `DataSvcUtil.exe` を使用して、同じクライアント データ サービス クラスを手動で生成することもできます。 WCF Data Services に含まれるこのツールでは、データ サービス定義から .NET Framework クラスが生成されます。 このツールを使用して、概念モデル (.csdl) ファイル、および Visual Studio プロジェクトの Entity Framework モデルを表す .edmx ファイルからデータ サービス クラスを生成することもできます。

 このトピックの例は、Northwind サンプル データ サービスに基づいてクライアント データ サービス クラスを作成します。 このサービスは、[WCF Data Services クイック スタート](quickstart-wcf-data-services.md)を完了したときに作成されます。 このトピックのいくつかの例では、Northwind モデルの概念モデル ファイルが必要です。 詳細については、[EdmGen.exe を使用してモデル ファイルとマッピング ファイルを生成する](../adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)」を参照してください。 このトピックのいくつかの例では、Northwind モデルの .edmx ファイルが必要です。 詳しくは、「[.edmx ファイルの概要](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))」をご覧ください。

### <a name="to-generate-c-classes-that-support-data-binding"></a>データ バインディングをサポートする C# クラスを生成するには

- コマンド プロンプトで、次のコマンド (改行なし) を実行します。

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /dataservicecollection /version:2.0 /language:CSharp /out:Northwind.cs /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > `/uri:` パラメーターの値は Northwind サンプル データ サービスのインスタンスの URI で置き換える必要があります。

### <a name="to-generate-visual-basic-classes-that-support-data-binding"></a>データ バインディングをサポートする Visual Basic クラスを生成するには

- コマンド プロンプトで、次のコマンド (改行なし) を実行します。

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /dataservicecollection /version:2.0 /language:VB /out:Northwind.vb /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > `/uri:` パラメーターの値は Northwind サンプル データ サービスのインスタンスの URI で置き換える必要があります。

### <a name="to-generate-c-classes-based-on-the-service-uri"></a>サービス URI に基づいて C# クラスを生成するには

- コマンド プロンプトで、次のコマンド (改行なし) を実行します。

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /language:CSharp /out:northwind.cs /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > `/uri:` パラメーターの値は Northwind サンプル データ サービスのインスタンスの URI で置き換える必要があります。

### <a name="to-generate-visual-basic-classes-based-on-the-service-uri"></a>サービス URI に基づいて Visual Basic クラスを生成するには

- コマンド プロンプトで、次のコマンド (改行なし) を実行します。

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /out:Northwind.vb /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > `/uri:` パラメーターの値は Northwind サンプル データ サービスのインスタンスの URI で置き換える必要があります。

### <a name="to-generate-c-classes-based-on-the-conceptual-model-file-csdl"></a>概念モデル ファイル (CSDL) に基づいて C# を生成するには

- コマンド プロンプトで、次のコマンド (改行なし) を実行します。

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:CSharp /in:Northwind.csdl /out:Northwind.cs
    ```

### <a name="to-generate-visual-basic-classes-based-on-the-conceptual-model-file-csdl"></a>概念モデル ファイル (CSDL) に基づいて Visual Basic を生成するには

- コマンド プロンプトで、次のコマンド (改行なし) を実行します。

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /in:Northwind.csdl /out:Northwind.vb
    ```

### <a name="to-generate-c-classes-based-on-the-edmx-file"></a>.edmx ファイルに基づいて C# クラスを生成するには

- コマンド プロンプトで、次のコマンド (改行なし) を実行します。

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:CSharp /in:Northwind.edmx /out:c:\northwind.cs
    ```

### <a name="to-generate-visual-basic-classes-based-on-the-edmx-file"></a>.edmx ファイルに基づいて Visual Basic クラスを生成するには

- コマンド プロンプトで、次のコマンド (改行なし) を実行します。

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /in:Northwind.edmx /out:c:\northwind.vb
    ```

## <a name="see-also"></a>関連項目

- [データ サービス クライアント ライブラリの生成](generating-the-data-service-client-library-wcf-data-services.md)
- [方法: データ サービス参照を追加する](how-to-add-a-data-service-reference-wcf-data-services.md)
- [WCF Data Service クライアント ユーティリティ (DataSvcUtil.exe) ](wcf-data-service-client-utility-datasvcutil-exe.md)
