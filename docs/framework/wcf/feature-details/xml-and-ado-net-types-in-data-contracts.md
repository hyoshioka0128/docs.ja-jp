---
title: データ コントラクトの XML および ADO.NET の種類
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c2ce8461-3c15-4c41-8c81-1cb78f5b59a6
ms.openlocfilehash: 975d4f4f37bbbd895cab4e87686f15017e90f382
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600076"
---
# <a name="xml-and-adonet-types-in-data-contracts"></a>データ コントラクトの XML および ADO.NET の種類
Windows Communication Foundation (WCF) データコントラクトモデルでは、XML を直接表す特定の型がサポートされています。 シリアライザーは、これらの型を XML にシリアル化するとき、型の XML コンテンツを書き出しますが、それ以上の処理は行いません。 サポートされている型は、<xref:System.Xml.XmlElement>、<xref:System.Xml.XmlNode> の配列 (`XmlNode` 型自体はサポートされていません)、および <xref:System.Xml.Serialization.IXmlSerializable> を実装した型です。 データベース プログラミングでは、<xref:System.Data.DataSet> 型、<xref:System.Data.DataTable> 型、および型指定されたデータセットが一般的に使用されます。 これらの型は `IXmlSerializable` インターフェイスを実装するので、データ コントラクト モデルでシリアル化可能です。 この型に関する考慮事項について、このトピックの最後に説明します。  
  
## <a name="xml-types"></a>XML 型  
  
### <a name="xml-element"></a>XmlElement  
 `XmlElement` 型は、その XML コンテンツを使用してシリアル化されます。 たとえば、次の型を使用するとします。  
  
 [!code-csharp[DataContractAttribute#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/datacontractattribute/cs/overview.cs#4)]
 [!code-vb[DataContractAttribute#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/datacontractattribute/vb/overview.vb#4)]  
  
 これは、次のように XML にシリアル化されます。  
  
```xml  
<MyDataContract xmlns="http://schemas.contoso.com">  
    <myDataMember>  
        <myElement xmlns="" myAttribute="myValue">  
            myContents  
        </myElement>  
    </myDataMember>  
</MyDataContract>  
```  
  
 ラッパー データ メンバー要素 `<myDataMember>` が引き続き存在している点に注意してください。 データ コントラクト モデルにはこの要素を削除する方法がありません。 このモデルを処理するシリアライザー (<xref:System.Runtime.Serialization.DataContractSerializer> と <xref:System.Runtime.Serialization.NetDataContractSerializer>) では、このラッパー要素に特別な属性が出力されることがあります。 この特別な属性には、標準の XML スキーマ インスタンスの "nil" 属性 (`XmlElement` を `null` に設定できるようにする属性) や "type" 属性 (`XmlElement` をポリモーフィックに使用できるようにする属性) などがあります。 また、次の XML 属性は、WCF に固有のものです。 "Id"、"Ref"、"Type"、および "Assembly"。 これらの属性が出力されるのは、オブジェクト グラフの保存モードを有効にするか `XmlElement` を使用する場合に <xref:System.Runtime.Serialization.NetDataContractSerializer> をサポートするためです  (オブジェクトグラフの保存モードの詳細については、「[シリアル化と逆シリアル化](serialization-and-deserialization.md)」を参照してください)。  
  
 `XmlElement` の配列またはコレクションを使用できます。これらは、他の配列またはコレクションとして処理されます。 つまり、コレクション全体のラッパー要素と、配列に含まれる `<myDataMember>` ごとに個別のラッパー要素 (上記の例の `XmlElement` と同様) が存在することになります。  
  
 逆シリアル化時には、デシリアライザーによって受信 XML から `XmlElement` が作成されます。 有効な親 <xref:System.Xml.XmlDocument> は、デシリアライザーによって提供されます。  
  
 `XmlElement` に逆シリアル化される XML フラグメントでは、先祖要素のプレフィックス定義に依存するのではなく、使用するすべてのプレフィックスを定義しておく必要があります。 これは、`DataContractSerializer` を使用して、`DataContractSerializer` 以外の別のソースから XML にアクセスする場合にのみ考慮する必要があります。  
  
 と共に使用する場合、には `DataContractSerializer` `XmlElement` ポリモーフィックを割り当てることができますが、型のデータメンバーにのみ割り当てられ <xref:System.Object> ます。 <xref:System.Collections.IEnumerable> が実装されていても、`XmlElement` をコレクション型として使用したり、<xref:System.Collections.IEnumerable> データ メンバーに割り当てることはできません。 すべてのポリモーフィックな割り当てと同様に、は、 `DataContractSerializer` 結果の XML にデータコントラクト名を出力します。この場合、"" 名前空間の "XmlElement" になり http://schemas.datacontract.org/2004/07/System.Xml ます。  
  
 `NetDataContractSerializer` を使用する場合、`XmlElement` の有効なポリモーフィック割り当て (`Object` または `IEnumerable` への割り当て) がすべてサポートされます。  
  
 `XmlElement` から派生した型がポリモーフィックに割り当てられているかどうかに関係なく、このような型と上記の 2 つのシリアライザーを一緒に使用しないでください。  
  
### <a name="array-of-xmlnode"></a>XmlNode の配列  
 <xref:System.Xml.XmlNode> の配列の使用は、`XmlElement` の使用に非常に似ています。 `XmlNode` の配列を使用すると、`XmlElement` を使用する場合よりも高い柔軟性が得られます。 たとえば、データ メンバーがラップする要素内に複数の要素を作成できます。 データ メンバーがラップする要素内には、XML コメントなどの要素以外のコンテンツを挿入することもできます。 さらに、ラップする側のデータ メンバー要素にも属性を挿入できます。 これらはすべて、`XmlNode` の配列に `XmlNode` の特定の派生クラス (<xref:System.Xml.XmlAttribute>、`XmlElement`、<xref:System.Xml.XmlComment> など) を追加することによって実現できます。 たとえば、次の型を使用するとします。  
  
 [!code-csharp[DataContractAttribute#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/datacontractattribute/cs/overview.cs#5)]
 [!code-vb[DataContractAttribute#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/datacontractattribute/vb/overview.vb#5)]  
  
 シリアル化すると、生成される XML は次のコードのようになります。  
  
```xml  
<MyDataContract xmlns="http://schemas.contoso.com">  
  <myDataMember myAttribute="myValue">  
     <!--myComment-->  
     <myElement xmlns="" myAttribute="myValue">  
 myContents  
     </myElement>  
     <myElement xmlns="" myAttribute="myValue">  
       myContents  
     </myElement>  
  </myDataMember>  
</MyDataContract>  
```  
  
 データ メンバー ラッパー要素 `<myDataMember>` には、1 つの属性、1 つのコメント、および 2 つの要素が含まれています。 これらが、シリアル化された 4 つの `XmlNode` インスタンスです。  
  
 結果的に無効な XML になる `XmlNode` の配列は、シリアル化できません。 たとえば、最初のインスタンスが `XmlNode` で、次のインスタンスが `XmlElement` という 2 つの <xref:System.Xml.XmlAttribute> インスタンスの配列は、無効です。このシーケンスは、有効な XML インスタンスに対応していません (属性を関連付ける場所がありません)。  
  
 `XmlNode` の配列の逆シリアル化時には、ノードが作成され、そのノードに受信 XML からの情報が追加されます。 有効な親 <xref:System.Xml.XmlDocument> は、デシリアライザーによって提供されます。 すべてのノードは、ラッパーデータメンバー要素のすべての属性を含めて逆シリアル化されますが、WCF シリアライザーによって配置された属性 (ポリモーフィックな割り当てを示すために使用される属性など) は除外されます。 XML フラグメントですべての名前空間プレフィックスを定義するときの注意点は、`XmlNode` の逆シリアル化に適用されるのと同様に、`XmlElement` の配列の逆シリアル化にも適用されます。  
  
 オブジェクト グラフの保存を有効にしてシリアライザーを使用した場合、オブジェクトの等価性は、個別の `XmlNode` インスタンスではなく、`XmlNode` 配列のレベルでのみ保存されます。  
  
 1 つ以上のノードが `XmlNode` に設定された `null` の配列をシリアル化しないようにしてください。 配列メンバー全体を `null` にすることはできますが、配列に格納された個々の `XmlNode` を null にすることはできません。 配列メンバー全体が null の場合、ラッパー データ メンバー要素には、配列メンバー全体が null であることを示す特別な属性が含まれます。 逆シリアル化時にも、配列メンバー全体が null になります。  
  
 `XmlNode` の正規の配列だけが、シリアライザーによって特別に処理されます。 `XmlNode` を含む他のコレクション型として宣言されたデータ メンバーや、`XmlNode` から派生した型の配列として宣言されたデータ メンバーには、特別な処理は行われません。 このため、これらのデータ メンバーは、シリアル化に関するその他の条件のいずれかを満たしている場合を除き、通常はシリアル化できません。  
  
 `XmlNode` の配列の配列またはコレクションを使用できます。 コレクション全体のラッパー要素と、外側の配列またはコレクションに含まれる `<myDataMember>` の配列ごとに個別のラッパー要素 (上記の例の `XmlNode` と同様) が存在することになります。  
  
 <xref:System.Array> の `Object` または `Array` の `IEnumerable` 型のデータ メンバーに `XmlNode` インスタンスを追加しても、そのデータ メンバーが `Array` インスタンスの `XmlNode` として扱われることはありません。 配列の各メンバーは個別にシリアル化されます。  
  
 `DataContractSerializer` を使用する場合、`XmlNode` の配列をポリモーフィックに割り当てることができますが、その対象は `Object` 型のデータ メンバーだけです。 `IEnumerable` が実装されていても、`XmlNode` の配列をコレクション型として使用したり、`IEnumerable` データ メンバーに割り当てることはできません。 すべてのポリモーフィックな割り当てと同様に、は、 `DataContractSerializer` 結果の XML にデータコントラクト名を出力します。この場合、"" 名前空間の "ArrayOfXmlNode" になり http://schemas.datacontract.org/2004/07/System.Xml ます。 と共に使用する場合 `NetDataContractSerializer` 、配列の有効な代入 `XmlNode` がサポートされます。  
  
### <a name="schema-considerations"></a>スキーマの考慮事項  
 XML 型のスキーママッピングの詳細については、「[データコントラクトスキーマの参照](data-contract-schema-reference.md)」を参照してください。 ここでは、重要な点の概要について説明します。  
  
 `XmlElement` 型のデータ メンバーは、次の匿名型を使用して定義された要素にマップされます。  
  
```xml  
<xsd:complexType>  
   <xsd:sequence>  
      <xsd:any minOccurs="0" processContents="lax" />  
   </xsd:sequence>  
</xsd:complexType>  
```  
  
 `XmlNode` の Array 型のデータ メンバーは、次の匿名型を使用して定義された要素にマップされます。  
  
```xml  
<xsd:complexType mixed="true">  
   <xsd:sequence>  
      <xsd:any minOccurs="0" maxOccurs="unbounded" processContents="lax" />  
   </xsd:sequence>  
   <xsd:anyAttribute/>  
</xsd:complexType>  
```  
  
## <a name="types-implementing-the-ixmlserializable-interface"></a>IXmlSerializable インターフェイスを実装する型  
 `IXmlSerializable` インターフェイスを実装する型は、`DataContractSerializer` で完全にサポートされます。 これらの型には、スキーマを制御するために必ず <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> 属性を適用する必要があります。  
  
 `IXmlSerializable` を実装する型には、任意のコンテンツを表す型、1 つの要素を表す型、および従来の <xref:System.Data.DataSet> 型の 3 種類があります。  
  
- コンテンツ型では、`XmlSchemaProviderAttribute` 属性によって指定されたスキーマ プロバイダー メソッドが使用されます。 このメソッドから `null` が返されることはなく、属性の <xref:System.Xml.Serialization.XmlSchemaProviderAttribute.IsAny%2A> プロパティは既定値 `false` のままになります。 これは、`IXmlSerializable` 型の最も一般的な使用方法です。  
  
- 要素型は、`IXmlSerializable` 型が自身のルート要素名を制御する必要があるときに使用します。 型を要素型としてマークするには、<xref:System.Xml.Serialization.XmlSchemaProviderAttribute.IsAny%2A> 属性の <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> プロパティを `true` に設定するか、スキーマ プロバイダー メソッドから null を返します。 スキーマ プロバイダー メソッドの使用は、要素型ではオプションです。`XmlSchemaProviderAttribute` でメソッド名の代わりに null を指定できます。 ただし、`IsAny` が `true` で、スキーマ プロバイダー メソッドが指定されている場合、メソッドは null を返す必要があります。  
  
- 従来の <xref:System.Data.DataSet> 型は、`IXmlSerializable` 属性でマークされていない `XmlSchemaProviderAttribute` 型です。 これらの型は、スキーマ生成に関して <xref:System.Xml.Serialization.IXmlSerializable.GetSchema%2A> メソッドに依存しています。 以前のバージョンの .NET Framework では、このパターンが `DataSet` 型に使用され、型指定されたデータセットからクラスが派生されます。ただし、現在、このパターンは使用されなくなっており、従来の型に対応することだけを目的としてサポートされています。 このパターンに依存せず、必ず `XmlSchemaProviderAttribute` を `IXmlSerializable` 型に適用してください。  
  
### <a name="ixmlserializable-content-types"></a>IXmlSerializable コンテンツ型  
 `IXmlSerializable` を実装しており、以前に定義したコンテンツ型である型のデータ メンバーをシリアル化すると、シリアライザーはそのデータ メンバーのラッパー要素を書き込み、<xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> メソッドに制御を渡します。 <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> 実装により、ラッパー要素に属性が追加されるなど、任意の XML が書き込まれることがあります。 `WriteXml` の実行後、シリアライザーは要素を閉じます。  
  
 `IXmlSerializable` を実装しており、以前に定義したコンテンツ型である型のデータ メンバーを逆シリアル化すると、デシリアライザーはそのデータ メンバーのラッパー要素に XML リーダーを配置し、<xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> メソッドに制御を渡します。 このメソッドは、開始タグと終了タグを含む、要素全体を読み取る必要があります。 `ReadXml` コードでは、要素が空の場合も忘れずに処理してください。 また、`ReadXml` の実装では、特定の方法で名前が付けられたラッパー要素に依存しないようにしてください。 シリアライザーによって選択される名前は、異なる場合があります。  
  
 `IXmlSerializable` コンテンツ型は、たとえば <xref:System.Object> 型のデータ メンバーなどに、ポリモーフィックに割り当てることができます。 また、型インスタンスを null にすることもできます。 さらに、`IXmlSerializable` 型は、オブジェクト グラフの保存を有効にして <xref:System.Runtime.Serialization.NetDataContractSerializer> で使用することも可能です。 これらのすべての機能では、WCF シリアライザーが特定の属性をラッパー要素にアタッチする必要があります (XML スキーマインスタンス名前空間の "nil" と "type"、WCF 固有の名前空間の "Id"、"Ref"、"Type"、"Assembly")。  
  
#### <a name="attributes-to-ignore-when-implementing-readxml"></a>ReadXml を実装するときに無視する属性  
 `ReadXml` コードに制御を渡す前に、デシリアライザーは、XML 要素を調べ、前述の特別な XML 属性を検出し、その属性に従って動作します。 たとえば、"nil" が `true` の場合は、null 値が逆シリアル化され、`ReadXml` は呼び出されません。 ポリモーフィズムが検出された場合は、要素のコンテンツが別の型と同様に逆シリアル化されます。 ポリモーフィックに割り当てられた型の `ReadXml` 実装が呼び出されます。 どの場合も、これらの特別な属性がデシリアライザーによって処理されるため、`ReadXml` 実装ではこれらの属性を無視する必要があります。  
  
### <a name="schema-considerations-for-ixmlserializable-content-types"></a>IXmlSerializable コンテンツ型のスキーマに関する考慮事項  
 `IXmlSerializable` コンテンツ型のスキーマをエクスポートすると、スキーマ プロバイダー メソッドが呼び出されます。 このスキーマ プロバイダー メソッドには、<xref:System.Xml.Schema.XmlSchemaSet> が渡されます。 このメソッドは、有効なスキーマをスキーマ セットに追加できます。 スキーマ セットには、スキーマをエクスポートした時点で既に認識されていたスキーマが格納されます。 スキーマ プロバイダー メソッドは、スキーマ セットに項目を追加する必要があるときに、適切な名前空間を持つ <xref:System.Xml.Schema.XmlSchema> がそのセットに既に存在するかどうかを確認する必要があります。 存在する場合、スキーマ プロバイダー メソッドは新しい項目を既存の `XmlSchema` に追加する必要があります。 存在しない場合、新しい `XmlSchema` インスタンスを作成する必要があります。 これは、`IXmlSerializable` 型の配列を使用する場合に重要です。 たとえば、`IXmlSerializable` 型を名前空間 "B" の "A" 型としてエクスポートする場合、スキーマ プロバイダー メソッドが呼び出される前に、"B" が "ArrayOfA" 型を保持するためのスキーマがスキーマ セットに既に存在している可能性があります。  
  
 型を <xref:System.Xml.Schema.XmlSchemaSet> に追加する以外に、コンテンツ型のスキーマ プロバイダー メソッドは null 以外の値を返す必要があります。 このメソッドは、特定の <xref:System.Xml.XmlQualifiedName> 型で使用するスキーマ型の名前を指定する `IXmlSerializable` を返すことができます。 この修飾名は、その型のデータ コントラクト名および名前空間としても使用されます。 スキーマ プロバイダー メソッドは、スキーマ セットにまだ存在していない型であっても、復帰時に返すことができます。 ただし、関連するすべての型がエクスポートされる (<xref:System.Runtime.Serialization.XsdDataContractExporter.Export%2A> の関連するすべての型に対して <xref:System.Runtime.Serialization.XsdDataContractExporter> メソッドが呼び出され、<xref:System.Runtime.Serialization.XsdDataContractExporter.Schemas%2A> プロパティにアクセスする) までに、その型がスキーマ セットに存在している必要があります。 関連するすべての `Schemas` 呼び出しが実行される前に `Export` プロパティにアクセスすると、<xref:System.Xml.Schema.XmlSchemaException> が発生する可能性があります。 エクスポートプロセスの詳細については、「[クラスからのスキーマのエクスポート](exporting-schemas-from-classes.md)」を参照してください。  
  
 スキーマ プロバイダー メソッドは、使用する <xref:System.Xml.Schema.XmlSchemaType> を返すこともできます。 その型は、匿名の場合とそうでない場合があります。 匿名の場合、`IXmlSerializable` 型のスキーマは、`IXmlSerializable` 型がデータ メンバーとして使用されるたびに匿名型としてエクスポートされます。 `IXmlSerializable` 型には、データ コントラクト名と名前空間が引き続き保持されます  (これは、「[データコントラクト名](data-contract-names.md)」で説明されているように、 <xref:System.Runtime.Serialization.DataContractAttribute> 名前のカスタマイズには属性を使用できない点が異なります)。匿名でない場合は、内のいずれかの型である必要があり `XmlSchemaSet` ます。 これは、型の `XmlQualifiedName` を返す場合と同じです。  
  
 さらに、型のグローバル要素宣言がエクスポートされます。 型に <xref:System.Xml.Serialization.XmlRootAttribute> 属性が適用されていない場合、その要素にはデータ コントラクトと同じ名前と名前空間が使用され、その "nillable" プロパティは true に設定されます。 唯一の例外は、スキーマの名前空間 (" http://www.w3.org/2001/XMLSchema ") です。型のデータコントラクトがこの名前空間にある場合、対応するグローバル要素は、スキーマの名前空間に新しい要素を追加することが禁止されているため、空の名前空間にあります。 型に `XmlRootAttribute` 属性が適用されている場合、グローバル要素宣言は、<xref:System.Xml.Serialization.XmlRootAttribute.ElementName%2A>、<xref:System.Xml.Serialization.XmlRootAttribute.Namespace%2A>、および <xref:System.Xml.Serialization.XmlRootAttribute.IsNullable%2A> の各プロパティを使用してエクスポートされます。 `XmlRootAttribute` が適用された場合の既定値は、データ コントラクト名、空白の名前空間、および true に設定された "nillable" です。  
  
 同じグローバル要素宣言の規則が、従来のデータセット型に適用されます。 `XmlRootAttribute` は、カスタム コードによって追加されたグローバル要素宣言をオーバーライドできません。これには、スキーマ プロバイダー メソッドを使用して `XmlSchemaSet` に追加された場合と、従来のデータセット型に対して `GetSchema` を使用して追加された場合があります。  
  
### <a name="ixmlserializable-element-types"></a>IXmlSerializable 要素型  
 `IXmlSerializable` 要素型には、`IsAny` に設定された `true` プロパティか、`null` を返すスキーマ プロバイダー メソッドのいずれかが含まれています。  
  
 要素型のシリアル化と逆シリアル化は、コンテンツ型のシリアル化と逆シリアル化に非常に似ています。 ただし、重要な違いがいくつかあります。  
  
- `WriteXml` の実装では、要素 (これには複数の子要素が含まれている可能性もありますが) を 1 つだけ出力することが想定されています。 この 1 つの要素の外側にある属性、複数の兄弟要素、またはこれらが混在したコンテンツを出力することはできません。 要素は空であってもかまいません。  
  
- `ReadXml` の実装では、ラッパー要素の読み取りは想定されていません。 読み取ることが想定されているのは、`WriteXml` で生成される要素 1 つのみです。  
  
- 要素型を一様にシリアル化する場合 (データ コントラクトのデータ メンバーとしてシリアル化する場合など) は、コンテンツ型の場合と同様に、`WriteXml` を呼び出す前にラッパー要素が出力されます。 ただし、`WriteXml` コンストラクターまたは `DataContractSerializer` コンストラクターによるシリアライザーの構築時にルート名と名前空間が明示的に指定されていない限り、トップ レベルで要素型をシリアル化しても、通常は `NetDataContractSerializer` で書き出される要素を囲むラッパー要素が出力されることはありません。 詳細については、「[シリアル化と逆シリアル化](serialization-and-deserialization.md)」を参照してください。  
  
- 構築時にルート名と名前空間を指定せずにトップ レベルで要素型をシリアル化した場合、<xref:System.Runtime.Serialization.XmlObjectSerializer.WriteStartObject%2A> と <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteEndObject%2A> では基本的に何も実行されず、<xref:System.Runtime.Serialization.XmlObjectSerializer.WriteObjectContent%2A> によって `WriteXml` が呼び出されます。 このモードでは、シリアル化されるオブジェクトは null にできず、ポリモーフィックに割り当てることができません。 また、オブジェクト グラフの保存を有効化できず、`NetDataContractSerializer` も使用できません。  
  
- 構築時にルート名と名前空間を指定せずにトップ レベルで要素型を逆シリアル化したときに、要素の先頭を検出できた場合は、<xref:System.Runtime.Serialization.XmlObjectSerializer.IsStartObject%2A> が `true` を返します。 <xref:System.Runtime.Serialization.XmlObjectSerializer.ReadObject%2A> パラメーターが `verifyObjectName` に設定されている `true` は、実際にオブジェクトを読み取る前の動作が `IsStartObject` と同様です。 その後、`ReadObject` は制御を `ReadXml` メソッドに渡します。  
  
 要素型の場合も、エクスポートされるスキーマは、前のセクションで説明した `XmlElement` 型に対するスキーマと同じです。ただし、スキーマ プロバイダー メソッドは、コンテンツ型と同様、追加のスキーマを <xref:System.Xml.Schema.XmlSchemaSet> に追加できます。 要素型には `XmlRootAttribute` 属性を使用することはできないので、グローバル要素宣言は要素型に対して出力されません。  
  
### <a name="differences-from-the-xmlserializer"></a>XmlSerializer との相違点  
 `IXmlSerializable` インターフェイス、`XmlSchemaProviderAttribute` 属性、および `XmlRootAttribute` 属性は、<xref:System.Xml.Serialization.XmlSerializer> でも認識されます。 ただし、データ コントラクト モデルでの処理方法に違いがあります。 重要な違いを以下にまとめます。  
  
- スキーマ プロバイダー メソッドは、`XmlSerializer` で使用できるようにするためにパブリックにする必要がありますが、データ コントラクト モデルで使用するためにパブリックにする必要はありません。  
  
- スキーマ プロバイダー メソッドは、データ コントラクト モデルで `IsAny` が true の場合に呼び出されますが、`XmlSerializer` では呼び出されません。  
  
- コンテンツ型または従来のデータセット型に `XmlRootAttribute` 属性がない場合、`XmlSerializer` は、グローバル要素宣言を空白の名前空間にエクスポートします。 データ コントラクト モデルで通常使用される名前空間は、前に説明したとおりデータ コントラクトの名前空間です。  
  
 両方のシリアル化技術で使用する型を作成する場合には、これらの違いに注意してください。  
  
### <a name="importing-ixmlserializable-schema"></a>IXmlSerializable スキーマのインポート  
 `IXmlSerializable` 型から生成されたスキーマをインポートする場合、次のような状況が考えられます。  
  
- 生成されるスキーマは、「[データコントラクトスキーマの参照](data-contract-schema-reference.md)」で説明されている有効なデータコントラクトスキーマである場合があります。 この場合は、スキーマを通常どおりにインポートでき、通常のデータ コントラクト型が生成されます。  
  
- 生成されたスキーマが、有効なデータ コントラクト スキーマではない場合があります。 たとえば、スキーマ プロバイダー メソッドによって、データ コントラクト モデルでサポートされていない XML 属性を含むスキーマが生成されることがあります。 この場合、スキーマを `IXmlSerializable` 型としてインポートできます。 このインポートモードは、既定ではオンになっていませんが、 `/importXmlTypes` [ServiceModel メタデータユーティリティツール (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)へのコマンドラインスイッチなどを使用して、簡単に有効にすることができます。 この詳細については、「[クラスを生成するためのスキーマのインポート](importing-schema-to-generate-classes.md)」を参照してください。 型インスタンスを処理するには、XML を直接操作する必要があります。 `XmlSerializer` の使用方法に関するトピックを参照し、より広い範囲のスキーマをサポートする別のシリアル化技術を使用することを検討することもできます。  
  
- 新しい型を生成する代わりに、プロキシ内の既存の `IXmlSerializable` 型を再利用できます。 この場合、「型を作成するためのスキーマのインポート」で説明する参照型の機能を使用して、再利用する型を示すことができます。 これは、Svcutil.exe で `/reference` スイッチを使用して、再利用する型を含むアセンブリを指定することに相当します。  
  
## <a name="representing-arbitrary-xml-in-data-contracts"></a>データ コントラクトでの任意の XML の表現  
 `XmlElement` 型、`XmlNode` の配列、および `IXmlSerializable` 型を使用すると、任意の XML をデータ コントラクト モデルに挿入できます。 `DataContractSerializer` と `NetDataContractSerializer` は、プロセスには介入せずに、使用している XML ライターにこの XML コンテンツを渡します。 ただし、XML ライターは、出力する XML に対して特定の制限を適用することがあります。 次に重要な例を具体的に示します。  
  
- 通常、XML ライターでは、 \<?xml version=’1.0’ ?> 別のドキュメントの書き込み中に xml ドキュメント宣言 (など) を使用することはできません。 完全な XML ドキュメントを取得して、それを `Array` データ メンバーの `XmlNode` としてシリアル化したりすることはできません。 これを実行するには、ドキュメントの宣言を取り除くか、独自のエンコード方法でこの宣言を表現する必要があります。  
  
- SOAP メッセージでは許可されていないため、WCF で提供されるすべての XML ライターは XML 処理命令 ( \<? … ?> ) およびドキュメント型定義 ( \<! … > ) を拒否します。 この場合も、独自のエンコード機構を使用して、この制限に対処できます。 生成される XML に XML 処理命令と文書型定義を含める必要がある場合は、この 2 つをサポートする XML ライターを使用するカスタム エンコーダーを作成できます。  
  
- `WriteXml` を実装するときは、XML ライターで <xref:System.Xml.XmlWriter.WriteRaw%2A> メソッドを呼び出さないようにします。 WCF では、さまざまな XML エンコーディング (バイナリを含む) を使用し `WriteRaw` ます。そのため、結果を任意のエンコーディングで使用できるようにすることは非常に困難または不可能です。  
  
- を実装する場合は、 `WriteXml` <xref:System.Xml.XmlWriter.WriteEntityRef%2A> <xref:System.Xml.XmlWriter.WriteNmToken%2A> WCF で提供される XML ライターでサポートされていないメソッドとメソッドを使用しないようにしてください。  
  
## <a name="using-dataset-typed-dataset-and-datatable"></a>DataSet、Typed DataSet、および DataTable の使用  
 データ コントラクト モデルでは、この 3 つの型の使用が完全にサポートされています。 これらの型を使用する場合は、次の点に注意してください。  
  
- これらの型 (特に、型指定された派生クラス) のスキーマは、 <xref:System.Data.DataSet> 一部の非 WCF プラットフォームと相互運用できない可能性があります。また、これらのプラットフォームで使用する場合、使いやすさが低下する可能性があります。 また、`DataSet` 型の使用はパフォーマンスに影響を与えることがあります。 さらに、将来的にアプリケーションのバージョン管理が通常より難しくなる可能性もあります。 コントラクトでは、`DataSet` 型の代わりに、明示的に定義されたデータ コントラクト型を使用することを検討してください。  
  
- `DataSet` スキーマまたは `DataTable` スキーマをインポートする際には、これらの型を参照することが重要です。 Svcutil.exe コマンドラインツールを使用すると、スイッチに system.servicemodel アセンブリ名を渡すことによってこれを実現できます。 `/reference` 型指定されたデータセット スキーマをインポートする場合、その型指定されたデータセットの型を参照する必要があります。 Svcutil.exe を使用して、型指定されたデータセットのアセンブリの場所をスイッチに渡し `/reference` ます。 参照型の詳細については、「[クラスを生成するためのスキーマのインポート](importing-schema-to-generate-classes.md)」を参照してください。  
  
 データ コントラクト モデルでは、型指定された DataSet のサポートが制限されています。 型指定された DataSet は、シリアル化と逆シリアル化が可能であり、スキーマをエクスポートすることもできます。 ただし、データ コントラクト スキーマのインポートでは、既存のスキーマの再利用のみが行われるため、型指定された新しい DataSet 型をスキーマから生成することはできません。 Svcutil.exe ツールで `/r` スイッチを使用して、型指定された既存の DataSet を指し示すことができます。 型指定されたデータセットを使用するサービスで、`/r` スイッチを指定せずに Svcutil.exe を使用しようとすると、代替のシリアライザー (XmlSerializer) が自動的に選択されます。 DataContractSerializer を使用することも、スキーマから DataSet を生成することも必要である場合は、(サービスで `/d` スイッチを指定した Xsd.exe ツールを使用して) 型指定された DataSet 型を生成し、型をコンパイルした後に、Svcutil.exe で `/r` スイッチを使用して、それらの型を指し示します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Xml.Serialization.IXmlSerializable>
- [データ コントラクトの使用](using-data-contracts.md)
- [データ コントラクト シリアライザーでサポートされる型](types-supported-by-the-data-contract-serializer.md)
