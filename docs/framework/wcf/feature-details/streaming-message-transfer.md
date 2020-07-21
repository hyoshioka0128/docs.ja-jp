---
title: メッセージ転送ストリーミング
ms.date: 03/30/2017
ms.assetid: 72a47a51-e5e7-4b76-b24a-299d51e0ae5a
ms.openlocfilehash: 462144856750a1b8726b574fdc82746da2d72ff7
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594791"
---
# <a name="streaming-message-transfer"></a>メッセージ転送ストリーミング
Windows Communication Foundation (WCF) トランスポートでは、メッセージを転送するための2つのモードがサポートしています。  
  
- バッファー転送では、転送が完了するまで、メッセージ全体がメモリ バッファーに保持されます。 受信側がメッセージを読み取るためには、バッファー内のメッセージが完全に配信される必要があります。  
  
- ストリーミング転送では、ストリームとしてメッセージが公開されます。 受信側は、メッセージが完全に配信される前にメッセージの処理を開始できます。  
  
- ストリーミング転送では、大容量のメモリ バッファーが不要なため、サービスのスケーラビリティを向上できます。 転送モードを変更することによってスケーラビリティが向上するかどうかは、転送されるメッセージのサイズによって決まります。 メッセージのサイズが大きい場合は、ストリーム転送の使用をお勧めします。  
  
 既定では、HTTP、TCP/IP、および名前付きパイプの各トランスポートはバッファー転送を使用します。 ここでは、これらのトランスポートをバッファー転送モードからストリーミング転送モードに切り替える方法と、その結果について説明します。  
  
## <a name="enabling-streamed-transfers"></a>ストリーミング転送の有効化  
 バッファー転送モードとストリーミング転送モードは、トランスポートのバインド要素で切り替えます。 バインディング要素には、<xref:System.ServiceModel.TransferMode> プロパティがあり、`Buffered`、`Streamed`、`StreamedRequest`、または `StreamedResponse` に設定できます。 転送モードを `Streamed` に設定すると、両方向のストリーミング通信が可能になります。 転送モードを `StreamedRequest` または `StreamedResponse` に設定すると、指定した方向のストリーミング通信だけが有効になります。  
  
 <xref:System.ServiceModel.BasicHttpBinding>、<xref:System.ServiceModel.NetTcpBinding>、および <xref:System.ServiceModel.NetNamedPipeBinding> の各バインディングは、<xref:System.ServiceModel.TransferMode> プロパティを公開します。 他のトランスポートの場合、転送モードを設定するにはカスタム バインドを作成する必要があります。  
  
 バッファー転送とストリーミング転送のどちらを使用するかは、エンドポイントごとにローカルに決定します。 HTTP トランスポートの場合、転送モードは、接続、つまりサーバーなどの中継局に伝達されません。 転送モードの設定は、サービス インターフェイスの記述に反映されません。 サービスに対してクライアント クラスを生成した後、ストリーミング転送で使用する予定のサービスの構成ファイルを編集し、転送モードを設定する必要があります。 TCP トランスポートと名前付きパイプ トランスポートの場合、転送モードはポリシー アサーションとして伝達されます。  
  
 コードサンプルについては、「[方法: ストリーミングを有効にする](how-to-enable-streaming.md)」を参照してください。  
  
## <a name="enabling-asynchronous-streaming"></a>非同期ストリーミングの有効化  
 非同期ストリーミングを有効にするには、エンドポイントの <xref:System.ServiceModel.Description.DispatcherSynchronizationBehavior> 動作をサービス ホストに追加し、その <xref:System.ServiceModel.Description.DispatcherSynchronizationBehavior.AsynchronousSendEnabled%2A> プロパティを `true` に設定します。  
  
 WCF のこのバージョンでは、他にも送信側の実際の非同期ストリーミング機能が追加されています。 これによって、複数のクライアントにメッセージをストリーム出力するシナリオで、一部のクライアントがネットワークの混雑により読み取りが遅いか、読み取りをまったく行っていない場合に、サービスのスケーラビリティが向上します。 このようなシナリオでは、WCF はクライアントごとのサービスの個別のスレッドをブロックしません。 サービスはこれによってこれまで以上のクライアントを処理できるようになり、スケーラビリティが向上します。  
  
## <a name="restrictions-on-streamed-transfers"></a>ストリーミング転送の制限  
 ストリーミング転送モードを使用すると、ランタイムによって追加の制限が適用されます。  
  
 ストリーミングされたトランスポートで発生する操作は、最大で 1 つの入力パラメーターまたは出力パラメーターが指定されたコントラクトを持つことができます。 設定するパラメーターは、メッセージの本文全体に対応し、<xref:System.ServiceModel.Channels.Message>、 <xref:System.IO.Stream> の派生型、または <xref:System.Xml.Serialization.IXmlSerializable> 実装であることが必要です。 操作の戻り値を取得することは、出力パラメーターを取得することと同じです。  
  
 信頼できるメッセージング、トランザクション、SOAP メッセージレベルのセキュリティなどの一部の WCF 機能では、送信メッセージのバッファリングに依存しています。 これらの機能を使用すると、ストリーミングによって得られるパフォーマンス上の利点が減少したり、失われたりする可能性があります。 ストリーミングされたトランスポートをセキュリティで保護する場合は、トランスポート レベルのセキュリティだけを使用するか、または、トランスポート レベルのセキュリティと認証のみのメッセージ セキュリティを組み合わせて使用してください。  
  
 SOAP ヘッダーは、転送モードがストリーミングに設定されている場合でも、必ずバッファーされます。 メッセージのヘッダーが `MaxBufferSize` トランスポート クォータのサイズを超えないようにしてください。 この設定の詳細については、「[トランスポートクォータ](transport-quotas.md)」を参照してください。  
  
## <a name="differences-between-buffered-and-streamed-transfers"></a>バッファー転送とストリーミング転送の違い  
 転送モードをバッファーからストリーミングに変更すると、TCP トランスポートと名前付きパイプ トランスポートのネイティブなチャネル形状も変更されます。 バッファー転送では、ネイティブなチャネル形状は <xref:System.ServiceModel.Channels.IDuplexSessionChannel> です。 ストリーム転送では、ネイティブなチャネル形状は <xref:System.ServiceModel.Channels.IRequestChannel> と <xref:System.ServiceModel.Channels.IReplyChannel> です。 これらのトランスポートを直接 (つまり、サービス コントラクトを介さずに) 使用する既存のアプリケーションで転送モードを変更するには、チャネル ファクトリおよびリスナーの予測されるチャネル形状を変更する必要があります。  
  
## <a name="see-also"></a>関連項目

- [方法: ストリーミングを有効にする](how-to-enable-streaming.md)
