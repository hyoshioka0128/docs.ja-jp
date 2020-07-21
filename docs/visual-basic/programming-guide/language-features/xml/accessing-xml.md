---
title: XML へのアクセス
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ to XML [Visual Basic], accessing XML
- Visual Basic code, XML
- accessing XML [Visual Basic], axis properties
- XML [Visual Basic], axis properties
- XML [Visual Basic], accessing
ms.assetid: c47f88b2-3cbc-4bb1-b4b9-be60f71ffc6a
ms.openlocfilehash: 282b7d91ec7cfe2f587c67bc9a982f0da22ad925
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410310"
---
# <a name="accessing-xml-in-visual-basic"></a>Visual Basic での XML へのアクセス
Visual Basic には、[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 構造体にアクセスして移動するための XML 軸プロパティが用意されています。 これらのプロパティでは、XML 名を指定して、要素と属性にアクセスできる特殊な構文を使用します。  
  
 次の表に、Visual Basic で XML 要素と属性にアクセスできる言語機能を一覧表示しています。  
  
### <a name="xml-axis-properties"></a>XML 軸プロパティ  
  
|プロパティの説明|例|説明|  
|--------------------------|-------------|-----------------|  
|*子軸*|`contact.<phone>`|`contact` 要素の子要素であるすべての `phone` 要素を取得します。|  
|*属性軸*|`phone.@type`|`phone` 要素のすべての `type` 属性を取得します。|  
|*子孫軸*|`contacts...<name>`|`contacts` 要素のすべての `name` 要素を、それらが存在する階層の深さに関係なく、取得します。|  
|*拡張インデクサー*|`contacts...<name>(0)`|シーケンスから最初の `name` 要素を取得します。|  
|*value*|`contacts...<name>.Value`|シーケンス内の最初のオブジェクトの文字列表現、またはシーケンスが空の場合は `Nothing` を取得します。|  
  
## <a name="in-this-section"></a>このセクションの内容  
 [方法: XML 子孫要素にアクセスする](how-to-access-xml-descendant-elements.md)  
 子孫軸プロパティを使用して、指定した名前を持ち、指定した XML 要素の下に含まれているすべての XML 要素にアクセスする方法を示します。  
  
 [方法: XML 子要素にアクセスする](how-to-access-xml-child-elements.md)  
 子軸プロパティを使用して、XML 要素内で指定した名前を持つすべての XML 子要素にアクセスする方法を示します。  
  
 [方法: XML 属性にアクセスする](how-to-access-xml-attributes.md)  
 属性軸プロパティを使用して、XML 要素内で指定した名前を持つすべての XML 属性にアクセスする方法を示します。  
  
 [方法: XML 名前空間プレフィックスを宣言して使用する](how-to-declare-and-use-xml-namespace-prefixes.md)  
 XML 名前空間プレフィックスを宣言し、それを使用して XML 要素を作成し、アクセスする方法を示します。  
  
## <a name="related-sections"></a>関連項目  
 [XML 軸プロパティ](../../../language-reference/xml-axis/index.md)  
 さまざまな XML アクセス プロパティについて説明するセクションへのリンクを示します。  
  
 [Visual Basic における LINQ to XML の概要](overview-of-linq-to-xml.md)  
 Visual Basic での [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の使用の概要について説明します。  
  
 [Visual Basic での XML の作成](creating-xml.md)  
 Visual Basic での XML リテラルの使用の概要について説明します。  
  
 [Visual Basic での XML の操作](manipulating-xml.md)  
 Visual Basic での XML の読み込みと変更に関するセクションへのリンクを示します。  
  
 [XML](index.md)  
 Visual Basic での [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] の使用方法を説明するセクションへのリンクを示します。
