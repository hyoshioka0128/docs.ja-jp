---
title: オブジェクト初期化子:名前付きの型と匿名型
ms.date: 07/20/2015
f1_keywords:
- vb.ObjectInitializer
helpviewer_keywords:
- object initializers [Visual Basic]
- anonymous types [Visual Basic], object initializers
- initializing properties [Visual Basic]
- initializers [Visual Basic]
- named types [Visual Basic]
ms.assetid: e2df3807-a70f-49dd-ac94-f1e07f472b1b
ms.openlocfilehash: 5561812a53e2fe45c3ad4d12d0e18a8a1e948559
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411767"
---
# <a name="object-initializers-named-and-anonymous-types-visual-basic"></a>オブジェクト初期化子:名前付きの型と匿名型 (Visual Basic)
オブジェクト初期化子を使用すると、1 つの式を使用して複雑なオブジェクトのプロパティを指定できます。 それらを使用して、名前付きの型と匿名型のインスタンスを作成できます。  
  
## <a name="declarations"></a>宣言  
 名前付きの型と匿名型のインスタンスの宣言はほぼ同じように見えますが、それらの効果は同じではありません。 各カテゴリには、独自の機能と制限があります。 次の例は、オブジェクト初期化子リストを使用して、名前付きクラス `Customer` のインスタンスを宣言して初期化する便利な方法を示しています。 クラスの名前がキーワード `New` の後に指定されていることに注意してください。  
  
 [!code-vb[VbVbalrObjectInit#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#1)]  
  
 匿名型には使用可能な名前がありません。 そのため、匿名型のインスタンス化でクラス名を含めることはできません。  
  
 [!code-vb[VbVbalrObjectInit#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#2)]  
  
 2 つの宣言の要件と結果は同じではありません。 `namedCust` の場合、`Name` プロパティを持つ `Customer` クラスが既に存在している必要があり、宣言によってそのクラスのインスタンスが作成されます。 `anonymousCust` の場合、コンパイラによって、1 つのプロパティ、`Name` という文字列を持つ新しいクラスが定義され、そのクラスの新しいインスタンスが作成されます。  
  
## <a name="named-types"></a>名前付きの型  
 オブジェクト初期化子は、型のコンストラクターを呼び出し、1 つのステートメントで一部またはすべてのプロパティの値を設定するシンプルな方法を提供します。 コンパイラによって、ステートメントの適切なコンストラクターが呼び出されます。引数が指定されていない場合はパラメーターなしのコンストラクター、または 1 つ以上の引数が渡された場合はパラメーター化されたコンストラクターです。 その後、指定したプロパティが、初期化子リストに提示されている順序で初期化されます。  
  
 初期化子リストの各初期化は、クラスのメンバーへの初期値の代入から構成されます。 メンバーの名前とデータ型は、クラスを定義するときに決定します。 次の例では、`Customer` クラスが存在する必要があり、文字列値を受け入れる `Name` と `City` という名前のメンバーが必要です。  
  
 [!code-vb[VbVbalrObjectInit#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#3)]  
  
 または、次のコードを使用して同じ結果を得ることができます。  
  
 [!code-vb[VbVbalrObjectInit#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#4)]  
  
 これらの各宣言は、次の例と同じです。この例では、パラメーターなしのコンストラクターを使用して `Customer` オブジェクトを作成し、次に `With` ステートメントを使用して、`Name` および `City` プロパティの初期値を指定しています。  
  
 [!code-vb[VbVbalrObjectInit#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#5)]  
  
 `Customer` クラスに、たとえば `Name` の値を渡すことができるパラメーター化されたコンストラクターが含まれている場合、次の方法で `Customer` オブジェクトを宣言して初期化することもできます。  
  
 [!code-vb[VbVbalrObjectInit#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#6)]  
  
 次のコードに示すように、すべてのプロパティを初期化する必要はありません。  
  
 [!code-vb[VbVbalrObjectInit#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#7)]  
  
 ただし、初期化リストを空にすることはできません。 初期化されていないプロパティでは、それらの既定値が保持されます。  
  
### <a name="type-inference-with-named-types"></a>名前付きの型による型の推定  
 オブジェクト初期化子とローカル型推論を組み合わせて、`cust1` の宣言のコードを短縮できます。 これにより、変数宣言で `As` 句を省略できます。 変数のデータ型は、代入によって作成されたオブジェクトの型から推論されます。 次の例では、`cust6` の型は `Customer` です。  
  
 [!code-vb[VbVbalrObjectInit#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#8)]  
  
### <a name="remarks-about-named-types"></a>名前付きの型に関する注意  
  
- オブジェクト初期化子リストでクラス メンバーを複数回初期化することはできません。 `cust7` の宣言によってエラーが発生します。  
  
     [!code-vb[VbVbalrObjectInit#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#9)]  
  
- メンバーは、それ自体または別のフィールドを初期化するために使用できます。 次の `cust8` の宣言のように、メンバーが初期化される前にアクセスされた場合は、既定値が使用されます。 オブジェクト初期化子を使用する宣言が処理されるときに最初に行われることは、適切なコンストラクターの呼び出しです。 その後、初期化子リスト内の個々のフィールドが初期化されます。 次の例では、`Name` の既定値が `cust8` に代入され、初期化された値が `cust9` に代入されています。  
  
     [!code-vb[VbVbalrObjectInit#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#10)]  
  
     次の例では、`cust3` と `cust4` のパラメーター化されたコンストラクターを使用して、`cust10` と `cust11` を宣言して初期化しています。  
  
     [!code-vb[VbVbalrObjectInit#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#11)]  
  
- オブジェクト初期化子は入れ子にすることができます。 次の例では、`AddressClass` は `City` と `State` の 2 つのプロパティを持つクラスであり、`Customer` クラスには `Address` のインスタンスである `AddressClass` プロパティがあります。  
  
     [!code-vb[VbVbalrObjectInit#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#12)]  
  
- 初期化リストは空にすることはできません。  
  
- 初期化されるインスタンスはオブジェクト型にすることはできません。  
  
- 初期化されるクラス メンバーは、共有メンバー、読み取り専用のメンバー、定数、またはメソッド呼び出しにすることはできません。  
  
- 初期化されるクラス メンバーにインデックスを作成したり、修飾したりすることはできません。 次の例ではコンパイラ エラーが発生します。  
  
     `'' Not valid.`  
  
     `' Dim c1 = New Customer With {.OrderNumbers(0) = 148662}`  
  
     `' Dim c2 = New Customer with {.Address.City = "Springfield"}`  
  
## <a name="anonymous-types"></a>匿名型  
 匿名型では、オブジェクト初期化子を使用して、明示的に定義して名前を付けない新しい型のインスタンスを作成します。 代わりに、コンパイラによって、オブジェクト初期化子リストに指定したプロパティに従って型が生成されます。 型の名前を指定しないため、*匿名型*と呼ばれます。 たとえば、次の宣言を先述の `cust6` の宣言と比較します。  
  
 [!code-vb[VbVbalrObjectInit#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#13)]  
  
 構文上の違いは、`New` の後に、データ型についての名前が指定されていないことだけです。 しかし、何が起こるかはかなり異なります。 コンパイラによって、`Name` と `City` の 2 つのプロパティを持つ新しい匿名型が定義され、指定した値を使用してそのインスタンスが作成されます。 型の推定によって、例の `Name` と `City` の型が文字列であると判断されます。  
  
> [!CAUTION]
> 匿名型の名前はコンパイラによって生成され、コンパイルごとに異なる可能性があります。 コードでは、匿名型の名前を使用したり、それに依存したりしないでください。  
  
 型の名前を使用できないため、`As` 句を使用して `cust13` を宣言することはできません。 その型は推論される必要があります。 遅延バインディングを使用しない場合、これによって、匿名型の使用がローカル変数に限定されます。  
  
 匿名型は、LINQ クエリのクリティカルなサポートを提供します。 クエリでの匿名型の使用の詳細については、「[匿名型](anonymous-types.md)」と「[Visual Basic における LINQ の概要](../linq/introduction-to-linq.md)」を参照してください。  
  
### <a name="remarks-about-anonymous-types"></a>匿名型に関する注意  
  
- 一般に、匿名型の宣言に含まれるすべてまたはほとんどのプロパティがキー プロパティになります。これは、プロパティ名の前に `Key` キーワードを入力することによって示されます。  
  
     [!code-vb[VbVbalrObjectInit#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#14)]  
  
     キー プロパティの詳細については、「[Key](../../../language-reference/modifiers/key.md)」を参照してください。  
  
- 名前付きの型と同様に、匿名型定義の初期化子リストには、少なくとも 1 つのプロパティを宣言する必要があります。  
  
     [!code-vb[VbVbalrObjectInit#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#2)]  
  
- 匿名型のインスタンスが宣言されている場合、コンパイラによって、一致する匿名型定義が生成されます。 プロパティの名前とデータ型が、インスタンス宣言から取得され、コンパイラによって定義に含まれます。 名前付きの型の場合と同じように、プロパティには事前に名前が付けられて定義されません。 それらの型は推論されます。 `As` 句を使用してプロパティのデータ型を指定することはできません。  
  
- 匿名型では、他のいくつかの方法でプロパティの名前と値を設定することもできます。 たとえば、匿名型のプロパティは、変数の名前と値の両方、または別のオブジェクトのプロパティの名前と値の両方を受け取ることができます。  
  
     [!code-vb[VbVbalrObjectInit#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#15)]  
  
     匿名型でプロパティを定義するためのオプションの詳細については、「[方法:匿名型の宣言におけるプロパティ名と型を推論する](how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [ローカル型の推論](../variables/local-type-inference.md)
- [匿名型](anonymous-types.md)
- [Visual Basic における LINQ の概要](../linq/introduction-to-linq.md)
- [方法: 匿名型の宣言におけるプロパティ名と型を推論する](how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)
- [Key](../../../language-reference/modifiers/key.md)
- [方法: オブジェクト初期化子を使用してオブジェクトを宣言する](how-to-declare-an-object-by-using-an-object-initializer.md)
