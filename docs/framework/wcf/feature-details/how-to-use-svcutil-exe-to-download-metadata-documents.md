---
title: '方法: Svcutil.exe を使用してメタデータ ドキュメントをダウンロードする'
description: Svcutil.exe を使用して実行中のサービスからメタデータをダウンロードし、メタデータをローカルファイルに保存する方法について説明します。
ms.date: 03/30/2017
ms.assetid: 15524274-3167-4627-b722-d6cedb9fa8c6
ms.openlocfilehash: 42df55fe7bbae6d8c977263e05053d8a8fa87aff
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246767"
---
# <a name="how-to-use-svcutilexe-to-download-metadata-documents"></a>方法: Svcutil.exe を使用してメタデータ ドキュメントをダウンロードする
Svcutil.exe を使用すると、実行中のサービスからメタデータをダウンロードして、ローカル ファイルに保存できます。 HTTP および HTTPS の URL スキームの場合、Svcutil.exe は、Ws-metadataexchange と[XML Web サービス探索](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/fxx6cfx2(v=vs.100))を使用してメタデータを取得しようとします。 その他の URL スキームの場合、Svcutil.exe は WS-MetadataExchange のみを使用します。  
  
 既定で、Svcutil.exe は <xref:System.ServiceModel.Description.MetadataExchangeBindings> クラスに定義されているバインディングを使用します。 WS-MetadataExchange で使用するバインディングを構成するには、Svcutil.exe の構成ファイル (svcutil.exe.config) でクライアント エンドポイントを定義する必要があります。このとき、クライアント エンドポイントが `IMetadataExchange` コントラクトを使用し、メタデータ エンドポイントのアドレスの URI (Uniform Resource Identifier) スキームと同じ名前を持つように定義します。  
  
> [!CAUTION]
> Svcutil.exe を実行して、それぞれに同じ名前の操作が含まれる2つの異なるサービスコントラクトを公開するサービスのメタデータを取得する場合、Svcutil.exe に "メタデータを取得できません" というエラーが表示されます。たとえば、操作を持つという名前のサービスコントラクトを公開 `ICarService` `Get(Car c)` し、同じサービスが操作を持つという名前のサービスコントラクトを公開するサービスがあるとし `IBookService` `Get(Book b)` ます。 この問題を回避するには、次のいずれかのようにします。
>
> - 操作の名前を変更する。
> - <xref:System.ServiceModel.OperationContractAttribute.Name%2A> を別の名前に設定する。
> - <xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A> プロパティを使用して、操作の名前空間のいずれかを別の名前空間に設定する。
  
## <a name="to-download-metadata-using-svcutilexe"></a>Svcutil.exe を使用してメタデータをダウンロードするには  
  
1. 次の場所で Svcutil.exe ツールを検索します。  
  
     C:\Program Files\Microsoft SDKs\Windows\v1.0.\bin  
  
2. コマンド プロンプトで、次の形式を使用してツールを起動します。  
  
    ```console
    svcutil.exe /t:metadata  <url>* | <epr>  
    ```  
  
     メタデータをダウンロードするには `/t:metadata` オプションを指定する必要があります。 このオプションを指定しないと、クライアントのコードと構成が生成されます。  
  
3. <>引数には、 `url` メタデータを提供するサービスエンドポイントの URL、またはオンラインでホストされているメタデータドキュメントを指定します。 <`epr`> 引数は、 `EndpointAddress` ws-metadataexchange をサポートするサービスエンドポイントの ws-addressing を含む XML ファイルへのパスを指定します。  
  
 メタデータのダウンロードにこのツールを使用する方法の詳細については、「 [ServiceModel Metadata Utility tool (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコマンドにより、実行中のサービスからメタデータ ドキュメントがダウンロードされます。  
  
```console
svcutil /t:metadata http://service/metadataEndpoint  
```  
  
## <a name="see-also"></a>関連項目

- [ServiceModel メタデータ ユーティリティ ツール (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)
