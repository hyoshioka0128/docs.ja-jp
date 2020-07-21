---
title: LINQ to Objects (C#)
ms.date: 07/20/2015
ms.assetid: c5c2c178-3529-4f6c-b3df-2d5267af7f22
ms.openlocfilehash: f4ca6e57ffff026cb73121ecaf443ae54b25262c
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84990029"
---
# <a name="linq-to-objects-c"></a>LINQ to Objects (C#)

"LINQ to Objects" という用語は、[LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md) や [LINQ to XML](./linq-to-xml-overview.md) などの中間 LINQ プロバイダーまたは API を使用せずに、LINQ クエリを任意の <xref:System.Collections.IEnumerable> コレクションまたは <xref:System.Collections.Generic.IEnumerable%601> コレクションと直接組み合わせて使用することを意味します。 LINQ を使用して、<xref:System.Collections.Generic.List%601>、<xref:System.Array>、<xref:System.Collections.Generic.Dictionary%602> などの任意の列挙可能なコレクションを照会できます。 このコレクションは、ユーザー定義のコレクションでも、.NET API から返されたコレクションでもかまいません。  
  
 本質的に、LINQ to Objects は、コレクションを扱うための新しい方法です。 従来の方法では、複雑な `foreach` ループを記述して、コレクションからデータを取得する方法を指定する必要がありました。 LINQ を使用する場合は、何を取得するかを表す宣言コードを記述します。  
  
 また、LINQ クエリには、従来の `foreach` ループと比べて、次の 3 つの重要な利点があります。  
  
- 簡潔で読みやすい (特に複数の条件をフィルター処理する場合)。  
  
- 強力なフィルター処理、並べ替え、およびグループ化機能を最小限のアプリケーション コードで実現できる。  
  
- ほとんど、またはまったく変更せずに、他のデータ ソースに移植できる。  
  
 通常、データに対して実行する操作が複雑なほど、従来の反復処理手法の代わりに LINQ を使用する利便性が高くなります。  
  
 このセクションでは、いくつか例を挙げながら、LINQ を使った方法を具体的に説明します。 すべてを網羅したものではありません。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [LINQ と文字列 (C#)](./linq-and-strings.md)  
 LINQ を使用して、文字列および文字列のコレクションの照会と変換を行う方法について説明します。 これらの基本原則を具体的に示す記事へのリンクも含まれます。  
  
 [LINQ とリフレクション (C#)](how-to-query-an-assembly-s-metadata-with-reflection-linq.md)  
 LINQ でリフレクションを使用する方法を示すサンプルへのリンクを示します。  
  
 [LINQ とファイル ディレクトリ (C#)](./linq-and-file-directories.md)  
 LINQ を使用して、ファイル システムとやり取りする方法について説明します。 これらの概念を具体的に示す記事へのリンクも含まれます。  
  
 [LINQ を使用して ArrayList にクエリを実行する方法 (C#)](./how-to-query-an-arraylist-with-linq.md)  
 C# で ArrayList を照会する方法を示します。  
  
 [LINQ クエリのカスタム メソッドを追加する方法 (C#)](./how-to-add-custom-methods-for-linq-queries.md)  
 <xref:System.Collections.Generic.IEnumerable%601> インターフェイスに拡張メソッドを追加して、LINQ クエリに使用できるメソッド セットを拡張する方法について説明します。  
  
 [統合言語クエリ (LINQ) (C#)](./index.md)  
 LINQ について説明している記事へのリンクと、クエリを実行するコードの例を示します。
