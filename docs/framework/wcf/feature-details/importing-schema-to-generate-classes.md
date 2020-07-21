---
title: クラスを作成するためのスキーマのインポート
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, schema import and export
- XsdDataContractImporter class
ms.assetid: b9170583-8c34-43bd-97bb-6c0c8dddeee0
ms.openlocfilehash: 01f5162727a213fa5dcdf8a70e4e8e4c3627f086
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596904"
---
# <a name="importing-schema-to-generate-classes"></a>クラスを作成するためのスキーマのインポート
Windows Communication Foundation (WCF) で使用できるスキーマからクラスを生成するには、クラスを使用し <xref:System.Runtime.Serialization.XsdDataContractImporter> ます。 ここでは、生成時に指定できる各種のオプションについて解説します。  
  
## <a name="the-import-process"></a>インポート処理
 スキーマのインポート処理は、<xref:System.Xml.Schema.XmlSchemaSet> を用意し、<xref:System.CodeDom.CodeCompileUnit> を生成することから始まります。  
  
 は、 `XmlSchemaSet` XML スキーマ定義言語 (XSD) スキーマドキュメントのセットを表す .NET Framework のスキーマオブジェクトモデル (SOM) の一部です。 一連の XSD ドキュメントから `XmlSchemaSet` オブジェクトを生成する過程では、各ドキュメントを逆シリアル化して <xref:System.Xml.Schema.XmlSchema> オブジェクトにし (<xref:System.Xml.Serialization.XmlSerializer> を使用)、新規に作っておいた空の `XmlSchemaSet` に追加していきます。  
  
 は、 `CodeCompileUnit` 抽象的な方法で .NET Framework コードを表す .NET Framework の Code Document Object Model (CodeDOM) の一部です。 実際のコードを `CodeCompileUnit` から生成するには、<xref:System.CodeDom.Compiler.CodeDomProvider> のサブクラスである、<xref:Microsoft.CSharp.CSharpCodeProvider> や <xref:Microsoft.VisualBasic.VBCodeProvider> を使います。  
  
### <a name="to-import-a-schema"></a>スキーマをインポートするには  
  
1. <xref:System.Runtime.Serialization.XsdDataContractImporter> のインスタンスを作成します。  
  
2. 任意。 `CodeCompileUnit` をコンストラクターに渡します。 スキーマのインポート時に生成された型がこの `CodeCompileUnit` インスタンスに追加されるので、以降の処理は、`CodeCompileUnit` が空でない状態から始まります。  
  
3. 任意。 <xref:System.Runtime.Serialization.XsdDataContractImporter.CanImport%2A> メソッドのいずれかを呼び出します。 指定されたスキーマが有効なデータ コントラクト スキーマであって、インポートしても問題ないかどうかを判断するメソッドです。 `CanImport` メソッドには、次の手順に出てくる `Import` と同様に、オーバーロードがあります。  
  
4. オーバーロードされた `Import` メソッドのいずれか、たとえば <xref:System.Runtime.Serialization.XsdDataContractImporter.Import%28System.Xml.Schema.XmlSchemaSet%29> を呼び出します。  
  
     これは、指定しなければならない引数が `XmlSchemaSet` だけという最も簡潔なオーバーロードであり、匿名型を含め、一連のスキーマに記述されている型をすべてインポートできます。 他に、XSD 型、あるいはインポートする型のリストを (<xref:System.Xml.XmlQualifiedName>、または `XmlQualifiedName` オブジェクトのコレクションとして) 指定できるオーバーロードもあります。 この場合は、指定した型だけがインポートされます。 また、引数として <xref:System.Xml.Schema.XmlSchemaElement> を受け取り、`XmlSchemaSet` のうち特定の要素を、対応する型 (匿名型を含む) と併せてインポートするオーバーロードもあります。 このメソッドの戻り値は `XmlQualifiedName` であり、この要素に対応して生成された型のデータ コントラクト名を表します。  
  
     `Import` メソッドを何度も呼び出すと、同じ `CodeCompileUnit` に複数の項目が追加されます。 `CodeCompileUnit` に既に存在する型は生成されません。 したがって、`Import` オブジェクトをいくつも使うのではなく、同じ `XsdDataContractImporter` の `XsdDataContractImporter` を必要な回数呼び出すようにしてください。 同じ型が重複して生成されることがないので、この方法をお勧めします。  
  
    > [!NOTE]
    > インポート中に障害が発生した場合の `CodeCompileUnit` の状態は不定です。 このような `CodeCompileUnit` を使うと、セキュリティ上の脆弱性につながるおそれがあります。  
  
5. `CodeCompileUnit` プロパティを介して、 <xref:System.Runtime.Serialization.XsdDataContractImporter.CodeCompileUnit%2A> にアクセスします。  
  
### <a name="import-options-customizing-the-generated-types"></a>インポート オプション : 生成された型のカスタマイズ  
 <xref:System.Runtime.Serialization.XsdDataContractImporter.Options%2A> の <xref:System.Runtime.Serialization.XsdDataContractImporter> プロパティとして <xref:System.Runtime.Serialization.ImportOptions> クラスのインスタンスを設定することにより、インポート処理の方法を制御できます。 生成される型に直接影響するオプションが多数あります。  
  
#### <a name="controlling-the-access-level-generateinternal-or-the-internal-switch"></a>アクセス レベルの制御 (GenerateInternal または /internal スイッチ)  
 これは、 [ServiceModel メタデータユーティリティツール (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)の **/内部**スイッチに相当します。  
  
 通常、スキーマから生成されるのはパブリック型です。ここにプライベート フィールドや対応するパブリック データ メンバー プロパティが定義されます。 パブリック型ではなく内部型を生成したい場合は、<xref:System.Runtime.Serialization.ImportOptions.GenerateInternal%2A> プロパティを `true` としてください。  
  
 次の例は、<xref:System.Runtime.Serialization.ImportOptions.GenerateInternal%2A> プロパティが `true.` の場合に、スキーマがどのように内部型に変換されるかを表します。  
  
 [!code-csharp[c_SchemaImportExport#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#2)]
 [!code-vb[c_SchemaImportExport#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#2)]  
  
#### <a name="controlling-namespaces-namespaces-or-the-namespace-switch"></a>名前空間の制御 (Namespaces または /namespace スイッチ)  
 これは、ツールの **/namespace**スイッチに相当し `Svcutil.exe` ます。  
  
 通常、スキーマから生成された型は .NET Framework 名前空間に生成されます。各 XSD 名前空間は、「[データコントラクトスキーマリファレンス](data-contract-schema-reference.md)」で説明されているマッピングに従って、特定の .NET Framework 名前空間に対応します。 この対応関係は、<xref:System.Runtime.Serialization.ImportOptions.Namespaces%2A> の <xref:System.Collections.Generic.Dictionary%602> プロパティでカスタマイズできます。 指定された XSD 名前空間がディクショナリで見つかった場合は、一致する .NET Framework 名前空間もディクショナリから取得されます。  
  
 たとえば、次のスキーマを考えます。  
  
 [!code-xml[c_SchemaImportExport#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/common/source.config#10)]  
  
 次の例では、プロパティを使用して `Namespaces` 、 `http://schemas.contoso.com/carSchema` 名前空間を "Contoso. 車" にマップしています。  
  
 [!code-csharp[c_SchemaImportExport#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#8)]
 [!code-vb[c_SchemaImportExport#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#8)]  
  
#### <a name="adding-the-serializableattribute-generateserializable-or-the-serializable-switch"></a>SerializableAttribute の追加 (GenerateSerializable または /serializable スイッチ)  
 これは、ツールの **/シリアル化**可能なスイッチに対応し `Svcutil.exe` ます。  
  
 場合によっては、スキーマから生成された型を .NET Framework ランタイムシリアル化エンジン (クラス、クラスなど) で使用できるようにすることが重要になり <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=nameWithType> <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> ます。 これは、.NET Framework のリモート処理に型を使用する場合に便利です。 そのためには、生成された型に対して、通常の <xref:System.SerializableAttribute> 属性に加え、<xref:System.Runtime.Serialization.DataContractAttribute> 属性も適用する必要があります。 `GenerateSerializable` オプションを `true` に設定すると、この属性が自動的に生成されます。  
  
 `Vehicle` オプションを `GenerateSerializable` に設定して `true` クラスを生成する例を示します。  
  
 [!code-csharp[c_SchemaImportExport#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#4)]
 [!code-vb[c_SchemaImportExport#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#4)]  
  
#### <a name="adding-data-binding-support-enabledatabinding-or-the-enabledatabinding-switch"></a>データ バインディング機能の追加 (EnableDataBinding または /enableDataBinding スイッチ)  
 これは、Svcutil.exe ツールの **/enabledatabinding**スイッチに対応しています。  
  
 スキーマから生成された型を GUI コンポーネントにバインドして、この型のインスタンスを更新したとき、自動的に UI にも反映されるようにする場合があります。 `XsdDataContractImporter` は、生成する型に <xref:System.ComponentModel.INotifyPropertyChanged> インターフェイスを実装して、プロパティが変更されるとイベントが発生するようにすることができます。 このインターフェイスをサポートするクライアント UI プログラミング環境 (Windows Presentation Foundation (WPF) など) で使用する型を生成する場合は、プロパティをに設定して、 <xref:System.Runtime.Serialization.ImportOptions.EnableDataBinding%2A> `true` この機能を有効にします。  
  
 `Vehicle` プロパティを <xref:System.Runtime.Serialization.ImportOptions.EnableDataBinding%2A> に設定して生成した `true` クラスの例を以下に示します。  
  
 [!code-csharp[C_SchemaImportExport#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#5)]
 [!code-vb[C_SchemaImportExport#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#5)]  
  
### <a name="import-options-choosing-collection-types"></a>インポート オプション: コレクション型の選択  
 XML でアイテムのコレクションを表すパターンには、アイテムのリストと、アイテム間の関連付けの 2 種類があります。 文字列のリストの例を次に示します。  
  
 [!code-xml[C_SchemaImportExport#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/common/source.config#11)]  
  
 文字列と整数 (`city name` と `population`) を関連付ける例を次に示します。  
  
 [!code-xml[C_SchemaImportExport#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/common/source.config#12)]  
  
> [!NOTE]
> 関連付けもリストと見なすことができます。 たとえば、上記の関連付けは、文字列と整数の 2 つのフィールドから成る複雑な `city` オブジェクトのリストと考えることも可能です。 どちらの方法であっても、XSD スキーマで表現できます。 リストとアソシエーションを区別する方法はありません。そのため、このようなパターンは、WCF に固有の注釈がスキーマ内に存在しない限り、常にリストとして扱われます。 注釈がある場合は、関連付けを表すものとして扱われます。 詳細については、「[データコントラクトスキーマの参照](data-contract-schema-reference.md)」を参照してください。  
  
 通常、リストは、コレクションの標準の名前付けパターンに従っているかどうかによって、ジェネリックリストまたは .NET Framework 配列から派生したコレクションデータコントラクトとしてインポートされます。 詳細については、「[データコントラクトのコレクション型](collection-types-in-data-contracts.md)」を参照してください。 関連付けは通常、<xref:System.Collections.Generic.Dictionary%602>、または辞書オブジェクトから派生したコレクション データ コントラクトとしてインポートされます。 たとえば、次のスキーマを考えます。  
  
 [!code-xml[c_SchemaImportExport#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/common/source.config#13)]  
  
 これをインポートすると次のようになります (読みやすいようプロパティの代わりにフィールドを記載)。  
  
 [!code-csharp[c_SchemaImportExport#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#6)]
 [!code-vb[c_SchemaImportExport#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#6)]  
  
 このようなスキーマ パターンに対し、生成されるコレクション型をカスタマイズすることも可能です。 たとえば、<xref:System.ComponentModel.BindingList%601> クラスではなく <xref:System.Collections.Generic.List%601> クラスからコレクションを生成することにより、型をリスト ボックスにバインドし、コレクションの内容が変わると自動的にリスト ボックスにも反映されるようにすることを考えてみましょう。 これは、<xref:System.Runtime.Serialization.ImportOptions.ReferencedCollectionTypes%2A> クラスの <xref:System.Runtime.Serialization.ImportOptions> プロパティとして、実際に使うコレクション型 (以下、"参照される" 型) のリストを設定すると実現できます。 コレクションのインポート時には、参照されるコレクション型のリストが順に調べられ、最も適したコレクションがあれば、それが使用されます。 関連付けは <xref:System.Collections.IDictionary> インターフェイス (ジェネリックか否かにかかわらず) を実装した型にしか照合されませんが、リストはサポートされているすべてのコレクション型に照合されます。  
  
 たとえば <xref:System.Runtime.Serialization.ImportOptions.ReferencedCollectionTypes%2A> プロパティに <xref:System.ComponentModel.BindingList%601> を設定すると、上記の例にある `people` 型は次のように生成されます。  
  
 [!code-csharp[C_SchemaImportExport#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#7)]
 [!code-vb[C_SchemaImportExport#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#7)]  
  
 クローズ ジェネリック型 (型パラメーターすべてに具体的な型が指定されているジェネリック型) は、合致度が最も高いと見なされます。 したがって、たとえば `BindingList(Of Integer)` と <xref:System.Collections.ArrayList> の 2 つの型を "参照される" 型のコレクションに渡した場合、スキーマ内に整数のリストがあると、すべて `BindingList(Of Integer)` としてインポートされます。 一方、それ以外のリスト (`List(Of String)` など) は、`ArrayList` としてインポートされます。  
  
 ジェネリック `IDictionary` インターフェイスを実装する型を "参照される" 型のコレクションに追加した場合、型パラメーターは、完全にオープンであるか完全にクローズであるかのどちらかです。  
  
 複製は使用できません。 たとえば `List(Of Integer)` と `Collection(Of Integer)` の両方を "参照される" 型に追加することはできません。 仮に追加したとしても、整数のリストがスキーマ中に表れたとき、どちらを使うか決められないからです。 もっとも、このような重複が検出されるのは、それが問題になるような型がスキーマ中にある場合だけです。 インポートするスキーマ中に、たとえば整数のリストがないのであれば、`List(Of Integer)` と `Collection(Of Integer)` の両方が "参照される" 型のコレクションにあっても問題はなく、単に何にも使われなかったというだけのことです。  
  
 参照されるコレクション型のしくみは、プリミティブ型のコレクションばかりでなく、複合型のコレクション (他のコレクションから成るコレクションを含む) にも同様に働きます。  
  
 プロパティは、 `ReferencedCollectionTypes` svcutil.exe ツールの **/collectionType**スイッチに対応します。 複数のコレクション型を参照するには、 **/collectionType**スイッチを複数回指定する必要があることに注意してください。 型が Mscorlib.dll に含まれていない場合は、そのアセンブリも **/reference**スイッチを使用して参照する必要があります。  
  
#### <a name="import-options-referencing-existing-types"></a>インポート オプション : 既存の型の参照  
 場合によっては、スキーマの型が既存の .NET Framework 型に対応しており、これらの型を最初から生成する必要はありません。 (以下の説明は、非コレクション型にのみ当てはまります。 コレクション型については、前のセクションを参照してください)。  
  
 たとえば、企業全体で共通に、"Person" というデータ コントラクト型を使っており、人を表す場合には常にこれを使いたいとします。 いくつかのサービスでこの型を利用し、そのスキーマがサービス メタデータに表示される場合は、このスキーマをインポートするときに既存の `Person` 型を再利用でき、サービスごとに新たに生成する必要がありません。  
  
 これを行うには、再利用する .NET Framework の種類の一覧を、 <xref:System.Runtime.Serialization.ImportOptions.ReferencedTypes%2A> プロパティがクラスで返すコレクションに渡し <xref:System.Runtime.Serialization.ImportOptions> ます。 これらの型のいずれかが、スキーマ型の名前および名前空間と一致すれば、その構造が比較されます。 型に一致する名前と一致する構造体の両方があると判断された場合は、新しい型を生成する代わりに、既存の .NET Framework 型が再利用されます。 名前だけが一致して構造が一致しない場合は、例外が発生します。 型の参照時に、バージョンによる (オプションのデータ メンバーの追加などの) 差異は許容されません。 構造は厳密に合致しなければなりません。  
  
 "参照される" 型のコレクションに、データ コントラクト名と名前空間が同一である型を重複して追加しても、その名前と名前空間でスキーマ型をインポートしない限り問題ありません。 したがって、実際にはスキーマに現れることのない型については重複を気にすることなく、アセンブリ内の型をすべてコレクションに追加してしまうことができます。  
  
 プロパティは、 `ReferencedTypes` svcutil.exe ツールの特定の操作モードでの **/reference**スイッチに対応しています。  
  
> [!NOTE]
> **サービス参照の追加**ツールで svcutil.exe または (Visual Studio では) を使用すると、mscorlib.dll 内のすべての型が自動的に参照されます。  
  
#### <a name="import-options-importing-non-datacontract-schema-as-ixmlserializable-types"></a>インポート オプション : 非データ コントラクト スキーマを IXmlSerializable 型としてインポート  
 <xref:System.Runtime.Serialization.XsdDataContractImporter> は、どのようなスキーマでもインポートできるわけではありません。 未対応のスキーマ構造 (たとえば XML 属性) をインポートしようとすると例外が発生します。 ただし <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A> プロパティを `true` に設定すると、対応可能なスキーマの範囲が広がります。 `true` に設定すると、<xref:System.Runtime.Serialization.XsdDataContractImporter> は、<xref:System.Xml.Serialization.IXmlSerializable> インターフェイスを実装した型を生成します。 そのため、これらの型の XML 表現に直接アクセスできるようになります。  
  
##### <a name="design-considerations"></a>デザインに関する考慮事項  
  
- 弱く型指定された XML 表現を直接扱うのは困難です。 データ コントラクトと互換性がないスキーマを厳密に型指定された方法で操作するには、<xref:System.Xml.Serialization.XmlSerializer> などの別のシリアル化エンジンの使用を検討します。 詳細については、「 [XmlSerializer クラスの使用](using-the-xmlserializer-class.md)」を参照してください。  
  
- スキーマ構造によっては、<xref:System.Runtime.Serialization.XsdDataContractImporter> プロパティを <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A> に設定しても、`true` でインポートできない場合があります。 このような場合も、<xref:System.Xml.Serialization.XmlSerializer> の使用を検討します。  
  
- がである場合、 <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A> `true` または `false` 「[データコントラクトスキーマの参照](data-contract-schema-reference.md)」で説明されている場合に、サポートされているスキーマ構造を正確に示します。  
  
- 生成された <xref:System.Xml.Serialization.IXmlSerializable> 型に対するスキーマには、いったんインポートしてからエクスポートした場合、忠実性が維持されません。 つまり、生成された型を基にスキーマをエクスポートし、再びこれをクラスとしてインポートした場合、元どおりのスキーマにはなりません。  
  
 <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A> のオプションは、上記の <xref:System.ServiceModel.Description.ServiceContractGenerator.ReferencedTypes%2A> オプションと組み合わせて指定できます。 <xref:System.Xml.Serialization.IXmlSerializable> を実装する形で生成される型に関しては、<xref:System.ServiceModel.Description.ServiceContractGenerator.ReferencedTypes%2A> で型を指定する際、構造がチェックされません。  
  
 オプションは、 <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A> svcutil.exe ツールの **/importxmltypes**スイッチに対応しています。  
  
##### <a name="working-with-generated-ixmlserializable-types"></a>生成された IXmlSerializable 型の使い方  
 生成された `IXmlSerializable` 型には、<xref:System.Xml.XmlNode> オブジェクトの配列を返す "nodesField" というプライベート フィールドがあります。 このような型のインスタンスを逆シリアル化すると、XML ドキュメント オブジェクト モデルに基づき、このフィールドを介して XML データに直接アクセスできるようになります。 この型のインスタンスをシリアル化する際、"nodesField" フィールドに XML データを設定しておくと、これもシリアル化の対象になります。  
  
 以上の処理は `IXmlSerializable` インターフェイスで実装されます。 生成された `IXmlSerializable` 型では、<xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> の実装により、<xref:System.Runtime.Serialization.XmlSerializableServices.ReadNodes%2A> クラスの <xref:System.Runtime.Serialization.XmlSerializableServices> メソッドが呼び出されます。 これは <xref:System.Xml.XmlReader> を介して渡された XML を <xref:System.Xml.XmlNode> オブジェクトに変換するヘルパー メソッドです。 <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> を実装したコードは逆に、`XmlNode` オブジェクトの配列を、一連の <xref:System.Xml.XmlWriter> の呼び出しに変換します。 それには <xref:System.Runtime.Serialization.XmlSerializableServices.WriteNodes%2A> メソッドを使います。  
  
 スキーマのエクスポート処理は、生成された `IXmlSerializable` クラスに対して実行できます。 ただし、先に述べたように、元どおりのスキーマは再現されません。 代わりに、XSD 型のワイルドカードである "anyType" という標準 XSD 型が取得されます。  
  
 これを実現するには、 <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> 生成されたクラスに属性を適用 `IXmlSerializable` し、メソッドを呼び出して <xref:System.Runtime.Serialization.XmlSerializableServices.AddDefaultSchema%2A> "anyType" 型を生成するメソッドを指定します。  
  
> [!NOTE]
> <xref:System.Runtime.Serialization.XmlSerializableServices> 型は、この機能を提供するためだけに用意されています。 他の目的で使用することはお勧めできません。  
  
#### <a name="import-options-advanced-options"></a>インポート オプション : 高度なオプション  
 他にも、次のようなオプションがあります。  
  
- <xref:System.Runtime.Serialization.ImportOptions.CodeProvider%2A> プロパティ。 生成されたクラスに組み込むコードを生成するために使用する、<xref:System.CodeDom.Compiler.CodeDomProvider> を指定します。 インポートの際は、<xref:System.CodeDom.Compiler.CodeDomProvider> でサポートされていない機能が回避されます。 が設定されて <xref:System.Runtime.Serialization.ImportOptions.CodeProvider%2A> いない場合は、.NET Framework 機能の完全なセットが制限なしで使用されます。  
  
- <xref:System.Runtime.Serialization.ImportOptions.DataContractSurrogate%2A> プロパティ。 <xref:System.Runtime.Serialization.IDataContractSurrogate> の実装を指定するために使います。 <xref:System.Runtime.Serialization.IDataContractSurrogate> は、インポート処理をカスタマイズします。 詳細については、「[データコントラクトサロゲート](../extending/data-contract-surrogates.md)」を参照してください。 既定では、サロゲートは使用されません。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Runtime.Serialization.XsdDataContractImporter>
- <xref:System.Runtime.Serialization.XsdDataContractExporter>
- <xref:System.Runtime.Serialization.ImportOptions>
- [データ コントラクト スキーマの参照](data-contract-schema-reference.md)
- [データ コントラクト サロゲート](../extending/data-contract-surrogates.md)
- [スキーマのインポートとエクスポート](schema-import-and-export.md)
- [クラスからのスキーマのエクスポート](exporting-schemas-from-classes.md)
- [データ コントラクト スキーマの参照](data-contract-schema-reference.md)
