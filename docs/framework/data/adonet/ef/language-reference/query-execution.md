---
title: クエリの実行
description: 遅延クエリ実行、即時クエリ実行、ストア実行など、LINQ to Entities クエリを実行するさまざまな方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c0e6cf23-63ac-47dd-bfe9-d5bdca826fac
ms.openlocfilehash: e776df6d35b6cc8c24cd83e902bc4d050347343b
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286793"
---
# <a name="query-execution"></a>クエリの実行
ユーザーによって作成された LINQ クエリは、コマンド ツリーに変換されます。 コマンド ツリーは、Entity Framework と互換性のあるクエリの表現です。 コマンド ツリーは、その後データ ソースに対して実行されます。 クエリの実行時には、すべてのクエリ式 (つまりクエリの全コンポーネント) が評価されます。これには結果の具体化で使用される式も含まれます。  
  
 クエリ式が評価されるタイミングはさまざまです。 LINQ クエリは、クエリ変数の作成時ではなく、常にクエリ変数の反復処理時に実行されます。 これを "*遅延実行*" といいます。 クエリを即時に実行することもできます。これは、クエリの結果をキャッシュする場合に有効です。 このことについては、このトピックの後半で説明します。  
  
 LINQ to Entities クエリを実行すると、クエリ内の一部の式がサーバー上で実行され、別の一部の式がクライアント上でローカルに実行される場合があります。 クライアント側での式の評価は、サーバー上でクエリが実行される前に行われます。 式がクライアント上で評価される場合、クエリ内の式がその評価の結果に置き換えられた後、サーバー上でクエリが実行されます。 クエリはデータ ソースに対して実行されるため、クライアントで指定された動作よりもデータ ソースの構成がオーバーライドされます。 たとえば、Null 値の処理方法や、数値の有効桁数などはサーバーの設定によって異なります。 クエリの実行中にサーバーに対してスローされた例外は、クライアントに直接渡されます。  

> [!TIP]
> 演算子の実行動作が簡単にわかる表形式のクエリ演算子の便利なまとめについては、「[実行方法による標準クエリ演算子の分類 (C#)](../../../../../csharp/programming-guide/concepts/linq/classification-of-standard-query-operators-by-manner-of-execution.md)」をご覧ください。

## <a name="deferred-query-execution"></a>クエリの遅延実行  
 一連の値を返すクエリでは、クエリ変数そのものはクエリ結果を保持しません。クエリ変数には、クエリのコマンドが格納されるだけです。 クエリ変数が `foreach` ループまたは `For Each` ループで反復処理されるまで、クエリは実行されません。 これは "*遅延実行*" と呼ばれます。つまり、作成されたクエリはすぐには実行されません。 これは、任意のタイミングでクエリを実行できるということを意味します。 これは、たとえば他のアプリケーションによって更新されるデータベースがある場合に便利です。 アプリケーションで、最新情報を取得するクエリを作成し、それを繰り返し実行することにより、更新のたびに最新の情報を取得できます。  
  
 遅延実行により、複数のクエリを組み合わせたり、クエリを拡張したりすることが可能となります。 クエリを拡張して新しい操作を追加すると、その変更が最終的な実行時に反映されます。 次の例の最初のクエリでは、すべての製品が返されます。 2 つ目のクエリでは、サイズが "L" のすべての製品を返すように、`Where` を使って 1 つ目のクエリを拡張しています。  
  
 [!code-csharp[DP L2E Conceptual Examples#Composing1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#composing1)]
 [!code-vb[DP L2E Conceptual Examples#Composing1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#composing1)]  
  
 クエリが実行された後、後続のすべてのクエリでメモリ内の LINQ 演算子が使用されます。 `foreach` ステートメントや `For Each` ステートメントを使用することによって、または LINQ 変換演算子の 1 つを呼び出すことによって、クエリ変数を反復処理すると、即時実行が発生します。 これらの変換演算子には、<xref:System.Linq.Enumerable.ToList%2A>、<xref:System.Linq.Enumerable.ToArray%2A>、<xref:System.Linq.Enumerable.ToLookup%2A>、<xref:System.Linq.Enumerable.ToDictionary%2A> などがあります。  
  
## <a name="immediate-query-execution"></a>クエリの即時実行  
 一連の値を生成するクエリの遅延実行とは対照的に、シングルトン値を返すクエリは直ちに実行されます。 シングルトン クエリの例としては、<xref:System.Linq.Enumerable.Average%2A>、<xref:System.Linq.Enumerable.Count%2A>、<xref:System.Linq.Enumerable.First%2A>、<xref:System.Linq.Enumerable.Max%2A> があります。 これらのシングルトン クエリは、結果を計算するためにはシーケンスを生成する必要があるため、直ちに実行されます。 即時実行は強制することもできます。 これはクエリの結果をキャッシュする場合などに便利です。 クエリまたはクエリ変数で <xref:System.Linq.Enumerable.ToList%2A> メソッド、<xref:System.Linq.Enumerable.ToDictionary%2A> メソッド、または <xref:System.Linq.Enumerable.ToArray%2A> メソッドを呼び出すと、シングルトン値を生成しないクエリの即時実行を強制できます。 次の例では、<xref:System.Linq.Enumerable.ToArray%2A> メソッドを使用して、シーケンスを配列として即時評価します。  
  
 [!code-csharp[DP L2E Examples#ToArray](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#toarray)]
 [!code-vb[DP L2E Examples#ToArray](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#toarray)]  
  
 また、`foreach` ループまたは `For Each` ループをクエリ式の直後に配置して実行を強制することも、<xref:System.Linq.Enumerable.ToList%2A> または <xref:System.Linq.Enumerable.ToArray%2A> を呼び出すことにより、単一のコレクション オブジェクト内のすべてのデータをキャッシュすることにより、実行を強制することもできます。  
  
## <a name="store-execution"></a>ストア実行  
 一般的に、LINQ to Entities の式はサーバー上で評価されるため、式の動作がデータ ソースのセマンティクスではなく、共通言語ランタイム (CLR) セマンティクスに従っているとは限りません。 ただし、これには式がクライアント上で実行された場合などの例外があります。 これは、サーバーとクライアントが異なるタイム ゾーンに存在する場合など、予期しない結果をもたらすことがあります。  
  
 クエリ内の一部の式はクライアント上で実行される場合があります。 通常、ほとんどのクエリ実行はサーバーで発生するものと見なされます。 データ ソースにマップされたクエリ要素に対して実行されたメソッドの他に、クエリにはローカルで実行できる式が含まれる場合がよくあります。 クエリ式のローカルでの実行では、クエリ実行または結果の作成で使用できる値が生成されます。  
  
 値のバインド、サブ式、終了からのサブクエリ、およびクエリ結果へのオブジェクトの具体化などの特定の操作は、常にクライアントで実行されます。 その最終的な結果として、これらの要素 (パラメーター値など) は実行中には更新できなくなります。 匿名型は、データ ソースでインラインで作成できますが、必ずしもそれを想定することはできません。 インラインのグループはデータ ソースでも作成できますが、すべてのインスタンスでそれが可能であると見なすことはできません。 通常、サーバー上で何を作成できるかについて想定しないことが賢明です。  
  
 このセクションでは、コードをクライアント上でローカルに実行するシナリオについて説明します。 ローカルで実行される式の種類について詳しくは、「[LINQ to Entities クエリ内の式](expressions-in-linq-to-entities-queries.md)」をご覧ください。  
  
### <a name="literals-and-parameters"></a>リテラルとパラメーター  
 次の例に示した `orderID` 変数などのローカル変数は、クライアントで評価されます。  
  
 [!code-csharp[DP L2E Conceptual Examples#LiteralParameter1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#literalparameter1)]
 [!code-vb[DP L2E Conceptual Examples#LiteralParameter1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#literalparameter1)]  
  
 メソッド パラメーターもクライアントで評価されます。 下の `orderID` メソッドに渡される `MethodParameterExample` パラメーターがその例です。  
  
 [!code-csharp[DP L2E Conceptual Examples#MethodParameterExample](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#methodparameterexample)]
 [!code-vb[DP L2E Conceptual Examples#MethodParameterExample](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#methodparameterexample)]  
  
### <a name="casting-literals-on-the-client"></a>クライアントでのリテラルのキャスト  
 `null` から CLR 型へのキャストは、次のようにクライアントで実行されます。  
  
 [!code-csharp[DP L2E Conceptual Examples#NullCastToString](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#nullcasttostring)]
 [!code-vb[DP L2E Conceptual Examples#NullCastToString](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#nullcasttostring)]  
  
 Null 値が許容される <xref:System.Decimal> などの型へのキャストは、次のようにクライアントで実行されます。  
  
 [!code-csharp[DP L2E Conceptual Examples#CastToNullable](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#casttonullable)]
 [!code-vb[DP L2E Conceptual Examples#CastToNullable](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#casttonullable)]  
  
### <a name="constructors-for-literals"></a>リテラルのコンストラクター  
 概念モデル型にマップできる新しい CLR 型は、次のようにクライアントで実行されます。  
  
 [!code-csharp[DP L2E Conceptual Examples#ConstructorForLiteral](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#constructorforliteral)]
 [!code-vb[DP L2E Conceptual Examples#ConstructorForLiteral](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#constructorforliteral)]  
  
 新しい配列もクライアントで実行されます。  
  
## <a name="store-exceptions"></a>ストアの例外  
 クエリ実行時に発生したストア エラーはすべてクライアントに渡され、マッピングも処理もされません。  
  
## <a name="store-configuration"></a>ストアの構成  
 ストアでクエリが実行される場合、ストアの構成はすべてのクライアント動作をオーバーライドし、ストア セマンティクスはすべての演算および式で表現されます。 これにより、Null 比較、GUID 順序付け、precise 以外のデータ型 (浮動小数点型や <xref:System.DateTime> など) を含む演算の精度や正確性、および文字列型演算などの領域において、CLR とストアの実行間で違いが発生する可能性があります。 クエリ結果を調べる場合にはこのことに留意することが重要です。  
  
 CLR および SQL Server 間での動作の違いの例を次に示します。  
  
- SQL Server は CLR とは異なる方法で GUID を順序付けます。  
  
- SQL Server で Decimal 型を扱う場合は、結果の精度でも差違が発生する場合もあります。 これは、SQL Server の decimal 型の固定有効桁数の要件によります。 たとえば、<xref:System.Decimal> 値 0.0、0.0、および 1.0 の平均は、クライアント上のメモリでは 0.3333333333333333333333333333 ですが、ストアでは 0.333333 です (SQL Server の decimal 型の既定の有効桁数に基づきます)。  
  
- SQL Server では、一部の文字列比較演算も CLR とは異なった方法で処理されます。 文字列比較の動作は、サーバー上の照合順序の設定によって異なります。  
  
- LINQ to Entities クエリに含まれる関数呼び出しまたはメソッド呼び出しは、Entity Framework の正規関数にマップされ、その後 Transact-SQL に変換され、SQL Server データベースで実行されます。 マップされたこれらの関数が表す動作は、基本クラス ライブラリでの実装とは異なる場合もあります。 たとえば、空の文字列をパラメーターとして <xref:System.String.Contains%2A>, <xref:System.String.StartsWith%2A> メソッドおよび <xref:System.String.EndsWith%2A> メソッドを呼び出すと、CLR での実行では `true` が返されますが、SQL Server での実行では `false` が返されます。 また、末尾の空白のみが異なる 2 つの文字列は SQL Server では同じと見なされますが、CLR では同じではないと見なされるため、<xref:System.String.EndsWith%2A> メソッドは、異なる結果を返す場合があります。 この例を次に示します。  
  
 [!code-csharp[DP L2E Conceptual Examples#CanonicalFuncVsCLRBaseType](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#canonicalfuncvsclrbasetype)]
 [!code-vb[DP L2E Conceptual Examples#CanonicalFuncVsCLRBaseType](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#canonicalfuncvsclrbasetype)]
