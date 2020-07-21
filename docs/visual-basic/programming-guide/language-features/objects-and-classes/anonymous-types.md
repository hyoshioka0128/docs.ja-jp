---
title: 匿名型
ms.date: 07/20/2015
f1_keywords:
- vb.AnonymousType
helpviewer_keywords:
- anonymous types [Visual Basic], about anonymous types
- anonymous types [Visual Basic]
- types [Visual Basic], anonymous
ms.assetid: 7b87532c-4b3e-4398-8503-6ea9d67574a4
ms.openlocfilehash: bbe84ce8a62705027c00bc26db74a3c21fa34fd9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411801"
---
# <a name="anonymous-types-visual-basic"></a>匿名型 (Visual Basic)
Visual Basic では匿名型がサポートされています。これを使用すると、データ型のクラス定義を記述せずにオブジェクトを作成できます。 クラスは、コンパイラによって生成されます。 このクラスには使用可能な名前がなく、<xref:System.Object> から直接継承され、オブジェクトの宣言時に指定したプロパティが格納されます。 データ型の名前を指定しないため、*匿名型*と呼ばれます。  
  
 次の例では、`Name` と `Price` の 2 つのプロパティを持つ匿名型のインスタンスとして、変数 `product` を宣言して作成します。  
  
 [!code-vb[VbVbalrAnonymousTypes#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#1)]  
  
 *クエリ式*は、匿名型を使用して、クエリによって選択されたデータの列を結合します。 特定のクエリによって選択される可能性のある列を予測できないため、結果の型を事前に定義することはできません。 匿名型を使用すると、任意の数の列を任意の順序で選択するクエリを記述できます。 コンパイラは、指定されたプロパティと指定された順序に一致するデータ型を作成します。  
  
 次の例では、`products` は Product オブジェクトの一覧であり、それぞれに多くのプロパティがあります。 変数 `namePriceQuery` は、実行されると `Name` と `Price` の 2 つのプロパティを持つ匿名型のインスタンスのコレクションを返すクエリの定義を保持します。  
  
 [!code-vb[VbVbalrAnonymousTypes#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#2)]  
  
 変数 `nameQuantityQuery` は、実行されると `Name` と `OnHand` の 2 つのプロパティを持つ匿名型のインスタンスのコレクションを返すクエリの定義を保持します。  
  
 [!code-vb[VbVbalrAnonymousTypes#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#3)]  
  
 コンパイラによって作成される匿名型のコードの詳細については、「[匿名型の定義](anonymous-type-definition.md)」を参照してください。  
  
> [!CAUTION]
> 匿名型の名前はコンパイラによって生成され、コンパイルごとに異なる可能性があります。 プロジェクトが再コンパイルされるときに名前が変更される可能性があるため、コードでは、匿名型の名前を使用したり、それに依存したりしないでください。  
  
## <a name="declaring-an-anonymous-type"></a>匿名型の宣言  
 匿名型のインスタンスの宣言では、初期化子リストを使用して型のプロパティを指定します。 メソッドやイベントなどの他のクラス要素ではなく、匿名型を宣言する場合は、プロパティのみを指定できます。 次の例では、`product1` は、`Name` と `Price` の 2 つのプロパティを持つ匿名型のインスタンスです。  
  
 [!code-vb[VbVbalrAnonymousTypes#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#4)]  
  
 プロパティをキー プロパティとして指定した場合は、これらを使用して、2 つの匿名型インスタンスが等しいかどうかを比較できます。 ただし、キー プロパティの値は変更できません。 詳細については、このトピックで後述する「キー プロパティ」のセクションを参照してください。  
  
 匿名型のインスタンスの宣言は、オブジェクト初期化子を使用して名前付きの型のインスタンスを宣言するのと似ていることに注意してください。  
  
 [!code-vb[VbVbalrAnonymousTypes#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#5)]  
  
 匿名型のプロパティを指定するその他の方法の詳細については、「[方法: 匿名型の宣言におけるプロパティ名と型を推論する](how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)」を参照してください。  
  
## <a name="key-properties"></a>キー プロパティ  
 キー プロパティは、次のいくつかの基本的な点で、キー以外のプロパティとは異なります。  
  
- 2 つのインスタンスが等しいかどうかを確認するためには、キー プロパティの値のみが比較されます。  
  
- キー プロパティの値は読み取り専用であり、変更することはできません。  
  
- コンパイラによって生成された匿名型のハッシュ コード アルゴリズムには、キー プロパティ値のみが含まれます。  
  
### <a name="equality"></a>等式  
 匿名型のインスタンスは、同じ匿名型のインスタンスである場合にのみ等しくすることができます。 コンパイラは、次の条件を満たす場合、2 つのインスタンスを同じ型のインスタンスとして扱います。  
  
- これらは同じアセンブリ内で宣言されています。  
  
- これらのプロパティは同じ名前を持ち、推論される型は同じであり、同じ順序で宣言されています。 名前の比較では、大文字と小文字は区別されません。  
  
- それぞれに含まれる同じプロパティは、キー プロパティとしてマークされます。  
  
- 各宣言の少なくとも 1 つのプロパティがキー プロパティです。  
  
 キー プロパティを持たない匿名型のインスタンスは、それ自体とのみ等しくなります。  
  
 [!code-vb[VbVbalrAnonymousTypes#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#6)]  
  
 同じ匿名型の 2 つのインスタンスは、それらのキー プロパティの値が等しい場合に等しいとされます。 次の例は、等価性のテスト方法を示しています。  
  
 [!code-vb[VbVbalrAnonymousTypes#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#7)]  
  
### <a name="read-only-values"></a>読み取り専用の値  
 キー プロパティの値は変更できません。 たとえば、前の例の `prod8` では、`Name` フィールドと `Price` フィールドは `read-only` ですが、`OnHand` は変更できます。  
  
 [!code-vb[VbVbalrAnonymousTypes#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#8)]  
  
## <a name="anonymous-types-from-query-expressions"></a>クエリ式からの匿名型  
 クエリ式では、必ずしも匿名型を作成する必要はありません。 可能な場合は、既存の型を使用して列データを保持します。 これは、クエリがデータ ソースからレコード全体を返すか、または各レコードのフィールドを 1 つだけ返す場合に行われます。 次のコード例では、`customers` は `Customer` クラスのオブジェクトのコレクションです。 クラスには多くのプロパティがあり、クエリの結果には、任意の順序で 1 つ以上のプロパティを含めることができます。 最初の 2 つの例では、クエリで名前付きの型の要素が選択されるため、匿名型は必要ありません。  
  
- `custs1` には文字列のコレクションが含まれます。`cust.Name` が文字列であるためです。  
  
     [!code-vb[VbVbalrAnonymousTypes#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#30)]  
  
- `custs2` には `Customer` オブジェクトのコレクションが含まれます。`customers` の各要素が `Customer` オブジェクトであり、要素全体がクエリによって選択されるためです。  
  
     [!code-vb[VbVbalrAnonymousTypes#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#31)]  
  
 ただし、適切な名前付きの型が常に使用可能とは限りません。 ある目的のために顧客の名前と住所を、別の目的のために顧客の ID 番号と場所を、そして 3 つ目の目的のために顧客の名前、住所、および注文履歴を選択することができます。 匿名型を使用すると、プロパティの任意の組み合わせを任意の順序で選択でき、最初に結果を保持するために新しい名前付きの型を宣言する必要はありません。 代わりに、コンパイラは、プロパティのコンパイルごとに匿名型を作成します。 次のクエリでは、`customers` の各 `Customer` オブジェクトから、顧客の名前と ID 番号のみを選択します。 そのため、コンパイラは、それら 2 つのプロパティのみが含まれている匿名型を作成します。  
  
 [!code-vb[VbVbalrAnonymousTYpes#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#32)]  
  
 匿名型のプロパティの名前とデータ型は両方とも、`Select`、`cust.Name`、および `cust.ID` の引数から取得されます。 クエリによって作成される匿名型のプロパティは、常にキー プロパティです。 次の `For Each` ループで `custs3` を実行すると、結果は `Name` と `ID` の 2 つのキー プロパティを持つ匿名型のインスタンスのコレクションになります。  
  
 [!code-vb[VbVbalrAnonymousTypes#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#33)]  
  
 `custs3` によって表されるコレクション内の要素は厳密に型指定されます。IntelliSense を使用して、使用可能なプロパティ間を移動したり、その型を検証したりできます。  
  
 詳細については、「[Visual Basic における LINQ の概要](../linq/introduction-to-linq.md)」を参照してください。  
  
## <a name="deciding-whether-to-use-anonymous-types"></a>匿名型を使用するかどうかの決定  
 オブジェクトを匿名クラスのインスタンスとして作成する前に、それが最適な選択肢かどうかを検討してください。 たとえば、関連データを格納する一時オブジェクトを作成する場合に、完全なクラスに含まれる可能性のある他のフィールドやメソッドが不要な場合は、匿名型が適切な解決策です。 匿名型は、宣言ごとに異なるプロパティを選択する場合や、プロパティの順序を変更する場合にも便利です。 ただし、プロジェクトに同じプロパティを持つ複数のオブジェクトが一定の順序で含まれている場合は、クラス コンストラクターを持つ名前付きの型を使用して、より簡単に宣言することができます。 たとえば、適切なコンストラクターを使用すると、匿名型の複数のインスタンスを宣言するよりも、`Product` クラスの複数のインスタンスを宣言する方が簡単になります。  
  
 [!code-vb[VbVbalrAnonymousTypes#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#9)]  
  
 名前付きの型のもう 1 つの利点は、コンパイラがプロパティ名の誤入力をキャッチできることです。 前の例では、`firstProd2`、`secondProd2`、および `thirdProd2` は、同じ匿名型のインスタンスとして意図されています。 ただし、次のいずれかの方法で誤って `thirdProd2` を宣言すると、その型が `firstProd2` と `secondProd2` とは異なることになります。  
  
 [!code-vb[VbVbalrAnonymousTypes#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#10)]  
  
 さらに重要な点として、匿名型の使用には、名前付きの型のインスタンスには適用されない制限があります。 `firstProd2`、`secondProd2`、`thirdProd2` は、同じ匿名型のインスタンスです。 ただし、共有されている匿名型の名前は使用できません。また、コードで型名を指定する場所を指定することはできません。 たとえば、匿名型を使用して、メソッド シグネチャを定義したり、別の変数やフィールドを宣言したり、任意の型宣言で宣言したりすることはできません。 そのため、メソッド間で情報を共有する必要がある場合、匿名型は適切ではありません。  
  
## <a name="an-anonymous-type-definition"></a>匿名型の定義  
 匿名型のインスタンスの宣言に応答して、コンパイラは、指定されたプロパティを含む新しいクラス定義を作成します。  
  
 匿名型に少なくとも 1 つのキー プロパティが含まれている場合、<xref:System.Object>: <xref:System.Object.Equals%2A>、<xref:System.Object.GetHashCode%2A>、および <xref:System.Object.ToString%2A> から継承された 3 つのメンバーは、この定義によってオーバーライドされます。 等価性をテストし、ハッシュ コード値を決定するために生成されたコードは、キー プロパティのみを考慮します。 匿名型にキー プロパティが含まれていない場合は、<xref:System.Object.ToString%2A> のみがオーバーライドされます。 匿名型の明示的に名前が付けられたプロパティは、生成されたこれらのメソッドと競合しません。 つまり、`.Equals`、`.GetHashCode`、または `.ToString` を使用してプロパティの名前を指定することはできません。  
  
 少なくとも 1 つのキー プロパティを持つ匿名型定義は、<xref:System.IEquatable%601?displayProperty=nameWithType> インターフェイスも実装します。ここで `T` は匿名型の型です。  
  
 コンパイラによって作成される匿名型のコードとオーバーライドされたメソッドの機能の詳細については、「[匿名型の定義](anonymous-type-definition.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [オブジェクト初期化子: 名前付きの型と匿名型](object-initializers-named-and-anonymous-types.md)
- [ローカル型の推論](../variables/local-type-inference.md)
- [Visual Basic における LINQ の概要](../linq/introduction-to-linq.md)
- [方法: 匿名型の宣言におけるプロパティ名と型を推論する](how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)
- [匿名型の定義](anonymous-type-definition.md)
- [Key](../../../language-reference/modifiers/key.md)
