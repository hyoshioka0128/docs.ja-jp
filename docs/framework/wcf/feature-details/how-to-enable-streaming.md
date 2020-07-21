---
title: '方法: ストリーミングを有効にする'
description: 既定のバッファー転送ではなく、WCF でストリーミングメッセージを有効にする方法について説明します。これは、処理前に完全に受信する必要があります。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6ca2cf4b-c7a1-49d8-a79b-843a90556ba4
ms.openlocfilehash: 538fd8634094aa6fbf097ddb94469d7bca749a63
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247027"
---
# <a name="how-to-enable-streaming"></a>方法: ストリーミングを有効にする
Windows Communication Foundation (WCF) は、バッファーまたはストリーム転送を使用してメッセージを送信できます。 既定のバッファー転送モードでは、受信側がメッセージを読み取る前に、メッセージの送信が完了している必要があります。 ストリーミング転送モードでは、送信が完了していなくても、受信側でメッセージの処理を開始できます。 ストリーミング モードは、渡される情報が長い場合、または連続的に処理する場合に役立ちます。 ストリーミング モードは、メッセージが大きすぎてすべてをバッファーできない場合にも役立ちます。  
  
 ストリーミングを有効にするには、`OperationContract` を適切に定義し、トランスポート レベルでストリーミングを有効にします。  
  
### <a name="to-stream-data"></a>データをストリーミングするには  
  
1. データをストリーミングするには、サービスの `OperationContract` が次の 2 つの要件を満たしている必要があります。  
  
    1. ストリーミングするデータを保持するパラメーターが、メソッド内の唯一のパラメーターになるようにします。 たとえば、入力メッセージをストリーミングする場合、厳密に 1 つの入力パラメーターが操作に含まれている必要があります。 同様に、出力メッセージをストリーミングする場合、厳密に 1 つの出力パラメーターまたは戻り値が操作に含まれている必要があります。  
  
    2. パラメーターおよび戻り値の型の少なくとも 1 つが、<xref:System.IO.Stream>、<xref:System.ServiceModel.Channels.Message> または <xref:System.Xml.Serialization.IXmlSerializable> になる必要があります。  
  
     ストリーミングされたデータのコントラクトの例を次に示します。  
  
     [!code-csharp[c_HowTo_EnableStreaming#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming/cs/service.cs#1)]
     [!code-vb[c_HowTo_EnableStreaming#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_enablestreaming/vb/service.vb#1)]  
  
     `GetStream` 操作は、バッファーされた入力データを `string` として受信し、ストリーミングされた `Stream` を返します。 逆に言えば、`UploadStream` は `Stream` (ストリーミング) を取り込んで、`bool` (バッファー) を返します。 `EchoStream` は `Stream` を出し入れします。これは、入力および出力メッセージがどちらもストリーミングされる操作の例です。 最後に、`GetReversedStream` は入力を行わずに `Stream` (ストリーミング) を返します。  
  
2. バインディングではストリーミングを有効にする必要があります。 `TransferMode` プロパティを次の値のいずれかに設定します。  
  
    1. `Buffered`,  
  
    2. `Streamed` (両方向のストリーミング通信を有効にする)。  
  
    3. `StreamedRequest` (要求に対してのみストリーミングを有効にする)。  
  
    4. `StreamedResponse` (応答に対してのみストリーミングを有効にする)。  
  
     `BasicHttpBinding` は、バインディングの `TransferMode` プロパティを公開し、`NetTcpBinding` と `NetNamedPipeBinding` も公開します。 `TransferMode` プロパティをトランスポート バインド要素に設定し、カスタム バインドで使用することもできます。  
  
     次のサンプルは、コードで `TransferMode` を設定する方法と、構成ファイルを変更して設定する方法を示しています。 どちらのサンプルも、受信可能なメッセージの最大サイズを決定する `maxReceivedMessageSize` プロパティを 64 MB に設定します。 既定の `maxReceivedMessageSize` は 64 KB です。これは、多くの場合ストリーミングを行うには小さすぎます。 アプリケーションでの受信が予想されるメッセージ最大サイズに応じて、このクォータ設定を適切に変更してください。 また、`maxBufferSize` によりバッファーの最大サイズが決定されるので、適切に設定してください。  
  
    1. 次のサンプルの構成スニペットでは、`TransferMode` とカスタム HTTP バインディングで、`basicHttpBinding` プロパティをストリーミングに設定しています。  
  
         [!code-xml[c_HowTo_EnableStreaming#103](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming/common/app.config#103)]
  
    2. 次のコード スニペットでは、`TransferMode` とカスタム HTTP バインディングで、`basicHttpBinding` プロパティをストリーミングに設定しています。  
  
         [!code-csharp[c_HowTo_EnableStreaming_code#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming_code/cs/c_howto_enablestreaming_code.cs#2)]
         [!code-vb[c_HowTo_EnableStreaming_code#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_enablestreaming_code/vb/c_howto_enablestreaming_code.vb#2)]  
  
    3. 次のコード スニペットでは、カスタム TCP バインディングで、`TransferMode` プロパティをストリーミングに設定しています。  
  
         [!code-csharp[c_HowTo_EnableStreaming_code#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming_code/cs/c_howto_enablestreaming_code.cs#3)]
         [!code-vb[c_HowTo_EnableStreaming_code#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_enablestreaming_code/vb/c_howto_enablestreaming_code.vb#3)]  
  
3. `GetStream`、`UploadStream`、および `EchoStream` の各操作では、ファイルからデータを直接送信したり、受信したデータを直接ファイルに保存します。 次のコードは、`GetStream` の例です。  
  
     [!code-csharp[c_HowTo_EnableStreaming#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming/cs/service.cs#4)]
     [!code-vb[c_HowTo_EnableStreaming#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_enablestreaming/vb/service.vb#4)]  
  
### <a name="writing-a-custom-stream"></a>カスタム ストリームの書き込み  
  
1. 送受信中のデータ ストリームの各チャンクに対して特殊な処理を行うには、<xref:System.IO.Stream> からカスタム ストリーム クラスを派生します。 カスタム ストリームの例として、`GetReversedStream` メソッドと `ReverseStream` クラスのコードを次に示します。  
  
     `GetReversedStream` では、`ReverseStream` の新しいインスタンスを作成して返します。 実際の処理は、システムが `ReverseStream` オブジェクトの読み取りを行うときに発生します。 `ReverseStream.Read` メソッドは、基になるファイルからバイトのチャンクを読み取り、バイトを反転し、その反転したバイトを返します。 このメソッドは、ファイル全体の内容を反転しません。一度に 1 つのバイト チャンクを反転します。 この例では、ストリームの内容の読み取りやストリームへの書き込み時に、ストリーミング処理を実行する方法を示します。  
  
     [!code-csharp[c_HowTo_EnableStreaming#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming/cs/service.cs#2)]
     [!code-vb[c_HowTo_EnableStreaming#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_enablestreaming/vb/service.vb#2)]  
  
## <a name="see-also"></a>関連項目

- [大規模データとストリーミング](large-data-and-streaming.md)
- [Stream](../samples/stream.md)
