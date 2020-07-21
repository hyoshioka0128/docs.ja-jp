---
title: Const ステートメント
ms.date: 05/12/2018
f1_keywords:
- vb.Const
helpviewer_keywords:
- Const statement [Visual Basic]
ms.assetid: 495b318d-b7c5-4198-94f8-0790a541b07a
ms.openlocfilehash: 3b05d4067ef99e03df07d2c316c982051180d961
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84382108"
---
# <a name="const-statement-visual-basic"></a>Const ステートメント (Visual Basic)

1 つ以上の定数を宣言して定義します。

## <a name="syntax"></a>構文

```vb
[ <attributelist> ] [ accessmodifier ] [ Shadows ]
Const constantlist
```

## <a name="parts"></a>指定項目

`attributelist`  
任意。 このステートメントで宣言されているすべての定数に適用される属性の一覧。 山かっこ ("`<`" および "`>`") 内の[属性リスト](attribute-list.md)を参照してください。

`accessmodifier`  
任意。 これらの定数にアクセスできるコードを指定するには、これを使用します。 [Public](../modifiers/public.md)、[Protected](../modifiers/protected.md)、[Friend](../modifiers/friend.md)、[Protected Friend](../modifiers/protected-friend.md)、[Private](../modifiers/private.md)、または [Private Protected](../modifiers/private-protected.md) を指定できます。

`Shadows`  
任意。 基底クラスのプログラミング要素を再宣言し、隠すには、これを使用します。 「[Shadows](../modifiers/shadows.md)」を参照してください。

`constantlist`  
必須です。 このステートメントで宣言されている定数の一覧。

`constant` `[ ,` `constant` `... ]`

`constant` の構文と指定項目は次のとおりです。

`constantname` `[ As` `datatype` `] =` `initializer`

|パーツ|説明|
|----------|-----------------|
|`constantname`|必須です。 定数の名前。 「 [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。|
|`datatype`|`Option Strict` が `On` の場合は必須です。 定数のデータ型。|
|`initializer`|必須です。 コンパイル時に評価され、定数に代入される式。|

## <a name="remarks"></a>Remarks

アプリケーションで変更されない値がある場合は、名前付き定数を定義し、リテラル値の代わりに使用できます。 名前は、値よりも覚えやすくなります。 定数は 1 回だけ定義すれば、コード内の多くの場所で使用できます。 後のバージョンで値を再定義する必要がある場合、変更する必要がある場所は、`Const` ステートメントだけです。

`Const` はモジュールまたはプロシージャ レベルでのみ使用できます。 つまり、変数の*宣言コンテキスト*は、クラス、構造体、モジュール、プロシージャ、またはブロックであることが必要で、ソース ファイル、名前空間、インターフェイスにすることはできません。 詳細については、「[宣言コンテキストと既定のアクセス レベル](declaration-contexts-and-default-access-levels.md)」を参照してください。

プロシージャ内のローカル定数は、既定でパブリック アクセスに設定されていて、それらでアクセス修飾子を使用することはできません。 クラスおよびモジュール メンバー定数 (プロシージャの外部) の既定は、プライベート アクセスに設定され、構造体メンバー定数の既定は、パブリック アクセスに設定されます。 アクセス修飾子を使用してこれらのアクセス レベルを調整できます。

## <a name="rules"></a>ルール

- **宣言コンテキスト。** モジュール レベルでプロシージャの外部で宣言された定数は*メンバー定数*です。これは、それを宣言するクラス、構造体、またはモジュールのメンバーです。

  プロシージャ レベルで宣言された定数は*ローカル定数*です。これは、それを宣言するプロシージャまたはブロックに対してローカルです。

- **属性。** 属性は、メンバー定数にのみ適用でき、ローカル定数には適用できません。 属性は、アセンブリのメタデータに情報を提供します。これは、ローカル定数などの一時ストレージには意味がありません。

- **修飾子。** 既定で、すべての定数は `Shared`、`Static`、および `ReadOnly` です。 定数の宣言時に、これらのキーワードを使用することはできません。

  プロシージャ レベルで、`Shadows` または任意のアクセス修飾子を使用して、ローカル定数を宣言することはできません。

- **複数の定数。** 同じ宣言ステートメントで複数の定数を宣言し、それぞれに `constantname` 部分を指定できます。 複数の定数はコンマで区切ります。

## <a name="data-type-rules"></a>データ型ルール

- **データ型。** `Const` ステートメントでは、変数のデータ型を宣言できます。 任意のデータ型や列挙の名前を指定できます。

- **既定の型。** `datatype` を指定しない場合、定数は `initializer` のデータ型を受け取ります。 `datatype` と `initializer` の両方を指定した場合、`initializer` のデータ型は `datatype` に変換可能である必要があります。 `datatype` も `initializer` も存在しない場合、データ型は既定で `Object` に設定されます。

- **さまざまな型。** 宣言する定数ごとに個別の `As` 句を使用して、異なる定数に異なるデータ型を指定できます。 ただし、共通の `As` 句を使用して、複数の定数を同じ型として宣言することはできません。

- **初期化。** `constantlist` 内のすべての定数の値を初期化する必要があります。 `initializer` を使用して、定数に代入される式を指定します。 式には、リテラルの任意の組み合わせ、既に定義されている他の定数、および既に定義されている列挙型メンバーを指定できます。 算術演算子と論理演算子を使用して、そのような要素を組み合わせることができます。

  `initializer` では、変数や関数を使用することはできません。 ただし、`CByte` や `CShort` などの変換キーワードを使用できます。 定数 `String` または `Char` 引数でそれを呼び出す場合は、コンパイル時に評価できるため、`AscW` を使用することもできます。

## <a name="behavior"></a>動作

- **範囲**。 ローカル定数は、それらのプロシージャまたはブロック内からのみアクセスできます。 メンバー定数は、それらのクラス、構造体、またはモジュール内のどこからでもアクセスできます。

- **修飾。** クラス、構造体、またはモジュールの外部のコードでは、メンバー定数の名前を、そのクラス、構造体、またはモジュールの名前で修飾する必要があります。 プロシージャまたはブロックの外部のコードでは、そのプロシージャまたはブロック内のローカル定数を参照することはできません。

## <a name="example"></a>例

次の例では、`Const` ステートメントを使用して、リテラル値の代わりに使用する定数を宣言しています。

[!code-vb[VbVbalrStatements#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#13)]

## <a name="example"></a>例

`Object` データ型の定数を定義すると、Visual Basic コンパイラによって `Object` ではなく `initializer` の型が指定されます。 次の例では、定数 `naturalLogBase` はランタイム型 `Decimal` になります。

[!code-vb[VbVbalrStatements#87](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#87)]

前の例では、[GetType 演算子](../operators/gettype-operator.md)によって返された <xref:System.Type> オブジェクトに対して <xref:System.Type.ToString%2A> メソッドを使用しています。<xref:System.Type> は `CStr` を使用して `String` に変換できないためです。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Strings.Asc%2A>
- <xref:Microsoft.VisualBasic.Strings.AscW%2A>
- [Enum ステートメント](enum-statement.md)
- [#Const ディレクティブ](../directives/const-directive.md)
- [Dim ステートメント](dim-statement.md)
- [ReDim ステートメント](redim-statement.md)
- [暗黙の型変換と明示的な型変換](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [定数と列挙体](../../programming-guide/language-features/constants-enums/index.md)
- [定数と列挙体](../constants-and-enumerations.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
