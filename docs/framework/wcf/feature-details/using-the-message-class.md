---
title: メッセージ クラスの使用
description: WCF の基礎となる Message クラスについて説明します。 一部の高度なシナリオでは、メッセージクラスを直接使用するようにプログラミングする必要があります。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d1d62bfb-2aa3-4170-b6f8-c93d3afdbbed
ms.openlocfilehash: f806e257cfd3ccc5118a5783e2eda48eef4ba0bf
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246494"
---
# <a name="using-the-message-class"></a>メッセージ クラスの使用
クラスは、 <xref:System.ServiceModel.Channels.Message> Windows Communication Foundation (WCF) の基本となります。 クライアントとサービスの間のすべての通信は、最終的には <xref:System.ServiceModel.Channels.Message> インスタンスの送受信となります。  
  
 通常は、<xref:System.ServiceModel.Channels.Message> クラスと直接対話することはありません。 代わりに、データコントラクト、メッセージコントラクト、操作コントラクトなどの WCF サービスモデル構造を使用して、受信メッセージと送信メッセージを記述します。 ただし、一部の高度なシナリオでは、<xref:System.ServiceModel.Channels.Message> を直接使用してプログラムを作成することができます。 たとえば、次のような場合に <xref:System.ServiceModel.Channels.Message> クラスを使用できます。  
  
- .NET Framework オブジェクトをシリアル化するのではなく、送信メッセージの内容を作成する別の方法が必要な場合 (ディスク上のファイルから直接メッセージを作成する場合など)。  
  
- .NET Framework オブジェクトに逆シリアル化するのではなく、受信メッセージの内容を使用する別の方法が必要な場合 (たとえば、生の XML コンテンツに XSLT 変換を適用する場合)。  
  
- メッセージ コンテンツに関係なく、一般的な方法でメッセージを処理する必要がある場合 (メッセージをルーティングまたは転送する場合や、ルーターシステム、負荷分散システム、または発行/定期受信システムを構築する場合など)。  
  
 クラスを使用する前に <xref:System.ServiceModel.Channels.Message> 、[データ転送アーキテクチャの概要](data-transfer-architectural-overview.md)に関する WCF データ転送アーキテクチャについて理解しておいてください。  
  
 <xref:System.ServiceModel.Channels.Message> は、一般的な目的で使用するデータ コンテナーですが、その設計は SOAP プロトコルのメッセージ設計に厳密に従っています。 SOAP と同様に、メッセージには本文とヘッダーの両方があります。 メッセージ本文には実際のペイロード データが格納され、ヘッダーには追加の名前付きデータ コンテナーが格納されます。 本文とヘッダーの読み書きルールは異なります。たとえば、ヘッダーは必ずメモリにバッファーされるので順序や回数に関係なくアクセスできますが、本文は 1 度だけ読み取ってストリーミングできます。 通常 SOAP を使用する場合、メッセージ本文は SOAP 本文にマップされ、メッセージ ヘッダーは SOAP ヘッダーにマップされます。  
  
## <a name="using-the-message-class-in-operations"></a>処理におけるメッセージ クラスの使用  
 <xref:System.ServiceModel.Channels.Message> クラスは、処理の入力パラメーター、処理の戻り値、またはその両方として使用できます。 <xref:System.ServiceModel.Channels.Message> を処理のどこかで使用する場合、次の制限が適用されます。  
  
- 処理に `out` パラメーターまたは `ref` パラメーターを含めることはできません。  
  
- 複数の `input` パラメーターを指定できません。 パラメーターがある場合は、そのパラメーターを Message 型またはメッセージ コントラクト型にする必要があります。  
  
- 戻り値の型は、`void` 型、`Message` 型、またはメッセージ コントラクト型にする必要があります。  
  
 有効な操作コントラクトを次のコード例に示します。  
  
 [!code-csharp[C_UsingTheMessageClass#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#1)]
 [!code-vb[C_UsingTheMessageClass#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#1)]  
  
## <a name="creating-basic-messages"></a>基本メッセージの作成  
 <xref:System.ServiceModel.Channels.Message> クラスには、基本メッセージを作成できる静的な `CreateMessage` ファクトリ メソッドが用意されています。  
  
 すべての `CreateMessage` オーバーロードは、<xref:System.ServiceModel.Channels.MessageVersion> 型のバージョン パラメーターを受け取ります。これは、メッセージに使用する SOAP や WS-Addressing のバージョンを示します。 受信メッセージと同じプロトコル バージョンを使用する場合は、<xref:System.ServiceModel.OperationContext.IncomingMessageVersion%2A> プロパティから取得した <xref:System.ServiceModel.OperationContext> インスタンスの <xref:System.ServiceModel.OperationContext.Current%2A> プロパティを使用できます。 また、ほとんどの `CreateMessage` オーバーロードには、メッセージで使用する SOAP アクションを示す文字列パラメーターもあります。 バージョンを `None` に設定すると、SOAP エンベロープの生成を無効にできます。この場合、メッセージは本文のみで構成されます。  
  
## <a name="creating-messages-from-objects"></a>オブジェクトからのメッセージの作成  
 最も基本的な `CreateMessage` オーバーロードは、バージョンとアクションだけを受け取り、本文が空のメッセージを作成します。 別のオーバーロードは、追加の <xref:System.Object> パラメーターを受け取ります。このオーバーロードで作成されるメッセージは、メッセージ本文が、指定されたオブジェクトでシリアル化された表現になります。 シリアル化の既定の設定で、<xref:System.Runtime.Serialization.DataContractSerializer> を使用します。 異なるシリアライザーを使用する場合、または `DataContractSerializer` の構成を変更する場合は、`CreateMessage` パラメーターも受け取る `XmlObjectSerializer` オーバーロードを使用します。  
  
 たとえば、メッセージにオブジェクトを返す場合は、次のコードを使用できます。  
  
 [!code-csharp[C_UsingTheMessageClass#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#2)]
 [!code-vb[C_UsingTheMessageClass#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#2)]  
  
## <a name="creating-messages-from-xml-readers"></a>XML リーダーからのメッセージの作成  
 `CreateMessage` オーバーロードの中には、オブジェクトの代わりに <xref:System.Xml.XmlReader> または <xref:System.Xml.XmlDictionaryReader> を本文として受け取るものがあります。 この場合、メッセージの本文には、渡された XML リーダーから読み取られた XML が格納されます。 たとえば、次のコードは、XML ファイルから読み取られた内容を本文に持つメッセージを返します。  
  
 [!code-csharp[C_UsingTheMessageClass#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#3)]
 [!code-vb[C_UsingTheMessageClass#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#3)]  
  
 さらに、本文だけではなくメッセージ全体を表す `CreateMessage` または <xref:System.Xml.XmlReader> を受け取る <xref:System.Xml.XmlDictionaryReader> オーバーロードもあります。 これらのオーバーロードは、整数の `maxSizeOfHeaders` パラメーターも受け取ります。 メッセージが作成されると直ちにヘッダーがメモリに必ずバッファーされます。このパラメーターは、発生するバッファーの量を制限します。 XML が信頼できないソースから取り込まれる場合は、このパラメーターを安全な値に設定してサービス拒否攻撃の可能性を軽減することが重要です。 XML リーダーが表す、メッセージの SOAP バージョンと WS-Addressing バージョンは、バージョン パラメーターを使用して示されるバージョンと一致する必要があります。  
  
## <a name="creating-messages-with-bodywriter"></a>BodyWriter によるメッセージの作成  
 `CreateMessage` オーバーロードの 1 つには、メッセージ本文を記述するための `BodyWriter` インスタンスを受け取るものがあります。 `BodyWriter` は、メッセージ本文の作成方法をカスタマイズするために派生させることのできる抽象クラスです。 独自の `BodyWriter` 派生クラスを作成すると、カスタマイズした方法でメッセージ本文を記述できます。 本文を書き出す処理は、`BodyWriter.OnWriteBodyContents` を受け取る <xref:System.Xml.XmlDictionaryWriter> メソッドによって行われます。したがって、このメソッドをオーバーライドする必要があります。  
  
 本文ライターでは、バッファリングを行うことも、行わないようにする (ストリームする) こともできます。 バッファリングされる本文ライターでは、その内容を何度でも出力できますが、ストリームされる本文ライターの内容は 1 度しか出力できません。 `IsBuffered` プロパティは、本文ライターがバッファリングされるかどうかを示します。 独自の本文ライターでこれを設定するには、ブール型の `BodyWriter` パラメーターを受け取る `isBuffered` プロテクト コンストラクターを呼び出します。 本文ライターでは、バッファリングされない本文ライターから、バッファリングされた本文ライターを作成することがサポートされています。 `OnCreateBufferedCopy` メソッドをオーバーライドすると、この処理をカスタマイズできます。 既定では、`OnWriteBodyContents` から返された XML が格納されているメモリ内のバッファーが使用されます。 `OnCreateBufferedCopy` は、整数の `maxBufferSize` パラメーターを受け取ります。このメソッドをオーバーライドする場合は、この最大サイズを超えるバッファーを作成しないようにする必要があります。  
  
 `BodyWriter` クラスには、`WriteBodyContents` メソッドと `CreateBufferedCopy` メソッドが用意されています。基本的にこれらは、それぞれ `OnWriteBodyContents` メソッドと `OnCreateBufferedCopy` メソッドの薄いラッパー (thin wrapper) です。 これらのメソッドは、バッファリングされない本文ライターが 2 回以上アクセスされないように状態チェックを実行します。 これらのメソッドは、`Message` に基づいたカスタム `BodyWriters` 派生クラスを作成する場合にのみ直接呼び出されます。  
  
## <a name="creating-fault-messages"></a>エラー メッセージの作成  
 特定の `CreateMessage` オーバーロードを使用して SOAP エラー メッセージを作成できます。 このオーバーロードの最も基本的なものは、エラーを説明する <xref:System.ServiceModel.Channels.MessageFault> オブジェクトを受け取ります。 他のオーバーロードは、利便性のために用意されています。 このようなオーバーロードの 1 つは、`FaultCode` と理由の文字列を受け取り、その情報を `MessageFault` で使用して `MessageFault.CreateFault` を作成します。 他のオーバーロードは、詳細オブジェクトを受け取り、そのオブジェクトをエラー コードと理由と共に `CreateFault` に渡します。 たとえば、次の操作はエラーを返します。  
  
 [!code-csharp[C_UsingTheMessageClass#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#4)]
 [!code-vb[C_UsingTheMessageClass#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#4)]  
  
## <a name="extracting-message-body-data"></a>メッセージ本文データの抽出  
 `Message` クラスでは、その本文から情報を抽出する複数の方法がサポートされています。 方法は次のカテゴリに分類されます。  
  
- XML ライターに 1 度に書き込まれるメッセージ本文全体の取得。 これを *、メッセージの書き込み*と呼びます。  
  
- メッセージ本文での XML リーダーの取得。 これにより、必要に応じてメッセージ本文に後で少しずつアクセスできます。 これは *、メッセージの読み取り*と呼ばれます。  
  
- 本文を含むメッセージ全体を、メモリ内の <xref:System.ServiceModel.Channels.MessageBuffer> 型のバッファーにコピーできます。 これは *、メッセージのコピー*と呼ばれます。  
  
 `Message` の本文には、アクセス方法に関係なく 1 回しかアクセスできません。 メッセージ オブジェクトには `State` プロパティがあります。このプロパティは Created として初期化されます。 この状態は、前の 3 つのアクセス方法により、それぞれ Written、Read、Copied に設定されます。 また、メッセージ本文の内容が不要になったときは、`Close` メソッドによって状態が Closed に設定されます。 メッセージ本文には、状態が Created の場合にのみアクセスできます。状態が変更された後で Created に戻す方法はありません。  
  
## <a name="writing-messages"></a>メッセージの書き込み  
 <xref:System.ServiceModel.Channels.Message.WriteBodyContents%28System.Xml.XmlDictionaryWriter%29> メソッドは、指定された `Message` インスタンスの本文の内容を指定された XML ライターに書き込みます。 メソッドは、 <xref:System.ServiceModel.Channels.Message.WriteBody%2A> 本文の内容を適切なラッパー要素 (たとえば、<>) に囲む点を除いて、同じことを行い `soap:body` ます。 最後の <xref:System.ServiceModel.Channels.Message.WriteMessage%2A> は、ラップしている SOAP エンベロープとヘッダーを含めて、メッセージ全体を書き込みます。 SOAP がオフになっている ( <xref:System.ServiceModel.Channels.Message.Version> が <xref:System.ServiceModel.Channels.MessageVersion.None?displayProperty=nameWithType> ) 場合、3つのメソッドはすべて同じ処理を行います。つまり、メッセージ本文の内容を書き出します。  
  
 たとえば、次のコードは、受信メッセージの本文をファイルに書き込みます。  
  
 [!code-csharp[C_UsingTheMessageClass#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#5)]
 [!code-vb[C_UsingTheMessageClass#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#5)]  
  
 さらに、特定の SOAP 開始要素タグを書き込む 2 つのヘルパー メソッドがあります。 これらのメソッドはメッセージ本文にアクセスしないため、メッセージの状態は変わりません。 次の設定があります。  
  
- <xref:System.ServiceModel.Channels.Message.WriteStartBody%2A> は、本文の開始要素を書き込みます (例 : `<soap:Body>`)。  
  
- <xref:System.ServiceModel.Channels.Message.WriteStartEnvelope%2A> は、エンベロープの開始要素を書き込みます (例 : `<soap:Envelope>`)。  
  
 対応する終了要素タグを書き込むには、対応する XML ライターで `WriteEndElement` を呼び出します。 これらのメソッドが直接呼び出されることはほとんどありません。  
  
## <a name="reading-messages"></a>メッセージの読み取り  
 メッセージ本文を読み取る主な方法は、<xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A> を呼び出すことです。 これにより、メッセージ本文の読み取りに使用できる <xref:System.Xml.XmlDictionaryReader> が取得されます。 <xref:System.ServiceModel.Channels.Message> の状態は、<xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A> が呼び出されるとすぐに Read に移行します。返された XML リーダーの使用時に移行するのではない点に注意してください。  
  
 <xref:System.ServiceModel.Channels.Message.GetBody%2A> メソッドを使用することでも、型指定されたオブジェクトとしてメッセージ本文にアクセスできます。 このメソッドは内部的に `GetReaderAtBodyContents` を使用するため、メッセージの状態は <xref:System.ServiceModel.Channels.MessageState.Read> 状態に移行します (<xref:System.ServiceModel.Channels.Message.State%2A> プロパティを参照してください)。  
  
 <xref:System.ServiceModel.Channels.Message.IsEmpty%2A> プロパティを確認することをお勧めします。このプロパティが true の場合、メッセージ本文は空であり、<xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A> から <xref:System.InvalidOperationException> がスローされます。 また、メッセージが受信メッセージ (返信など) の場合は、<xref:System.ServiceModel.Channels.Message.IsFault%2A> を確認することもできます。このプロパティは、メッセージにエラーがあるかどうかを示します。  
  
 <xref:System.ServiceModel.Channels.Message.GetBody%2A> の最も基本的なオーバーロードでは、既定の設定で構成され、<xref:System.Runtime.Serialization.DataContractSerializer> クォータが無効にされた <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A> を使用して、メッセージ本文を型のインスタンス (ジェネリック パラメーターで示される) に逆シリアル化します。 別のシリアル化エンジンを使用したり、既定以外の方法で `DataContractSerializer` を構成したりする場合は、<xref:System.ServiceModel.Channels.Message.GetBody%2A> パラメーターを受け取る <xref:System.Runtime.Serialization.XmlObjectSerializer> オーバーロードを使用します。  
  
 たとえば、次のコードは、シリアル化された `Person` オブジェクトを含むメッセージ本文からデータを抽出し、その人の名前を出力します。  
  
 [!code-csharp[C_UsingTheMessageClass#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#6)]
 [!code-vb[C_UsingTheMessageClass#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#6)]  
  
## <a name="copying-a-message-into-a-buffer"></a>バッファーへのメッセージのコピー  
 場合によっては、メッセージ本文に 2 回以上アクセスする必要が生じます。たとえば、パブリッシャー/サブスクライバー システムの一部として、同じメッセージを複数の宛先に転送する場合です。 この場合、メッセージ全体 (本文を含む) をメモリ内にバッファーする必要があります。 これを行うには、<xref:System.ServiceModel.Channels.Message.CreateBufferedCopy%28System.Int32%29> を呼び出します。 このメソッドは、最大バッファー サイズを表す整数パラメーターを受け取り、このサイズ以下のバッファーを作成します。 信頼されていないソースからメッセージを受信する場合は、これを安全な値に設定することが重要です。  
  
 バッファーは <xref:System.ServiceModel.Channels.MessageBuffer> インスタンスとして返されます。 バッファー内のデータには、いくつかの方法でアクセスできます。 中心となる方法は、<xref:System.ServiceModel.Channels.Message.CreateMessage%2A> を呼び出し、バッファーから `Message` インスタンスを作成する方法です。  
  
 バッファー内のデータにアクセスする他の方法として、<xref:System.Xml.XPath.IXPathNavigable> クラスを実装する <xref:System.ServiceModel.Channels.MessageBuffer> インターフェイスを実装し、基になる XML に直接アクセスする方法があります。 一部の <xref:System.ServiceModel.Channels.MessageBuffer.CreateNavigator%2A> オーバーロードを使用すると、ノード クォータで保護された <xref:System.Xml.XPath> ナビゲーターを作成して、アクセス可能な XML ノード数を制限できます。 これにより、非常に長い処理時間によるサービス拒否攻撃を防止できます。 このクォータは、既定では無効です。 一部の `CreateNavigator` オーバーロードでは、<xref:System.Xml.XmlSpace> 列挙体を使用して XML 内で空白を処理する方法を指定できます。既定では `XmlSpace.None` です。  
  
 メッセージ バッファーの内容にアクセスする最後の方法は、<xref:System.ServiceModel.Channels.Message.WriteMessage%2A> を使用して内容をストリームに書き込む方法です。  
  
 `MessageBuffer` を操作する手順を次の例に示します。受信メッセージを複数の受信者に転送してからファイルに記録します。 バッファリングを行わないと、メッセージの本文には 1 回しかアクセスできないため、この処理は不可能になります。  
  
 [!code-csharp[C_UsingTheMessageClass#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#7)]
 [!code-vb[C_UsingTheMessageClass#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#7)]  
  
 `MessageBuffer` クラスには、この他にも注目すべきメンバーがあります。 バッファーの内容が不要になったときは、<xref:System.ServiceModel.Channels.MessageBuffer.Close%2A> メソッドを呼び出してリソースを解放できます。 <xref:System.ServiceModel.Channels.MessageBuffer.BufferSize%2A> プロパティは、割り当てられたバッファーのサイズを返します。 <xref:System.ServiceModel.Channels.MessageBuffer.MessageContentType%2A> プロパティは、メッセージの MIME コンテンツ タイプを返します。  
  
## <a name="accessing-the-message-body-for-debugging"></a>デバッグのためのメッセージ本文へのアクセス  
 デバッグの目的では、<xref:System.ServiceModel.Channels.Message.ToString%2A> メソッドを呼び出して、メッセージの文字列表現を取得できます。 一般に、メッセージがテキスト エンコーダーでエンコードされていれば、この表現はネットワーク上でのメッセージの表示形式と一致します。ただし、XML の場合は人間にとって読みやすいように書式設定されます。 1 つの例外はメッセージ本文です。 本文は 1 度しか読み取ることができません。また、`ToString` はメッセージの状態を変更しません。 このため、 `ToString` メソッドは本体にアクセスできず、プレースホルダー (たとえば、"...") に置き換えられる可能性があります。または3つのドット) をメッセージ本文の代わりに、 したがって、メッセージ本文の内容が重要な場合は、`ToString` を使用してメッセージを記録しないでください。  
  
## <a name="accessing-other-message-parts"></a>メッセージの他の部分へのアクセス  
 メッセージの本文以外の情報にアクセスするさまざまなプロパティが用意されています。 ただし、これらのプロパティは、メッセージを閉じると呼び出すことができなくなります。  
  
- <xref:System.ServiceModel.Channels.Message.Headers%2A> プロパティは、メッセージのヘッダーを表します。 このトピックで後述する「ヘッダーの操作」のセクションを参照してください。  
  
- <xref:System.ServiceModel.Channels.Message.Properties%2A> プロパティは、メッセージ プロパティを表します。これは、メッセージに結び付けられた名前付きデータの一部で、一般的に、メッセージ送信時に送出されません。 このトピックの後の「プロパティの操作」を参照してください。  
  
- <xref:System.ServiceModel.Channels.Message.Version%2A> プロパティは、メッセージに関連付けられている SOAP と WS-Addressing のバージョンを示します。SOAP が無効の場合は `None` を示します。  
  
- <xref:System.ServiceModel.Channels.Message.IsFault%2A> プロパティは、メッセージが SOAP のエラー メッセージの場合に `true` を返します。  
  
- <xref:System.ServiceModel.Channels.Message.IsEmpty%2A> プロパティは、メッセージが空の場合に `true` を返します。  
  
 <xref:System.ServiceModel.Channels.Message.GetBodyAttribute%28System.String%2CSystem.String%29> メソッドを使用すると、特定の名前や名前空間で識別される本文のラッパー要素 (`<soap:Body>` など) の特定の属性にアクセスできます。 このような属性が見つからない場合は、`null` が返されます。 このメソッドは、`Message` の状態が Created の場合 (メッセージ本文がまだアクセスされていない場合) にのみ呼び出すことができます。  
  
## <a name="working-with-headers"></a>ヘッダーの操作  
 には、 `Message` *ヘッダー*と呼ばれる任意の数の名前付き XML フラグメントを含めることができます。 通常、各フラグメントは SOAP ヘッダーにマップされます。 ヘッダーには、`Headers` 型の <xref:System.ServiceModel.Channels.MessageHeaders> プロパティを使用してアクセスします。 <xref:System.ServiceModel.Channels.MessageHeaders> は、<xref:System.ServiceModel.Channels.MessageHeaderInfo> オブジェクトのコレクションです。個々のヘッダーには、その <xref:System.Collections.IEnumerable> インターフェイスまたはインデクサーを使用してアクセスできます。 たとえば、次のコードでは、`Message` のすべてのヘッダー名を表示します。  
  
 [!code-csharp[C_UsingTheMessageClass#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#8)]
 [!code-vb[C_UsingTheMessageClass#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#8)]  
  
#### <a name="adding-removing-finding-headers"></a>ヘッダーの追加、削除、検索  
 <xref:System.ServiceModel.Channels.MessageHeaders.Add%2A> メソッドを使用すると、新しいヘッダーを既存のすべてのヘッダーの最後に追加できます。 また、<xref:System.ServiceModel.Channels.MessageHeaders.Insert%2A> メソッドを使用すると、ヘッダーを特定のインデックスの場所に挿入できます。 挿入されたアイテムに応じて既存のヘッダーは移動します。 ヘッダーは、インデックスに従って順序付けられ、使用できる最初のインデックスは 0 です。 さまざまな <xref:System.ServiceModel.Channels.MessageHeaders.CopyHeadersFrom%2A> メソッド オーバーロードを使用して、別の `Message` や `MessageHeaders` インスタンスからヘッダーを追加できます。 一部のオーバーロードはヘッダーを 1 つだけコピーします。すべてのヘッダーをコピーする別のオーバーロードもあります。 <xref:System.ServiceModel.Channels.MessageHeaders.Clear%2A> メソッドは、すべてのヘッダーを削除します。 <xref:System.ServiceModel.Channels.MessageHeaders.RemoveAt%2A> メソッドは、特定のインデックスのヘッダーを 1 つ削除します (以降のすべてのヘッダーは移動されます)。 <xref:System.ServiceModel.Channels.MessageHeaders.RemoveAll%2A> メソッドは、特定の名前や名前空間を持つすべてのヘッダーを削除します。  
  
 <xref:System.ServiceModel.Channels.MessageHeaders.FindHeader%2A> メソッドを使用して、特定のヘッダーを取得します。 このメソッドは、検索するヘッダーの名前と名前空間を受け取り、そのインデックスを返します。 複数のヘッダーが見つかった場合は、例外がスローされます。 ヘッダーが見つからなかい場合は、-1 が返されます。  
  
 SOAP ヘッダー モデルでは、ヘッダーに `Actor` 値を持たせ、ヘッダーの受信者を指定できます。 最も基本的な `FindHeader` オーバーロードでは、メッセージの最終受信者を表すヘッダーのみを検索します。 ただし、別のオーバーロードでは、検索に含める `Actor` 値を指定できます。 詳細については、SOAP 仕様を参照してください。  
  
 ヘッダーを <xref:System.ServiceModel.Channels.MessageHeaders.CopyTo%28System.ServiceModel.Channels.MessageHeaderInfo%5B%5D%2CSystem.Int32%29> コレクションから <xref:System.ServiceModel.Channels.MessageHeaders> オブジェクトの配列にコピーする <xref:System.ServiceModel.Channels.MessageHeaderInfo> メソッドが用意されています。  
  
 ヘッダーの XML データにアクセスするには、<xref:System.ServiceModel.Channels.MessageHeaders.GetReaderAtHeader%2A> を呼び出し、特定のヘッダー インデックスの XML リーダーを返すことができます。 ヘッダーの内容をオブジェクトに逆シリアル化する場合は、<xref:System.ServiceModel.Channels.MessageHeaders.GetHeader%60%601%28System.Int32%29> または他のいずれかのオーバーロードを使用します。 最も基本的なオーバーロードは、既定の設定で構成された <xref:System.Runtime.Serialization.DataContractSerializer> を使用してヘッダーを逆シリアル化します。 異なるシリアライザーを使用したり、異なる構成の `DataContractSerializer` を使用したりする場合は、`XmlObjectSerializer` を受け取るオーバーロードの 1 つを使用します。 インデックスの代わりに、ヘッダー名、名前空間、オプションとして `Actor` 値のリストを受け取るオーバーロードもあります。これは、`FindHeader` と `GetHeader` の組み合わせです。  
  
## <a name="working-with-properties"></a>プロパティの操作  
 `Message` インスタンスには、任意の数の任意の型の名前付きオブジェクトを含めることができます。 このコレクションは、`Properties` 型の `MessageProperties` プロパティを使用してアクセスできます。 コレクションは、<xref:System.Collections.Generic.IDictionary%602> インターフェイスを実装しており、<xref:System.String> から <xref:System.Object> へのマッピングの機能を果たします。 通常、プロパティ値は、ネットワーク上のメッセージのどの部分にも直接マップされるのではなく、WCF チャネルスタックまたはサービスフレームワークのさまざまなチャネルに対して、さまざまなメッセージ処理ヒントを提供し <xref:System.ServiceModel.Channels.MessageHeaders.CopyTo%28System.ServiceModel.Channels.MessageHeaderInfo%5B%5D%2CSystem.Int32%29> ます。 例については、「[データ転送アーキテクチャの概要](data-transfer-architectural-overview.md)」を参照してください。  
  
## <a name="inheriting-from-the-message-class"></a>Message クラスからの継承  
 `CreateMessage` を使用して作成された組み込みのメッセージ型がユーザーの要件を満たさない場合は、`Message` クラスから派生するクラスを作成します。  
  
### <a name="defining-the-message-body-contents"></a>メッセージ本文の内容の定義  
 メッセージ本文内のデータにアクセスする主な手法は、書き込み、読み取り、バッファーへのコピーの 3 つです。 これらの操作は最終的に、<xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%2A> の派生クラスで、<xref:System.ServiceModel.Channels.Message.OnGetReaderAtBodyContents%2A> メソッド、<xref:System.ServiceModel.Channels.Message.OnCreateBufferedCopy%2A> メソッド、または `Message` メソッドをそれぞれ呼び出すことになります。 `Message` 基本クラスでは、これらのメソッドは `Message` インスタンスごとに 1 つしか呼び出されないようになっており、そのメソッドが 2 回以上呼び出されることもありません。 また、この基本クラスは、閉じられているメッセージでメソッドが呼び出されないことも保証します。 実装の中でメッセージ状態を追跡する必要はありません。  
  
 <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%2A> は抽象メソッドであり、実装が必要です。 メッセージの本文内容を定義する最も基本的な方法は、このメソッドを使用して書き込むことです。 たとえば、次のメッセージには 1 から 20 までの 100,000 個の乱数が含まれています。  
  
 [!code-csharp[C_UsingTheMessageClass#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#9)]
 [!code-vb[C_UsingTheMessageClass#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#9)]  
  
 <xref:System.ServiceModel.Channels.Message.OnGetReaderAtBodyContents> メソッドと <xref:System.ServiceModel.Channels.Message.OnCreateBufferedCopy%2A> メソッドには、ほとんどの場合に有効な既定の実装があります。 既定の実装は、<xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%2A> を呼び出し、結果をバッファーに格納して、格納後のバッファーを操作します。 ただし、これが十分ではない場合もあります。 前の例では、メッセージを読み込むと 100,000 個の XML 要素がバッファーに格納されることになりますが、これは望ましくありません。 <xref:System.ServiceModel.Channels.Message.OnGetReaderAtBodyContents> をオーバーライドすると、乱数を提供するカスタムの <xref:System.Xml.XmlDictionaryReader> 派生クラスを返すことができます。 次の例に示すように、をオーバーライドし <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%2A> て、メソッドが返すリーダーを使用することができ <xref:System.ServiceModel.Channels.Message.OnGetReaderAtBodyContents> ます。  
  
 [!code-csharp[C_UsingTheMessageClass#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#10)]
 [!code-vb[C_UsingTheMessageClass#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#10)]  
  
 同様に `OnCreateBufferedCopy` をオーバーライドして、独自の `MessageBuffer` 派生クラスを返すこともできます。  
  
 メッセージの派生クラスでは、メッセージ本文の内容を提供するだけでなく、`Version`、`Headers`、`Properties` の各プロパティをオーバーライドする必要もあります。  
  
 メッセージのコピーを作成した場合、作成したコピーでは、元のメッセージのメッセージ ヘッダーが使用されます。  
  
### <a name="other-members-that-can-be-overridden"></a>オーバーライド可能なその他のメンバー  
 、、およびの各メソッドをオーバーライドして <xref:System.ServiceModel.Channels.Message.OnWriteStartEnvelope%2A> 、 <xref:System.ServiceModel.Channels.Message.OnWriteStartHeaders%2A> <xref:System.ServiceModel.Channels.Message.OnWriteStartBody%2A> SOAP エンベロープ、soap ヘッダー、および soap 本文要素の開始タグの書き込み方法を指定できます。通常 `<soap:Envelope>` 、これらは、、、およびに対応 `<soap:Header>` `<soap:Body>` します。 一般的に、<xref:System.ServiceModel.Channels.Message.Version> プロパティで <xref:System.ServiceModel.Channels.MessageVersion.None> が返された場合、これらのメソッドで何も書き込まないでください。  
  
> [!NOTE]
> `OnGetReaderAtBodyContents` の既定の実装では、`OnWriteStartEnvelope` を呼び出して結果をバッファーに格納する前に、`OnWriteStartBody` と `OnWriteBodyContents` を呼び出します。 ヘッダーは書き込まれません。  
  
 <xref:System.ServiceModel.Channels.Message.OnWriteMessage%2A> メソッドをオーバーライドして、さまざまな部分からメッセージ全体を構築する方法を変更します。 `OnWriteMessage` メソッドは、<xref:System.ServiceModel.Channels.Message.WriteMessage%2A> や既定の <xref:System.ServiceModel.Channels.Message.OnCreateBufferedCopy%2A> 実装から呼び出されます。 <xref:System.ServiceModel.Channels.Message.WriteMessage%2A> をオーバーライドすることは、ベスト プラクティスではありません。 適切な `On` メソッド (たとえば、<xref:System.ServiceModel.Channels.Message.OnWriteStartEnvelope%2A>、<xref:System.ServiceModel.Channels.Message.OnWriteStartHeaders%2A>、および <xref:System.ServiceModel.Channels.BodyWriter.OnWriteBodyContents%2A>) をオーバーライドすることをお勧めします。  
  
 <xref:System.ServiceModel.Channels.Message.OnBodyToString%2A> をオーバーライドして、デバッグ中のメッセージ本文の表現方法をオーバーライドします。 既定では、3 つのドット ("...") で表されます。 このメソッドは、メッセージの状態が Closed 以外のときに複数回呼び出すことができます。 このメソッドを実装すると、1 度だけ実行する必要のある処理 (転送のみのストリームからの読み取りなど) は発生しません。  
  
 <xref:System.ServiceModel.Channels.Message.OnGetBodyAttribute%2A> メソッドをオーバーライドして、SOAP 本文要素の属性にアクセスできるようにします。 このメソッドは何度でも呼び出すことができますが、`Message` 基本型は、メッセージの状態が Created の時にのみ呼び出されることを保証します。 実装の中で状態をチェックする必要はありません。 既定の実装は、本文要素に属性がないことを示す `null` を常に返します。  
  
 メッセージ本文が必要でなくなったときに、`Message` オブジェクトに特別なクリーンアップを実行する必要がある場合は、<xref:System.ServiceModel.Channels.Message.OnClose%2A> をオーバーライドします。 既定の実装では、何も行われません。  
  
 `IsEmpty` プロパティと `IsFault` プロパティは、オーバーライド可能です。 既定では、両方とも `false` を返します。
