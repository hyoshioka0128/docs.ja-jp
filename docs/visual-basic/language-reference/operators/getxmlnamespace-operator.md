---
title: GetXmlNamespace 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.GetXmlNamespace
- GetXmlNamespace
helpviewer_keywords:
- GetXmlNamespace operator [Visual Basic]
- GetXmlNamespace keyword [Visual Basic]
ms.assetid: d0d28cfd-0755-4896-ae0b-4981aa35517c
ms.openlocfilehash: 85422fb9e11d78e228577adc25cba746149c645a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371117"
---
# <a name="getxmlnamespace-operator-visual-basic"></a>GetXmlNamespace 演算子 (Visual Basic)
指定した XML 名前空間プレフィックスに対応する <xref:System.Xml.Linq.XNamespace> オブジェクトを取得します。  
  
## <a name="syntax"></a>構文  
  
```vb  
GetXmlNamespace(xmlNamespacePrefix)  
```  
  
## <a name="parts"></a>指定項目  
 `xmlNamespacePrefix`  
 任意。 XML 名前空間プレフィックスを識別する文字列です。 指定する場合、文字列は有効な XML 識別子である必要があります。 詳細については、「[宣言する XML 要素と属性の名前](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)」を参照してください。 プレフィックスが指定されていない場合は、既定の名前空間が返されます。 既定の名前空間が指定されていない場合は、空の名前空間が返されます。  
  
## <a name="return-value"></a>戻り値  
 XML 名前空間プレフィックスに対応する <xref:System.Xml.Linq.XNamespace> オブジェクト。  
  
## <a name="remarks"></a>Remarks  
 `GetXmlNamespace` 演算子は、XML 名前空間プレフィックス `xmlNamespacePrefix` に対応する <xref:System.Xml.Linq.XNamespace> オブジェクトを取得します。  
  
 XML 名前空間プレフィックスは、XML リテラルと XML 軸プロパティで直接使用できます。 ただし、コードで名前空間プレフィックスを使用する前に、`GetXmlNamespace` 演算子を使用して、それを <xref:System.Xml.Linq.XNamespace> オブジェクトに変換しておく必要があります。 <xref:System.Xml.Linq.XNamespace> オブジェクトに非修飾要素名を追加して、多くの [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] メソッドで必要となる完全修飾 <xref:System.Xml.Linq.XName> オブジェクトを取得できます。  
  
## <a name="example"></a>例  
 次の例では、名前空間プレフィックスとして `ns` をインポートしています。 その後、この名前空間のプレフィックスを使用して XML リテラルを作成し、修飾名が `ns:phone` である最初の子ノードにアクセスします。 次に、その子ノードを `ShowName` サブルーチンに渡します。これにより、`GetXmlNamespace` 演算子を使用して修飾名が作成されます。 次に、`ShowName` サブルーチンが修飾名を <xref:System.Xml.Linq.XNode.Ancestors%2A> メソッドに渡して、親の `ns:contact` ノードを取得します。  
  
 [!code-vb[VbXMLSamples#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/GetXmlNamespace.vb#38)]  
  
 `TestGetXmlNamespace.RunSample()` を呼び出すと、次のテキストを含むメッセージ ボックスが表示されます。  
  
 `Name: Patrick Hines`  
  
## <a name="see-also"></a>関連項目

- [Imports ステートメント (XML 名前空間)](../statements/imports-statement-xml-namespace.md)
- [Visual Basic での XML へのアクセス](../../programming-guide/language-features/xml/accessing-xml.md)
