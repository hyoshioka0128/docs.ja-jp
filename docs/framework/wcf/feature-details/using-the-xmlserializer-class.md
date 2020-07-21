---
title: XmlSerializer クラスの使用
description: WCF がクライアントとサービスの間で送信される XML にアプリケーションのデータをシリアル化するために使用する XmlSerializer について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XmlSerializer [WCF], using
ms.assetid: c680602d-39d3-44f1-bf22-8e6654ad5069
ms.openlocfilehash: f7473de3f34ba543b4fabfe93167ea267f16dda5
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246384"
---
# <a name="using-the-xmlserializer-class"></a>XmlSerializer クラスの使用

Windows Communication Foundation (WCF) では、2つの異なるシリアル化テクノロジを使用して、アプリケーション内のデータを、クライアントとサービスの間で送信される XML に変換できます。これは、シリアル化と呼ばれるプロセスです。

## <a name="datacontractserializer-as-the-default"></a>既定としての DataContractSerializer

既定では、WCF はクラスを使用して <xref:System.Runtime.Serialization.DataContractSerializer> データ型をシリアル化します。 このシリアライザーは、次の型をサポートします。

- プリミティブ型 (整数、文字列、バイト配列など) や、プリミティブとして処理される <xref:System.Xml.XmlElement> や <xref:System.DateTime> などの特殊な型。

- データ コントラクト型 (<xref:System.Runtime.Serialization.DataContractAttribute> 属性でマークされた型)。

- <xref:System.SerializableAttribute> インターフェイスを実装する型など、<xref:System.Runtime.Serialization.ISerializable> 属性でマークされた型。

- <xref:System.Xml.Serialization.IXmlSerializable> インターフェイスを実装する型。

- 多くのジェネリック コレクション型を含む多くの共通コレクション型。

多くの .NET Framework 型は、後者の2つのカテゴリに分類されるため、シリアル化できます。 シリアル化可能な型の配列もシリアル化可能です。 完全な一覧については、「[サービスコントラクトでのデータ転送の指定](specifying-data-transfer-in-service-contracts.md)」を参照してください。

<xref:System.Runtime.Serialization.DataContractSerializer>新しい WCF サービスを記述するには、データコントラクト型と共に使用されるを使用することをお勧めします。 詳細については、「[データコントラクトの使用](using-data-contracts.md)」を参照してください。

## <a name="when-to-use-the-xmlserializer-class"></a>XmlSerializer クラスを使用する場合

WCF では、クラスもサポートさ <xref:System.Xml.Serialization.XmlSerializer> れています。 <xref:System.Xml.Serialization.XmlSerializer>クラスは WCF に固有ではありません。 これは、ASP.NET Web サービスが使用するのと同じシリアル化エンジンです。 <xref:System.Xml.Serialization.XmlSerializer> クラスでは、<xref:System.Runtime.Serialization.DataContractSerializer> クラスよりもサポートされる型の範囲がずっと狭くなりますが、結果の XML に対する制御の柔軟性に優れています。また、XML スキーマ定義言語 (XSD) 標準のサポート範囲が広く、 シリアル化可能な型で宣言型属性が要求されません。 詳細については、.NET Framework のドキュメントの XML シリアル化に関するトピックを参照してください。 <xref:System.Xml.Serialization.XmlSerializer> クラスは、データ コントラクト型をサポートしません。

Svcutil.exe または Visual Studio の**サービス参照の追加**機能を使用して、サードパーティのサービスのクライアントコードを生成したり、サードパーティのスキーマにアクセスしたりする場合は、適切なシリアライザーが自動的に選択されます。 スキーマに <xref:System.Runtime.Serialization.DataContractSerializer> との互換性がない場合は、<xref:System.Xml.Serialization.XmlSerializer> が選択されます。

## <a name="manually-switching-to-the-xmlserializer"></a>XmlSerializer への手動切り替え

<xref:System.Xml.Serialization.XmlSerializer> に手動で切り替える必要が生じる場合もあります。 たとえば、次のような場合です。

- アプリケーションを ASP.NET Web サービスから WCF に移行する場合は、新しいデータコントラクト型を作成するのではなく、既存の互換性のある型を再利用することが必要になる場合があり <xref:System.Xml.Serialization.XmlSerializer> ます。

- メッセージに表示する XML に対する正確な制御が必要で、Web サービス記述言語 (WSDL) ドキュメントが利用できない場合。たとえば、DataContractSerializer と互換性がなく、標準化および公開されている特定のスキーマに従う必要のある型を使用して、サービスを作成する場合。

- 従来の SOAP エンコード標準に従うサービスを作成する場合。

上記を含めた多様な状況で、次のコードに示すように、<xref:System.Xml.Serialization.XmlSerializer> 属性をサービスに適用することにより、`XmlSerializerFormatAttribute` クラスに手動で切り替えることができます。

[!code-csharp[c_XmlSerializer#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_xmlserializer/cs/source.cs#1)]
[!code-vb[c_XmlSerializer#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_xmlserializer/vb/source.vb#1)]

## <a name="security-considerations"></a>セキュリティの考慮事項

> [!NOTE]
> シリアル化エンジンを切り替える場合は注意が必要です。 同じ型でも、使用するシリアライザーによって XML へのシリアル化方法が異なる場合があります。 誤って、不適切なシリアライザーを使用すると、公開する意図のない型の情報が公開されるおそれがあります。

たとえば、<xref:System.Runtime.Serialization.DataContractSerializer> クラスは、データ コントラクト型をシリアル化する場合、<xref:System.Runtime.Serialization.DataMemberAttribute> 属性でマークされたメンバーのみをシリアル化します。 <xref:System.Xml.Serialization.XmlSerializer> クラスは、すべてのパブリック メンバーをシリアル化します。 たとえば、次のコードの型を見てください。

[!code-csharp[c_XmlSerializer#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_xmlserializer/cs/source.cs#2)]
[!code-vb[c_XmlSerializer#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_xmlserializer/vb/source.vb#2)]

<xref:System.Xml.Serialization.XmlSerializer> クラスが選択されているサービス コントラクトでこの型が誤って使用された場合、意図したものではなくても `creditCardNumber` メンバーがシリアル化されます。

<xref:System.Runtime.Serialization.DataContractSerializer> クラスが既定の場合でも、<xref:System.ServiceModel.DataContractFormatAttribute> 属性をサービス コントラクト型に適用することで、このクラスをサービスに対して明示的に選択できます (ただし、この操作が必要になることはありません)。

サービスで使用するシリアライザーはコントラクトにとって不可欠な部分です。別のバインディングを選択しても他の構成設定に変更しても、このシリアライザーを変更することはできません。

<xref:System.Xml.Serialization.XmlSerializer> クラスについては、セキュリティに関する重要な考慮事項が他にもあります。 まず、クラスを使用するすべての WCF アプリケーション <xref:System.Xml.Serialization.XmlSerializer> が、開示から保護されたキーで署名されていることを強くお勧めします。 このことは、<xref:System.Xml.Serialization.XmlSerializer> に手動で切り替える場合と、自動切り替えが行われる場合 (Svcutil.exe やサービス参照の追加などのツールによる) の両方でお勧めします。 これは、 <xref:System.Xml.Serialization.XmlSerializer> シリアル化エンジンは、アプリケーションと同じキーで署名されている限り、*事前に生成されたシリアル化アセンブリ*の読み込みをサポートするためです。 署名されていないアプリケーションは、アプリケーション フォルダーやグローバル アセンブリ キャッシュに配置される事前生成済みのシリアル化アセンブリで予想される名前に、悪意のあるアセンブリが一致するという危険性に対して完全に無防備になります。 もちろん、攻撃者がこのようなアクションを行うには、この 2 つの場所のいずれかに対する書き込みアクセスをまず取得する必要があります。

<xref:System.Xml.Serialization.XmlSerializer> を使用するときに必ず存在するもう 1 つの脅威は、システムの一時フォルダーへの書き込みアクセスに関連するものです。 シリアル化エンジンは、 <xref:System.Xml.Serialization.XmlSerializer> このフォルダー内に一時的な*シリアル化アセンブリ*を作成して使用します。 一時フォルダーへの書き込みアクセスのあるプロセスであれば、悪意のあるコードによってこれらのシリアル化アセンブリが上書きされるおそれがあることに注意してください。

## <a name="rules-for-xmlserializer-support"></a>XmlSerializer サポートのルール

<xref:System.Xml.Serialization.XmlSerializer> 互換の属性は、コントラクト操作のパラメーターまたは戻り値に直接適用できません。 ただし、次のコードに示すように、型指定されたメッセージ (メッセージ コントラクトの本文) には適用できます。

[!code-csharp[c_XmlSerializer#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_xmlserializer/cs/source.cs#3)]
[!code-vb[c_XmlSerializer#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_xmlserializer/vb/source.vb#3)]

型指定されたメッセージのメンバーに適用する場合、型指定されたメッセージ属性で競合するプロパティは、この属性によりオーバーライドされます。 たとえば、次のコードの `ElementName` は、`Name` をオーバーライドします。

[!code-csharp[c_XmlSerializer#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_xmlserializer/cs/source.cs#4)]
[!code-vb[c_XmlSerializer#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_xmlserializer/vb/source.vb#4)]

<xref:System.ServiceModel.MessageHeaderArrayAttribute> の使用時は、<xref:System.Xml.Serialization.XmlSerializer> 属性はサポートされません。

> [!NOTE]
> この場合、は、 <xref:System.Xml.Serialization.XmlSerializer> WCF より前にリリースされた次の例外をスローします。 "スキーマの最上位で宣言された要素は > 1 を持つことができません `maxOccurs` 。 `XmlArray` ではなく、`XmlArrayItem` または `XmlElementAttribute` を使うか、Wrapped パラメーター スタイルを使って 'more' のラッパー要素を指定してください。" という例外がスローされます。
>
> この例外が出力された場合は、この状況が当てはまるかどうかを調査します。

WCF は、 <xref:System.Xml.Serialization.SoapIncludeAttribute> <xref:System.Xml.Serialization.XmlIncludeAttribute> メッセージコントラクトおよび操作コントラクトの属性と属性をサポートしていません。 <xref:System.Runtime.Serialization.KnownTypeAttribute> 代わりに属性を使用してください。

## <a name="types-that-implement-the-ixmlserializable-interface"></a>IXmlSerializable インターフェイスを実装する型

`IXmlSerializable` インターフェイスを実装する型は、`DataContractSerializer` で完全にサポートされます。 これらの型には、スキーマを制御するために必ず <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> 属性を適用する必要があります。

> [!WARNING]
> ポリモーフィック型をシリアル化する場合、<xref:System.Xml.Serialization.XmlSchemaProviderAttribute> を型に適用して、正しい型がシリアル化されるようにする必要があります。

`IXmlSerializable` を実装する型には、任意のコンテンツを表す型、1 つの要素を表す型、および従来の <xref:System.Data.DataSet> 型の 3 種類があります。

- コンテンツ型では、`XmlSchemaProviderAttribute` 属性によって指定されたスキーマ プロバイダー メソッドが使用されます。 このメソッドから `null` が返されることはなく、属性の <xref:System.Xml.Serialization.XmlSchemaProviderAttribute.IsAny%2A> プロパティは既定値 `false` のままになります。 これは、`IXmlSerializable` 型の最も一般的な使用方法です。

- 要素型は、`IXmlSerializable` 型が自身のルート要素名を制御する必要があるときに使用します。 型を要素型としてマークするには、<xref:System.Xml.Serialization.XmlSchemaProviderAttribute.IsAny%2A> 属性の <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> プロパティを `true` に設定するか、スキーマ プロバイダー メソッドから `null` を返します。 スキーマ プロバイダー メソッドの使用は、要素型ではオプションです。`null` でメソッド名の代わりに `XmlSchemaProviderAttribute` を指定できます。 ただし、`IsAny` が `true` で、スキーマ プロバイダー メソッドが指定されている場合、メソッドは `null` を返す必要があります。

- 従来の <xref:System.Data.DataSet> 型は、`IXmlSerializable` 属性でマークされていない `XmlSchemaProviderAttribute` 型です。 これらの型は、スキーマ生成に関して <xref:System.Xml.Serialization.IXmlSerializable.GetSchema%2A> メソッドに依存しています。 以前のバージョンの .NET Framework では、このパターンが `DataSet` 型に使用され、型指定されたデータセットからクラスが派生されます。ただし、現在、このパターンは使用されなくなっており、従来の型に対応することだけを目的としてサポートされています。 このパターンに依存せず、必ず `XmlSchemaProviderAttribute` を `IXmlSerializable` 型に適用してください。

### <a name="ixmlserializable-content-types"></a>IXmlSerializable コンテンツ型

`IXmlSerializable` を実装しており、以前に定義したコンテンツ型である型のデータ メンバーをシリアル化すると、シリアライザーはそのデータ メンバーのラッパー要素を書き込み、<xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> メソッドに制御を渡します。 <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> 実装により、ラッパー要素に属性が追加されるなど、任意の XML が書き込まれることがあります。 `WriteXml` の実行後、シリアライザーは要素を閉じます。

`IXmlSerializable` を実装しており、以前に定義したコンテンツ型である型のデータ メンバーを逆シリアル化すると、デシリアライザーはそのデータ メンバーのラッパー要素に XML リーダーを配置し、<xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> メソッドに制御を渡します。 このメソッドは、開始タグと終了タグを含む、要素全体を読み取る必要があります。 `ReadXml` コードでは、要素が空の場合も忘れずに処理してください。 また、`ReadXml` の実装では、特定の方法で名前が付けられたラッパー要素に依存しないようにしてください。 シリアライザーによって選択される名前は、異なる場合があります。

`IXmlSerializable` コンテンツ型は、たとえば <xref:System.Object> 型のデータ メンバーなどに、ポリモーフィックに割り当てることができます。 また、型インスタンスを null にすることもできます。 さらに、`IXmlSerializable` 型は、オブジェクト グラフの保存を有効にして <xref:System.Runtime.Serialization.NetDataContractSerializer> で使用することも可能です。 これらのすべての機能では、WCF シリアライザーが特定の属性をラッパー要素にアタッチする必要があります (XML スキーマインスタンス名前空間の "nil" と "type"、WCF 固有の名前空間の "Id"、"Ref"、"Type"、"Assembly")。

#### <a name="attributes-to-ignore-when-implementing-readxml"></a>ReadXml を実装するときに無視する属性

`ReadXml` コードに制御を渡す前に、デシリアライザーは、XML 要素を調べ、前述の特別な XML 属性を検出し、その属性に従って動作します。 たとえば、"nil" が `true` の場合は、null 値が逆シリアル化され、`ReadXml` は呼び出されません。 ポリモーフィズムが検出された場合は、要素のコンテンツが別の型と同様に逆シリアル化されます。 ポリモーフィックに割り当てられた型の `ReadXml` 実装が呼び出されます。 どの場合も、これらの特別な属性がデシリアライザーによって処理されるため、`ReadXml` 実装ではこれらの属性を無視する必要があります。

### <a name="schema-considerations-for-ixmlserializable-content-types"></a>IXmlSerializable コンテンツ型のスキーマに関する考慮事項

スキーマと `IXmlSerializable` コンテンツ型をエクスポートすると、スキーマ プロバイダー メソッドが呼び出されます。 このスキーマ プロバイダー メソッドには、<xref:System.Xml.Schema.XmlSchemaSet> が渡されます。 このメソッドは、有効なスキーマをスキーマ セットに追加できます。 スキーマ セットには、スキーマをエクスポートした時点で既に認識されていたスキーマが格納されます。 スキーマ プロバイダー メソッドは、スキーマ セットに項目を追加する必要があるときに、適切な名前空間を持つ <xref:System.Xml.Schema.XmlSchema> がそのセットに既に存在するかどうかを確認する必要があります。 存在する場合、スキーマ プロバイダー メソッドは新しい項目を既存の `XmlSchema` に追加する必要があります。 存在しない場合、新しい `XmlSchema` インスタンスを作成する必要があります。 これは、`IXmlSerializable` 型の配列を使用する場合に重要です。 たとえば、`IXmlSerializable` 型を名前空間 "B" の "A" 型としてエクスポートする場合、スキーマ プロバイダー メソッドが呼び出される前に、"B" が "ArrayOfA" 型を保持するためのスキーマがスキーマ セットに既に存在している可能性があります。

型を <xref:System.Xml.Schema.XmlSchemaSet> に追加する以外に、コンテンツ型のスキーマ プロバイダー メソッドは null 以外の値を返す必要があります。 このメソッドは、特定の <xref:System.Xml.XmlQualifiedName> 型で使用するスキーマ型の名前を指定する `IXmlSerializable` を返すことができます。 この修飾名は、その型のデータ コントラクト名および名前空間としても使用されます。 スキーマ プロバイダー メソッドは、スキーマ セットにまだ存在していない型であっても、復帰時に返すことができます。 ただし、関連するすべての型がエクスポートされる (<xref:System.Runtime.Serialization.XsdDataContractExporter.Export%2A> の関連するすべての型に対して <xref:System.Runtime.Serialization.XsdDataContractExporter> メソッドが呼び出され、<xref:System.Runtime.Serialization.XsdDataContractExporter.Schemas%2A> プロパティにアクセスする) までに、その型がスキーマ セットに存在している必要があります。 関連するすべての `Schemas` 呼び出しが実行される前に `Export` プロパティにアクセスすると、<xref:System.Xml.Schema.XmlSchemaException> が発生する可能性があります。 エクスポートプロセスの詳細については、「[クラスからのスキーマのエクスポート](exporting-schemas-from-classes.md)」を参照してください。

スキーマ プロバイダー メソッドは、使用する <xref:System.Xml.Schema.XmlSchemaType> を返すこともできます。 その型は、匿名の場合とそうでない場合があります。 匿名の場合、`IXmlSerializable` 型のスキーマは、`IXmlSerializable` 型がデータ メンバーとして使用されるたびに匿名型としてエクスポートされます。 `IXmlSerializable` 型には、データ コントラクト名と名前空間が引き続き保持されます  (これは、「[データコントラクト名](data-contract-names.md)」で説明されているように、 <xref:System.Runtime.Serialization.DataContractAttribute> 名前のカスタマイズには属性を使用できない点が異なります)。匿名でない場合は、内のいずれかの型である必要があり `XmlSchemaSet` ます。 これは、型の `XmlQualifiedName` を返す場合と同じです。

さらに、型のグローバル要素宣言がエクスポートされます。 型に <xref:System.Xml.Serialization.XmlRootAttribute> 属性が適用されていない場合、その要素にはデータ コントラクトと同じ名前と名前空間が使用され、その "nillable" プロパティは `true` に設定されます。 唯一の例外は、スキーマ名前空間 ( `http://www.w3.org/2001/XMLSchema` ) です。型のデータコントラクトがこの名前空間にある場合、スキーマ名前空間に新しい要素を追加することは禁止されているため、対応するグローバル要素は空の名前空間にあります。 型に `XmlRootAttribute` 属性が適用されている場合、グローバル要素宣言は、<xref:System.Xml.Serialization.XmlRootAttribute.ElementName%2A>、<xref:System.Xml.Serialization.XmlRootAttribute.Namespace%2A>、および <xref:System.Xml.Serialization.XmlRootAttribute.IsNullable%2A> の各プロパティを使用してエクスポートされます。 `XmlRootAttribute` が適用された場合の既定値は、データ コントラクト名、空白の名前空間、および `true` に設定された "nillable" です。

同じグローバル要素宣言の規則が、従来のデータセット型に適用されます。 `XmlRootAttribute` は、カスタム コードによって追加されたグローバル要素宣言をオーバーライドできません。これには、スキーマ プロバイダー メソッドを使用して `XmlSchemaSet` に追加された場合と、従来のデータセット型に対して `GetSchema` を使用して追加された場合があります。

### <a name="ixmlserializable-element-types"></a>IXmlSerializable 要素型

`IXmlSerializable` 要素型には、`IsAny` に設定された `true` プロパティか、`null` を返すスキーマ プロバイダー メソッドのいずれかが含まれています。

要素型のシリアル化と逆シリアル化は、コンテンツ型のシリアル化と逆シリアル化に非常に似ています。 ただし、重要な違いがいくつかあります。

- `WriteXml` の実装では、要素 (これには複数の子要素が含まれている可能性もありますが) を 1 つだけ出力することが想定されています。 この 1 つの要素の外側にある属性、複数の兄弟要素、またはこれらが混在したコンテンツを出力することはできません。 要素は空であってもかまいません。

- `ReadXml` の実装では、ラッパー要素の読み取りは想定されていません。 読み取ることが想定されているのは、`WriteXml` で生成される要素 1 つのみです。

- 要素型を一様にシリアル化する場合 (データ コントラクトのデータ メンバーとしてシリアル化する場合など) は、コンテンツ型の場合と同様に、`WriteXml` を呼び出す前にラッパー要素が出力されます。 ただし、`WriteXml` コンストラクターまたは `DataContractSerializer` コンストラクターによるシリアライザーの構築時にルート名と名前空間を明示的に指定しない限り、トップ レベルで要素型をシリアル化しても、通常は `NetDataContractSerializer` で書き出される要素を囲むラッパー要素が出力されることはありません。 詳細については、「[シリアル化と逆シリアル化](serialization-and-deserialization.md)」を参照してください。

- 構築時にルート名と名前空間を指定せずにトップ レベルで要素型をシリアル化した場合、<xref:System.Runtime.Serialization.XmlObjectSerializer.WriteStartObject%2A> と <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteEndObject%2A> では基本的に何も実行されず、<xref:System.Runtime.Serialization.XmlObjectSerializer.WriteObjectContent%2A> によって `WriteXml` が呼び出されます。 このモードでは、シリアル化されるオブジェクトは `null` にできず、ポリモーフィックに割り当てることができません。 また、オブジェクト グラフの保存を有効化できず、`NetDataContractSerializer` も使用できません。

- 構築時にルート名と名前空間を指定せずにトップ レベルで要素型を逆シリアル化したときに、要素の先頭を検出できた場合は、<xref:System.Runtime.Serialization.XmlObjectSerializer.IsStartObject%2A> が `true` を返します。 <xref:System.Runtime.Serialization.XmlObjectSerializer.ReadObject%2A> パラメーターが `verifyObjectName` に設定されている `true` は、実際にオブジェクトを読み取る前の動作が `IsStartObject` と同様です。 その後、`ReadObject` は制御を `ReadXml` メソッドに渡します。

要素型の場合も、エクスポートされるスキーマは、前のセクションで説明した `XmlElement` 型に対するスキーマと同じです。ただし、スキーマ プロバイダー メソッドは、コンテンツ型と同様、追加のスキーマを <xref:System.Xml.Schema.XmlSchemaSet> に追加できます。 要素型には `XmlRootAttribute` 属性を使用することはできないので、グローバル要素宣言は要素型に対して出力されません。

### <a name="differences-from-the-xmlserializer"></a>XmlSerializer との相違点

`IXmlSerializable` インターフェイス、`XmlSchemaProviderAttribute` 属性、および `XmlRootAttribute` 属性は、<xref:System.Xml.Serialization.XmlSerializer> でも認識されます。 ただし、データ コントラクト モデルでの処理方法に違いがあります。 重要な違いを以下にまとめます。

- スキーマ プロバイダー メソッドは、`XmlSerializer` で使用できるようにするためにパブリックにする必要がありますが、データ コントラクト モデルで使用するためにパブリックにする必要はありません。

- スキーマ プロバイダー メソッドは、データ コントラクト モデルで `IsAny` が `true` の場合に呼び出されますが、`XmlSerializer` では呼び出されません。

- コンテンツ型または従来のデータセット型に `XmlRootAttribute` 属性がない場合、`XmlSerializer` は、グローバル要素宣言を空白の名前空間にエクスポートします。 データ コントラクト モデルで通常使用される名前空間は、前に説明したとおりデータ コントラクトの名前空間です。

両方のシリアル化技術で使用する型を作成する場合には、これらの違いに注意してください。

### <a name="importing-ixmlserializable-schema"></a>IXmlSerializable スキーマのインポート

`IXmlSerializable` 型から生成されたスキーマをインポートする場合、次のような状況が考えられます。

- 生成されるスキーマは、「[データコントラクトスキーマの参照](data-contract-schema-reference.md)」で説明されている有効なデータコントラクトスキーマである場合があります。 この場合は、スキーマを通常どおりにインポートでき、通常のデータ コントラクト型が生成されます。

- 生成されたスキーマが、有効なデータ コントラクト スキーマではない場合があります。 たとえば、スキーマ プロバイダー メソッドによって、データ コントラクト モデルでサポートされていない XML 属性を含むスキーマが生成されることがあります。 この場合、スキーマを `IXmlSerializable` 型としてインポートできます。 このインポートモードは、既定では有効になっていませんが、たとえば、 `/importXmlTypes` [ServiceModel メタデータユーティリティツール (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)へのコマンドラインスイッチを使用して、簡単に有効にすることができます。 この詳細については、「[クラスを生成するためのスキーマのインポート](importing-schema-to-generate-classes.md)」を参照してください。 型インスタンスを処理するには、XML を直接操作する必要があります。 `XmlSerializer` の使用方法に関するトピックを参照し、より広い範囲のスキーマをサポートする別のシリアル化技術を使用することを検討することもできます。

- 新しい型を生成する代わりに、プロキシ内の既存の `IXmlSerializable` 型を再利用できます。 この場合、「型を作成するためのスキーマのインポート」で説明する参照型の機能を使用して、再利用する型を示すことができます。 これは、Svcutil.exe で `/reference` スイッチを使用して、再利用する型を含むアセンブリを指定することに相当します。

### <a name="xmlserializer-legacy-behavior"></a>XmlSerializer の従来の動作

.NET Framework 4.0 以前では、XmlSerializer が C# コードをファイルに書き込むことによって、一時的なシリアル化アセンブリが生成されます。 さらに、このファイルがアセンブリとしてコンパイルされます。  この動作では、シリアライザーの起動時間が長くなるなど、望ましくない結果が生じることがあります。 .NET Framework 4.5 では、この動作が変更され、コンパイラを使用せずに、アセンブリが生成されるようになりました。 開発者によっては、生成された C# コードを確認したい場合もあります。 次の構成によって、この従来の動作を使用するように指定できます。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.xml.serialization>
    <xmlSerializer tempFilesLocation='e:\temp\XmlSerializerBug' useLegacySerializerGeneration="true" />
  </system.xml.serialization>
  <system.diagnostics>
    <switches>
      <add name="XmlSerialization.Compilation" value="1" />
    </switches>
  </system.diagnostics>
</configuration>
```

非パブリックの新しいオーバーライドを使用して派生クラスをシリアル化できないなどの互換性の問題が発生した場合は、 `XmlSerializer` 次の `XMLSerializer` 構成を使用して従来の動作に戻すことができます。

```xml
<configuration>
  <appSettings>
    <add key="System:Xml:Serialization:UseLegacySerializerGeneration" value="true" />
  </appSettings>
</configuration>
```

上記の構成の代わりに、.NET Framework 4.5 以降のバージョンを実行しているコンピューターで次の構成を使用することもできます。

```xml
<configuration>
  <system.xml.serialization>
    <xmlSerializer useLegacySerializerGeneration="true"/>
  </system.xml.serialization>
</configuration>
```

> [!NOTE]
> `<xmlSerializer useLegacySerializerGeneration="true"/>`スイッチは .NET Framework 4.5 以降のバージョンを実行しているコンピューターでのみ機能します。 上記の `appSettings` 方法は、すべての .NET Framework バージョンで動作します。

## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.DataContractFormatAttribute>
- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Xml.Serialization.XmlSerializer>
- <xref:System.ServiceModel.MessageHeaderArrayAttribute>
- [サービス コントラクトでのデータ転送の指定](specifying-data-transfer-in-service-contracts.md)
- [データ コントラクトの使用](using-data-contracts.md)
- [方法: XmlSerializer を使用する WCF クライアント アプリケーションの起動時間を短縮する](startup-time-of-wcf-client-applications-using-the-xmlserializer.md)
