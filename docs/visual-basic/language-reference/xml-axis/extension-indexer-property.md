---
title: 拡張インデクサー プロパティ
ms.date: 07/20/2015
f1_keywords:
- vb.XmlPropertyExtensionIndexer
helpviewer_keywords:
- Visual Basic code, accessing XML
- XML extension indexer [Visual Basic]
- extension indexer [Visual Basic]
- XML [Visual Basic], accessing
ms.assetid: a16a4b13-54be-432c-82b3-a87091464ada
ms.openlocfilehash: c91061d49e22e648b7bf75a812071b352793abcb
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401343"
---
# <a name="extension-indexer-property-visual-basic"></a>拡張インデクサー プロパティ (Visual Basic)
コレクション内の個々の要素にアクセスできます。  
  
## <a name="syntax"></a>構文  
  
```vb  
object(index)  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`object`|必須です。 クエリ可能なコレクション。 つまり、<xref:System.Collections.Generic.IEnumerable%601> または <xref:System.Linq.IQueryable%601> を実装するコレクション。|  
|(|必須です。 インデクサー プロパティの先頭を表します。|  
|`index`|必須です。 コレクションの要素の 0 から始まる位置を指定する整数式。|  
|)|必須です。 インデクサー プロパティの末尾を表します。|  
  
## <a name="return-value"></a>戻り値  
 コレクション内の指定した位置からのオブジェクト、または `Nothing` (インデックスが範囲外の場合)。  
  
## <a name="remarks"></a>Remarks  
 拡張インデクサー プロパティを使用して、コレクションの個別の要素にアクセスできます。 このインデクサー プロパティは、通常、XML 軸プロパティの出力で使用されます。 XML 子軸プロパティおよび XML 子孫軸プロパティは、<xref:System.Xml.Linq.XElement> オブジェクトのコレクションまたは属性値を返します。  
  
 拡張インデクサーのプロパティは、Visual Basic コンパイラによって、`ElementAtOrDefault` メソッドへの呼び出しに変換されます。 配列インデクサーとは異なり、`ElementAtOrDefault` メソッドは、インデックスが範囲外の場合に `Nothing` を返します。 この動作は、コレクション内の要素の数を簡単には判断できない場合に便利です。  
  
 このインデクサー プロパティは、<xref:System.Collections.Generic.IEnumerable%601> または <xref:System.Linq.IQueryable%601> を実装するコレクションの拡張プロパティと似ています。つまり、コレクションにインデクサーまたは既定のプロパティがない場合にのみ使用されます。  
  
 <xref:System.Xml.Linq.XElement> または <xref:System.Xml.Linq.XAttribute> オブジェクト コレクションの最初の要素の値には、XML `Value` プロパティを使用してアクセスできます。 詳細については、「[XML Value プロパティ](xml-value-property.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例は、拡張インデクサーを使用して、<xref:System.Xml.Linq.XElement> オブジェクト コレクションの 2 番目の子ノードにアクセスする方法を示しています。 コレクションには子軸プロパティを使用してアクセスします。これにより、`contact` オブジェクトの `phone` という名前の子要素すべてが取得されます。  
  
 [!code-vb[VbXMLSamples#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples11.vb#24)]  
  
 このコードを実行すると、次のテキストが表示されます。  
  
 `Second phone number: 425-555-0145`  
  
## <a name="see-also"></a>関連項目

- <xref:System.Xml.Linq.XElement>
- [XML 軸プロパティ](index.md)
- [XML リテラル](../xml-literals/index.md)
- [Visual Basic での XML の作成](../../programming-guide/language-features/xml/creating-xml.md)
- [XML Value プロパティ](xml-value-property.md)
