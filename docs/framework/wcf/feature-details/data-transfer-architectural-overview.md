---
title: データ転送のアーキテクチャの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data transfer [WCF], architectural overview
ms.assetid: 343c2ca2-af53-4936-a28c-c186b3524ee9
ms.openlocfilehash: f34bf82ec44140827c5d8da59911afe10ab7a853
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84576474"
---
# <a name="data-transfer-architectural-overview"></a>データ転送のアーキテクチャの概要
Windows Communication Foundation (WCF) は、メッセージングインフラストラクチャと考えることができます。 WCF は、メッセージを受信し、それらのメッセージを処理し、さらにアクションを実行するためにユーザー コードにディスパッチすることができます。また、ユーザー コードで指定されたデータからメッセージを作成し、送信先に配布することもできます。 ここでは、メッセージを処理するためのアーキテクチャと格納されるデータについて説明します。このトピックは、上級開発者を対象としています。 データを送受信する方法のより簡単なタスク指向の概要については、「 [Specifying Data Transfer in Service Contracts](specifying-data-transfer-in-service-contracts.md)」を参照してください。  
  
> [!NOTE]
> このトピックでは、WCF のオブジェクトモデルを調べても表示されない WCF 実装の詳細について説明します。 文書化された実装の詳細について、2 つの注意事項があります。 1 つは、説明が簡略化されているという点です。実際の実装は、最適化やその他の理由から、より複雑であることが考えられます。 もう 1 つの注意事項として、特定の実装の詳細が文書化されていても、その詳細に依存しないようにしてください。これらの詳細は、バージョン間で予告なしに変更されることがあるからです。これは、サービス リリースにおいても同様です。  
  
## <a name="basic-architecture"></a>基本アーキテクチャ  
 WCF メッセージ処理機能の中核となるのは、 <xref:System.ServiceModel.Channels.Message> クラスです。これについては、「 [message クラスの使用](using-the-message-class.md)」で詳しく説明されています。 WCF のランタイムコンポーネントは、チャネルスタックとサービスフレームワークという2つの主要部分に分けることができます。 <xref:System.ServiceModel.Channels.Message> クラスは接続ポイントです。  
  
 チャネル スタックは、有効な <xref:System.ServiceModel.Channels.Message> インスタンスと、メッセージ データの送信または受信に対応するアクションとの間の変換を行います。 送信側のチャネル スタックは、有効な <xref:System.ServiceModel.Channels.Message> インスタンスを取得し、何らかの処理を行った後、メッセージの送信に論理的に対応するアクションを実行します。 このアクションには、TCP パケットまたは HTTP パケットの送信、メッセージ キューへのメッセージの配置、データベースへのメッセージの書き込み、ファイル共有へのメッセージの保存、実装によって異なるその他のアクションなどがあります。 最も一般的なアクションは、ネットワーク プロトコル上でのメッセージの送信です。 受信側では、この逆のことが行われます。つまり、アクション (TCP パケットまたは HTTP パケットの到着の場合もあれば、その他のアクションの場合もあります) が検出され、チャネル スタックが処理を行った後に、このアクションを有効な <xref:System.ServiceModel.Channels.Message> インスタンスに変換します。  
  
 WCF を使用するには、 <xref:System.ServiceModel.Channels.Message> クラスとチャネルスタックを直接使用します。 ただし、この作業は困難であり、時間もかかります。 また、 <xref:System.ServiceModel.Channels.Message> オブジェクトはメタデータをサポートしていないため、この方法で wcf を使用する場合は、厳密に型指定された wcf クライアントを生成することはできません。  
  
 そのため、WCF には、オブジェクトの構築と受信に使用できる使いやすいプログラミングモデルを提供するサービスフレームワークが含まれてい `Message` ます。 サービスフレームワークは、サービスコントラクトの概念によってサービスを .NET Framework 型にマップし、属性でマークされたメソッドを単に .NET Framework するユーザー操作にメッセージをディスパッチし <xref:System.ServiceModel.OperationContractAttribute> ます (詳細については、「[サービスコントラクトの設計](../designing-service-contracts.md)」を参照してください)。 これらのメソッドは、パラメーターと戻り値を持つことができます。 サービス側では、サービス フレームワークが受信 <xref:System.ServiceModel.Channels.Message> インスタンスをパラメーターに変換し、戻り値を送信 <xref:System.ServiceModel.Channels.Message> インスタンスに変換します。 クライアント側では、この逆のことが行われます。 たとえば、次のような `FindAirfare` の操作について考えてみます。  
  
 [!code-csharp[c_DataArchitecture#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#1)]
 [!code-vb[c_DataArchitecture#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#1)]  
  
 クライアントで `FindAirfare` が呼び出されたとします。 クライアントのサービス フレームワークは、 `FromCity` パラメーターと `ToCity` パラメーターを送信 <xref:System.ServiceModel.Channels.Message> インスタンスに変換し、これをチャネル スタックに渡して送信します。  
  
 サービス側では、チャネル スタックから <xref:System.ServiceModel.Channels.Message> インスタンスが到着すると、サービス フレームワークがメッセージから関連データを抽出して `FromCity` パラメーターと `ToCity` パラメーターを設定し、サービス側の `FindAirfare` メソッドを呼び出します。 メソッドから制御が戻ると、サービス フレームワークは、返された整数値と `IsDirectFlight` 出力パラメーターを取得し、この情報を格納する <xref:System.ServiceModel.Channels.Message> オブジェクトのインスタンスを作成します。 次に、この `Message` インスタンスをチャネル スタックに渡して、クライアントに返送します。  
  
 クライアント側では、応答メッセージが格納された <xref:System.ServiceModel.Channels.Message> インスタンスが、チャネル スタックから取り出されます。 サービス フレームワークは、戻り値と `IsDirectFlight` 値を抽出し、これらをクライアントの呼び出し元に返します。  
  
## <a name="message-class"></a>Message クラス  
 <xref:System.ServiceModel.Channels.Message> クラスはメッセージの抽象表現を意図したものですが、そのデザインは SOAP メッセージと密接に関連しています。 <xref:System.ServiceModel.Channels.Message> には、情報の 3 つの主要部分であるメッセージ本文、メッセージ ヘッダー、およびメッセージ プロパティが含まれます。  
  
## <a name="message-body"></a>メッセージ本文  
 メッセージ本文は、メッセージの実際のデータ ペイロードを表すためのものです。 メッセージ本文は、常に XML Infoset として表されます。 これは、WCF で作成または受信されるすべてのメッセージが XML 形式でなければならないという意味ではありません。 メッセージ本文を解釈する方法を決定するのはチャネル スタックです。 チャネル スタックは、メッセージ本文を XML として出力する場合もあれば、他の形式に変換する場合もあります。また、メッセージ本文を完全に除外する場合もあります。 もちろん、ほとんどのバインド WCF では、メッセージ本文は SOAP エンベロープの body セクションで XML コンテンツとして表されます。  
  
 `Message` クラスは、本文を表す XML データを保持するバッファーを必ずしも含むわけではないことを認識しておくことが重要です。 `Message` には XML Infoset が論理的に含まれますが、この Infoset は動的に構築可能であると同時に、メモリ内に物理的に存在することはありません。  
  
### <a name="putting-data-into-the-message-body"></a>メッセージ本文へのデータの配置  
 メッセージ本文にデータを配置するための統一された機構はありません。 <xref:System.ServiceModel.Channels.Message> クラスには、抽象メソッド <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%28System.Xml.XmlDictionaryWriter%29>があります。このメソッドは、 <xref:System.Xml.XmlDictionaryWriter>を取得します。 <xref:System.ServiceModel.Channels.Message> クラスの各サブクラスは、このメソッドをオーバーライドし、独自のコンテンツを書き込む必要があります。 メッセージ本文には、 `OnWriteBodyContent` によって生成された XML Infoset が論理的に含まれます。 たとえば、次のような `Message` サブクラスについて考えてみます。  
  
 [!code-csharp[c_DataArchitecture#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#2)]
 [!code-vb[c_DataArchitecture#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#2)]  
  
 物理的には、 `AirfareRequestMessage` インスタンスには 2 つの文字列 ("fromCity" と "toCity") しか含まれていません。 ただし、このメッセージには、次のような XML Infoset が論理的に含まれています。  
  
```xml  
<airfareRequest>  
    <from>Tokyo</from>  
    <to>London</to>  
</airfareRequest>  
```  
  
 もちろん、このようにメッセージを作成することは、通常はありません。上記のようなメッセージは、サービス フレームワークを使用して、操作コントラクト パラメーターから作成できるためです。 さらに、 <xref:System.ServiceModel.Channels.Message> クラスには、静的 `CreateMessage` メソッドもあります。このメソッドを使用すると、一般的な種類の内容を含むメッセージ (空のメッセージ、 <xref:System.Runtime.Serialization.DataContractSerializer>によって XML にシリアル化されたオブジェクトを含むメッセージ、SOAP エラーを含むメッセージ、 <xref:System.Xml.XmlReader>によって表された XML を含むメッセージなど) を作成できます。  
  
### <a name="getting-data-from-a-message-body"></a>メッセージ本文からのデータの取得  
 メッセージ本文に格納されたデータは、主に次の 2 とおりの方法で抽出できます。  
  
- <xref:System.ServiceModel.Channels.Message.WriteBodyContents%28System.Xml.XmlDictionaryWriter%29> メソッドを呼び出し、XML ライターに渡すことにより、メッセージ本文全体を一度に取得できます。 メッセージ本文全体がこのライターに書き込まれます。 メッセージ本文全体を一度に取得することを、 *メッセージの書き込み*とも呼びます。 書き込みは、メッセージの送信時に主にチャネル スタックによって実行されます。チャネル スタックには、通常、メッセージ本文全体にアクセスし、本文全体をエンコードして送信する部分があります。  
  
- メッセージ本文から情報を取得するもう 1 つの方法は、 <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents> を呼び出し、XML リーダーを取得する方法です。 リーダーでメソッドを呼び出すことにより、必要に応じてメッセージ本文に順次アクセスできます。 メッセージ本文を少しずつ取得することを、 *メッセージの読み取り*とも呼びます。 メッセージの読み取りは、メッセージの受信時にサービス フレームワークによって主に使用されます。 たとえば、 <xref:System.Runtime.Serialization.DataContractSerializer> の使用時に、サービス フレームワークは本文で XML リーダーを取得し、逆シリアル化エンジンに渡します。逆シリアル化エンジンは、要素単位でメッセージを読み取り、対応するオブジェクト グラフの構築を開始します。  
  
 メッセージ本文を取得できるのは一度だけです。 これにより、転送専用ストリームを使用することが可能になります。 たとえば、 <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%28System.Xml.XmlDictionaryWriter%29> から読み取り、XML Infoset として結果を返す <xref:System.IO.FileStream> のオーバーライドを作成できます。 ファイルの先頭まで "巻き戻す" 必要はありません。  
  
 `WriteBodyContents` メソッドと `GetReaderAtBodyContents` メソッドは、メッセージ本文がこれまで一度も取得されていないことを簡単にチェックした後、それぞれ `OnWriteBodyContents` と `OnGetReaderAtBodyContents`を呼び出します。  
  
## <a name="message-usage-in-wcf"></a>WCF でのメッセージの使用  
 ほとんどのメッセージは、 *送信* (チャネル スタックによって送信するために、サービス フレームワークが作成するメッセージ) または *受信* (チャネル スタックから到着し、サービス フレームワークが解釈するメッセージ) のいずれかに分類できます。 さらに、チャネル スタックは、バッファー モードまたはストリーミング モードで動作できます。 また、サービス フレームワークが、ストリーム プログラミング モデルを公開する場合もあれば、非ストリーム プログラミング モデルを公開する場合もあります。 この結果として生じるケースと、その実装の簡略化した詳細を次の表に示します。  
  
|メッセージ型|メッセージの本文データ|書き込み (OnWriteBodyContents) 実装|読み取り (OnGetReaderAtBodyContents) 実装|  
|------------------|--------------------------|--------------------------------------------------|-------------------------------------------------------|  
|送信 (非ストリーム プログラミング モデルから作成)|メッセージの書き込みに必要なデータ (例 : オブジェクトとそのシリアル化に必要な <xref:System.Runtime.Serialization.DataContractSerializer> インスタンス)*|格納されたデータに基づいてメッセージを書き込むためのカスタム ロジック (例 : `WriteObject` を使用している場合に、このシリアライザーで `DataContractSerializer` を呼び出す)*|`OnWriteBodyContents`を呼び出し、結果をバッファーに保持し、バッファーで XML リーダーを返します。|  
|送信 (ストリーム プログラミング モデルから作成)|書き込むデータを含む `Stream` *|<xref:System.Xml.IStreamProvider> 機構を使用して、格納されたストリームからデータを書き込みます*。|`OnWriteBodyContents`を呼び出し、結果をバッファーに保持し、バッファーで XML リーダーを返します。|  
|ストリーミング チャネル スタックからの受信|ネットワーク上で到着したデータを表す `Stream` オブジェクトと、このオブジェクトに配置された <xref:System.Xml.XmlReader>|`XmlReader` を使用して、格納された `WriteNode`からコンテンツを書き込みます。|格納された `XmlReader`を返します。|  
|非ストリーミング チャネル スタックからの受信|本文データを格納するバッファーと、このバッファーに配置された `XmlReader`|`XmlReader` を使用して、格納された `WriteNode`からコンテンツを書き込みます。|格納された lang を返します。|  
  
 \*これらの項目は、サブクラスに直接実装されるのではなく、 `Message` クラスのサブクラスにあり <xref:System.ServiceModel.Channels.BodyWriter> ます。 の詳細については <xref:System.ServiceModel.Channels.BodyWriter> 、「 [Message クラスの使用](using-the-message-class.md)」を参照してください。  
  
## <a name="message-headers"></a>メッセージ ヘッダー  
 メッセージには、ヘッダーを含めることができます。 ヘッダーは、名前、名前空間、および他の複数のプロパティに関連付けられた XML Infoset で論理的に構成されます。 メッセージ ヘッダーには、 `Headers` の <xref:System.ServiceModel.Channels.Message>プロパティを使用してアクセスします。 各ヘッダーは、 <xref:System.ServiceModel.Channels.MessageHeader> クラスによって表されます。 通常、SOAP メッセージを使用するように構成されたチャネル スタックを使用している場合、メッセージ ヘッダーは SOAP メッセージ ヘッダーにマップされます。  
  
 メッセージ ヘッダーへの情報の配置と、メッセージ ヘッダーからの情報の抽出は、メッセージ本文を使用する場合と似ています。 ストリーミングがサポートされていないため、プロセスは若干簡略化されます。 ヘッダーは常に強制的にバッファーに保持されるため、同じヘッダーの内容に何度もアクセスすることが可能であり、各ヘッダーに任意の順序でアクセスできます。 ヘッダーで XML リーダーを取得するために使用できる汎用の機構はありませんが、 `MessageHeader` このような機能を備えた読み取り可能なヘッダーを表す、WCF の内部のサブクラスがあります。 この種の `MessageHeader` は、カスタム アプリケーション ヘッダーを持つメッセージが到着したときにチャネル スタックによって作成されます。 これにより、サービス フレームワークは、逆シリアル化エンジン ( <xref:System.Runtime.Serialization.DataContractSerializer>など) を使用してこれらのヘッダーを解釈できます。  
  
 詳細については、「 [Message クラスの使用](using-the-message-class.md)」を参照してください。  
  
## <a name="message-properties"></a>メッセージ プロパティ  
 メッセージには、プロパティを含めることができます。 *プロパティ*は、文字列名に関連付けられている任意の .NET Framework オブジェクトです。 プロパティには、 `Properties` の `Message`プロパティからアクセスします。  
  
 通常、メッセージ本文とメッセージ ヘッダーは、それぞれ SOAP 本文および SOAP ヘッダーにマップされますが、メッセージ プロパティがメッセージと共に送信または受信されることは通常ありません。 メッセージ プロパティは、チャネル スタック内のさまざまなチャネル間、およびチャネル スタックとサービス モデルの間で、メッセージに関するデータを渡す通信機構として主に存在します。  
  
 たとえば、WCF の一部として含まれる HTTP トランスポートチャネルは、クライアントに応答を送信するときに、"404 (見つかりません)" や "500 (内部サーバーエラー)" などのさまざまな HTTP ステータスコードを生成することができます。 応答メッセージを送信する前に、 `Properties` のに `Message` 型のオブジェクトを含む "httpresponse.cache" というプロパティが含まれているかどうかを確認し <xref:System.ServiceModel.Channels.HttpResponseMessageProperty> ます。 このようなプロパティが見つかった場合、 <xref:System.ServiceModel.Channels.HttpResponseMessageProperty.StatusCode%2A> プロパティを調べ、そのステータス コードを使用します。 該当のプロパティが見つからなかった場合は、既定の "200 (OK)" コードが使用されます。  
  
 詳細については、「 [Message クラスの使用](using-the-message-class.md)」を参照してください。  
  
### <a name="the-message-as-a-whole"></a>メッセージ全体  
 これまで、メッセージのさまざまな部分に個別にアクセスするためのメソッドについて説明してきましたが、 <xref:System.ServiceModel.Channels.Message> クラスには、メッセージ全体を使用するためのメソッドも用意されています。 たとえば、 `WriteMessage` メソッドは、メッセージ全体を XML ライターに書き込みます。  
  
 これを可能にするには、 `Message` インスタンス全体と XML Infoset 間のマッピングが定義されている必要があります。 実際には、このようなマッピングが存在します。 WCF は SOAP 標準を使用して、このマッピングを定義します。 `Message` インスタンスが XML Infoset として書き込まれると、書き込まれた Infoset はメッセージを含む有効な SOAP エンベロープになります。 したがって、通常、 `WriteMessage` は次の手順を実行します。  
  
1. SOAP エンベロープ要素の開始タグを書き込みます。  
  
2. SOAP ヘッダー要素の開始タグを書き込み、すべてのヘッダーを書き込んで、ヘッダー要素を閉じます。  
  
3. SOAP 本文要素の開始タグを書き込みます。  
  
4. `WriteBodyContents` または同等のメソッドを呼び出して、本文を書き込みます。  
  
5. 本文要素とエンベロープ要素を閉じます。  
  
 上記の手順は、SOAP 標準に密接に関連しています。 これは、SOAP の複数のバージョンが存在することで複雑になります。たとえば、使用している SOAP のバージョンがわからなければ、SOAP エンベロープ要素を正しく書き込むことはできません。 また、SOAP 固有のこの複雑なマッピングを完全に無効にすることが望ましい場合もあります。  
  
 このため、 `Version` には `Message`プロパティが用意されています。 このプロパティをメッセージの書き込み時に使用する SOAP バージョンに設定できます。また、 `None` に設定することで、SOAP 固有のマッピングを使用しないようにすることもできます。 `Version` プロパティを `None`に設定すると、メッセージ全体を使用するメソッドは、メッセージが本文だけで構成されている場合と同様に機能します。たとえば、 `WriteMessage` は前述の複数の手順を実行するのではなく、 `WriteBodyContents` を呼び出すだけです。 受信メッセージでは、 `Version` が自動検出され、適切に設定されることが求められます。  
  
## <a name="the-channel-stack"></a>チャネル スタック  
  
### <a name="channels"></a>チャンネル  
 既に説明したように、チャネル スタックは、送信 <xref:System.ServiceModel.Channels.Message> インスタンスをアクション (ネットワーク上でのパケットの送信など) に変換したり、アクション (ネットワーク パケットの受信など) を受信 `Message` インスタンスに変換したりする役割を担います。  
  
 チャネル スタックは、一連の順序付けられた 1 つ以上のチャネルで構成されます。 送信 `Message` インスタンスは、スタック内の最初のチャネル ( *"最上位チャネル"* とも呼ばれます) に渡され、このチャネルからスタック内の 1 つ下のチャネルに渡されます。以降、同様にスタック内の 1 つ下のチャネルに順次渡されていきます。 メッセージは、 *"トランスポート チャネル"* と呼ばれる最後のチャネルで終了します。 受信メッセージはトランスポート チャネルから始まり、スタック内の下位のチャネルから上位のチャネルに順次渡されていきます。 通常、メッセージは最上位チャネルからサービス フレームワークに渡されます。 これは、アプリケーション メッセージの通常のパターンですが、若干動作が異なるチャネルもあります。たとえば、上のチャネルからメッセージが渡されることなく、独自のインフラストラクチャ メッセージを送信する場合があります。  
  
 メッセージがスタックを通過するときに、チャネルではさまざまな方法でメッセージを処理できます。 最も一般的な処理は、送信メッセージにヘッダーを追加し、受信メッセージのヘッダーを読み取ることです。 たとえば、チャネルでメッセージのデジタル署名を計算し、ヘッダーとして追加できます。 また、受信メッセージのこのデジタル署名ヘッダーを検査し、有効な署名のないメッセージがチャネル スタック内の上位のチャネルに渡されないようにブロックすることもできます。 多くの場合、チャネルはメッセージ プロパティの設定や検査も行います。 通常、メッセージ本文は変更されませんが、これは許可されますが、たとえば、WCF セキュリティチャネルはメッセージ本文を暗号化できます。  
  
### <a name="transport-channels-and-message-encoders"></a>トランスポート チャネルとメッセージ エンコーダー  
 他のチャネルによって変更された送信 <xref:System.ServiceModel.Channels.Message>を実際に何らかのアクションに変換するのは、スタック内の最下位チャネルです。 受信側では、このチャネルがアクションを `Message` に変換して、他のチャネルが処理できるようにします。  
  
 既に説明したように、アクションはさまざまです。たとえば、各種プロトコル上でのネットワーク パケットの送信/受信、データベースでのメッセージの読み取り/書き込み、メッセージ キューへのメッセージの配置/キューからのメッセージの削除などがあります。 これらのアクションにはすべて共通するものがあります。 WCF `Message` インスタンスと、送信、受信、読み取り、書き込み、キューに登録、デキューが可能な実際のバイトグループとの間で変換を行う必要があります。 `Message` をバイト グループに変換するプロセスは *エンコード*と呼ばれ、バイト グループから `Message` を作成する逆のプロセスは *デコード*と呼ばれます。  
  
 ほとんどのトランスポート チャネルでは、 *メッセージ エンコーダー* と呼ばれるコンポーネントを使用して、エンコードとデコードの処理を行います。 メッセージ エンコーダーは、 <xref:System.ServiceModel.Channels.MessageEncoder> クラスのサブクラスです。 `MessageEncoder` には、 `ReadMessage` とバイト グループとの間の変換を行う `WriteMessage` メソッドと `Message` メソッドのさまざまなオーバーロードが含まれます。  
  
 送信側では、バッファー トランスポート チャネルが上のチャネルから受け取った `Message` オブジェクトを `WriteMessage`に渡します。 バッファー トランスポート チャネルはバイト配列を取得し、アクション (これらのバイトを有効な TCP パケットとしてパッケージングし、適切な送信先に送信するなど) を実行するために使用します。 ストリーミング トランスポート チャネルは、(たとえば、送信 TCP 接続で) まず `Stream` を作成します。次に、この `Stream` と送信に必要な `Message` の両方を適切な `WriteMessage` オーバーロードに渡し、このオーバーロードによってメッセージが書き込まれます。  
  
 受信側では、バッファー トランスポート チャネルは、(たとえば、受信 TCP パケットから) 受信バイトを配列に抽出し、 `ReadMessage` を呼び出して、チャネル スタックの上位に渡すことができる `Message` オブジェクトを取得します。 ストリーミング トランスポート チャネルは、 `Stream` オブジェクト (受信 TCP 接続のネットワーク ストリームなど) を作成し、 `ReadMessage` に渡して `Message` オブジェクトを取得します。  
  
 トランスポート チャネルとメッセージ エンコーダーの分離は必須ではありません。つまり、メッセージ エンコーダーを使用しないトランスポート チャネルの作成が可能です。 ただし、この分離には、構成しやすいという利点があります。 トランスポートチャネルでベースのみが使用されて <xref:System.ServiceModel.Channels.MessageEncoder> いる限り、任意の WCF またはサードパーティのメッセージエンコーダーで動作できます。 同様に、通常はどのトランスポート チャネルでも同じエンコーダーを使用できます。  
  
### <a name="message-encoder-operation"></a>メッセージ エンコーダーの動作  
 エンコーダーの一般的な動作を記述する場合、次の 4 つのケースについて検討すると有益です。  
  
|操作|解説|  
|---------------|-------------|  
|エンコード (バッファー)|バッファー モードでは、通常、エンコーダーは可変サイズのバッファーを作成し、このバッファーに XML ライターを作成します。 エンコーダーは、エンコードするメッセージに対して <xref:System.ServiceModel.Channels.Message.WriteMessage%28System.Xml.XmlWriter%29> を呼び出してヘッダーを書き込みます。次に、このトピックの <xref:System.ServiceModel.Channels.Message.WriteBodyContents%28System.Xml.XmlDictionaryWriter%29>に関するセクションで説明したように、 `Message` を使用して本文を書き込みます。 その後、トランスポート チャネルで使用できるように、(バイト配列として表される) バッファーの内容が返されます。|  
|エンコード (ストリーミング)|ストリーミング モードでは、動作が上記に似ていますが、より単純です。 バッファーは必要ありません。 通常、XML ライターがストリームに作成され、このライターに書き込むために <xref:System.ServiceModel.Channels.Message.WriteMessage%28System.Xml.XmlWriter%29> に対して `Message` が呼び出されます。|  
|デコード (バッファー)|バッファー モードでデコードする場合、通常、バッファーされたデータを格納する特殊な `Message` サブクラスが作成されます。 メッセージのヘッダーが読み取られ、メッセージ本文に配置する XML リーダーが作成されます。 これは、 <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents>で返されるリーダーです。|  
|デコード (ストリーミング)|ストリーミング モードでデコードする場合、通常、特殊な Message サブクラスが作成されます。 ストリームは、すべてのヘッダーを読み取り、メッセージ本文に配置できる位置まで進められます。 次に、ストリームに XML リーダーが作成されます。 これは、 <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents>で返されるリーダーです。|  
  
 エンコーダーでは、他の機能も実行できます。 たとえば、エンコーダーは XML リーダーとライターをプールできます。 新しい XML リーダーまたはライターが必要になるたびに作成すると負荷がかかります。 したがって、通常、エンコーダーは構成可能なサイズのリーダーのプールとライターのプールを保持しています。 前述のエンコーダー操作の説明では、"XML リーダー/ライターの作成" という語句が使用されている場合は、通常、"プールから取得する" または "使用できない場合に1つを作成" という意味になります。 エンコーダー (およびデコード時にエンコーダーが作成する `Message` サブクラス) には、リーダーとライターが必要でなくなったら ( `Message` を閉じたときなどに) プールに戻すためのロジックが含まれています。  
  
 WCF には3つのメッセージエンコーダーが用意されていますが、追加のカスタム型を作成することもできます。 用意されているエンコーダーは、Text、Binary、および MTOM (Message Transmission Optimization Mechanism) の 3 種類です。 これらの詳細については、「 [Choosing a Message Encoder](choosing-a-message-encoder.md)」を参照してください。  
  
### <a name="the-istreamprovider-interface"></a>IStreamProvider インターフェイス  
 ストリーミングされた本文を含む送信メッセージを XML ライターに書き込むときに、 <xref:System.ServiceModel.Channels.Message> は <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%28System.Xml.XmlDictionaryWriter%29> 実装で次のような一連の呼び出しを使用します。  
  
- ストリームの前に必要な情報を書き込みます (XML 開始タグなど)。  
  
- ストリームを書き込みます。  
  
- ストリームの後に情報を書き込みます (XML 終了タグなど)。  
  
 これは、テキスト XML エンコーディングに類似するエンコードで有効に機能します。 ただし、XML Infoset 情報 (XML 要素を開始および終了するためのタグなど) を、要素内に含まれるデータと共には配置しないエンコードもあります。 たとえば、MTOM エンコーディングでは、メッセージは複数の部分に分割されます。 ある部分に XML Infoset が含まれ、要素の実際のコンテンツについては他の部分への参照が含まれている場合があります。 通常、XML Infoset は、ストリーミングされたコンテンツと比べてサイズが小さいため、Infoset をバッファーに格納し、これを書き込んだ後に、ストリーミング方式でコンテンツを書き込むことには意味があります。 これは、終了要素タグが書き込まれるまでは、ストリームを書き込むことができないことを意味します。  
  
 このために、 <xref:System.Xml.IStreamProvider> インターフェイスが使用されます。 このインターフェイスには、書き込むストリームを返す <xref:System.Xml.IStreamProvider.GetStream> メソッドがあります。 <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%28System.Xml.XmlDictionaryWriter%29> でストリーミングされたメッセージ本文を書き込む適切な方法は次のとおりです。  
  
1. ストリームの前に必要な情報を書き込みます (XML 開始タグなど)。  
  
2. 書き込むストリームを返す `WriteValue` 実装で、 <xref:System.Xml.XmlDictionaryWriter> を受け取る <xref:System.Xml.IStreamProvider>に対して `IStreamProvider` オーバーロードを呼び出します。  
  
3. ストリームの後に情報を書き込みます (XML 終了タグなど)。  
  
 この方法を使用すると、XML ライターは <xref:System.Xml.IStreamProvider.GetStream> を呼び出し、ストリーミングされたデータを書き込む時期を選択できます。 たとえば、テキスト XML ライターやバイナリ XML ライターは、このメソッドをすぐに呼び出し、開始タグと終了タグの間にストリーミングされたコンテンツを書き込むことができます。 MTOM ライターは、メッセージの適切な部分を書き込む準備ができたときに、後で <xref:System.Xml.IStreamProvider.GetStream> を呼び出すことができます。  
  
## <a name="representing-data-in-the-service-framework"></a>サービス フレームワークでのデータの表現  
 このトピックの「基本アーキテクチャ」セクションで説明したように、サービスフレームワークは WCF の一部であり、特に、メッセージデータと実際のインスタンスのユーザーフレンドリなプログラミングモデル間の変換を行い `Message` ます。 通常、メッセージ交換は、属性でマークされた .NET Framework メソッドとしてサービスフレームワークで表され <xref:System.ServiceModel.OperationContractAttribute> ます。 このメソッドは複数のパラメーターを取得でき、戻り値または出力パラメーター (または両方) を返すことができます。 サービス側では、入力パラメーターは受信メッセージを表し、戻り値と出力パラメーターは送信メッセージを表します。 クライアント側では、この逆になります。 パラメーターと戻り値を使用してメッセージを記述するためのプログラミング モデルの詳細については、「 [Specifying Data Transfer in Service Contracts](specifying-data-transfer-in-service-contracts.md)」を参照してください。 ここでは、概要を簡単に説明します。  
  
## <a name="programming-models"></a>プログラミング モデル  
 WCF サービスフレームワークでは、メッセージを記述するための5つの異なるプログラミングモデルがサポートされています。  
  
### <a name="1-the-empty-message"></a>1.空のメッセージ  
 これは、最も簡単なケースです。 空の受信メッセージを記述する場合は、次のように入力パラメーターは使用しないでください。  
  
 [!code-csharp[C_DataArchitecture#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#3)]
 [!code-vb[C_DataArchitecture#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#3)]  
  
 空の送信メッセージを記述する場合は、次のように void 戻り値を使用し、出力パラメーターは使用しないでください。  
  
 [!code-csharp[C_DataArchitecture#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#4)]
 [!code-vb[C_DataArchitecture#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#4)]  
  
 次のように、一方向の操作コントラクトとは異なることに注意してください。  
  
 [!code-csharp[C_DataArchitecture#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#5)]
 [!code-vb[C_DataArchitecture#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#5)]  
  
 `SetDesiredTemperature` の例では、双方向メッセージ交換パターンが記述されています。 メッセージは操作から返されますが、このメッセージは空です。 操作からエラーを返すことができます。 "SetLightbulb" の例では、メッセージ交換パターンは一方向であるため、記述する送信メッセージはありません。 この場合、サービスはクライアントにステータスを通知できません。  
  
### <a name="2-using-the-message-class-directly"></a>2.Message クラスの直接使用  
 操作コントラクトで <xref:System.ServiceModel.Channels.Message> クラス (またはサブクラスのいずれか) を直接使用できます。 この場合、サービス フレームワークは、操作からチャネル スタックおよびチャネル スタックから操作に `Message` を渡すだけであり、それ以上の処理は行いません。  
  
 `Message` を直接使用するケースとして、主に 2 つのケースがあります。 1 つは、他のプログラミング モデルでは、メッセージを記述できるだけの柔軟性を得ることができない高度なシナリオで使用します。 たとえば、ディスク上のファイルを使用して、ファイルのプロパティがメッセージ ヘッダーになり、ファイルの内容がメッセージ本文になるようにメッセージを記述することが必要になる場合があります。 これは、次のように作成できます。  
  
 [!code-csharp[C_DataArchitecture#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#6)]
 [!code-vb[C_DataArchitecture#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#6)]  
  
 操作コントラクトで `Message` を一般的に使用するもう 1 つのケースは、サービスがメッセージの特定の内容に留意しているわけではなく、ブラック ボックスと同様にメッセージを処理する場合です。 たとえば、メッセージを他の複数の受信者に転送するサービスを使用することがあります。 コントラクトは、次のように作成できます。  
  
 [!code-csharp[C_DataArchitecture#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#7)]
 [!code-vb[C_DataArchitecture#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#7)]  
  
 Action = "*" 行によって、メッセージのディスパッチが実質的にオフになり、コントラクトに送信されるすべてのメッセージが操作に対して行われるようになり `IForwardingService` `ForwardMessage` ます。 (通常、ディスパッチャーは、メッセージの "Action" ヘッダーを調べて、目的の操作を判断します。 Action = " \* " は、"action header で使用可能なすべての値" を意味します。Action = "" の組み合わせ \* と、Message をパラメーターとして使用することは、すべての可能なメッセージを受信できるため、"ユニバーサルコントラクト" と呼ばれます。 可能なすべてのメッセージを送信できるようにするには、メッセージを戻り値として使用し、 `ReplyAction` を "" に設定し \* ます。 これにより、サービス フレームワークは独自の Action ヘッダーを追加できなくなるため、開発者が返す `Message` オブジェクトを使用して、このヘッダーを制御できます。  
  
### <a name="3-message-contracts"></a>3.メッセージ コントラクト  
 WCF には、メッセージ*コントラクト*と呼ばれるメッセージを記述するための宣言型プログラミングモデルが用意されています。 このモデルの詳細については、「 [Using Message Contracts](using-message-contracts.md)」を参照してください。 基本的に、メッセージ全体は、メッセージ <xref:System.ServiceModel.MessageBodyMemberAttribute> <xref:System.ServiceModel.MessageHeaderAttribute> コントラクトクラスのどの部分をメッセージのどの部分にマップする必要があるかを説明するために、やなどの属性を使用する1つの .NET Framework 型によって表されます。  
  
 メッセージ コントラクトは、結果として生成される `Message` インスタンスに対してさまざまな制御を行うことができます (ただし、 `Message` クラスを直接使用した場合と同様に制御できるわけではありません)。 たとえば、多くの場合、メッセージ本文は情報の複数の部分で構成され、各部分は独自の XML 要素によって表されます。 これらの要素は、本文に直接出現することも (*ベア* モード)、XML 要素で囲んで *ラップ* することもできます。 メッセージ コントラクト プログラミング モデルを使用すると、ベアとラップのどちらを使用するかを決定し、ラッパー名と名前空間の名前を制御できます。  
  
 前述の機能を示すメッセージ コントラクトのコード例を次に示します。  
  
 [!code-csharp[C_DataArchitecture#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#9)]
 [!code-vb[C_DataArchitecture#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#9)]  
  
 <xref:System.ServiceModel.MessageBodyMemberAttribute>、 <xref:System.ServiceModel.MessageHeaderAttribute>、または他の関連する属性を使用して、シリアル化対象としてマークされた項目は、メッセージ コントラクトに関与するためにシリアル化可能であることが必要です。 詳細については、このトピックで後述する「シリアル化」のセクションを参照してください。  
  
### <a name="4-parameters"></a>4.パラメーター  
 多くの場合、データの複数の部分に作用する操作を記述する開発者は、メッセージ コントラクトによって実現される制御のレベルを必要としていません。 たとえば、新しいサービスの作成時に、ベアとラップのどちらを使用するかを決定し、ラッパー要素名を決めることは通常望まれていません。 多くの場合、これらを決定するには Web サービスと SOAP の深い知識が必要となります。  
  
 WCF サービスフレームワークでは、ユーザーに対してこれらの選択を強制することなく、関連する複数の情報を送受信するための最適で相互運用性の高い SOAP 表現を自動的に選択できます。 これは、情報のこのような部分を操作コントラクトのパラメーターまたは戻り値として記述するだけで実現されます。 たとえば、次のような操作コントラクトについて考えてみます。  
  
 [!code-csharp[C_DataArchitecture#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#11)]
 [!code-vb[C_DataArchitecture#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#11)]  
  
 サービス フレームワークは、情報の 3 つの部分 (`customerID`、 `item`、および `quantity`) をすべてメッセージ本文に配置し、 `SubmitOrderRequest`というラッパー要素にラップすることを自動的に決定します。  
  
 より複雑なメッセージ コントラクトや `Message`ベースのプログラミング モデルに移行する特別な理由がない限り、操作コントラクト パラメーターの簡単なリストとして送信または受信するように情報を記述することをお勧めします。  
  
### <a name="5-stream"></a>5.ストリーム  
 `Stream` またはそのサブクラスのいずれかを、操作コントラクトで使用したり、メッセージ コントラクトでメッセージ本文の単独の部分として使用したりすることは、これまでに説明したものとは別のプログラミング モデルと考えることができます。 ストリーミングに対応する独自の `Stream` サブクラスを作成する場合を除き、 `Message` をこのように使用することは、コントラクトをストリーミング方式で使用できることを保証する唯一の方法です。 詳細については、「 [Large Data And Streaming](large-data-and-streaming.md)」を参照してください。  
  
 `Stream` またはそのサブクラスのいずれかをこのように使用した場合、シリアライザーは呼び出されません。 送信メッセージの場合、 `Message` インターフェイスのセクションで説明したように、特殊なストリーミング <xref:System.Xml.IStreamProvider> サブクラスが作成され、ストリームが書き込まれます。 受信メッセージの場合は、サービス フレームワークが受信メッセージに `Stream` サブクラスを作成し、操作に提供します。  
  
## <a name="programming-model-restrictions"></a>プログラミング モデルの制限  
 前述のプログラミング モデルを任意に組み合わせることはできません。 たとえば、ある操作でメッセージ コントラクトを受け入れる場合、そのメッセージ コントラクトは入力パラメーターのみであることが必要です。 さらに、操作では、空のメッセージ (戻り値の型が void) または別のメッセージ コントラクトを返す必要があります。 プログラミング モデルのこれらの制限については、各プログラミング モデルに関するトピック (「 [Using Message Contracts](using-message-contracts.md)」、「 [Using the Message Class](using-the-message-class.md)」、および「 [Large Data and Streaming](large-data-and-streaming.md)」) に記載されています。  
  
## <a name="message-formatters"></a>メッセージ フォーマッタ  
 前述の各プログラミング モデルは、 *"メッセージ フォーマッタ"* と呼ばれるコンポーネントをサービス フレームワークにプラグインすることによってサポートされます。 メッセージフォーマッタは、インターフェイスまたはインターフェイスを実装する型、または <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter> クライアントとサービスの WCF クライアントで使用するための、両方を実装する型です。  
  
 通常、メッセージ フォーマッタは動作によってプラグインされます。 たとえば、 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> は、データ コントラクト メッセージ フォーマッタをプラグインします。 これを行うには、サービス側では <xref:System.ServiceModel.Dispatcher.DispatchOperation.Formatter%2A> メソッドで <xref:System.ServiceModel.Description.IOperationBehavior.ApplyDispatchBehavior%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Dispatcher.DispatchOperation%29> を適切なフォーマッタに設定します。クライアント側では、 <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A> メソッドで <xref:System.ServiceModel.Description.IOperationBehavior.ApplyClientBehavior%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Dispatcher.ClientOperation%29> を適切なフォーマッタに設定します。  
  
 メッセージ フォーマッタが実装できるメソッドを次の表に示します。  
  
|インターフェイス|Method|アクション|  
|---------------|------------|------------|  
|<xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter>|<xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter.DeserializeRequest%28System.ServiceModel.Channels.Message%2CSystem.Object%5B%5D%29>|受信 `Message` を操作パラメーターに変換します。|  
|<xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter>|<xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter.SerializeReply%28System.ServiceModel.Channels.MessageVersion%2CSystem.Object%5B%5D%2CSystem.Object%29>|操作の戻り値または出力パラメーターから送信 `Message` を作成します。|  
|<xref:System.ServiceModel.Dispatcher.IClientMessageFormatter>|<xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.SerializeRequest%28System.ServiceModel.Channels.MessageVersion%2CSystem.Object%5B%5D%29>|操作パラメーターから送信 `Message` を作成します。|  
|<xref:System.ServiceModel.Dispatcher.IClientMessageFormatter>|<xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.DeserializeReply%28System.ServiceModel.Channels.Message%2CSystem.Object%5B%5D%29>|受信 `Message` を戻り値または出力パラメーターに変換します。|  
  
## <a name="serialization"></a>シリアル化  
 メッセージコントラクトまたはパラメーターを使用してメッセージの内容を記述するときは常に、シリアル化を使用して .NET Framework の型と XML Infoset 表現の間で変換を行う必要があります。 シリアル化は、WCF 内の他の場所で使用されます。たとえば、に <xref:System.ServiceModel.Channels.Message> は、 <xref:System.ServiceModel.Channels.Message.GetBody%2A> オブジェクトに逆シリアル化されたメッセージの本文全体を読み取るために使用できるジェネリックメソッドがあります。  
  
 WCF では、パラメーターとメッセージ部分をシリアル化および逆シリアル化するための、"すぐに使用できる" 2 つのシリアル化テクノロジがサポートされています。 <xref:System.Runtime.Serialization.DataContractSerializer> と `XmlSerializer` 。 また、カスタム シリアライザーを作成することもできます。 ただし、WCF のその他の部分 (ジェネリック `GetBody` メソッドや SOAP エラーのシリアル化など) は、サブクラスのみを使用するように制限することができます (ただし、は使用でき <xref:System.Runtime.Serialization.XmlObjectSerializer> <xref:System.Runtime.Serialization.DataContractSerializer> <xref:System.Runtime.Serialization.NetDataContractSerializer> ません <xref:System.Xml.Serialization.XmlSerializer> )。また、を使用するようにハードコーディングすることもでき <xref:System.Runtime.Serialization.DataContractSerializer> ます。  
  
 は、 `XmlSerializer` ASP.NET Web サービスで使用されるシリアル化エンジンです。 `DataContractSerializer` は、新しいデータ コントラクト プログラミング モデルを認識する新しいシリアル化エンジンです。 `DataContractSerializer` が既定で選択されています。 `XmlSerializer` を使用する場合は、 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.DataContractFormatAttribute%2A> 属性を使用して操作ごとに選択できます。  
  
 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> と <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior> は、それぞれ `DataContractSerializer` および `XmlSerializer`のメッセージ フォーマッタをプラグインする役割を担う操作の動作です。 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> の動作は、 <xref:System.Runtime.Serialization.XmlObjectSerializer>など、 <xref:System.Runtime.Serialization.NetDataContractSerializer> から派生した任意のシリアライザーで実際に操作できます (詳細については、「スタンドアロンのシリアル化の使用」を参照してください)。 この動作では、 `CreateSerializer` 仮想メソッド オーバーロードのいずれかを呼び出して、シリアライザーを取得します。 別のシリアライザーをプラグインするには、新しい <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> サブクラスを作成し、 `CreateSerializer` の両方のオーバーロードをオーバーライドします。  
  
## <a name="see-also"></a>関連項目

- [サービス コントラクトでのデータ転送の指定](specifying-data-transfer-in-service-contracts.md)
