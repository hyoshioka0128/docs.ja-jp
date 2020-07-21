---
title: LINQ to XML の概要
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ to XML [Visual Basic], about LINQ to XML
- LINQ [Visual Basic], LINQ to XML
ms.assetid: 01c62a79-6d58-468e-84fb-039c05947701
ms.openlocfilehash: 044aca634f5a0aa6e557a7dd9c0e1de64e35dc15
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84374656"
---
# <a name="overview-of-linq-to-xml-in-visual-basic"></a>Visual Basic における LINQ to XML の概要
Visual Basic は、XML リテラルおよび XML 軸プロパティを使用した [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] のサポートを提供しています。 これにより、使い慣れた便利な構文を使用して、Visual Basic コードで XML を操作できます。 *XML リテラル*を使用すると、コードに XML を直接含めることができます。 *XML 軸プロパティ*を使用すると、XML リテラルの子ノード、子孫ノード、および属性にアクセスできます。 詳細については、「[XML リテラルの概要](xml-literals-overview.md)」と「[Visual Basic での XML へのアクセス](accessing-xml.md)」を参照してください。  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] は、統合言語クエリ (LINQ) を利用するために設計された、メモリ内の XML プログラミング API です。 LINQ API は直接呼び出すことができますが、XML リテラルを宣言して XML 軸プロパティに直接アクセスできるのは、Visual Basic だけです。  
  
> [!NOTE]
> XML リテラルおよび XML 軸プロパティは、ASP.NET ページの宣言型コードではサポートされません。 Visual Basic の XML 機能を使用するには、ASP.NET アプリケーションの分離コード ページにコードを配置します。  
  
 [再生ボタン](./media/overview-of-linq-to-xml/play-video-icon-example.gif) 関連するビデオ デモについては、「[LINQ to XML を使ってみる](/aspnet/web-forms/videos/data-access/linq-videos-from-the-vb-team/how-do-i-get-started-with-linq-to-xml)」と「[LINQ to XML を使用して Excel スプレッドシートを作成する](/aspnet/web-forms/videos/data-access/linq-videos-from-the-vb-team/how-do-i-create-excel-spreadsheets-using-linq-to-xml)」を参照してください。
  
## <a name="creating-xml"></a>XML の作成  
 Visual Basic で XML ツリーを作成する方法は 2 つあります。 XML リテラルをコード内に直接宣言するか、LINQ API を使用してツリーを作成することができます。 どちらのプロセスでも、XML ツリーの最終的な構造をコードに反映させることができます。 たとえば、次のコード例では、XML 要素を作成しています。  
  
 [!code-vb[VbXmlSamples#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples2.vb#5)]  
  
 詳細については、「[Visual Basicでの XML の作成](creating-xml.md)」を参照してください。  
  
## <a name="accessing-and-navigating-xml"></a>XML へのアクセスおよび移動  
 Visual Basic には、XML 構造体にアクセスして移動するための XML 軸プロパティが用意されています。 これらのプロパティを使用すると、XML の子要素名を指定することによって、XML の要素と属性にアクセスできます。 または、LINQ メソッドを明示的に呼び出して、要素と属性の移動や検索を行うこともできます。 たとえば、次のコード例では、XML 要素の属性と子要素を参照するために XML 軸プロパティを使用しています。 このコード例では、LINQ クエリを使用して子要素を取得し、それらを XML 要素として出力し、変換を効果的に実行しています。  
  
 [!code-vb[VbXmlSamples#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples3.vb#8)]  
  
 詳細については、「[Visual Basicでの XML へのアクセス](accessing-xml.md)」を参照してください。  
  
## <a name="xml-namespaces"></a>XML 名前空間  
 Visual Basic を使用すると、`Imports` ステートメントを使用して、グローバルな XML 名前空間の別名を指定できます。 次の例は、`Imports` ステートメントを使用して XML 名前空間をインポートする方法を示しています。  
  
 [!code-vb[VbXMLSamples#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#1)]  
  
 XML 名前空間の別名は、XML 軸プロパティにアクセスする場合や、XML ドキュメントおよび XML 要素の XML リテラルを宣言する場合に使用できます。  
  
 [GetXmlNamespace 演算子](../../../language-reference/operators/getxmlnamespace-operator.md)を使用すると、特定の名前空間プレフィックスの <xref:System.Xml.Linq.XNamespace> オブジェクトを取得できます。  
  
 詳細については、「[Imports ステートメント (XML 名前空間)](../../../language-reference/statements/imports-statement-xml-namespace.md)」を参照してください。  
  
### <a name="using-xml-namespaces-in-xml-literals"></a>XML リテラルでの XML 名前空間の使用  
 次の例は、グローバルな名前空間 `ns` を使用する <xref:System.Xml.Linq.XElement> オブジェクトを作成する方法を示しています。  
  
 [!code-vb[VbXMLSamples#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#2)]  
  
 Visual Basic コンパイラは、XML 名前空間の別名を含む XML リテラルを同等のコードに変換します。このコードは、`xmlns` 属性に XML 名前空間を使用するために XML 表記を使用します。 前のセクションの例のコードをコンパイルすると、次の例と基本的に同じ実行可能コードが生成されます。  
  
 [!code-vb[VbXMLSamples#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#3)]  
  
### <a name="using-xml-namespaces-in-xml-axis-properties"></a>XML 軸プロパティでの XML 名前空間の使用  
 XML リテラルで宣言された XML 名前空間を XML 軸プロパティで使用することはできません。 ただし、XML 軸プロパティではグローバルな名前空間を使用できます。 XML 名前空間プレフィックスとローカルな要素名を区切るには、コロンを使用します。 例を次に示します。  
  
 [!code-vb[VbXMLSamples#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#4)]  
  
## <a name="see-also"></a>関連項目

- [XML](index.md)
- [Visual Basic での XML の作成](creating-xml.md)
- [Visual Basic での XML へのアクセス](accessing-xml.md)
- [Visual Basic での XML の操作](manipulating-xml.md)
