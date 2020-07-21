---
title: XML ツリーの変更 (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 4ae511a5-4fc9-4178-9c8e-761357deae3f
ms.openlocfilehash: 3402188c4e34ef81bad41ed49f9236b4fb7c47ef
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406886"
---
# <a name="modifying-xml-trees-linq-to-xml-visual-basic"></a>XML ツリーの変更 (LINQ to XML) (Visual Basic)
[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] は、XML ツリーのメモリ内ストアです。 ソースから XML ツリーを読み込んだり解析したりした後に、[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] を使用してツリーを直接変更することができます。その後、ツリーをシリアル化して、ファイルに保存したり、リモート サーバーに送信したりできます。  
  
 ツリーを直接変更する際には、<xref:System.Xml.Linq.XContainer.Add%2A> などの特定のメソッドを使用します。  
  
 ただし、これには別の方法もあります。それは、関数型構築を使用して、別の新しいツリーを生成する方法です。 XML ツリーに対する変更の種類やツリーのサイズによっては、この方法の方が堅牢で、開発も容易になります。 このセクションの最初のトピックでは、この 2 つの方法を比較します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[メモリ内の XML ツリーの変更と関数型構築 (LINQ to XML) (Visual Basic)](in-memory-xml-tree-modification-vs-functional-construction.md)|XML ツリーのメモリ内での変更と関数型構築とを比較します。|  
|[XML ツリーへの要素、属性、およびノードの追加 (Visual Basic)](adding-elements-attributes-and-nodes-to-an-xml-tree.md)|XML ツリーへの要素、属性、またはノードの追加に関する情報について説明します。|  
|[XML ツリー内の要素、属性、およびノードの変更](modifying-elements-attributes-and-nodes-in-an-xml-tree.md)|既存の要素、属性、またはノードの変更に関する情報について説明します。|  
|[XML ツリーからの要素、属性、およびノードの削除 (Visual Basic)](removing-elements-attributes-and-nodes-from-an-xml-tree.md)|XML ツリーからの要素、属性、またはノードの削除に関する情報について説明します。|  
|[名前と値のペアの保持 (Visual Basic)](maintaining-name-value-pairs.md)|アプリケーションの情報を名前/値のペアとして保持する方法について説明します。このような情報には、構成情報やグローバル設定があります。|  
|[方法: XML ツリー全体の名前空間を変更する (Visual Basic)](how-to-change-the-namespace-for-an-entire-xml-tree.md)|XML ツリーを名前空間の間で移動する方法について説明します。|  
  
## <a name="see-also"></a>関連項目

- [プログラミング ガイド (LINQ to XML) (Visual Basic)](programming-guide-linq-to-xml.md)
