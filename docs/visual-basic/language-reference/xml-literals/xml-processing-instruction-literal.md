---
title: XML 処理命令リテラル
ms.date: 07/20/2015
f1_keywords:
- vb.XmlLiteralProcessingInstruction
helpviewer_keywords:
- XML literals [Visual Basic], processing instruction
- XML processing instruction literal [Visual Basic]
- processing instruction literal [Visual Basic]
ms.assetid: cef4f7f8-0011-4f64-8602-795077ad4f15
ms.openlocfilehash: 9bd1781e01bc4cbf1ce5da8c454ab2f5a679aead
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400177"
---
# <a name="xml-processing-instruction-literal-visual-basic"></a>XML 処理命令リテラル (Visual Basic)
<xref:System.Xml.Linq.XProcessingInstruction> オブジェクトを表すリテラル。  
  
## <a name="syntax"></a>構文  
  
```xml  
<?piName [ = piData ] ?>  
```  
  
## <a name="parts"></a>指定項目  
 `<?`  
 必須です。 XML 処理命令リテラルの先頭を表します。  
  
 `piName`  
 必須です。 処理命令の対象となるアプリケーションを示す名前。 "xml" または "XML" では開始できません。  
  
 `piData`  
 任意。 `piName` の対象となるアプリケーションが XML ドキュメントを処理する方法を示す文字列。  
  
 `?>`  
 必須です。 処理命令の末尾を表します。  
  
## <a name="return-value"></a>戻り値  
 <xref:System.Xml.Linq.XProcessingInstruction> オブジェクト。  
  
## <a name="remarks"></a>Remarks  
 XML 処理命令リテラルは、アプリケーションが XML ドキュメントを処理する方法を示します。 アプリケーションは XML ドキュメントを読み込むとき、XML 処理命令を確認して、そのドキュメントの処理方法を判断します。 アプリケーションによって解釈されるのは、`piName` と `piData` の意味です。  
  
 XML ドキュメント リテラルでは、XML 処理命令と似た構文が使用されます。 詳細については、「[XML ドキュメント リテラル](xml-document-literal.md)」を参照してください。  
  
> [!NOTE]
> `piName` 要素の先頭に "xml" または "XML" 文字列を使用することはできません。これらの識別子は、XML 1.0 仕様で予約されているためです。  
  
 XML 処理命令リテラルは、変数に代入するか、XML ドキュメント リテラルに含めることができます。  
  
> [!NOTE]
> XML リテラルは、行連結文字なしで複数行にまたがることができます。 これにより、XML ドキュメントからコンテンツをコピーして、Visual Basic プログラムに直接貼り付けることができます。  
  
 XML 処理命令リテラルは、Visual Basic コンパイラによって、<xref:System.Xml.Linq.XProcessingInstruction.%23ctor%2A> コンストラクターへの呼び出しに変換されます。  
  
## <a name="example"></a>例  
 次の例では、XML ドキュメントのスタイルシートを特定する処理命令を作成します。  
  
 [!code-vb[VbXMLSamples#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#28)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Xml.Linq.XProcessingInstruction>
- [XML ドキュメント リテラル](xml-document-literal.md)
- [XML リテラル](index.md)
- [Visual Basic での XML の作成](../../programming-guide/language-features/xml/creating-xml.md)
