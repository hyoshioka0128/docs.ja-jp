---
title: XML シリアル化の詳細
description: シリアル化は転送できる形式にオブジェクトを変換します。 この記事では、XML シリアル化と XmlSerializer クラスの概要について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XML serialization, about XML serialization
- ICollection interface, serializing
- XmlSerializer class, serializing
- serialization, about serialization
- DataSet class, serializing
- XML Schema, serializing
ms.assetid: 8c63200d-db63-4a03-a93d-21641623df62
ms.openlocfilehash: d9b71b7530debde7708ee107c990541e2b97cd44
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "84277961"
---
# <a name="xml-serialization"></a>XML シリアル化

シリアル化とは、転送できる形式にオブジェクトを変換するプロセスのことです。 たとえば、オブジェクトをシリアル化し、HTTP を使用してインターネット経由でクライアントとサーバー間で転送できます。 一方、逆シリアル化とは、ストリームから元のオブジェクトを再構築する処理です。

 XML シリアル化では、オブジェクトのパブリック フィールドとプロパティ値のみを XML ストリームにシリアル化します。 型情報は対象に含まれません。 たとえば、**Library** 名前空間に **Book** オブジェクトがある場合、逆シリアル化時に、ストリームから同じ型のオブジェクトが再構築されるという保証はありません。

> [!NOTE]
> XML シリアル化では、メソッド、インデクサー、プライベート フィールド、または読み取り専用プロパティ (読み取り専用コレクションを除く) は変換されません。 オブジェクトのフィールドとプロパティをすべてシリアル化するには、パブリックとプライベートのいずれの場合も、XML シリアル化ではなく、<xref:System.Runtime.Serialization.DataContractSerializer> を使用します。

 XML シリアル化の中核となるクラスは <xref:System.Xml.Serialization.XmlSerializer> クラスです。このクラスの最も重要なメソッドは、**Serialize** メソッドと **Deserialize** メソッドです。 <xref:System.Xml.Serialization.XmlSerializer> は、C# ファイルを作成し、これを .dll ファイルにコンパイルすることによってシリアル化を行います。 .NET Framework 2.0 では、こうしたシリアル化アセンブリをあらかじめ生成してアプリケーションと共に配置し、起動時のパフォーマンスを向上させるため、[XML シリアライザー ジェネレーター ツール (Sgen.exe)](xml-serializer-generator-tool-sgen-exe.md) が用意されています。 **XmlSerializer** によって生成される XML ストリームは、World Wide Web コンソーシアム (W3C) による勧告『[XML スキーマ定義言語 (XSD) 1.0](https://www.w3.org/TR/xslt)』に準拠します。 さらに、生成されるデータ型は、ドキュメント『XML Schema Part 2:Datatypes』に準拠します。

 オブジェクトのデータは、クラス、フィールド、プロパティ、プリミティブ型、配列などのプログラミング構成要素、および **XmlElement** オブジェクトまたは **XmlAttribute** オブジェクトの形で埋め込まれている XML を使用して記述されます。 属性で注釈を付けて独自のクラスを作成するか、または XML スキーマ定義ツールを使用して、既存の XML スキーマに基づいたクラスを生成できます。

 XML スキーマがある場合は、XML スキーマ定義ツールを実行して、そのスキーマに厳密に型指定された一連のクラスを生成し、属性を使用して注釈を付けることができます。 このようなクラスのインスタンスをシリアル化すると、元の XML スキーマに準拠した XML が生成されます。 このようなクラスを用意することにより、操作が簡単なオブジェクト モデルを使用してプログラミングできると同時に、生成される XML も確実に XML スキーマに準拠したものになります。 .NET Framework の他のクラス (**XmlReader** クラス、**XmlWriter** クラスなど) を使用する代わりに、この方法を使用して XML ストリームの解析や書き込みを実行できます。 詳細については、「[XML ドキュメントと XML データ](../data/xml/index.md)」を参照してください。 これらのクラスを使用すると、任意の XML ストリームを解析できます。 これに対し、既知の XML スキーマに準拠した XML ストリームが求められる場合には、**XmlSerializer** を使用します。

 属性を使用して XML ストリームの XML 名前空間、要素名、属性名などを設定することで、**XmlSerializer** クラスによって生成される XML ストリームを制御できます。 これらの属性、および属性による XML シリアル化の制御方法については、「[属性を使用した XML シリアル化の制御](controlling-xml-serialization-using-attributes.md)」を参照してください。 また、生成される XML を制御するこれらの属性の一覧については、「[XML シリアル化を制御する属性](attributes-that-control-xml-serialization.md)」を参照してください。

 さらに、**XmlSerializer** クラスでは、オブジェクトをシリアル化し、エンコードされた SOAP XML ストリームを生成することができます。 このようにして生成される XML は、W3C のドキュメント『Simple Object Access Protocol (SOAP) 1.1』のセクション 5 に準拠します。 このプロセスの詳細については、「[方法:オブジェクトを SOAP エンコード済み XML ストリームとしてシリアル化する](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)」を参照してください。 生成される XML を制御する属性の一覧については、「[エンコード済み SOAP シリアル化を制御する属性](attributes-that-control-encoded-soap-serialization.md)」を参照してください。

 **XmlSerializer** クラスは、XML Web サービスによって作成され、XML Web サービスに渡される SOAP メッセージを生成します。 この SOAP メッセージを制御するには、XML Web サービス ファイル (.asmx) 内のクラス、戻り値、パラメーター、およびフィールドに属性を適用します。 XML Web サービスでは、リテラルまたはエンコード済みのいずれの SOAP スタイルも使用できるため、「XML シリアル化を制御する属性」と「エンコード済み SOAP シリアル化を制御する属性」の両方に示されている属性を使用できます。 XML Web サービスによって生成された XML を属性を使用して制御する方法については、「[XML Web サービスを使用した XML シリアル化](xml-serialization-with-xml-web-services.md)」を参照してください。 SOAP と XML Web サービスの詳細については、「[SOAP メッセージの書式のカスタマイズ](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dkwy2d72(v=vs.100))」を参照してください。

## <a name="security-considerations-for-xmlserializer-applications"></a>XmlSerializer アプリケーションのセキュリティに関する考慮事項

**XmlSerializer** を使用するアプリケーションを作成するときには、次の項目とその関連事項に注意する必要があります。

- **XmlSerializer** は、TEMP 環境変数で指定されたディレクトリ内に C# ファイル (.cs) を作成し、これらを .dll ファイルにコンパイルします。シリアル化はこれらの DLL で行われます。

  > [!NOTE]
  > SGen.exe ツールを使用すると、このシリアル化アセンブリを事前に生成して署名することができます。 これは、サーバー側の Web サービスに対しては機能せず、 クライアント側での手動シリアル化にのみ使用できます。

  作成時とコンパイル時、このコードと DLL には悪意のあるプロセスに対する脆弱性があります。 Microsoft Windows NT 4.0 以降を実行しているコンピューターでは、複数のユーザーが一時ディレクトリを共有する可能性があります。 2 つのアカウントが異なるセキュリティ特権を持ち、高い特権を持つアカウントが **XmlSerializer** を使用してアプリケーションを実行する場合、一時ディレクトリの共有は危険です。 この場合、一方のユーザーが .cs ファイルまたはコンパイルされた .dll ファイルのいずれかを置き換えることにより、コンピューターのセキュリティが侵害される可能性があります。 これを防ぐためには、コンピューター上の各アカウントが常に固有のプロファイルを持つようにしてください。 既定では、TEMP 環境変数はアカウントごとに異なるディレクトリを示します。

- 悪意のあるユーザーが XML データの連続ストリームを Web サーバーに送り続けた場合 (サービス拒否攻撃)、**XmlSerializer** はコンピューターがリソース不足に陥るまでデータの処理を続行します。

  インターネット インフォメーション サービス (IIS) を実行しているコンピューターを使用し、IIS 内でアプリケーションを実行することによって、この種の攻撃を防ぐことができます。 IIS には、一定量 (既定では 4 KB) を超える長さのストリームを処理しないゲート機能があります。 IIS を使用しないアプリケーションを作成し、**XmlSerializer** による逆シリアル化を行う場合は、同様のゲート機能を実装してサービス拒否攻撃を防ぐ必要があります。

- **XmlSerializer** はデータをシリアル化し、指定された任意の型を使用してすべてのコードを実行します。

  悪意のあるオブジェクトが脅威を与える方法には、次の 2 とおりがあります。 悪意のあるコードを実行する方法と、**XmlSerializer** によって作成された C# ファイルに悪意のあるコードを挿入する方法です。 最初のケースでは、悪意のあるオブジェクトが破壊的なプロシージャを実行しようとしたときに、コード アクセス セキュリティによって実行が防止され、被害を防ぐことができます。 2 番目のケースでは、**XmlSerializer** によって作成された C# ファイルに、悪意のあるオブジェクトがなんらかの方法でコードを挿入する可能性が論理的にあります。 この問題は十分に調査されており、このような攻撃を受ける可能性は低いと考えられますが、不明または信頼されていない型のデータは絶対にシリアル化しないことが重要です。

- 機密情報をシリアル化すると脆弱性が生じる可能性があります。

  **XmlSerializer** がシリアル化したデータは、XML ファイルなどのデータ ストアとして格納されます。 このデータ ストアが他のプロセスからも利用できたり、イントラネットまたはインターネットで表示できたりする場合、データの盗用や悪用の可能性が生じます。 たとえば、クレジット カード番号を含む注文をシリアル化するアプリケーションを作成すると、データは非常に脆弱になります。 これを避けるには、データ ストアを常に保護し、機密を保つための処置が必要です。

## <a name="serialization-of-a-simple-class"></a>単純なクラスのシリアル化

パブリック フィールドを持つ基本クラスのコード例を次に示します。

```vb
Public Class OrderForm
    Public OrderDate As DateTime
End Class
```

```csharp
public class OrderForm
{
    public DateTime OrderDate;
}
```

このクラスのインスタンスをシリアル化すると、次のようなストリームが生成されます。

```xml
<OrderForm>
    <OrderDate>12/12/01</OrderDate>
</OrderForm>
```

シリアル化の例については、「[XML シリアル化の例](examples-of-xml-serialization.md)」を参照してください。

## <a name="items-that-can-be-serialized"></a>シリアル化できる項目

**XmlSerializer** クラスを使用して、次の項目をシリアル化できます。

- パブリックな読み取り/書き込みプロパティとパブリック クラスのフィールド

- **ICollection** または **IEnumerable** を実装するクラス。

  > [!NOTE]
  > パブリック プロパティではなく、コレクションのみがシリアル化されます。

- **XmlElement** オブジェクト。

- **XmlNode** オブジェクト。

- **DataSet** オブジェクト。

 オブジェクトのシリアル化と逆シリアル化の詳細については、「[方法:オブジェクトをシリアル化する](how-to-serialize-an-object.md)」および「[方法:オブジェクトを逆シリアル化する](how-to-deserialize-an-object.md)」を参照してください。

## <a name="advantages-of-using-xml-serialization"></a>XML シリアル化を使用する利点

**XmlSerializer** クラスを使用すると、オブジェクトを XML としてシリアル化するときに、シリアル化を完全かつ柔軟に制御できます。 XML Web サービスを作成する場合は、シリアル化を制御する属性をクラスやメンバーに適用して、XML 出力を特定のスキーマに準拠させることができます。

たとえば、**XmlSerializer** を使用すると、次のことができます。

- フィールドやプロパティを属性または要素としてエンコードするかどうか

- 使用する XML 名前空間

- 要素または属性の名前 (フィールド名やプロパティ名が適切ではない場合)

XML シリアル化のもう 1 つの利点は、生成される XML ストリームが特定のスキーマに準拠している限りは、開発するアプリケーションに制約が課されないことです。 たとえば、書籍の説明に使用するスキーマがあるとします。 このスキーマでは、書籍名、著者、出版社、ISBN 番号などの要素を扱います。 書籍発注や在庫管理など、この XML データを任意の方法で処理するアプリケーションを開発できます。 いずれの場合も、指定された XML スキーマ定義言語 (XSD) スキーマに XML ストリームが準拠していることが唯一の要件です。

## <a name="xml-serialization-considerations"></a>XML シリアル化に関する考慮事項

**XmlSerializer** クラスを使用する場合には、次の点を考慮する必要があります。

- Sgen.exe ツールは、特に、シリアル化アセンブリを生成して最適なパフォーマンスを実現するように設計されています。

- シリアル化されたデータには、データ自体とクラスの構造のみが含まれます。 型の ID やアセンブリの情報は含まれません。

- シリアル化できるのは、パブリック プロパティとパブリック フィールドのみです。 プロパティにパブリック アクセサー (get メソッドおよび set メソッド) が存在する必要があります。 非パブリック データをシリアル化する必要がある場合は、XML シリアル化ではなく <xref:System.Runtime.Serialization.DataContractSerializer> クラスを使用します。

- クラスを **XmlSerializer** でシリアル化するには、そのクラスがパラメーターなしのコンストラクターを持つ必要があります。

- メソッドはシリアル化できません。

- **IEnumerable** または **ICollection** を異なる方法で実装しているクラスは、次のような特定の要件を満たしていれば、**XmlSerializer** で処理できます。

  **IEnumerable** を実装するクラスは、単一のパラメーターを受け取るパブリックな **Add** メソッドを実装している必要があります。 **Add** メソッドのパラメーターは、**GetEnumerator** メソッドによって返される **IEnumerator.Current** プロパティから返される型と一致している (ポリモーフィックである) 必要があります。

  **IEnumerable** の他に **ICollection** も実装するクラス (**CollectionBase** など) は、整数を受け取るパブリックなインデックス付き **Item** プロパティ (C# の場合はインデクサー) と、**integer** 型のパブリックな **Count** プロパティを持つ必要があります。 **Add** メソッドに渡されるパラメーターは、**Item** プロパティから返された型と同じ型か、またはその型の基本型の 1 つである必要があります。

  **ICollection** を実装するクラスの場合、シリアル化される値は、**GetEnumerator** を呼び出して取得されるのではなく、インデックス付き **Item** プロパティから取得されます。 また、パブリック フィールドとパブリック プロパティは、別のコレクション クラス (**ICollection** を実装するクラス) を返すパブリック フィールドを除き、シリアル化されません。 例については、「[XML シリアル化の例](examples-of-xml-serialization.md)」を参照してください。

## <a name="xsd-data-type-mapping"></a>XSD データ型のマッピング

W3C のドキュメント『[XML Schema Part 2:Datatypes](https://www.w3.org/TR/xmlschema-2/)』で、XML スキーマ定義言語 (XSD) スキーマで使用できる単純なデータ型が指定されています。 これらのデータ型の多く (**int**、**decimal** など) については、対応するデータ型が .NET Framework にあります。 ただし、**NMTOKEN** データ型など、.NET Framework には対応するものがない XML データ型もあります。 その場合、XML スキーマ定義ツール ([XML スキーマ定義ツール (Xsd.exe)](xml-schema-definition-tool-xsd-exe.md)) を使用してスキーマからクラスを生成すると、適切な属性が文字列型のメンバーに適用され、その **DataType** プロパティが XML データ型名に設定されます。 たとえば、XML データ型が **NMTOKEN** である "MyToken" という名前の要素がスキーマに含まれている場合、生成されるクラスには、次の例に示すようなメンバーが含まれます。

```vb
<XmlElement(DataType:="NMTOKEN")> _
Public MyToken As String
```

```csharp
[XmlElement(DataType = "NMTOKEN")]
public string MyToken;
```

同様に、特定の XML スキーマ (XSD) に準拠する必要があるクラスを作成する場合は、そのクラスに適切な属性を適用し、**DataType** プロパティを必要な XML データ型名に設定する必要があります。

型のマップの一覧については、次の属性クラスの **DataType** プロパティを参照してください。

- <xref:System.Xml.Serialization.SoapAttributeAttribute>

- <xref:System.Xml.Serialization.SoapElementAttribute>

- <xref:System.Xml.Serialization.XmlArrayItemAttribute>

- <xref:System.Xml.Serialization.XmlAttributeAttribute>

- <xref:System.Xml.Serialization.XmlElementAttribute>

- <xref:System.Xml.Serialization.XmlRootAttribute>

## <a name="see-also"></a>関連項目

- <xref:System.Xml.Serialization.XmlSerializer>
- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.IO.FileStream>
- [XML シリアル化および SOAP シリアル化](xml-and-soap-serialization.md)
- [バイナリ シリアル化](binary-serialization.md)
- [シリアル化](index.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [XML シリアル化の例](examples-of-xml-serialization.md)
- [方法: オブジェクトをシリアル化する](how-to-serialize-an-object.md)
- [方法: オブジェクトを逆シリアル化する](how-to-deserialize-an-object.md)
