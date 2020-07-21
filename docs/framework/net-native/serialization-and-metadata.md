---
title: シリアル化とメタデータ
ms.date: 03/30/2017
ms.assetid: 619ecf1c-1ca5-4d66-8934-62fe7aad78c6
ms.openlocfilehash: cc9adf0e6627ef3190e74fea5d4f0f3afd581811
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "81389228"
---
# <a name="serialization-and-metadata"></a>シリアル化とメタデータ

アプリでオブジェクトをシリアル化および逆シリアル化する場合、ランタイム ディレクティブ (.rd.xml) ファイルにエントリを追加して、必要なメタデータが実行時に確実に存在するようにする必要があることがあります。 シリアライザーには次の 2 つのカテゴリがあり、それぞれランタイム ディレクティブ ファイルで異なる処理が必要です。  
  
- リフレクション ベースのサードパーティ シリアライザー。 この場合、ランタイム ディレクティブ ファイルの変更が必要です。詳細については次のセクションで説明します。  
  
- .NET Framework クラスライブラリで、非リフレクションベースのシリアライザーが見つかりました。 この場合、ランタイム ディレクティブ ファイルの変更が必要なことがあります。詳細については、「[Microsoft のシリアライザー](#Microsoft)」セクションで説明します。  
  
<a name="ThirdParty"></a>
## <a name="third-party-serializers"></a>サードパーティ シリアライザー

 Newtonsoft.JSON などのサードパーティ シリアライザーは通常リフレクション ベースです。 シリアル化データのバイナリ ラージ オブジェクト (BLOB) の場合、対象の型のフィールドを名前で検索することで、データ内のフィールドが具象型に割り当てられます。 少なくとも、これらのライブラリを使用すると、`List<Type>` コレクションでシリアル化または逆シリアル化しようとする <xref:System.Type> オブジェクトごとに [MissingMetadataException](missingmetadataexception-class-net-native.md) 例外が発生します。  
  
 これらのシリアライザーでメタデータの欠落により引き起こされる問題に対処する最も簡単な方法は、1 つの名前空間 (`App.Models` など) でシリアル化に使用される型を収集し、`Serialize` メタデータ ディレクティブを適用することです。  
  
```xml  
<Namespace Name="App.Models" Serialize="Required PublicAndInternal" />  
```  
  
 この例で使用されている構文の詳細については、「 [ \<Namespace> Element](namespace-element-net-native.md)」を参照してください。  
  
<a name="Microsoft"></a>
## <a name="microsoft-serializers"></a>Microsoft のシリアライザー

 <xref:System.Runtime.Serialization.DataContractSerializer>、<xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>、および <xref:System.Xml.Serialization.XmlSerializer> クラスではリフレクションを利用しませんが、シリアル化または逆シリアル化されるオブジェクトに基づいてコードが生成される必要があります。 各シリアライザーのオーバーロードされたコンストラクターには、シリアル化または逆シリアル化される型を指定する <xref:System.Type> パラメーターが含まれます。 次の 2 つのセクションで説明するように、コードでのその型の指定方法によってユーザーが実行する必要のあるアクションが定義されます。  
  
### <a name="typeof-used-in-the-constructor"></a>コンストラクターで使用される typeof

 これらのシリアル化クラスのコンストラクターを呼び出し、メソッド呼び出しに C# [typeof](../../csharp/language-reference/operators/type-testing-and-cast.md#typeof-operator)演算子を含める場合は、**追加の作業を行う必要はありません**。 たとえば、シリアル化クラス コンストラクターに対する次の各呼び出しでは、`typeof` キーワードがコンストラクターに渡される式の一部として使用されます。  
  
 [!code-csharp[ProjectN#5](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#5)]  
  
 このコードは、.NET ネイティブコンパイラによって自動的に処理されます。  
  
### <a name="typeof-used-outside-the-constructor"></a>コンストラクターの外部で使用される typeof

 次のコードのように、これらのシリアル化クラスのコンストラクターを呼び出し、コンストラクターのパラメーターに指定された式の外部で C# [typeof](../../csharp/language-reference/operators/type-testing-and-cast.md#typeof-operator)演算子を使用した場合、 <xref:System.Type> .NET ネイティブコンパイラは型を解決できません。  
  
 [!code-csharp[ProjectN#6](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#6)]  
  
 この場合は、次のようなエントリを追加して、ランタイム ディレクティブ ファイルで型を指定する必要があります。  
  
```xml  
<Type Name="DataSet" Browse="Required Public" />  
```  
  
 同様に、のようなコンストラクターを呼び出し、次のコードのよう <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Type%5B%5D%29> に、シリアル化する追加のオブジェクトの配列を指定すると、 <xref:System.Type> .NET ネイティブコンパイラはこれらの型を解決できません。  
  
 [!code-csharp[ProjectN#7](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#7)]  
  
各型について、次のようなエントリをランタイムディレクティブファイルに追加します。  
  
```xml  
<Type Name="t" Browse="Required Public" />  
```  
  
この例で使用されている構文の詳細については、「 [ \<Type> Element](type-element-net-native.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [ランタイム ディレクティブ (rd.xml) 構成ファイル リファレンス](runtime-directives-rd-xml-configuration-file-reference.md)
- [ランタイム ディレクティブ要素](runtime-directive-elements.md)
- [\<Type>Element](type-element-net-native.md)
- [\<Namespace>Element](namespace-element-net-native.md)
