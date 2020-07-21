---
title: '方法: MetadataResolver を使用してバインディング メタデータを動的に取得する'
ms.date: 03/30/2017
ms.assetid: 56ffcb99-fff0-4479-aca0-e3909009f605
ms.openlocfilehash: 98fe4977f270b008c51039af19261ca86b8d6642
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84601128"
---
# <a name="how-to-use-metadataresolver-to-obtain-binding-metadata-dynamically"></a>方法: MetadataResolver を使用してバインディング メタデータを動的に取得する
ここでは、<xref:System.ServiceModel.Description.MetadataResolver> クラスを使用してバインディング メタデータを動的に取得する方法を示します。  
  
### <a name="to-dynamically-obtain-binding-metadata"></a>バインディング メタデータを動的に取得するには  
  
1. メタデータ エンドポイントのアドレスを持つ <xref:System.ServiceModel.EndpointAddress> オブジェクトを作成します。  
  
    ```csharp
    EndpointAddress metaAddress  
      = new EndpointAddress(new Uri("http://localhost:8080/SampleService/mex"));  
    ```  
  
2. サービス型とメタデータ エンドポイント アドレスを渡して、<xref:System.ServiceModel.Description.MetadataResolver.Resolve%28System.Type%2CSystem.ServiceModel.EndpointAddress%29> を呼び出します。 これにより、指定したコントラクトを実装したエンドポイントのコレクションが返されます。 メタデータからはバインディング情報のみがインポートされます。コントラクト情報はインポートされません。 提供されたコントラクトが代わりに使用されます。  
  
    ```csharp  
    ServiceEndpointCollection endpoints = MetadataResolver.Resolve(typeof(SampleServiceClient),metaAddress);  
    ```  
  
3. これで、サービス エンドポイントのコレクションを反復処理して必要なバインディング情報を抽出できます。 次のコードは、エンドポイントを反復処理し、現在のエンドポイントに関連付けられたバインディングとアドレスを渡すサービス クライアント オブジェクトを作成し、そのサービスでメソッドを呼び出します。  
  
    ```csharp  
    foreach (ServiceEndpoint point in endpoints)  
    {  
       if (point != null)  
       {  
          // Create a new wcfClient using retrieved endpoints.  
          using (wcfClient = new SampleServiceClient(point.Binding, point.Address))  
          {  
             Console.WriteLine(  
               wcfClient.SampleMethod("Client used the "  
               + point.Address.ToString() + " address."));  
          }  
      }  
    }  
    ```  
  
## <a name="see-also"></a>関連項目

- [Metadata](metadata.md)
