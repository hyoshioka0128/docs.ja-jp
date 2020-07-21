---
title: メッセージ エンコーダーを選択する
ms.date: 03/30/2017
ms.assetid: 2204d82d-d962-4922-a79e-c9a231604f19
ms.openlocfilehash: dbc5981013fe5e023f1d6d9eaf64b2e1fa18e2df
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84587340"
---
# <a name="choose-a-message-encoder"></a>メッセージエンコーダーを選択する

この記事では、Windows Communication Foundation (WCF) に含まれるメッセージエンコーダー (バイナリ、テキスト、メッセージ伝送最適化メカニズム (MTOM)) を選択するための基準について説明します。  
  
 WCF では、バインディングを使用して、エンドポイント間でネットワーク経由でデータを転送する方法を指定します。*バインディング*はバインド*要素*のシーケンスで構成されます。 メッセージ エンコーダーは、バインディング スタックにあるメッセージ エンコーディング バインド要素によって表されます。 バインディングには、オプションのプロトコル バインド要素 (セキュリティ バインド要素や信頼できるメッセージング バインド要素など)、必須のメッセージ エンコーディング バインド要素、および必須のトランスポート バインド要素が含まれます。  
  
 メッセージ エンコーディング バインド要素は、オプションのプロトコル バインド要素の下、必須のトランスポート バインド要素の上に位置します。 送信側では、メッセージ エンコーダーにより出力 <xref:System.ServiceModel.Channels.Message> がシリアル化されてトランスポートに渡されます。 受信側では、メッセージ エンコーダーがトランスポートからシリアル化形式の <xref:System.ServiceModel.Channels.Message> を受信し、上位のプロトコル層が存在する場合はその層に、存在しない場合はアプリケーションに渡します。  
  
 既存のクライアントまたはサーバーに接続するときには、相手側が予測している方法でメッセージをエンコードする必要があるため、特定のメッセージ エンコーディングを選択できない場合があります。 ただし、WCF サービスを作成する場合は、それぞれ異なるメッセージエンコーディングを使用して、複数のエンドポイントを介してサービスを公開できます。 これにより、クライアントは最適なエンドポイントでのサービスとの対話に最も適したエンコーディングを選択でき、最適なエンコーディングを選択する際の柔軟性が得られます。 複数のエンドポイントを使用することにより、異なるメッセージ エンコーディングの利点を他のバインド要素と組み合わせることも可能になります。  
  
## <a name="system-provided-encoders"></a>システム指定のエンコーダー  
 WCF には、次の3つのクラスによって表される3つのメッセージエンコーダーが含まれています。  
  
- <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> は、書式なし XML エンコーディングと SOAP エンコーディングの両方をサポートするテキスト メッセージ エンコーダーです。 テキスト メッセージ エンコーダーの書式なし XML エンコーディング モードは、テキスト ベースの SOAP エンコーディングと区別するために、"POX" (Plain Old XML) と呼ばれます。 POX を有効にするには、<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement.MessageVersion%2A> プロパティを <xref:System.ServiceModel.Channels.MessageVersion.None%2A> に設定します。 非 WCF エンドポイントと相互運用するには、テキストメッセージエンコーダーを使用します。  
  
- <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>バイナリメッセージエンコーダーは、コンパクトなバイナリ形式を使用し、WCF から WCF への通信に最適化されているため、相互運用できません。 これは、WCF が提供するすべてのエンコーダーの最もパフォーマンスの高いエンコーダーでもあります。  
  
- <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> は、MTOM エンコーディングを使用して、メッセージの文字エンコーディングとバージョン管理を指定するバインド要素です。 MTOM は、WCF メッセージでバイナリ データを転送するための効率的なテクノロジです。 MTOM エンコーダーは、効率と相互運用性のバランスをとろうとします。 MTOM エンコーディングは、ほとんどの XML をテキスト形式で転送しますが、大きいサイズのバイナリ データ ブロックはテキストに変換せずにそのまま転送することによって最適化します。 WCF に用意されているエンコーダーの効率性の点から、MTOM はテキスト (最も低速) とバイナリ (最速) の間にあります。  
  
## <a name="how-to-choose-a-message-encoder"></a>メッセージ エンコーダーを選択する方法  
 メッセージ エンコーダーを選択するために使用される一般的な要因を、次の表に示します。 アプリケーションにとって重要な要因に優先順位を与えて、それらの要因に対して最適なメッセージ エンコーダーを選択します。 この表には示されていないその他の要因と、アプリケーションで必要になることがあるカスタム メッセージ エンコーダーも考慮するようにしてください。  
  
|要素|説明|この要因をサポートするエンコーダー|  
|------------|-----------------|---------------------------------------|  
|サポートされている文字セット|<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>および <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> は、UTF8 および UTF16 Unicode (*ビッグエンディアン*および*リトルエンディアン*) エンコーディングのみをサポートしています。 UTF7 や ASCII など、別のエンコーディングが要求される場合はカスタム エンコーディングを使用する必要があります。 カスタムエンコーダーのサンプルについては、「[カスタムメッセージエンコーダー](https://docs.microsoft.com/dotnet/framework/wcf/samples/custom-message-encoder-custom-text-encoder)」を参照してください。|テキスト|  
|検査|検査は、転送中にメッセージを調べる機能です。 SOAP の使用に関係なく、テキスト エンコーディングでは、多くのアプリケーションで特別なツールを使用することなくメッセージの検査と分析が可能です。 メッセージレベルまたはトランスポートレベルで転送セキュリティを使用すると、メッセージを検査する機能に影響します。 機密性はメッセージが検査されないように保護し、整合性はメッセージが変更されないように保護します。|テキスト|  
|[信頼性]|信頼性は、転送エラーに対するエンコーダーの復元能力です。 信頼性はメッセージ層、トランスポート層、またはアプリケーション層でも提供できます。 標準の WCF エンコーダーでは、他のレイヤーが信頼性を提供していると想定しています。 エンコーダーは、転送エラーから回復する機能をほとんど備えていません。|なし|  
|簡便性|単純さは、エンコード仕様に対応するエンコーダーとデコーダーの作成の容易さを表します。 テキスト エンコーディングは、単純さの面で特に優れており、POX テキスト エンコーディングは SOAP 処理のサポートが不要なため、さらに優れています。|テキスト (POX)|  
|サイズ|エンコーディングによって、コンテンツに課せられるオーバーヘッドの量が決まります。 エンコードされたメッセージのサイズは、サービス操作の最大スループットに直接影響します。 バイナリ エンコーディングは、一般にテキスト エンコーディングよりサイズが小さくなります。 メッセージのサイズが優先事項である場合は、エンコーディング中にメッセージ コンテンツを圧縮することも検討してください。 ただし、圧縮を行うとメッセージの送信者と受信者の両方で処理コストが大きくなります。|2 項|  
|ストリーミング|ストリーミングでは、アプリケーションはメッセージ全体が到着する前にメッセージの処理を開始できます。 ストリーミングを効果的に使用するには、受信するアプリケーションが重要なデータの到着を待つ必要をなくすために、メッセージの冒頭で重要なデータが利用可能になっている必要があります。 さらに、ストリーミングされた転送を使用するアプリケーションでは、メッセージ コンテンツに前方依存性がないように、メッセージ内のデータを順次編成していく必要があります。 多くの場合、コンテンツのストリーミングと必要最小限のサイズで転送を行うこととの間で妥協を図る必要があります。|なし|  
|サードパーティ製ツールのサポート|エンコーディングのサポート領域には、開発と診断があります。 サードパーティの開発者は、POX 形式でエンコードされたメッセージを処理するためのライブラリとツールキットに多大な投資をしています。|テキスト (POX)|  
|相互運用性|この要因は、wcf エンコーダーが WCF 以外のサービスと相互運用する機能を指します。|テキスト<br /><br /> MTOM (部分的)|  
  
メモ: バイナリ エンコーダーを使用している場合、XMLReader を作成するときに IgnoreWhitespace の設定を使用しても効果はありません。  たとえば、サービス操作内で次の操作を実行するとします。  

```csharp
public void OperationContract(XElement input)
{
    Console.WriteLine("{0}", input.Value);
    int counter = 0;
    var xreader = input.CreateReader();
    var reader = XmlReader.Create(xreader, new XmlReaderSettings() { IgnoreWhitespace = true });
    while (reader.Read())
    {
        counter++;
    }

    Console.WriteLine("Read {0} lines with reader", counter);
}
```  
  
IgnoreWhitespace の設定は無視されます。  
  
## <a name="compression-and-the-binary-encoder"></a>圧縮およびバイナリ エンコーダー

WCF 4.5 以降の WCF バイナリ エンコーダーでは、圧縮がサポートされます。 これにより、WCF クライアントから圧縮メッセージを送信するための gzip/deflate アルゴリズムを使用でき、さらに自己ホスト型 WCF サービスからの圧縮メッセージに応答することができます。 この機能は、HTTP トランスポートおよび TCP トランスポートの両方で圧縮を有効にします。 IIS のホスト サーバーを構成することによって、いつでも IIS でホストされる WCF サービスを有効にして圧縮された応答を送信できます。 圧縮の種類は <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.CompressionFormat%2A?displayProperty=nameWithType> プロパティで構成されます。 このプロパティは、いずれかの <xref:System.ServiceModel.Channels.CompressionFormat?displayProperty=nameWithType> 列挙値に設定されます。

- <xref:System.ServiceModel.Channels.CompressionFormat.Deflate>
- <xref:System.ServiceModel.Channels.CompressionFormat.GZip>
- <xref:System.ServiceModel.Channels.CompressionFormat.None>
  
このプロパティは binaryMessageEncodingBindingElement でのみ公開されているため、この機能を使用するには、次のようなカスタムバインドを作成する必要があります。

 ```xml
 <customBinding>
   <binding name="BinaryCompressionBinding">
     <binaryMessageEncoding compressionFormat ="GZip" />
     <httpTransport />
  </binding>
</customBinding>
 ```

クライアントとサービスはどちらも、圧縮されたメッセージの送受信に同意する必要があるため、クライアントとサービスの両方の binaryMessageEncoding 要素で compressionFormat プロパティを構成する必要があります。 プロトコル例外は、サービスまたはクライアントが圧縮用に構成されておらず、もう一方がである場合にスローされます。 圧縮の有効化は慎重に検討する必要があります。 圧縮は、ネットワーク帯域幅がボトルネックになっている場合に最も効果的です。 CPU がボトルネックである場合、圧縮によりスループットが低下します。 これがアプリケーションにとってメリットがあるかどうかを確認するために、適切なテストをシミュレートされた環境で行う必要があります。  
  
## <a name="see-also"></a>関連項目

- [バインド](bindings.md)
