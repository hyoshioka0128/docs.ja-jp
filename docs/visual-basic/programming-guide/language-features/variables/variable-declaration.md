---
title: 変数宣言
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], declaring
- member variables [Visual Basic], declarations
- Dim statement [Visual Basic], variable declaration
- declaring variables [Visual Basic]
- variables [Visual Basic], scope
- variables [Visual Basic], data types
- data types [Visual Basic], variable declarations
- lifetime [Visual Basic], variables
- variables [Visual Basic], lifetime
- access levels [Visual Basic], variables
- scope [Visual Basic], declaration statements
- variables [Visual Basic], access level
- local variables [Visual Basic], declarations
- scope [Visual Basic], variables
ms.assetid: d8f10226-92b1-480f-9f53-df377b2d7e15
ms.openlocfilehash: 587cb84faa09b686361c255c413ad852780b8971
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410297"
---
# <a name="variable-declaration-in-visual-basic"></a>Visual Basic での変数宣言
変数を宣言して、その名前と特性を指定します。 変数の宣言ステートメントは、[Dim ステートメント](../../../language-reference/statements/dim-statement.md)です。 その場所と内容によって、変数の特性が決まります。  
  
 変数の名前付け規則と考慮事項については、「[宣言された要素の名前](../declared-elements/declared-element-names.md)」を参照してください。  
  
## <a name="declaration-levels"></a>宣言レベル  
  
### <a name="local-and-member-variables"></a>ローカル変数とメンバー変数  
 "*ローカル変数*" は、プロシージャ内で宣言されている変数です。 "*メンバー変数*" は、Visual Basic 型のメンバーです。この変数は、クラス、構造体、またはモジュールの内部のモジュール レベルで宣言されますが、そのクラス、構造体、またはモジュールの内部のプロシージャ内では宣言されません。  
  
### <a name="shared-and-instance-variables"></a>共有変数とインスタンス変数  
 クラス内または構造体内のメンバー変数のカテゴリは、そのメンバーが共有されているかどうかによって異なります。 [Shared](../../../language-reference/modifiers/shared.md) キーワードを使用して宣言されている場合、それは "*共有変数*" であり、クラスまたは構造体のすべてのインスタンス間で共有される 1 つのコピーに存在します。  
  
 そうでない場合は "*インスタンス変数*" であり、クラスまたは構造体のインスタンスごとに別のコピーが作成されます。 インスタンス変数の特定のコピーは、それが作成されたクラスまたは構造体のインスタンスでのみ使用できます。 それは、そのクラスまたは構造体の他のすべてのインスタンスのインスタンス変数のコピーとは無関係です。  
  
## <a name="declaring-data-type"></a>データ型の宣言  
 宣言ステートメントの [As](../../../language-reference/statements/as-clause.md) 句を使用すると、宣言する変数のデータ型またはオブジェクト型を定義することができます。 変数には、次のいずれかの型を指定できます。  
  
- 基本データ型 (`Boolean`、`Long`、`Decimal` など)  
  
- 複合データ型 (配列や構造体など)  
  
- そのアプリケーション内または別のアプリケーション内で定義されているオブジェクト型 (クラス)  
  
- .NET Framework クラス (<xref:System.Windows.Forms.Label> や <xref:System.Windows.Forms.TextBox> など)  
  
- インターフェイス型 (<xref:System.IComparable> や <xref:System.IDisposable> など)  
  
 1 つのステートメントで複数の変数を宣言できます。データ型を繰り返す必要はありません。 次のステートメントでは、変数 `i`、`j`、`k` は `Integer` 型として、変数 `l` と `m` は `Long` 型として、変数 `x` と `y` は `Single` 型として、宣言されています。  
  
```vb  
Dim i, j, k As Integer  
' All three variables in the preceding statement are declared as Integer.  
Dim l, m As Long, x, y As Single  
' In the preceding statement, l and m are Long, x and y are Single.  
```  
  
 データ型について詳しくは、[データ型](../data-types/index.md)に関するページをご覧ください。 オブジェクトについて詳しくは、「[オブジェクトとクラス](../objects-and-classes/index.md)」および「[コンポーネントによるプログラミング](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/0ffkdtkf(v=vs.120))」をご覧ください。  
  
## <a name="local-type-inference"></a>ローカル型の推論  
 `As` 句を使用しないでローカル変数を宣言すると、"*型の推定*" を使用してそのデータ型が決定されます。 コンパイラでは、初期化式の型から変数の型が推定されます。 これにより、型を明示的に指定せずに変数を宣言できます。 次の例では、`num1` と `num2` はどちらも整数として厳密に型指定されます。  
  
 [!code-vb[VbVbalrTypeInference#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#1)]  
  
 ローカル型推論を使用する場合は、`Option Infer` を `On` に設定する必要があります。 詳細については、「[ローカル型の推論](local-type-inference.md)」と「[Option Infer ステートメント](../../../language-reference/statements/option-infer-statement.md)」を参照してください。  
  
## <a name="characteristics-of-declared-variables"></a>宣言された変数の特性  
 変数の "*有効期間*" は、その変数を使用できる期間です。 一般に、変数は、それが宣言されている要素 (プロシージャやクラスなど) が存在し続ける限り、存在しています。 変数が含まれる要素の有効期間より長く、変数が存在し続ける必要がない場合は、宣言で特に何も行う必要はありません。 変数が含まれる要素より長く、変数が存在し続ける必要がある場合は、その `Dim` ステートメントに `Static` または `Shared` キーワードを含めることができます。 詳しくは、「[Visual Basic における有効期間](../declared-elements/lifetime.md)」をご覧ください。  
  
 変数の "*スコープ*" は、名前を修飾せずに変数を参照できるすべてのコードのセットです。 変数のスコープは、変数が宣言されている場所によって決まります。 特定の領域にあるコードは、その領域内で定義されている変数を、名前を修飾する必要なしに使用できます。 詳細については、「 [Scope in Visual Basic](../declared-elements/scope.md)」を参照してください。  
  
 変数の "*アクセス レベル*" は、変数にアクセスする権限を持つコードの範囲です。 これは、`Dim` ステートメントで使用されているアクセス修飾子 ([Public](../../../language-reference/modifiers/public.md) や [Private](../../../language-reference/modifiers/private.md) など) によって決まります。 詳しくは、「[Visual Basic でのアクセス レベル](../declared-elements/access-levels.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [方法: 新しい変数を作成する](how-to-create-a-new-variable.md)
- [方法: 変数に値を格納する、および変数から値を取得する](how-to-move-data-into-and-out-of-a-variable.md)
- [データの種類](../../../language-reference/data-types/index.md)
- [Protected](../../../language-reference/modifiers/protected.md)
- [Friend](../../../language-reference/modifiers/friend.md)
- [Static](../../../language-reference/modifiers/static.md)
- [宣言された要素の特性](../declared-elements/declared-element-characteristics.md)
- [ローカル型の推論](local-type-inference.md)
- [Option Infer ステートメント](../../../language-reference/statements/option-infer-statement.md)
