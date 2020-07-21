---
title: 既知のデータ コントラクト型
description: データコントラクトモデルが KnownTypeAttribute クラスを使用して、WCF で逆シリアル化中に含める型を指定する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data contracts [WCF], known types
- KnownTypeAttribute [WCF]
- KnownTypes [WCF]
ms.assetid: 1a0baea1-27b7-470d-9136-5bbad86c4337
ms.openlocfilehash: 52b0caaaac976893dcf5ef5c228ccc4f53bdbe9e
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247482"
---
# <a name="data-contract-known-types"></a>既知のデータ コントラクト型
<xref:System.Runtime.Serialization.KnownTypeAttribute> クラスを使用すると、逆シリアル化において考慮する必要のある型を事前に指定できます。 実施例については、「 [Known Types](../samples/known-types.md) 」の例を参照してください。  
  
 通常は、クライアントとサービス間でパラメーターを渡したり、値を返したりするときに、転送するデータのデータ コントラクトのすべてが両方のエンドポイントで共有されます。 ただし、次の場合はこれが該当しません。  
  
- 送信データ コントラクトが、予想データ コントラクトから派生する場合。 詳細については、「[データコントラクトの等価性](data-contract-equivalence.md)の継承について」を参照してください。 この場合、送信されるデータには、受信エンドポイントで予想しているデータ コントラクトが含まれません。  
  
- クラス、構造体、または列挙とは対照的に、送信される情報の宣言型がインターフェイスである場合。 したがって、インターフェイスを実装するどの型が実際に送信されるかを事前に知ることができないため、受信エンドポイントでは送信されるデータのデータ コントラクトを事前に確認することができません。  
  
- 送信される情報の宣言型が <xref:System.Object>である場合。 すべての型が <xref:System.Object>から継承され、どの型が実際に送信されるかを事前に知ることができないため、受信エンドポイントでは送信されるデータのデータ コントラクトを事前に確認することができません。 これは最初の項目についての特殊なケースです。すべてのデータ コントラクトは既定で、 <xref:System.Object>に対して生成された空のデータ コントラクトから派生します。  
  
- .NET Framework 型を含む一部の型には、前の3つのカテゴリのいずれかに属するメンバーがあります。 たとえば、 <xref:System.Collections.Hashtable> は <xref:System.Object> を使用して、ハッシュ テーブルに実際のオブジェクトを保存します。 これらの型をシリアル化する場合、受信側ではこれらのメンバーのデータ コントラクトを事前に確認することができません。  
  
## <a name="the-knowntypeattribute-class"></a>KnownTypeAttribute クラス  
 受信エンドポイントにデータが到着すると、WCF ランタイムは、共通言語ランタイム (CLR) 型のインスタンスにデータを逆シリアル化しようとします。 逆シリアル化するためにインスタンス化される型は、まず受信メッセージを調べてメッセージの内容が従うデータ コントラクトを特定することで選択されます。 次に逆シリアル化エンジンは、メッセージの内容と互換性のあるデータ コントラクトを実装する CLR 型を探します。 逆シリアル化エンジンによってこの処理中に逆シリアル化の候補の型として許可される一連の型は、逆シリアル化の "既知の型" のセットと呼ばれます。  
  
 逆シリアル化エンジンに型の情報を知らせる方法として、 <xref:System.Runtime.Serialization.KnownTypeAttribute>を使用する方法があります。 この属性は、データ コントラクト型全体に適用できるだけで、個々のデータ メンバーには適用できません。 この属性は、クラスまたは構造体にすることが可能な *外部型* に適用されます。 最も簡単な使用方法は、属性を適用するときに "既知の型" として型を指定することです。 これによって、外部型のオブジェクトまたはメンバーを通して参照される任意のオブジェクトが逆シリアル化されるときに、必ず、その既知の型が既知の型のセットに追加されます。 複数の <xref:System.Runtime.Serialization.KnownTypeAttribute> 属性を同じ型に適用することができます。  
  
## <a name="known-types-and-primitives"></a>既知の型とプリミティブ  
 プリミティブとして扱われる特定の型 ( <xref:System.DateTime> 、 <xref:System.Xml.XmlElement>など) と同様に、プリミティブ型は、常に "既知" であり、このメカニズムを通して追加する必要がありません。 ただし、プリミティブ型の配列は明示的に追加する必要があります。 ほとんどのコレクションは、配列と同等に扱われます。 (非ジェネリック コレクションは、 <xref:System.Object>の配列と同等に扱われます)。 プリミティブ、プリミティブ配列、およびプリミティブ コレクションの使用例については、例 4 を参照してください。  
  
> [!NOTE]
> 他のプリミティブ型とは異なり、 <xref:System.DateTimeOffset> 構造は、既定では既知の型ではないため、既知の型のリストに手動で追加する必要があります。  
  
## <a name="examples"></a>使用例  
 <xref:System.Runtime.Serialization.KnownTypeAttribute> クラスの使用例を次に示します。  
  
#### <a name="example-1"></a>例 1  
 継承関係にある 3 つのクラスがあります。  
  
 [!code-csharp[C_KnownTypeAttribute#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#1)]
 [!code-vb[C_KnownTypeAttribute#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#1)]  
  
 次の `CompanyLogo` クラスはシリアル化できますが、 `ShapeOfLogo` メンバーが `CircleType` オブジェクトと `TriangleType` オブジェクトのどちらかに設定されている場合は、逆シリアル化エンジンが "Circle" や "Triangle" という名前のデータ コントラクト型を認識しないため、逆シリアル化することはできません。  
  
 [!code-csharp[C_KnownTypeAttribute#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#2)]
 [!code-vb[C_KnownTypeAttribute#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#2)]  
  
 `CompanyLogo` 型の正しいコードの記述方法は次のとおりです。  
  
 [!code-csharp[C_KnownTypeAttribute#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#3)]
 [!code-vb[C_KnownTypeAttribute#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#3)]  
  
 外部型の `CompanyLogo2` が逆シリアル化されるときは、必ず、逆シリアル化エンジンが `CircleType` と `TriangleType` を認識するため、"Circle" データ コントラクトおよび "Triangle" データ コントラクトと一致する型を検出できます。  
  
#### <a name="example-2"></a>例 2  
 次の例では、 `CustomerTypeA` と `CustomerTypeB` の両方が `Customer` データ コントラクトを持っている場合でも、逆シリアル化エンジンは `CustomerTypeB` だけを認識するため、 `PurchaseOrder` が逆シリアル化されるときは必ず `CustomerTypeB` のインスタンスが作成されます。  
  
 [!code-csharp[C_KnownTypeAttribute#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#4)]
 [!code-vb[C_KnownTypeAttribute#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#4)]  
  
#### <a name="example-3"></a>例 3  
 次の例では、 <xref:System.Collections.Hashtable> が <xref:System.Object>として内部的にその内容を保存します。 ハッシュ テーブルを正常に逆シリアル化するには、逆シリアル化エンジンがそのテーブルに現れる可能性のある型のセットを認識している必要があります。 この場合は、 `Book` オブジェクトと `Magazine` オブジェクトだけが `Catalog`に保存されているため、この 2 つが <xref:System.Runtime.Serialization.KnownTypeAttribute> 属性を使用して追加されることが事前にわかっています。  
  
 [!code-csharp[C_KnownTypeAttribute#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#5)]
 [!code-vb[C_KnownTypeAttribute#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#5)]  
  
#### <a name="example-4"></a>例 4  
 次の例では、データ コントラクトには数値と、その数値に基づいて実行する演算が含まれています。 `Numbers` データ メンバーは、整数、整数の配列、または整数を含む <xref:System.Collections.Generic.List%601> にすることができます。  
  
> [!CAUTION]
> この例は、WCF プロキシを生成するために SVCUTIL.EXE が使用されている場合にのみ、クライアント側で機能します。 SVCUTIL.EXE は、サービスからメタデータ (任意の既知の型を含む) を取得します。 この情報がない場合、クライアントは型を逆シリアル化できません。  
  
 [!code-csharp[C_KnownTypeAttribute#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#6)]
 [!code-vb[C_KnownTypeAttribute#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#6)]  
  
 アプリケーション コードは次のとおりです。  
  
 [!code-csharp[C_KnownTypeAttribute#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#7)]
 [!code-vb[C_KnownTypeAttribute#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#7)]  
  
## <a name="known-types-inheritance-and-interfaces"></a>既知の型、継承、およびインターフェイス  
 `KnownTypeAttribute` 属性を使用して既知の型を特定の型に関連付けると、その既知の型がその特定の型から派生したすべての型に関連付けられます。 たとえば、次のコードを参照してください。  
  
 [!code-csharp[C_KnownTypeAttribute#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#8)]
 [!code-vb[C_KnownTypeAttribute#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#8)]  
  
 `DoubleDrawing` クラスは、 `KnownTypeAttribute` フィールドで `Square` と `Circle` を使用するために `AdditionalShape` 属性を必要としません。これは、既に基本クラス (`Drawing`) にこれらの属性が適用されているためです。  
  
 既知の型は、クラスと構造体にのみ関連付けることができます。インターフェイスに関連付けることはできません。  
  
## <a name="known-types-using-open-generic-methods"></a>オープン ジェネリック メソッドを使用する既知の型  
 既知の型としてジェネリック型の追加が必要な場合があります。 ただし、オープン ジェネリック型をパラメーターとして `KnownTypeAttribute` 属性に渡すことはできません。  
  
 この問題は、型の一覧を返すメソッドを作成して既知の型のコレクションに追加するという代替機構を使用することで解決できます。 次に、いくつかの制限事項があるため、このメソッドの名前を `KnownTypeAttribute` 属性への文字列引数として指定します。  
  
 このメソッドは、 `KnownTypeAttribute` 属性を適用する型上に存在し、静的で、パラメーターを必要とせず、 <xref:System.Collections.IEnumerable> の <xref:System.Type>に代入可能なオブジェクトを返す必要があります。  
  
 同じ型上で、メソッド名を持つ `KnownTypeAttribute` 属性と実際の型を持つ `KnownTypeAttribute` 属性を組み合わせることはできません。 また、メソッド名が同じ複数の `KnownTypeAttribute` を同じ型に適用することはできません。  
  
 次のクラスを参照してください。  
  
 [!code-csharp[C_KnownTypeAttribute#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#9)]
 [!code-vb[C_KnownTypeAttribute#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#9)]  
  
 `theDrawing` フィールドには、 `ColorDrawing` ジェネリック クラスおよび `BlackAndWhiteDrawing`ジェネリック クラスのインスタンスを格納でき、これらのクラスは両方とも `Drawing`ジェネリック クラスから継承されています。 通常、両クラスとも既知の型に追加する必要がありますが、次の属性の構文は無効です。  
  
```csharp  
// Invalid syntax for attributes:  
// [KnownType(typeof(ColorDrawing<T>))]  
// [KnownType(typeof(BlackAndWhiteDrawing<T>))]  
```  
  
```vb  
' Invalid syntax for attributes:  
' <KnownType(GetType(ColorDrawing(Of T))), _  
' KnownType(GetType(BlackAndWhiteDrawing(Of T)))>  
```  
  
 したがって、これらの型を返すメソッドを作成する必要があります。 この型の正しいコードの記述方法は次のとおりです。  
  
 [!code-csharp[C_KnownTypeAttribute#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#10)]
 [!code-vb[C_KnownTypeAttribute#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#10)]  
  
## <a name="additional-ways-to-add-known-types"></a>既知の型を追加するその他の方法  
 また、既知の型は、構成ファイルを使用して追加することもできます。 これは、Windows Communication Foundation (WCF) でサードパーティ製のタイプライブラリを使用する場合など、既知の型を適切に逆シリアル化する必要がある型を制御しない場合に便利です。  
  
 構成ファイルで既知の型を指定する方法を次に示します。  
  
 `<configuration>`  
  
 `<system.runtime.serialization>`  
  
 `<dataContractSerializer>`  
  
 `<declaredTypes>`  
  
 `<add type="MyCompany.Library.Shape,`  
  
 `MyAssembly, Version=2.0.0.0, Culture=neutral,`  
  
 `PublicKeyToken=XXXXXX, processorArchitecture=MSIL">`  
  
 `<knownType type="MyCompany.Library.Circle,`  
  
 `MyAssembly, Version=2.0.0.0, Culture=neutral,`  
  
 `PublicKeyToken=XXXXXX, processorArchitecture=MSIL"/>`  
  
 `</add>`  
  
 `</declaredTypes>`  
  
 `</dataContractSerializer>`  
  
 `</system.runtime.serialization>`  
  
 `</configuration>`  
  
 前の構成ファイルでは、 `MyCompany.Library.Shape` というコントラクト型が `MyCompany.Library.Circle` を既知の型として持つと宣言されています。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.KnownTypeAttribute>
- <xref:System.Collections.Hashtable>
- <xref:System.Object>
- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Runtime.Serialization.DataContractSerializer.KnownTypes%2A>
- [既知の型](../samples/known-types.md)
- [データ コントラクトの等価性](data-contract-equivalence.md)
- [サービス コントラクトの設計](../designing-service-contracts.md)
