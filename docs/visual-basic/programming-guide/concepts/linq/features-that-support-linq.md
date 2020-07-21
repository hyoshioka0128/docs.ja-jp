---
title: LINQ をサポートする機能
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic, LINQ features
- LINQ [Visual Basic], features supporting LINQ
ms.assetid: c821bb50-b6f6-4cf9-8aba-2717e465bd3a
ms.openlocfilehash: 15585cd8277b1a0df7e3b262db7c9b7a231b16fa
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84383431"
---
# <a name="visual-basic-features-that-support-linq"></a>LINQ をサポートする Visual Basic の機能
統合言語クエリ (LINQ) という名前は、クエリ構文などの言語コンストラクトを言語の中で直接サポートする、Visual Basic のテクノロジをいいます。 LINQ を使用すれば、外部のデータ ソースを照会するために新しい言語を習得する必要はありません。 Visual Basic を使用して、リレーショナル データベースや XML ストア、オブジェクトにデータを照会することができます。 このようにクエリの機能を言語に統合することで、構文エラーやタイプ セーフのチェックをコンパイル時に行えるようになります。 また、多くの場合、既にある知識だけで、豊富で多彩なクエリを Visual Basic で記述することができます。  
  
 以降の各セクションでは、これから皆さんが入門ドキュメントやコード例、サンプル アプリケーションを読むために最低限必要な知識が身に付くよう、LINQ をサポートする言語コンストラクトについて説明します。 また、リンク先のドキュメントもご覧ください。さまざまな言語機能がどのように組み合わさって統合言語クエリが実現されているかについて詳しく説明されています。 まずは、「[チュートリアル: Visual Basic でのクエリの作成](walkthrough-writing-queries.md)」を読むことをお勧めします。  
  
## <a name="query-expressions"></a>クエリ式  
 Visual Basic のクエリ式は、SQL や XQuery と同様の宣言型構文で表現することができます。 クエリ構文は、コンパイル時に、LINQ プロバイダーの標準クエリ演算子拡張メソッドの実装に対するメソッド呼び出しに変換されます。 アプリケーションは、`Imports` ステートメントを使用して適切な名前空間を指定することにより、スコープ内の標準クエリ演算子を制御します。 次に示したのは、Visual Basic のクエリ式の構文例です。  
  
 [!code-vb[VbLINQVbFeatures#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#1)]  
  
 詳細については、「[Visual Basic における LINQ の概要](../../language-features/linq/introduction-to-linq.md)」を参照してください。  
  
## <a name="implicitly-typed-variables"></a>暗黙的に型指定された変数  
 変数を宣言して初期化するときに、型を明示的に指定する代わりに、コンパイラに型を推測させて代入することができます。 これを "*ローカル型推論*" といいます。  
  
 明示的に型が指定される変数と同様、型が推測される変数も厳密に型指定されます。 ローカル型推論が正常に機能するのは、メソッド本体内にローカル変数を定義している場合のみです。 詳細については、「[Option Infer ステートメント](../../../language-reference/statements/option-infer-statement.md)」と[ローカル型推論](../../language-features/variables/local-type-inference.md)に関するページを参照してください。  
  
 ローカル型推論の例を次に示します。 この例を使用するには、`Option Infer` を `On` に設定する必要があります。  
  
 [!code-vb[VbLINQVbFeatures#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#2)]  
  
 LINQ クエリに必要な匿名型も、ローカル型推論で作成することができます。匿名型については、このセクションで後述します。  
  
 以下の LINQ の例では、`Option Infer` が `On` または `Off` の場合に型の推定が行われます。 `Option Infer` が `Off` で、なおかつ `Option Strict` が `On` の場合、コンパイル時のエラーが発生します。  
  
 [!code-vb[VbLINQVbFeatures#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#3)]  
  
## <a name="object-initializers"></a>オブジェクト初期化子  
 オブジェクト初期化子は、クエリ式の中で、クエリの結果を保持する匿名型を作成する必要があるときに使用します。 また、名前付きの型のオブジェクトをクエリの外側で初期化する際にも使用できます。 オブジェクト初期化子を使用すれば、コンストラクターを明示的に呼び出さなくても、オブジェクトを 1 行で初期化することができます。 `Customer` という名前のクラスがあるとしましょう。このクラスには、パブリック プロパティである `Name` と `Phone` のほか、いくつかのプロパティがあります。この場合、オブジェクト初期化子を次のように使用することができます。  
  
 [!code-vb[VbLINQVbFeatures#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#4)]  
  
 詳細については、「[オブジェクト初期化子: 名前付きの型と匿名型](../../language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)」を参照してください。  
  
## <a name="anonymous-types"></a>匿名型  
 クエリの結果に含めたい一連のプロパティを 1 つの要素として一時的にグループ化する場合に、匿名型は高い利便性を発揮します。 その要素に対して名前付きのデータ型を定義しなくても、選択可能なフィールドの組み合わせをクエリの中で自由に、かつ任意の順序で選ぶことができます。  
  
 "*匿名型*" は、コンパイラによって動的に構築されます。 型の名前はコンパイラによって割り当てられ、また、コンパイルのたびに変わる可能性があります。 したがって、その名前を直接使用することはできません。 匿名型の初期化方法は次のとおりです。  
  
 [!code-vb[VbLINQVbFeatures#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#5)]  
  
 詳細については、「[匿名型](../../language-features/objects-and-classes/anonymous-types.md)」を参照してください。  
  
## <a name="extension-methods"></a>拡張メソッド  
 データ型とインターフェイスには、その定義の外側から、拡張メソッドを通じてメソッドを追加することができます。 この機能を使用すると、既存の型を実際に変更しなくても、その型に新しいメソッドを実質的に追加できます。 標準クエリ演算子は、それ自体が、<xref:System.Collections.Generic.IEnumerable%601> を実装する任意の型で LINQ クエリ機能を実現する拡張メソッドのセットです。 <xref:System.Collections.Generic.IEnumerable%601> に対する拡張機能としては、他にも <xref:System.Linq.Enumerable.Count%2A>、<xref:System.Linq.Enumerable.Union%2A>、<xref:System.Linq.Enumerable.Intersect%2A> などがあります。  
  
 次の拡張メソッドは、<xref:System.String> クラスに Print メソッドを追加するものです。  
  
 [!code-vb[VbLINQVbFeatures#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#6)]  
  
 このメソッドの呼び出し方は、<xref:System.String> の通常のインスタンス メソッドと同様です。  
  
 [!code-vb[VbLINQVbFeatures#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#7)]  
  
 詳細については、「[拡張メソッド](../../language-features/procedures/extension-methods.md)」を参照してください。  
  
## <a name="lambda-expressions"></a>ラムダ式  
 ラムダ式は、単一の値を計算して返す、名前を持たない関数です。 名前付きの関数とは異なり、ラムダ式は、定義と実行を同時に行うことができます。 次の例では、"4" が表示されます。  
  
 [!code-vb[VbLINQVbFeatures#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#8)]  
  
 ラムダ式の定義を変数名に代入しておけば、その名前を使用して関数を呼び出すことができます。 次の例でも、"4" が表示されます。  
  
 [!code-vb[VbLINQVbFeatures#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#12)]  
  
 LINQ では、ラムダ式が、多くの標準クエリ演算子の基盤となっています。 基本的なクエリ メソッド (`Where`、`Select`、`Order By`、`Take While` など) で定義されている計算を取り込むためのラムダ式が、コンパイラによって作成されます。  
  
 たとえば、次のコードは、学生のリストからすべての最上級生を返すクエリの定義です。  
  
 [!code-vb[VbLINQVbFeatures#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#9)]  
  
 このクエリ定義は、次の例のようなコードにコンパイルされます。このコードでは、2 つのラムダ式を使用して `Where` と `Select` の引数が指定されています。  
  
 [!code-vb[VbLINQVbFeatures#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#10)]  
  
 どちらのバージョンも、`For Each` ループを使用して実行できます。  
  
 [!code-vb[VbLINQVbFeatures#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQVbFeatures/VB/Class1.vb#11)]  
  
 詳細については、「[ラムダ式](../../language-features/procedures/lambda-expressions.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [統合言語クエリ (LINQ) (Visual Basic)](index.md)
- [Visual Basic の LINQ の概要](getting-started-with-linq.md)
- [LINQ と文字列 (Visual Basic)](linq-and-strings.md)
- [Option Infer ステートメント](../../../language-reference/statements/option-infer-statement.md)
- [Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)
