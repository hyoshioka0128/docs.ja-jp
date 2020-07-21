---
title: LINQ の概要
ms.date: 07/20/2015
ms.assetid: c6339c12-9b2d-433e-961c-0d2b7f0091c2
ms.openlocfilehash: b0fa27fd81b85eb89712f9e81f42e06505878f86
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397559"
---
# <a name="introduction-to-linq-visual-basic"></a>LINQ の概要 (Visual Basic)
統合言語クエリ (LINQ) は、.NET Framework Version 3.5 で導入された、オブジェクトとデータの溝を埋める画期的な手法です。  
  
 これまでは、データに対するクエリは、コンパイル時の型チェックや IntelliSense のサポートがない単純な文字列として表現されてきました。 さらに、SQL データベース、XML ドキュメント、さまざまな Web サービスなど、各種データ ソースの異なるクエリ言語を学習する必要があります。 LINQ により、"*クエリ*" は Visual Basic の高度な言語構成要素になります。 厳密に型指定されているオブジェクトのコレクションに対して、言語キーワードと使い慣れた演算子を用いてクエリを記述します。  
  
 Visual Basic を使って LINQ クエリを記述できます。対象は、<xref:System.Collections.IEnumerable> またはジェネリック <xref:System.Collections.Generic.IEnumerable%601> インターフェイスをサポートする SQL Server データベース、XML ドキュメント、ADO.NET データセット、その他のオブジェクトのコレクションです。 サード パーティからも、多くの Web サービスとその他のデータベース実装に対する LINQ のサポートが提供されます。  
  
 新しいプロジェクトで LINQ クエリを使用できるほか、既存のプロジェクトで LINQ 以外のクエリを使用することもできます。 唯一の要件は、プロジェクトが .NET Framework 3.5 以降をターゲットとしていることです。  
  
 次の Visual Studio の図は、SQL Server データベースに対して部分的に完了した LINQ クエリを示しています。このクエリは C# および Visual Basic の両方で記述されており、完全な型チェックと IntelliSense に対応しています。  
  
 ![Intellisense を使用する LINQ クエリを示す図。](./media/introduction-to-linq/linq-query-intellisense.png)  
  
## <a name="next-steps"></a>次の手順  
 LINQ の詳細については、最初に「[Visual Basic の LINQ の概要](getting-started-with-linq.md)」の概要に関するセクションで基本的な概念を理解し、次に関心のある LINQ テクノロジのドキュメントを参照してください。  
  
- SQL Server データベース:[LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)  
  
- XML ドキュメント:[LINQ to XML (Visual Basic)](linq-to-xml.md)  
  
- ADO.NET データセット:[LINQ to DataSet](../../../../framework/data/adonet/linq-to-dataset.md)  
  
- .NET のコレクション、ファイル、文字列など:[LINQ to Objects (Visual Basic)](linq-to-objects.md)  
  
## <a name="see-also"></a>関連項目

- [統合言語クエリ (LINQ) (Visual Basic)](index.md)
