---
title: '方法 : WCF サービス操作を非同期に呼び出す'
description: イベントドリブンの非同期呼び出しモデルを使用してサービス操作に非同期にアクセスできる WCF クライアントを作成する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0face17f-43ca-417b-9b33-737c0fc360df
ms.openlocfilehash: aa31f64473111800f4cd01907a0446c94f368456
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247235"
---
# <a name="how-to-call-wcf-service-operations-asynchronously"></a>方法 : WCF サービス操作を非同期に呼び出す

この記事では、クライアントがサービス操作に非同期にアクセスする方法について説明します。 この記事のサービスでは、インターフェイスを実装し `ICalculator` ます。 クライアントは、イベント ドリブンの非同期呼び出しモデルを使用して、このインターフェイスで操作を非同期に呼び出すことができます  (イベントベースの非同期呼び出しモデルの詳細については、「[イベントベースの非同期パターンを使用したマルチスレッドプログラミング](../../../standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)」を参照してください)。 サービスで非同期に操作を実装する方法を示す例については、「[方法: 非同期サービス操作を実装](../how-to-implement-an-asynchronous-service-operation.md)する」を参照してください。 同期操作と非同期操作の詳細については、「[同期操作と非同期操作](../synchronous-and-asynchronous-operations.md)」を参照してください。  
  
> [!NOTE]
> <xref:System.ServiceModel.ChannelFactory%601> を使用している場合、イベント ドリブンの非同期呼び出しモデルはサポートされません。 を使用した非同期呼び出しの作成の詳細については <xref:System.ServiceModel.ChannelFactory%601> 、「[方法: チャネルファクトリを使用して非同期的に操作を呼び出す](how-to-call-operations-asynchronously-using-a-channel-factory.md)」を参照してください。  
  
## <a name="procedure"></a>手順  
  
#### <a name="to-call-wcf-service-operations-asynchronously"></a>WCF サービス操作を非同期に呼び出すには  
  
1. 次のコマンドに示すように、との両方のコマンドオプションを使用して、 [ServiceModel Metadata Utility tool (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)ツールを実行し `/async` `/tcv:Version35` ます。  
  
    ```console
    svcutil /n:http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples http://localhost:8000/servicemodelsamples/service/mex /a /tcv:Version35  
    ```  
  
     これにより、同期および標準のデリゲートベースの非同期操作に加えて、次のものを含む WCF クライアントクラスが生成されます。  
  
    - `operationName` > `Async` イベントベースの非同期呼び出し方法で使用する2つの <操作。 次に例を示します。  
  
         [!code-csharp[EventAsync#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/generatedclient.cs#1)]
         [!code-vb[EventAsync#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/generatedclient.vb#1)]  
  
    - `operationName` > `Completed` イベントベースの非同期呼び出し方法で使用するために <フォームの操作完了イベント。 次に例を示します。  
  
         [!code-csharp[EventAsync#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/generatedclient.cs#2)]
         [!code-vb[EventAsync#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/generatedclient.vb#2)]  
  
    - <xref:System.EventArgs?displayProperty=nameWithType>`operationName` > `CompletedEventArgs` イベントベースの非同期呼び出し方法で使用する各操作 (フォーム <) の型。 次に例を示します。  
  
         [!code-csharp[EventAsync#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/generatedclient.cs#3)]
         [!code-vb[EventAsync#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/generatedclient.vb#3)]  
  
2. 次のサンプル コードに示すように、呼び出し元アプリケーションで、非同期操作の完了時に呼び出されるコールバック メソッドを作成します。  
  
     [!code-csharp[EventAsync#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/client.cs#4)]
     [!code-vb[EventAsync#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/client.vb#4)]  
  
3. 操作を呼び出す前に、<型の新しいジェネリックを使用して、 <xref:System.EventHandler%601?displayProperty=nameWithType> `operationName` > `EventArgs` (前の手順で作成した) ハンドラーメソッドを <イベントに追加し `operationName` > `Completed` ます。 次に、<メソッドを呼び出し `operationName` > `Async` ます。 次に例を示します。  
  
     [!code-csharp[EventAsync#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/client.cs#5)]
     [!code-vb[EventAsync#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/client.vb#5)]  
  
## <a name="example"></a>例  
  
> [!NOTE]
> イベント ベースの非同期モデルのデザイン ガイドラインには、複数の値を返す場合に、1 つの値を `Result` プロパティとして返し、残りの値を <xref:System.EventArgs> オブジェクトのプロパティとして返すことが記載されています。 この 1 つの結果として、クライアントがイベント ベースの非同期コマンド オプションを使用してメタデータをインポートし、操作から複数の値が返される場合、既定の <xref:System.EventArgs> オブジェクトが 1 つの値を `Result` プロパティとして返し、残りの値は <xref:System.EventArgs> オブジェクトのプロパティになります。メッセージ オブジェクトを `Result` プロパティとして受け取り、返された値をそのオブジェクトのプロパティとして取得する場合は、`/messageContract` コマンド オプションを使用します。 これにより、`Result` オブジェクトの <xref:System.EventArgs> プロパティとして応答メッセージを返すシグネチャが生成されます。 すべての内部戻り値は、応答メッセージ オブジェクトのプロパティになります。  
  
 [!code-csharp[EventAsync#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/client.cs#6)]
 [!code-vb[EventAsync#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/client.vb#6)]  
  
## <a name="see-also"></a>関連項目

- [方法: 非同期サービス操作を実装する](../how-to-implement-an-asynchronous-service-operation.md)
