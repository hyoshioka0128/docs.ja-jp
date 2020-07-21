---
title: セキュリティに関するデータの考慮事項
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a7eb98da-4a93-4692-8b59-9d670c79ffb2
ms.openlocfilehash: 530bb54936f97f1d7460d63cfa316c760cbd449d
ms.sourcegitcommit: 2543a78be6e246aa010a01decf58889de53d1636
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2020
ms.locfileid: "86441818"
---
# <a name="security-considerations-for-data"></a>セキュリティに関するデータの考慮事項

Windows Communication Foundation (WCF) でデータを処理する場合は、いくつかの脅威のカテゴリを考慮する必要があります。 データ処理に関連する最も重要な脅威の種類を次の表に示します。 WCF には、これらの脅威を軽減するツールが用意されています。

信頼されていないデータを受信した場合、データが受信側によって膨大な量のリソース (メモリ、スレッド、利用可能な接続、プロセッササイクルなど) にアクセスすると、時間のかかる計算が発生する可能性があります。 サーバーに対するサービス拒否攻撃によって、サーバーがクラッシュし、正当なクライアントからのメッセージを処理できなくなる場合があります。

悪意のあるコードを実行する信頼されていないデータを実行すると、受信側は意図していなかったコードを実行します。

情報漏えいリモート攻撃者は、要求に対してより多くの情報を開示するような方法で、受信側パーティが要求に応答するように強制します。

## <a name="user-provided-code-and-code-access-security"></a>ユーザー指定のコードとコード アクセス セキュリティ

Windows Communication Foundation (WCF) インフラストラクチャのさまざまな場所で、ユーザーが提供するコードを実行します。 たとえば、 <xref:System.Runtime.Serialization.DataContractSerializer> シリアル化エンジンでは、ユーザー指定のプロパティの `set` アクセサーと `get` アクセサーが呼び出されることがあります。 WCF チャネルインフラストラクチャは、クラスのユーザー指定の派生クラスを呼び出すこともでき <xref:System.ServiceModel.Channels.Message> ます。

コード作成者は、コードにセキュリティの脆弱性が存在しないことを確認する必要があります。 たとえば、整数型のデータ メンバー プロパティを使用してデータ コントラクト型を作成し、 `set` アクセサー実装でこのプロパティ値に基づいて配列を割り当てた場合、悪質なメッセージにこのデータ メンバーの極端に大きな値が含まれていると、サービス拒否攻撃の危険にさらされることになります。 一般的に、受信データに基づく割り当てや、ユーザー指定のコードでの長時間に及ぶ処理は回避します (特に、長時間に及ぶ処理が少量の受信データによって発生する可能性がある場合)。 ユーザー指定のコードのセキュリティ分析を実行するときは、必ず失敗した場合 (つまり、例外をスローするすべてのコード分岐) も考慮してください。

ユーザー指定コードの特に重要な例は、各操作に対するサービス実装内部のコードです。 サービス実装のセキュリティを確保することはユーザーの責任です。 サービス拒否の脆弱性を生じるような、セキュリティで保護されていない操作実装は、不注意によって容易に作成されてしまいます。 たとえば、文字列を受け取り、名前がその文字列で始まる顧客のリストをデータベースから返す操作があるとします。 使用しているデータベースの規模が大きく、渡された文字列が 1 文字の場合、ユーザーのコードは、使用可能なメモリより大きなメッセージを作成しようとする可能性があります。これによって、サービス全体が失敗します ( <xref:System.OutOfMemoryException> .NET Framework では回復できず、常にアプリケーションが終了します。)

悪質なコードがさまざまな機能拡張ポイントに接続されないようにする必要があります。 これが特に関係するのは、部分信頼で実行する場合、部分信頼アセンブリの型を処理する場合、または部分信頼コードで使用できるコンポーネントを作成する場合です。 詳細については、後のセクションの「部分信頼に関する脅威」を参照してください。

部分信頼で実行する場合、データ コントラクトのシリアル化インフラストラクチャがサポートするのは、データ コントラクト プログラミング モデルの一部のサブセットのみです。たとえば、 <xref:System.SerializableAttribute> 属性を使用するプライベート データ メンバーや型はサポートされません。 詳細については、「[部分信頼](partial-trust.md)」を参照してください。

## <a name="avoiding-unintentional-information-disclosure"></a>意図しない情報公開の回避

セキュリティを念頭に置いてシリアル化可能な型を設計するとき、情報の漏えい公開は考慮事項の 1 つです。

次の点を考慮してください。

- <xref:System.Runtime.Serialization.DataContractSerializer> プログラミング モデルでは、シリアル化中に型またはアセンブリの外側で、プライベートな内部データの公開が許可されます。 さらに、スキーマのエクスポート時に型の形状が公開されることがあります。 必ず、型のシリアル化射影について理解してください。 型を公開しない場合は、シリアル化を無効にします (たとえば、データ コントラクトの場合、 <xref:System.Runtime.Serialization.DataMemberAttribute> 属性を適用しないことによって無効にします)。

- 使用するシリアライザーによっては、同じ型に対して複数のシリアル化射影が存在することがあります。 また、同じ型であっても、 <xref:System.Runtime.Serialization.DataContractSerializer> を使用したときに公開されるデータ セットと、 <xref:System.Xml.Serialization.XmlSerializer>を使用したとき公開されるデータ セットが異なる可能性があります。 使用するシリアライザーを誤ると、情報の漏えいを招く場合があります。

- 従来のリモート プロシージャ コール (RPC)/エンコード モードで <xref:System.Xml.Serialization.XmlSerializer> を使用すると、送信側のオブジェクト グラフの形状が誤って受信側に公開されることがあります。

## <a name="preventing-denial-of-service-attacks"></a>サービス拒否攻撃の防止

### <a name="quotas"></a>クォータ

受信側で大量のメモリ割り当てが発生した場合、サービス拒否攻撃の可能性があります。 ここでは、主に大きいメッセージが原因で起こるメモリ消費の問題について説明しますが、攻撃には他の種類もあります。 たとえば、メッセージに過度の処理時間が使用される場合があります。

サービス拒否攻撃の緩和には通常、クォータを使用します。 クォータを超えると、通常は <xref:System.ServiceModel.QuotaExceededException> 例外がスローされます。 クォータが設定されていないと、悪質なメッセージが使用可能なすべてのメモリにアクセスし、 <xref:System.OutOfMemoryException> 例外が発生したり、使用可能なすべてのスタックにアクセスし、 <xref:System.StackOverflowException>例外が発生したりする可能性があります。

クォータが超過した状況は、回復可能です。実行中のサービスでこの状況が発生した場合、現在処理されているメッセージは破棄されますが、サービスの実行は続行され、次のメッセージが処理されます。 ただし、メモリ不足とスタックオーバーフローのシナリオは、.NET Framework のどこでも回復できません。このような例外が発生した場合、サービスは終了します。

WCF のクォータには、事前割り当ては含まれません。 たとえば、さまざまなクラスにある <xref:System.ServiceModel.Channels.TransportBindingElement.MaxReceivedMessageSize%2A> クォータを 128 KB に設定した場合、各メッセージに 128 KB が自動的に割り当てられるわけではありません。 実際の割当量は、実際の受信メッセージのサイズによって異なります。

トランスポート層には、利用できるクォータが多数あります。 使用しているトランスポート チャネル (HTTP、TCP など) によって指定されるクォータもあります。 ここでは、これらのクォータの一部について説明しますが、詳細については、「 [Transport Quotas](transport-quotas.md)」を参照してください。

### <a name="hashtable-vulnerability"></a>ハッシュ テーブルの脆弱性

データ コントラクトにハッシュ テーブルまたはコレクションが含まれている場合は脆弱性が存在します。 多数の値がハッシュ テーブルに挿入されると問題が発生します。ハッシュ テーブルでは、このような多数の値によって同じハッシュ値が生成されます。 これは、DOS 攻撃に使用される可能性があります。  この脆弱性は、MaxReceivedMessageSize binding クォータを設定することによって軽減できます。 このような攻撃を防ぐためにこのクォータを設定している場合は注意が必要です。 このクォータにより、WCF メッセージのサイズに上限が設定されます。 また、データ コントラクトではハッシュ テーブルやコレクションを使用しないようにしてください。

## <a name="limiting-memory-consumption-without-streaming"></a>メモリ消費の制限 (ストリーミングなしの場合)

大きいメッセージに関するセキュリティ モデルは、ストリーミングが使用されているかどうかによって異なります。 ストリーミングを使用しない基本的なケースでは、メッセージはメモリにバッファーされます。 この場合、 <xref:System.ServiceModel.Channels.TransportBindingElement.MaxReceivedMessageSize%2A> またはシステム指定のバインディングで <xref:System.ServiceModel.Channels.TransportBindingElement> クォータを使用して、アクセスするメッセージの最大サイズを制限することによって、サイズの大きいメッセージからシステムを保護します。 サービスが複数のメッセージを同時に処理していることがありますが、この場合、メッセージはすべてメモリ内にあります。 この脅威を軽減するには、調整機能を使用します。

また、 `MaxReceivedMessageSize` ではメッセージごとのメモリ消費に対して上限値が設定されませんが、メッセージごとのメモリ消費が定数係数以内に制限されます。 たとえば、 `MaxReceivedMessageSize` が 1 MB のときに 1 MB のメッセージを受信し、逆シリアル化した場合、逆シリアル化されたオブジェクト グラフを格納するために追加のメモリが必要となるため、メモリの総消費量が 1 MB を超えることになります。 このため、受信するデータは大きくなくてもメモリ消費量が極端に大きくなるような、シリアル化可能な型は作成しないようにします。 たとえば、50のオプションのデータメンバーフィールドと100プライベートフィールドを含むデータコントラクト "MyContract" は、XML 構築 "" を使用してインスタンス化でき \<MyContract/> ます。 この XML は、150 個のフィールドに対応するメモリにアクセスすることになります。 既定では、このデータ メンバーは省略可能です。 このような型が配列に含まれていると、問題はさらに悪化します。

`MaxReceivedMessageSize` だけでは、すべてのサービス拒否攻撃を防止できません。 たとえば、受信メッセージによって、デシリアライザーが深く入れ子になったオブジェクト グラフ (オブジェクトに別のオブジェクトが格納され、その別のオブジェクトにさらに別のオブジェクトが格納されているということが繰り返されているオブジェクト) を逆シリアル化することを強制される場合があります。 <xref:System.Runtime.Serialization.DataContractSerializer> と <xref:System.Xml.Serialization.XmlSerializer> は、このオブジェクト グラフを逆シリアル化するために入れ子形態でメソッドを呼び出します。 メソッド呼び出しがレベルの深い入れ子構造になっていると、回復不可能な <xref:System.StackOverflowException>が発生する可能性があります。 この脅威は、このトピックの後半の「XML の安全な使用」で説明するように、 <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement.MaxDepth%2A> クォータを設定して、XML の入れ子レベルを制限することによって軽減できます。

バイナリ XML エンコーディングを使用する場合は、追加のクォータを `MaxReceivedMessageSize` に設定することが特に重要です。 バイナリ エンコーディングの使用は、圧縮に似ているところがあります。受信メッセージ内の少量のバイトで、大量のデータが表されていることがあります。 したがって、 `MaxReceivedMessageSize` の制限に収まるメッセージでも、完全に展開された形式では、さらに多くのメモリを消費する可能性があります。 このような XML 固有の脅威を軽減するには、すべての XML リーダーのクォータを、このトピックの後半の「XML の安全な使用」で説明するとおりに設定する必要があります。

## <a name="limiting-memory-consumption-with-streaming"></a>メモリ消費の制限 (ストリーミングありの場合)

ストリーミング中、 `MaxReceivedMessageSize` の設定値を小さくすることで、サービス拒否攻撃を防止できます。 ただし、ストリーミングを伴う場合、状況が複雑になります。 たとえば、ファイル アップロード サービスでは使用可能なメモリより大きいファイルが許容されます。 この場合、メモリにバッファーされるデータはほとんどなく、メッセージが直接ディスクにストリーミングされると予測して、 `MaxReceivedMessageSize` を非常に大きな値に設定します。 悪意のあるメッセージが何らかの方法で、ストリーミングではなくデータをバッファーに格納する場合、は、 `MaxReceivedMessageSize` 使用可能なすべてのメモリにアクセスするメッセージから保護することができなくなります。

この脅威を軽減するために、バッファリングを制限するさまざまな WCF データ処理コンポーネントに特定のクォータ設定が存在します。 この中で最も重要なのは、複数のトランスポート バインド要素と標準バインディングに存在する `MaxBufferSize` プロパティです。 ストリーミングを使用する場合は、メッセージごとに割り当て可能なメモリの最大量を考慮して、このクォータを設定する必要があります。 `MaxReceivedMessageSize`と同様、この設定ではメモリ消費の絶対的な最大値が設定されるのではなく、メモリ消費が定数係数以内に制限されるだけです。 また、 `MaxReceivedMessageSize`の場合と同じく、複数のメッセージが同時に処理されている可能性もあります。

### <a name="maxbuffersize-details"></a>MaxBufferSize の詳細

プロパティは、 `MaxBufferSize` WCF が行うすべての一括バッファリングを制限します。 たとえば、WCF では、常に SOAP ヘッダーと SOAP エラー、およびメッセージ伝送最適化メカニズム (MTOM) メッセージの自然な読み取り順序ではないと検出された MIME パートがバッファーに格納されます。 この設定では、このようなすべての状況でバッファー量が制限されます。

WCF では、バッファーに格納さ `MaxBufferSize` れる可能性のあるさまざまなコンポーネントに値を渡すことによってこれを実現します。 たとえば、 <xref:System.ServiceModel.Channels.Message.CreateMessage%2A> クラスの一部の <xref:System.ServiceModel.Channels.Message> オーバーロードは、 `maxSizeOfHeaders` パラメーターを受け取ります。 WCF は、 `MaxBufferSize` このパラメーターに値を渡して、SOAP ヘッダーのバッファー量を制限します。 <xref:System.ServiceModel.Channels.Message> クラスを直接使用する場合、このパラメーターを設定することが重要です。 一般に、クォータパラメーターを受け取る WCF のコンポーネントを使用する場合は、これらのパラメーターのセキュリティへの影響を理解し、それらを正しく設定することが重要です。

MTOM メッセージ エンコーダーには、 `MaxBufferSize` 設定もあります。 標準バインディングを使用する場合、この値は自動的にトランスポート レベルの `MaxBufferSize` に設定されます。 ただし、MTOM メッセージ エンコーダーのバインド要素を使用してカスタム バインディングを作成する場合、ストリーミングの使用時には `MaxBufferSize` プロパティを安全な値に設定することが重要です。

## <a name="xml-based-streaming-attacks"></a>XML ベースのストリーミング攻撃

`MaxBufferSize`だけでは、ストリーミングが予想される場合に WCF を強制的にバッファリングできないようにするだけでは不十分です。 たとえば、WCF XML リーダーは、新しい要素の読み取りを開始するときに、XML 要素の開始タグ全体を常にバッファーに格納します。 この処理は、名前空間と属性を適切に処理するために行われます。 (たとえば、大きいファイルを直接ディスクにストリーミングするシナリオを可能にする目的で) `MaxReceivedMessageSize` が大きい値に設定されている場合、メッセージの本文全体が大きい XML 要素の開始タグであるような、悪質なメッセージが作成される可能性があります。 このメッセージを読み取ろうとすると、 <xref:System.OutOfMemoryException>が発生します。 これは、xml ベースのサービス拒否攻撃の1つであり、このトピックの後半の「XML の安全な使用」で説明されている xml リーダーのクォータを使用してすべて軽減できます。 ストリーミングを使用する場合、これらのクォータをすべて設定することが特に重要です。

### <a name="mixing-streaming-and-buffering-programming-models"></a>ストリーミングとバッファー プログラミング モデルの混在

攻撃の多くは、同じサービス内にストリーミングとストリーミング以外のプログラミング モデルを混在させることによって発生することが考えられます。 2 つの操作が設定されたサービス コントラクトがあるとします。一方は <xref:System.IO.Stream> を使用し、他方はカスタム型の配列を使用します。 また、1 つ目の操作で、大きいストリームを処理できるように、 `MaxReceivedMessageSize` が大きい値に設定されているとします。 この場合、大きいメッセージを 2 つ目の操作でも受け取れることになってしまいます。デシリアライザーは、操作が呼び出される前にデータを配列としてメモリにバッファー化します。 この状況では、サービス拒否攻撃が発生する可能性があります。 `MaxBufferSize` クォータでは、メッセージ本文のサイズ、つまり、デシリアライザーが処理するデータのサイズは制限できません。

このため、同じコントラクトにストリーム ベースの操作とストリーム以外の操作を混合しないようにしてください。 この 2 つのプログラミング モデルを混合する必要がある場合は、次の予防策を使用します。

- <xref:System.Runtime.Serialization.IExtensibleDataObject> の <xref:System.ServiceModel.ServiceBehaviorAttribute.IgnoreExtensionDataObject%2A> プロパティを <xref:System.ServiceModel.ServiceBehaviorAttribute> に設定して、 `true`機能を無効にします。 これによって、コントラクトの一部であるメンバーだけが逆シリアル化されます。

- <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A> の <xref:System.Runtime.Serialization.DataContractSerializer> プロパティを安全な値に設定します。 このクォータは、 <xref:System.ServiceModel.ServiceBehaviorAttribute> 属性または構成からも操作できます。 このクォータは、1 回の逆シリアル化で逆シリアル化されるオブジェクトの数を制限します。 通常、1 回の逆シリアル化で、メッセージ コントラクト内の 1 つの操作パラメーターまたはメッセージ本文が逆シリアル化されます。 配列を逆シリアル化する場合、各配列エントリは個別のオブジェクトとしてカウントされます。

- すべての XML リーダーのクォータを安全な値に設定します。 <xref:System.Xml.XmlDictionaryReaderQuotas.MaxDepth%2A>、 <xref:System.Xml.XmlDictionaryReaderQuotas.MaxStringContentLength%2A>、および <xref:System.Xml.XmlDictionaryReaderQuotas.MaxArrayLength%2A> に注意して、ストリーミング以外の操作で文字列の使用を避けます。

- 既知の型のリストを確認し、ここにある型はいつでもインスタンス化が可能であることを覚えておいてください (このトピックの後半の「意図しない型の読み込み防止」を参照)。

- <xref:System.Xml.Serialization.IXmlSerializable> インターフェイスを実装して大量のデータをバッファー化する型は使用しないようにします。 このような型は既知の型のリストに追加しないでください。

- <xref:System.Xml.XmlElement>、 <xref:System.Xml.XmlNode> 、 <xref:System.Byte> の各配列や、 <xref:System.Runtime.Serialization.ISerializable> を実装する型をコントラクトで使用しないでください。

- <xref:System.Xml.XmlElement>、 <xref:System.Xml.XmlNode> 、 <xref:System.Byte> の各配列や、 <xref:System.Runtime.Serialization.ISerializable> を実装する型は、既知の型のリストで使用しないでください。

前述の予防策は、ストリーミング以外の操作で <xref:System.Runtime.Serialization.DataContractSerializer>を使用する場合に適用できます。 <xref:System.Xml.Serialization.XmlSerializer>を使用している場合、これには <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.MaxItemsInObjectGraph%2A> クォータによる保護がないので、同じサービスにストリーミングとストリーミング以外のプログラミング モデルを絶対に混在させないでください。

### <a name="slow-stream-attacks"></a>遅いストリームによる攻撃

ストリーミング サービス拒否攻撃では、メモリ消費は発生しません。 代わりに、この攻撃では送信側または受信側でデータの転送が遅くなります。 データが送信または受信されるのを待っている間、スレッドや利用可能な接続などのリソースが消耗します。 この状況は、悪質な攻撃を受けた結果として、または正当な送信側または受信側が遅いネットワーク接続を使用していることが原因で起こる可能性があります。

この攻撃を軽減するには、トランスポートのタイムアウトを適切に設定します。 詳細については、「[トランスポートクォータ](transport-quotas.md)」を参照してください。 第2に、 `Read` `Write` WCF でストリームを操作するときは、同期または操作を使用しないでください。

## <a name="using-xml-safely"></a>XML の安全な使用

> [!NOTE]
> このセクションは XML に関するものですが、ここに記載された情報は、JSON (JavaScript Object Notation) ドキュメントにも該当します。 [Mapping Between JSON and XML](mapping-between-json-and-xml.md)を使用することで、クォータは同様に機能します。

### <a name="secure-xml-readers"></a>セキュリティで保護された XML リーダー

XML Infoset は、WCF でのすべてのメッセージ処理の基礎を形成します。 信頼できない送信元からの XML データを受け入れる場合、多数のサービス拒否攻撃が存在する可能性があり、これを軽減する必要があります。 WCF は、特別なセキュリティで保護された XML リーダーを提供します。 これらのリーダーは、WCF の標準エンコーディング (テキスト、バイナリ、MTOM) のいずれかを使用するときに自動的に作成されます。

このリーダーでは、一部のセキュリティ機能が常にアクティブです。 たとえば、このリーダーは文書型定義 (DTD) を処理しません。文書型定義は、サービス拒否攻撃のソースの 1 つになり得るものであり、正当な SOAP メッセージに使用すべきではありません。 他のセキュリティ機能としてリーダーのクォータがあり、これらを設定する必要があります。この機能については、次のセクションで説明します。

XML リーダーを直接操作する場合 (独自のカスタムエンコーダーを作成する場合や、クラスを直接操作する場合など <xref:System.ServiceModel.Channels.Message> ) は、信頼されていないデータを処理する可能性がある場合は常に、WCF のセキュリティで保護されたリーダーを使用します。 セキュリティで保護されたリーダーは、 <xref:System.Xml.XmlDictionaryReader.CreateTextReader%2A>クラス上で <xref:System.Xml.XmlDictionaryReader.CreateBinaryReader%2A>、 <xref:System.Xml.XmlDictionaryReader.CreateMtomReader%2A> 、または <xref:System.Xml.XmlDictionaryReader> の静的ファクトリ メソッドのオーバーロードのいずれかを呼び出すことによって作成します。 リーダーを作成したら、安全なクォータ値を渡します。 `Create` メソッドのオーバーロードを呼び出さないでください。 これらの方法では、WCF リーダーは作成されません。 作成されるのは、このセクションで説明したセキュリティ機能で保護されていないリーダーです。

### <a name="reader-quotas"></a>リーダーのクォータ

セキュリティで保護された XML リーダーには、5 つの設定可能なクォータがあります。 これらのクォータは通常、標準バインディングまたはエンコーディング バインド要素で `ReaderQuotas` プロパティを使用するか、リーダーの作成時に渡される <xref:System.Xml.XmlDictionaryReaderQuotas> オブジェクトを使用して設定します。

#### <a name="maxbytesperread"></a>MaxBytesPerRead

このクォータは、要素の開始タグとその属性を読み取るときに、1 回の `Read` 操作で読み取るバイト数を制限します (ストリーミングを使用しない場合、要素名自体がクォータに照らし合わせてカウントされることはありません)。 <xref:System.Xml.XmlDictionaryReaderQuotas.MaxBytesPerRead%2A> が重要な理由は、次のとおりです。

- 要素名とその属性は、読み取り時に必ずメモリ内でバッファー化されます。 このため、ストリーミングが予想されるときにこのクォータをストリーミング モードで適切に設定して、過度のバッファーを防止することが重要です。 実行されるバッファリングの実際の量については、 `MaxDepth` クォータのセクションを参照してください。

- XML 属性が多すぎると、属性名は一意かどうかを確認する必要があるため、処理時間が大幅に増加する可能性があります。 `MaxBytesPerRead` によってこの脅威を軽減できます。

#### <a name="maxdepth"></a>MaxDepth

このクォータは、XML 要素の入れ子の深さの最大値を制限します。 たとえば、ドキュメント "" の \<A> \<B> \<C/> \</B> \</A> 入れ子の深さは3です。 <xref:System.Xml.XmlDictionaryReaderQuotas.MaxDepth%2A> が重要な理由は、次のとおりです。

- `MaxDepth` は `MaxBytesPerRead`と相互に関係しています。リーダーは常に、現在の要素とそのすべての先祖に関するデータをメモリ内に維持します。このため、リーダーのメモリ消費の最大値は、この 2 つの設定値の積に比例します。

- 深く入れ子になったオブジェクト グラフを逆シリアル化する場合、デシリアライザーはスタック全体にアクセスし、回復不可能な <xref:System.StackOverflowException>をスローするしかありません。 <xref:System.Runtime.Serialization.DataContractSerializer> の場合も <xref:System.Xml.Serialization.XmlSerializer>の場合も、XML の入れ子構造とオブジェクトの入れ子構造との間に直接的な相関関係が存在します。 この脅威を軽減するには、 `MaxDepth` を使用します。

#### <a name="maxnametablecharcount"></a>MaxNameTableCharCount

このクォータは、リーダーの *nametable*のサイズを制限します。 nametable には、XML ドキュメントを処理するときに出現する特定の文字列 (名前空間やプレフィックスなど) が入っています。 この文字列はメモリ内でバッファー化されるので、ストリーミングが予想されるときは、このクォータを設定して過度のバッファーを防止します。

#### <a name="maxstringcontentlength"></a>MaxStringContentLength

このクォータは、XML リーダーが返す文字列の最大サイズを制限します。 このクォータは、XML リーダー自体のメモリ消費は制限しませんが、このリーダーを使用するコンポーネントのメモリ消費を制限します。 たとえば、 <xref:System.Runtime.Serialization.DataContractSerializer> が <xref:System.Xml.XmlDictionaryReaderQuotas.MaxStringContentLength%2A>でセキュリティ保護されたリーダーを使用するときは、このクォータを超える文字列を逆シリアル化することはありません。 <xref:System.Xml.XmlDictionaryReader> クラスを直接使用すると、すべてのメソッドではなく、文字列を読み取ることを目的としたメソッド ( <xref:System.Xml.XmlDictionaryReader.ReadContentAsString%2A> メソッドなど) だけがこのクォータに従います。 リーダー上の <xref:System.Xml.XmlReader.Value%2A> プロパティはこのクォータの影響を受けないので、このクォータによる保護が必要な場合はこのプロパティを使用しないでください。

#### <a name="maxarraylength"></a>MaxArrayLength

このクォータは、XML リーダーが返すプリミティブ配列 (バイト配列など) の最大サイズを制限します。 このクォータは、XML リーダー自体のメモリ消費は制限しませんが、このリーダーを使用するコンポーネントのメモリ消費を制限します。 たとえば、 <xref:System.Runtime.Serialization.DataContractSerializer> が <xref:System.Xml.XmlDictionaryReaderQuotas.MaxArrayLength%2A>でセキュリティ保護されたリーダーを使用するときは、このクォータを超えるバイト配列を逆シリアル化することはありません。 1 つのコントラクトでストリーミングとバッファー プログラミング モデルを混合する場合は、このクォータを設定することが重要です。 <xref:System.Xml.XmlDictionaryReader> クラスを直接使用すると、特定のプリミティブ型の任意のサイズの配列を読み取ることを目的としたメソッド ( <xref:System.Xml.XmlDictionaryReader.ReadInt32Array%2A>メソッドなど) だけがこのクォータに従います。

## <a name="threats-specific-to-the-binary-encoding"></a>バイナリ エンコーディングに固有の脅威

WCF でサポートされるバイナリ XML エンコーディングには、*ディクショナリ文字列*機能が含まれています。 長い文字列をわずかなバイト数でエンコードすることができます。 これによって、パフォーマンスは大幅に向上しますが、新たなサービス拒否攻撃の脅威を招き、その対策が必要になります。

ディクショナリには、 *静的ディクショナリ* と *動的ディクショナリ*の 2 種類があります。 静的ディクショナリは、バイナリ エンコーディングで短いコードを使用して表現できる長い文字列の組み込みリストです。 この文字列のリストは、リーダーの作成時に固定され、変更できません。 WCF が既定で使用する静的ディクショナリ内の文字列は、重大なサービス拒否攻撃の脅威をもたらすために十分な大きさではありませんが、ディクショナリ拡張攻撃でも使用される可能性があります。 独自の静的ディクショナリを使用する高度なシナリオでは、長いディクショナリ文字列を追加するときに注意が必要です。

動的ディクショナリ機能では、メッセージで独自の文字列を定義し、その文字列を短いコードに関連付けることができます。 この文字列とコードのマッピングは、通信セッション中にメモリに格納されるので、後続のメッセージは文字列を再送信する必要がなく、既に定義されているコードを利用できます。 この文字列は、任意の長さになるので、静的ディクショナリの場合よりも重大な脅威を招く可能性があります。

軽減する必要がある第 1 の脅威は、動的ディクショナリ (文字列とコードのマッピング テーブル) が大きくなりすぎる可能性です。 このディクショナリは、複数のメッセージを処理するうちに拡大する可能性があります。`MaxReceivedMessageSize` クォータは各メッセージに個別に適用されるだけなので、このクォータで保護することはできません。 このため、 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.MaxSessionSize%2A> にはディクショナリのサイズを制限する個別の <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement> プロパティがあります。

他のほとんどのクォータと異なり、このクォータはメッセージの書き込み時にも適用されます。 メッセージの読み取り時にこのクォータを超えた場合は、 `QuotaExceededException` が通常どおりスローされます。 メッセージの書き込み時にこのクォータを超えた場合は、クォータの超過を引き起こす文字列はそのまま書き込まれますが、動的ディクショナリ機能は使用されません。

### <a name="dictionary-expansion-threats"></a>ディクショナリ拡大攻撃

重大なバイナリ固有の攻撃は、ディクショナリの拡大が原因で発生します。 文字列ディクショナリ機能を利用した場合、バイナリ形式の小さいメッセージが、完全に展開されたテキスト形式では非常に大きいメッセージになることがあります。 動的ディクショナリの文字列がディクショナリ全体の最大サイズを超えることはないため、動的ディクショナリの文字列の拡大要因は、 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.MaxSessionSize%2A> クォータで制限できます。

<xref:System.Xml.XmlDictionaryReaderQuotas.MaxNameTableCharCount%2A>、 `MaxStringContentLength`、および `MaxArrayLength` の各プロパティで制限されるのは、メモリ消費だけです。 メモリ使用量は `MaxReceivedMessageSize`によって既に制限されているため、通常、ストリーミングを使用しない状況で脅威を軽減するためにこれらのプロパティを使用する必要はありません。 ただし、 `MaxReceivedMessageSize` では、展開前のバイト数がカウントされます。 バイナリ エンコーディングを使用しているとき、メモリ消費は、 `MaxReceivedMessageSize`という因数によってのみ制限される、 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.MaxSessionSize%2A>を超える可能性があります。 このため、バイナリ エンコーディングを使用するときはすべてのリーダーのクォータ (特に <xref:System.Xml.XmlDictionaryReaderQuotas.MaxStringContentLength%2A>) を必ず設定することが重要です。

<xref:System.Runtime.Serialization.DataContractSerializer>と共にバイナリ エンコーディングを使用する場合、 `IExtensibleDataObject` インターフェイスを誤用して、ディクショナリ拡大攻撃を引き起こす可能性があります。 このインターフェイスは、コントラクトの一部でない任意のデータに対して無制限のストレージを提供します。 `MaxSessionSize` に `MaxReceivedMessageSize` を掛けた値によって問題が起こらない程度に低くクォータを設定できない場合は、バイナリ エンコーディングを使用するときに `IExtensibleDataObject` 機能を無効にします。 `IgnoreExtensionDataObject` 属性では `true` プロパティを `ServiceBehaviorAttribute` に設定します。 または `IExtensibleDataObject` インターフェイスを実装しないという方法もあります。 詳細については、「[上位互換性のあるデータ コントラクト](forward-compatible-data-contracts.md)」を参照してください。

### <a name="quotas-summary"></a>クォータの概要

次の表では、クォータを使用するときのヒントを示します。

|条件|設定が重要なクォータ|
|---------------|-----------------------------|
|ストリーミングのない、またはストリーミングのある小さいメッセージ、テキスト、MTOM エンコーディング|`MaxReceivedMessageSize`、`MaxBytesPerRead`、`MaxDepth`|
|ストリーミングのない、またはストリーミングのある小さいメッセージ、バイナリ エンコーディング|`MaxReceivedMessageSize`、 `MaxSessionSize`、およびすべての `ReaderQuotas`|
|大きいストリーミング メッセージ、テキスト、MTOM エンコーディング|`MaxBufferSize` およびすべての `ReaderQuotas`|
|大きいストリーミング メッセージ、バイナリ エンコーディング|`MaxBufferSize`、 `MaxSessionSize`、およびすべての `ReaderQuotas`|

- トランスポート レベルのタイムアウトを常に設定する必要があります。ストリーミングを使用するときは、ストリーミングするメッセージが大きいか小さいかに関係なく、同期読み取りと書き込みを使用しないでください。

- クォータについて確信がない場合は、そのクォータを未決定のままにするのではなく、安全な値を設定します。

## <a name="preventing-malicious-code-execution"></a>悪質なコードの実行の防止

主に、次の種類の脅威が、コードを実行し、意図しない結果をもたらす可能性があります。

- デシリアライザーが、悪質、安全でない、またはセキュリティに注意する必要がある型を読み込んでしまう。

- 受信メッセージが原因で、デシリアライザーが通常は安全な型のインスタンスを作成する際に、意図しない結果を引き起こすようなインスタンスが生成されてしまう。

次の各セクションで、これらの種類の脅威について詳しく説明します。

## <a name="datacontractserializer"></a>DataContractSerializer

(のセキュリティ情報につい <xref:System.Xml.Serialization.XmlSerializer> ては、関連するドキュメントを参照してください。)のセキュリティモデルは、 <xref:System.Xml.Serialization.XmlSerializer> のセキュリティモデルと似ていますが、ほとんどの場合、 <xref:System.Runtime.Serialization.DataContractSerializer> 詳細は異なります。 たとえば、型を含めるために、 <xref:System.Xml.Serialization.XmlIncludeAttribute> 属性ではなく <xref:System.Runtime.Serialization.KnownTypeAttribute> 属性が使用されます。 <xref:System.Xml.Serialization.XmlSerializer> に固有のいくつかの脅威については、このトピックの後半で説明します。

### <a name="preventing-unintended-types-from-being-loaded"></a>意図しない型の読み込み防止

意図しない型を読み込むと、その型が悪質である場合も、単にセキュリティに影響するような副作用がある型の場合も、重大な結果を引き起こす可能性があります。 型は、悪用されやすいセキュリティの脆弱性を含んでいたり、その型のコンストラクターまたはクラス コンストラクターでセキュリティに影響するアクションを実行したりする可能性があります。また、サービス拒否攻撃の実行を容易にしてしまうほどメモリ フットプリントが大きい場合や、回復不可能な例外をスローする場合もあります。 型には、インスタンスが作成されるよりも前に、その型が読み込まれると直ちに実行されるクラス コンストラクターが用意されている可能性があります。 これらの理由から、デシリアライザーがどのような型を読み込むかを制御することが重要です。

<xref:System.Runtime.Serialization.DataContractSerializer> での逆シリアル化は、疎結合的な方法で行われます。 共通言語ランタイム (CLR) 型とアセンブリ名は、受信データから読み取られません。 これは、 <xref:System.Xml.Serialization.XmlSerializer>の動作と似ていますが、 <xref:System.Runtime.Serialization.NetDataContractSerializer>、 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>、および <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>の動作とは異なります。 疎結合的な方法をとることによって、ある程度の安全を確保できます。リモートの攻撃者は、メッセージ内で型の名前を示すだけでは、意図した型が読み込まれるように指定することができません。

<xref:System.Runtime.Serialization.DataContractSerializer> は常に、コントラクトに基づいて現在予期される型を読み込むことができます。 たとえば、データ コントラクトに `Customer`型のデータ メンバーが含まれている場合、 <xref:System.Runtime.Serialization.DataContractSerializer> は、このデータ メンバーを逆シリアル化するときに `Customer` 型を読み込むことができます。

また、 <xref:System.Runtime.Serialization.DataContractSerializer> はポリモーフィズムをサポートします。 データ メンバーを <xref:System.Object>として宣言しておき、受信データに `Customer` インスタンスを含めることができます。 これが可能なのは、次のいずれかのメカニズムにより、 `Customer` 型がデシリアライザーに対して既知の型になっている場合だけです。

- 型に<xref:System.Runtime.Serialization.KnownTypeAttribute> 属性を適用する。

- `KnownTypeAttribute` 属性で、型のリストを返すメソッドを指定する。

- `ServiceKnownTypeAttribute` 属性を使用する。

- `KnownTypes` 構成セクションを使用する。

- 構築時に <xref:System.Runtime.Serialization.DataContractSerializer> に既知の型のリストを明示的に渡す (シリアライザーを直接使用している場合)。

これらのメカニズムを使用すると、デシリアライザーが読み込むことのできる型が追加されるので、攻撃を受け得る表面積は拡大します。 既知の型リストに、悪質な型または意図しない型が追加されることのないように、これらのメカニズムを制御する必要があります。

型が既知の型リストに追加されると、コントラクトでその型の使用が禁止されている場合でも、その型をいつでも読み込むことができ、その型のインスタンスを作成できるようになります。 たとえば、前述のメカニズムのいずれかを使用して "MyDangerousType" という型が既知の型のリストに追加されるとします。 これは、次のことを意味します。

- `MyDangerousType` が読み込まれ、そのクラス コンストラクターが実行されます。

- 文字列データ メンバーが指定されたデータ コントラクトを逆シリアル化している場合でも、悪質なメッセージによって `MyDangerousType` のインスタンスが作成される可能性があります。 プロパティの setter など、 `MyDangerousType`のコードが実行される可能性があります。 その後で、デシリアライザーが文字列データ メンバーにこのインスタンスを割り当てる動作を試行し、例外が発生して失敗します。

既知の型のリストを返すメソッドを作成する場合、またはリストを直接 <xref:System.Runtime.Serialization.DataContractSerializer> コンストラクターに渡す場合は、リストを準備するためのコードをセキュリティで保護し、信頼されたデータだけを操作対象にします。

構成で既知の型を指定する場合は、構成ファイルをセキュリティで保護します。 構成では必ず厳密な名前を使用します (型が含まれている署名付きアセンブリの公開キーを指定します)。ただし、読み込む型のバージョンは指定しないでください。 型ローダーにより、可能であれば最新のバージョンが自動的に選択されます。 セキュリティの脆弱性を持つ型の場合、その脆弱性が今後のバージョンで修正される可能性があります。しかし、構成でバージョンを明示的に指定していると、脆弱なバージョンが引き続き読み込まれます。構成で特定のバージョンを指定した場合には、このリスクを負うことになります。

既知の型が多すぎると、もう 1 つ問題が生じます。 <xref:System.Runtime.Serialization.DataContractSerializer> は、アプリケーション ドメインでシリアル化コードまたは逆シリアル化コードのキャッシュを作成し、シリアル化または逆シリアル化する必要がある型ごとにエントリを作成します。 このキャッシュは、アプリケーション ドメインの実行中はクリアされません。 このため、アプリケーションに多くの既知の型が使用されていることを知る攻撃者は、これらの既知の型がすべて逆シリアル化され、キャッシュで大量のメモリが消費されるように仕向けることが可能です。

### <a name="preventing-types-from-being-in-an-unintended-state"></a>型の意図しない状態の防止

型には、従う必要がある内部の一貫性に対する制約が存在することがあります。 逆シリアル化中にこの制約に違反しないように注意する必要があります。

次の型は、宇宙船でのエアロックの状態を表します。この型では、内側のドアと外側のドアを両方同時に開くことはできないという制約が適用されます。

[!code-csharp[DataContractAttribute#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/datacontractattribute/cs/overview.cs#3)]
[!code-vb[DataContractAttribute#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/datacontractattribute/vb/overview.vb#3)]

攻撃者は、次のような悪質なメッセージを送信することによってこの制約を迂回し、オブジェクトを無効な状態にする可能性があります。これにより、意図しない予測不可能な結果を招くおそれがあります。

```xml
<SpaceStationAirlock>
    <innerDoorOpen>true</innerDoorOpen>
    <outerDoorOpen>true</outerDoorOpen>
</SpaceStationAirlock>
```

このような状況は、次の点を知っていると防止できます。

- <xref:System.Runtime.Serialization.DataContractSerializer> で逆シリアル化が行われる際に、ほとんどのクラスで、コンストラクターが実行されません。 このため、コンストラクターで実行される状態管理には依存できません。

- コールバックを使用して、オブジェクトを確実に有効な状態にします。 <xref:System.Runtime.Serialization.OnDeserializedAttribute> 属性でマークされたコールバックは、逆シリアル化の完了後に実行され、全体の状態を調査して訂正できるので便利です。 詳細については、「[バージョントレラントなシリアル化コールバック](version-tolerant-serialization-callbacks.md)」を参照してください。

- データ コントラクト型は、プロパティの setter が特定の順序で呼び出されなくてもよいように設計します。

- <xref:System.SerializableAttribute> 属性でマークされた従来の型を使用する場合は十分に注意します。 その多くは、信頼できるデータでのみ使用するために .NET Framework リモート処理と連携するように設計されています。 この属性でマークされた既存の型は、状態の安全性を考えて設計されていない可能性があります。

- 状態の安全性に関しては、データの存在を保証するために、 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 属性の <xref:System.Runtime.Serialization.DataMemberAttribute> プロパティに依存することはできません。 データは常に `null`、 `zero`、または `invalid`になります。

- 信頼できないデータ ソースから逆シリアル化されたオブジェクト グラフは、検証せずに信頼してはいけません。 各オブジェクトが整合状態にあっても、オブジェクト グラフ全体としては整合状態にない場合があります。 さらに、オブジェクト グラフの保存モードが無効になっている場合でも、逆シリアル化されたグラフに、同じオブジェクトへの複数の参照または循環参照が存在することがあります。 詳細については、「[シリアル化と逆シリアル化](serialization-and-deserialization.md)」を参照してください。

### <a name="using-the-netdatacontractserializer-securely"></a>NetDataContractSerializer の安全な使用

<xref:System.Runtime.Serialization.NetDataContractSerializer> は、型に対して密結合を使用するシリアル化エンジンです。 これは、 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> および <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>に類似しています。 つまり、受信データから .NET Framework アセンブリと型名を読み取って、インスタンス化する型を決定します。 これは WCF の一部ですが、このシリアル化エンジンにプラグインする方法は用意されていません。カスタムコードを記述する必要があります。 は、 `NetDataContractSerializer` 主に .NET Framework リモート処理から WCF への移行を容易にするために用意されています。 詳細については、「[シリアル化と逆シリアル化](serialization-and-deserialization.md)」の関連セクションを参照してください。

読み込むことができる型はメッセージ自身が示すことができるため、 <xref:System.Runtime.Serialization.NetDataContractSerializer> のメカニズムは本質的にセキュリティで保護されていません。このエンジンでは、信頼されたデータだけを使用してください。 詳細については、「 [Binaryformatter セキュリティガイド](/dotnet/standard/serialization/binaryformatter-security-guide)」を参照してください。

信頼されたデータを使用している場合でも、特に <xref:System.Runtime.Serialization.NetDataContractSerializer.AssemblyFormat%2A> プロパティが <xref:System.Runtime.Serialization.Formatters.FormatterAssemblyStyle.Simple>に設定されている場合は、読み込む型が受信データで適切に指定されないことがあります。 アプリケーションのディレクトリまたはグローバル アセンブリ キャッシュにアクセスできればだれにでも、読み込むべき型の代わりに、悪質な型を配置することができます。 アクセス許可を適切に設定することによって、アプリケーション ディレクトリとグローバル アセンブリ キャッシュのセキュリティを必ず確保してください。

通常、部分信頼コードで `NetDataContractSerializer` インスタンスにアクセスしたり、サロゲート セレクター (<xref:System.Runtime.Serialization.ISurrogateSelector>) やシリアル化バインダー (<xref:System.Runtime.Serialization.SerializationBinder>) を制御したりできるようにすると、コードによってシリアル化と逆シリアル化のプロセスが細かく制御される可能性があります。 たとえば、コードによって任意の型が挿入されたり、情報漏えいにつながったりする場合があります。また、生成されたオブジェクト グラフやシリアル化されたデータが改ざんされたり、生成されたシリアル化ストリームをオーバーフローさせたりする場合もあります。

`NetDataContractSerializer` に関するもう 1 つのセキュリティの問題は、悪質なコードの実行ではなく、サービス拒否攻撃です。 `NetDataContractSerializer`を使用する場合は、必ず <xref:System.Runtime.Serialization.NetDataContractSerializer.MaxItemsInObjectGraph%2A> クォータを安全な値に設定してください。 サイズがこのクォータでしか制限されないようなオブジェクトであれば、そのオブジェクトの配列を割り当てるための悪質な小さいメッセージを作成することは容易です。

### <a name="xmlserializer-specific-threats"></a>XmlSerializer 固有の脅威

<xref:System.Xml.Serialization.XmlSerializer> のセキュリティ モデルは、 <xref:System.Runtime.Serialization.DataContractSerializer>のセキュリティ モデルに似ています。 ただし、 <xref:System.Xml.Serialization.XmlSerializer>に固有の脅威がいくつか存在します。

<xref:System.Xml.Serialization.XmlSerializer> は、実際にシリアル化と逆シリアル化を実行するコードが含まれた *シリアル化アセンブリ* を実行時に生成します。これらのアセンブリは、ファイルの一時ディレクトリに作成されます。 他のプロセスまたはユーザーがこのディレクトリにアクセスできる場合は、シリアル化または逆シリアル化のコードが任意のコードで上書きされる可能性があります。 その結果、シリアル化または逆シリアル化のコードではなく、上書き後のコードのセキュリティ コンテキストを使用して、 <xref:System.Xml.Serialization.XmlSerializer> がこのコードを実行します。 一時ファイルのディレクトリへのアクセス許可が適切に設定されていることを確認し、この状況が起こらないようにしてください。

<xref:System.Xml.Serialization.XmlSerializer> には、シリアル化アセンブリを実行時に生成するのではなく、事前生成済みのシリアル化アセンブリを使用するモードもあります。 このモードは、 <xref:System.Xml.Serialization.XmlSerializer> が適切なシリアル化アセンブリを検出できるとトリガーされます。 <xref:System.Xml.Serialization.XmlSerializer> は、シリアル化アセンブリの署名に使用されているキーが、シリアル化する型を含むアセンブリの署名に使用されたものと同じであるかどうかをチェックします。 このチェックによって、シリアル化アセンブリに偽装した悪質なアセンブリからの保護が可能になります。 ただし、シリアル化可能な型を含むアセンブリが署名されていない場合、 <xref:System.Xml.Serialization.XmlSerializer> はこのチェックを実行できず、正しい名前を持つ任意のアセンブリを使用することになります。 これによって、悪質なコードの実行が生じる可能性があります。 シリアル化可能な型が属するアセンブリに必ず署名するか、アプリケーション ディレクトリとグローバル アセンブリ キャッシュへのアクセスを厳密に制御することによって、悪質なアセンブリの侵入を防止します。

<xref:System.Xml.Serialization.XmlSerializer> は、サービス拒否攻撃にもさらされる可能性があります。 <xref:System.Xml.Serialization.XmlSerializer> には、( `MaxItemsInObjectGraph` で利用できるような) <xref:System.Runtime.Serialization.DataContractSerializer>クォータがありません。 したがって、逆シリアル化されるオブジェクトの量は、メッセージ サイズによってのみ制限されるため、不定になります。

### <a name="partial-trust-threats"></a>部分信頼に関する脅威

部分信頼で実行されているコードに関連する脅威について、以下の懸念事項に注意してください。 これらの脅威には、悪質な部分信頼コードと、他の攻撃シナリオと結びついた悪質な部分信頼コード (特定の文字列を作成し、それを逆シリアル化する部分信頼コードなど) があります。

- シリアル化コンポーネントを使用するときは、使用前にどのアクセス許可もアサートしないでください。これは、シリアル化シナリオ全体がアサートのスコープ内であり、信頼できないデータまたはオブジェクトは処理しない場合も同様です。 アクセス許可をアサートすると、セキュリティ上の脆弱性の原因となる場合があります。

- 部分信頼コードで拡張ポイント (サロゲート)、シリアル化する型、または他の方法によってシリアル化プロセスを制御している場合、部分信頼コードが原因でシリアライザーが大量のデータをシリアル化ストリームに出力し、このストリームの受信側に対してサービス拒否 (DoS: Denial of Service) を引き起こす可能性があります。 DoS の脅威の影響を受けやすいターゲットを対象とするデータをシリアル化する場合、部分信頼の型をシリアル化したり、部分信頼コードでシリアル化を制御したりしないでください。

- 部分信頼コードがインスタンスにアクセスできるようにする場合 <xref:System.Runtime.Serialization.DataContractSerializer> 、または[データコントラクトサロゲート](../extending/data-contract-surrogates.md)を制御する場合は、シリアル化と逆シリアル化のプロセスを細かく制御することが必要になることがあります。 たとえば、コードによって任意の型が挿入されたり、情報漏えいにつながったりする場合があります。また、生成されたオブジェクト グラフやシリアル化されたデータが改ざんされたり、生成されたシリアル化ストリームをオーバーフローさせたりする場合もあります。 <xref:System.Runtime.Serialization.NetDataContractSerializer> に関する同等の脅威については、「NetDataContractSerializer の安全な使用」で説明しています。

- <xref:System.Runtime.Serialization.DataContractAttribute> 属性が型 (または <xref:System.SerializableAttribute> ではなく <xref:System.Runtime.Serialization.ISerializable>とマークされた型) に適用されている場合、すべてのコンストラクターが非パブリックであるか、または要求で保護されている場合でも、デシリアライザーはこのような型のインスタンスを作成できます。

- 逆シリアル化されるデータが信頼できるものであり、すべての既知の型が信頼した型であることが確実である場合を除き、逆シリアル化の結果を信頼しないでください。 部分信頼で実行されている場合、既知の型はアプリケーション構成ファイルから読み込まれません (ただし、コンピューター構成ファイルからは読み込まれます)。

- 部分信頼コードに追加されたサロゲートと共に <xref:System.Runtime.Serialization.DataContractSerializer> インスタンスを渡すと、コードによってそのサロゲートの変更可能な設定が変更される可能性があります。

- 逆シリアル化されたオブジェクトでは、XML リーダー (またはそれに含まれるデータ) が部分信頼コードからのものである場合、結果の逆シリアル化されたオブジェクトを信頼できないデータとして扱ってください。

- <xref:System.Runtime.Serialization.ExtensionDataObject> 型がパブリック メンバーを含んでいなくても、それに含まれるデータが安全であるとは限りません。 たとえば、特権が付与されたデータ ソースから、いくつかのデータを含むオブジェクトに逆シリアル化し、そのオブジェクトを部分信頼コードに渡した場合、部分信頼コードは、オブジェクトをシリアル化して `ExtensionDataObject` のデータを読み取ることができます。 特権が付与されたデータ ソースから、後で部分信頼コードに渡されるオブジェクトに逆シリアル化する場合は、 <xref:System.Runtime.Serialization.DataContractSerializer.IgnoreExtensionDataObject%2A> を `true` に設定するよう考慮してください。

- 完全信頼では、<xref:System.Runtime.Serialization.DataContractSerializer> および <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> support the serialization of private, protected, internal, および public members in full trust. 一方、部分信頼ではパブリック メンバーのシリアル化のみが可能です。 アプリケーションがパブリック メンバー以外のメンバーのシリアル化を試みると、 <xref:System.Security.SecurityException> がスローされます。

    部分信頼で内部メンバーまたはプロテクト内部メンバーをシリアル化するには、 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> アセンブリ属性を使用します。 この属性を使用すると、アセンブリは内部メンバーが他のアセンブリから参照できることを宣言できます。 この場合、内部メンバーのシリアル化が必要なアセンブリは、その内部メンバーが System.Runtime.Serialization.dll から参照できることを宣言します。

    この方法の利点は、昇格されたコード生成パスが不要なことです。

    ただし、2 つの大きな欠点もあります。

    1 つ目の欠点は、 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性のオプトイン プロパティがアセンブリ全体に適用されることです。 つまり、特定のクラスに対してのみ内部メンバーのシリアル化を可能にするような指定はできません。 もちろん、 <xref:System.Runtime.Serialization.DataMemberAttribute> 属性をメンバーに追加しないことで、特定の内部メンバーをシリアル化しないことは可能です。 同様に、メンバーをプライベート メンバーまたはプロテクト メンバーではなく内部メンバーにすることもできますが、参照可能範囲の問題が残ります。

    2 つ目の欠点は、プライベート メンバーやプロテクト メンバーがサポートされないことです。

    部分信頼での <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性の使用を理解するために、次のプログラムについて考えてみましょう。

    [!code-csharp[CDF_WCF_SecurityConsiderationsForData#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/cdf_wcf_securityconsiderationsfordata/cs/program.cs#1)]

    上の例で、 `PermissionsHelper.InternetZone` は部分信頼の <xref:System.Security.PermissionSet> に対応します。 属性を指定しないと、 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> アプリケーションは失敗し、 <xref:System.Security.SecurityException> 非パブリックメンバーが部分信頼でシリアル化できないことを示すがスローされます。

    ただし、ソース ファイルに次の行を追加すると、プログラムは正常に実行されます。

    [!code-csharp[CDF_WCF_SecurityConsiderationsForData#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/cdf_wcf_securityconsiderationsfordata/cs/program.cs#2)]

## <a name="other-state-management-concerns"></a>状態管理に関するその他の注意事項

オブジェクトの状態管理に関してその他の注意すべき点を以下に示します。

- ストリーミング トランスポートでストリーム ベースのプログラミング モデルを使用した場合、メッセージが到着するとメッセージの処理が開始されます。 メッセージの送信側によってストリームの途中で送信操作が中止されることはあり得ますが、このとき続きのコンテンツを待機していた場合、コードの状態を予想できなくなります。 一般に、ストリームは完全であると考えないでください。また、ストリーミングが中止されたときにロールバックできないようなストリーム ベースの操作では、処理を行わないでください。 このことは、ストリーミングの本文の後に続くメッセージの形式が正しくない可能性があるような状況にも当てはまります (たとえば、SOAP エンベロープの終了タグが不足している、または 2 つ目のメッセージ本文があるなど)。

- `IExtensibleDataObject` 機能を使用すると、機密データが出力される可能性があります。 `IExtensibleObjectData` を含むデータ コントラクトに、信頼できない送信元のデータを受け入れ、その後、メッセージが署名される、セキュリティで保護されたチャネルにそのデータを再送した場合、一切確認していないデータを保証していることになります。 さらに、既知のデータと不明なデータの両方を考慮すると、送信している全体の状態が無効になる可能性があります。 このような状況を回避するには、拡張データ プロパティを `null` に設定するか、 `IExtensibleObjectData` 機能を無効にします。

## <a name="schema-import"></a>スキーマのインポート

通常、型を生成するためにスキーマをインポートするプロセスは、設計時にのみ発生します。たとえば、クライアント クラスを生成するために Web サービス上で [ServiceModel Metadata Utility Tool (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) を使用しているときなどです。 ただし、さらに高度なシナリオでは、スキーマを実行時に処理することがあります。 この場合、サービス拒否攻撃の危険にさらされる可能性があることを覚えておく必要があります。 スキーマによっては、インポートに時間がかかる場合があります。 スキーマが信頼できないソースからのものである可能性がある場合は、このようなシナリオで <xref:System.Xml.Serialization.XmlSerializer> のスキーマ インポート コンポーネントを使用しないでください。

## <a name="threats-specific-to-aspnet-ajax-integration"></a>ASP.NET AJAX 統合に固有の脅威

ユーザーが <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> またはを実装すると <xref:System.ServiceModel.Description.WebHttpBehavior> 、WCF は XML メッセージと JSON メッセージの両方を受け入れることができるエンドポイントを公開します。 ただし、XML リーダーと JSON リーダーの両方が使用するリーダー クォータのセットは 1 つしかありません。 一部のクォータ設定が一方のリーダーには適切であっても、もう一方のリーダーには大きすぎる場合があります。

`WebScriptEnablingBehavior`を実装すると、ユーザーはエンドポイントで JavaScript プロキシを公開するオプションを使用できます。 セキュリティに関する次の問題を考慮する必要があります。

- JavaScript プロキシを調べることで、サービスに関する情報 (操作名、パラメーター名など) を取得できます。

- JavaScript エンドポイントを使用すると、機密性の高い情報やプライベートな情報がクライアントの Web ブラウザーのキャッシュに保持される可能性があります。

## <a name="a-note-on-components"></a>コンポーネントに関する注意事項

WCF は、柔軟でカスタマイズ可能なシステムです。 このトピックのほとんどの内容は、最も一般的な WCF 使用シナリオに焦点を当てています。 ただし、WCF に用意されているコンポーネントは、さまざまな方法で構成できます。 各コンポーネントを使用した場合のセキュリティへの影響について理解することが重要です。 特に次の点に違いがあります。

- XML リーダーを使用する必要があるときは、 <xref:System.Xml.XmlDictionaryReader> クラスに用意されたリーダーを使用し、それ以外のリーダーは使用しないようにします。 安全なリーダーは、 <xref:System.Xml.XmlDictionaryReader.CreateTextReader%2A>、 <xref:System.Xml.XmlDictionaryReader.CreateBinaryReader%2A>、 <xref:System.Xml.XmlDictionaryReader.CreateMtomReader%2A> のいずれかのメソッドを使用して作成できます。 <xref:System.Xml.XmlReader.Create%2A> メソッドは使用しないでください。 リーダーは、必ず安全なクォータを使用して設定します。 Wcf のシリアル化エンジンは、WCF のセキュリティで保護された XML リーダーと共に使用する場合にのみ、セキュリティで保護されます。

- <xref:System.Runtime.Serialization.DataContractSerializer> を使用して、信頼できない可能性のあるデータを逆シリアル化する場合は、必ず <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A> プロパティを設定します。

- メッセージを作成する場合、 `maxSizeOfHeaders` による保護が十分でないときは `MaxReceivedMessageSize` パラメーターを設定します。

- エンコーダーを作成する場合、 `MaxSessionSize` や `MaxBufferSize`などの関連クォータを必ず設定します。

- XPath メッセージ フィルターを使用する場合は、 <xref:System.ServiceModel.Dispatcher.XPathMessageFilter.NodeQuota%2A> を設定してそのフィルターがアクセスする XML ノードの量を制限します。 多数のノードにアクセスせず、計算に長い時間がかかる可能性がある XPath 式は使用しないようにします。

- 通常、クォータを受け入れるコンポーネントを使用する場合は、そのセキュリティへの影響を理解し、クォータを安全な値に設定します。

## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Xml.XmlDictionaryReader>
- <xref:System.Xml.Serialization.XmlSerializer>
- [既知のデータ コントラクト型](data-contract-known-types.md)
