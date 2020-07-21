---
title: Enum ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.Enum
helpviewer_keywords:
- enumerated constants [Visual Basic]
- Enum statement [Visual Basic]
- Private keyword [Visual Basic], Enum statements
- Public keyword [Visual Basic], in Enum statement
- variables [Visual Basic], enumeration
- constants [Visual Basic], enumerated
ms.assetid: a45e51f1-65ff-48e1-bf32-79130f137377
ms.openlocfilehash: 976cc68d67c69ec86918962ab2dd3406d15aed9a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404733"
---
# <a name="enum-statement-visual-basic"></a>Enum ステートメント (Visual Basic)

列挙型を宣言し、そのメンバーの値を定義します。

## <a name="syntax"></a>構文

```vb
[ <attributelist> ] [ accessmodifier ]  [ Shadows ]
Enum enumerationname [ As datatype ]
   memberlist
End Enum
```

## <a name="parts"></a>指定項目

- `attributelist`

  任意。 この列挙型に適用される属性の一覧です。 [属性リスト](attribute-list.md)は山かっこ ("`<`" および "`>`") で囲む必要があります。

  <xref:System.FlagsAttribute> 属性は、列挙型のインスタンスの値に複数の列挙型メンバーを含めることができること、および各メンバーが列挙値のビット フィールドを表すことを示します。

- `accessmodifier`

  任意。 どのようなコードからこの列挙型にアクセスできるのかを指定します。 次のいずれかの値を指定します。

  - [Public](../modifiers/public.md)

  - [Protected](../modifiers/protected.md)

  - [Friend](../modifiers/friend.md)

  - [Private](../modifiers/private.md)

  - [Protected Friend](../modifiers/protected-friend.md)

  - [Private Protected](../modifiers/private-protected.md)

- `Shadows`

  任意。 この列挙型により、基底クラスにある、同じ名前を持つプログラミング要素、またはオーバーロードされる要素のセットが宣言し直されて隠ぺいされることを指定します。 [Shadows](../modifiers/shadows.md) は、そのメンバーではなく、列挙型自体でのみ指定できます。

- `enumerationname`

  必須です。 列挙型の名前。 有効な名前については、「[宣言された要素の名前](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。

- `datatype`

  任意。 列挙型とそのすべてのメンバーのデータ型。

- `memberlist`

  必須です。 このステートメントで宣言されているメンバー定数の一覧。 個々のソース コード行に複数のメンバーが表示されます。

  `member` の構文と指定項目は次のとおりです。`[<attribute list>] member name [ = initializer ]`

  |パーツ|説明|
  |---|---|
  |`membername`|必須です。 このメンバーの名前。|
  |`initializer`|任意。 コンパイル時に評価され、このメンバーに代入される式。|

- `End` `Enum`

  `Enum` ブロックを終了します。

## <a name="remarks"></a>Remarks

論理的に相互に関連付けられている変化しない値のセットがある場合は、それらを列挙型でまとめて定義できます。 これにより、列挙型とそのメンバーにわかりやすい名前が指定され、その値よりも覚えやすくなります。 その後、コード内のさまざまな場所で列挙型メンバーを使用できます。

列挙型を使用する利点は次のとおりです。

- 数の入れ替えや入力間違いによるエラーを減らせます。

- 値を後で変更しやすくなります。

- コードが読みやすくなり、コードにエラーが生じる可能性を抑えられます。

- 上位互換性を確保できます。 列挙型を使用すると、今後メンバー名に対応する値が変更された場合に、コードでエラーが発生する確率が低くなります。

列挙型には、名前、基になるデータ型、およびメンバーのセットが含まれます。 各メンバーは定数を表します。

プロシージャの外部で、クラス、構造体、モジュール、またはインターフェイス レベルで宣言された列挙型は、*メンバー列挙型*です。 それを宣言するには、クラス、構造体、モジュール、またはインターフェイスのメンバーです。

メンバー列挙型には、クラス、構造体、モジュール、またはインターフェイス内のどこからでもアクセスできます。 クラス、構造体、またはモジュールの外部のコードでは、メンバー列挙型の名前を、そのクラス、構造体、またはモジュールの名前で修飾する必要があります。 [Imports](imports-statement-net-namespace-and-type.md) ステートメントをソース ファイルに追加することで、完全修飾名を使用する必要がなくなります。

クラス、構造体、モジュール、またはインターフェイスの外部で、名前空間レベルで宣言された列挙型は、それが表示される名前空間のメンバーになります。

列挙型の*宣言コンテキスト*は、ソース ファイル、名前空間、クラス、構造体、モジュール、またはインターフェイスのいずれかである必要があり、プロシージャでは宣言できません。 詳細については、「[宣言コンテキストと既定のアクセス レベル](declaration-contexts-and-default-access-levels.md)」を参照してください。

列挙型全体に属性を適用することはできますが、そのメンバーに個別に適用することはできません。 属性により、アセンブリのメタデータに情報が提供されます。

## <a name="data-type"></a>データの種類

`Enum` ステートメントでは、列挙型のデータ型を宣言できます。 各メンバーは、列挙型のデータ型を受け取ります。 `Byte`、`Integer`、`Long`、`SByte`、`Short`、`UInteger`、`ULong`、または `UShort` を指定できます。

列挙型に `datatype` を指定しない場合、各メンバーはその `initializer` のデータ型を受け取ります。 `datatype` と `initializer` の両方を指定した場合、`initializer` のデータ型は `datatype` に変換可能である必要があります。 `datatype` も `initializer` も存在しない場合、データ型は既定で `Integer` に設定されます。

## <a name="initializing-members"></a>メンバーの初期化

`Enum` ステートメントでは、`memberlist` で選択されたメンバーの内容を初期化できます。 `initializer` を使用して、メンバーに代入される式を指定します。

メンバーに `initializer` を指定しなかった場合、Visual Basic では、0 (`memberlist` の最初の `member` である場合)、または `member` の直前の値より 1 大きい値に初期化されます。

各 `initializer` で指定される式には、リテラルの任意の組み合わせ、既に定義されている他の定数、および既に定義されている列挙型メンバー (この列挙型の前のメンバーを含む) を使用できます。 算術演算子と論理演算子を使用して、そのような要素を組み合わせることができます。

`initializer` では、変数や関数を使用することはできません。 ただし、`CByte` や `CShort` などの変換キーワードを使用できます。 定数 `String` または `Char` 引数でそれを呼び出す場合は、コンパイル時に評価できるため、`AscW` を使用することもできます。

列挙型に浮動小数点値を指定することはできません。 メンバーに浮動小数点値が割り当てられていて `Option Strict` が on に設定されている場合は、コンパイラ エラーが発生します。 `Option Strict` が off に設定されている場合は、値は自動的に `Enum` 型に変換されます。

メンバーの値が、基になるデータ型で許容される範囲を超えている場合、またはメンバーを、基になるデータ型で許容される最大値に初期化した場合、コンパイラによってエラーが報告されます。

## <a name="modifiers"></a>修飾子

クラス、構造体、モジュール、およびインターフェイス メンバーの列挙型は、既定でパブリック アクセスに設定されます。 アクセス修飾子を使用してこれらのアクセス レベルを調整できます。 名前空間メンバーの列挙型は、既定で friend アクセスに設定されます。 アクセス レベルはパブリックに調整できますが、プライベートにしたり保護することはできません。 詳しくは、「[Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。

すべての列挙型メンバーにはパブリック アクセスがあり、それらのメンバーに対してアクセス修飾子を使用することはできません。 ただし、列挙型自体のアクセス レベルがより制限されている場合は、指定された列挙型アクセス レベルが優先されます。

既定では、すべての列挙型は型であり、そのフィールドは定数です。 したがって、列挙型またはそのメンバーを宣言するときに、`Shared`、`Static`、および `ReadOnly` キーワードを使用することはできません。

## <a name="assigning-multiple-values"></a>複数の値の割り当て

列挙型は、通常、相互に排他的な値を表します。 `Enum` 宣言に <xref:System.FlagsAttribute> 属性を含めることにより、複数の値を列挙型のインスタンスに割り当てることができます。 <xref:System.FlagsAttribute> 属性では、列挙型がビット フィールド、つまりフラグのセットとして扱われることが指定されます。 これらは、"*ビット単位の*" 列挙型と呼ばれます。

<xref:System.FlagsAttribute> 属性を使用して列挙型を宣言する場合は、値に対して 2 の累乗 (1、2、4、8、16 など) を使用することをお勧めします。 また、値が 0 のメンバーの名前を "None" にすることをお勧めします。 その他のガイドラインについては、「<xref:System.FlagsAttribute>」および「<xref:System.Enum>」を参照してください。

## <a name="example"></a>例

`Enum` ステートメントを使用する方法の例を次に示します。 メンバーは、`Medium` ではなく `EggSizeEnum.Medium` と呼ばれることに注意してください。

[!code-vb[VbEnumsTask#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#41)]

## <a name="example"></a>例

次の例のメソッドは、`Egg` クラスの外部にあります。 したがって、`EggSizeEnum` は `Egg.EggSizeEnum` として完全修飾されます。

[!code-vb[VbEnumsTask#42](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#42)]

## <a name="example"></a>例

次の例では、`Enum` ステートメントを使用して、関連する一連の名前付き定数値を定義します。 この場合、値は、データベースのデータ入力フォームをデザインするために選択できる色です。

[!code-vb[VbEnumsTask#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#30)]

## <a name="example"></a>例

次の例は、正の数と負の数の両方を含む値を示しています。

[!code-vb[VbEnumsTask#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#31)]

## <a name="example"></a>例

次の例では、`As` 句を使用して列挙型の `datatype` を指定します。

[!code-vb[VbEnumsTask#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#6)]

## <a name="example"></a>例

次の例は、ビット単位の列挙型を使用する方法を示しています。 ビット単位の列挙型のインスタンスには複数の値を割り当てることができます。 `Enum` 宣言には <xref:System.FlagsAttribute> 属性が含まれています。これは、列挙型をフラグのセットとして処理できることを示します。

[!code-vb[VbEnumsTask#61](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#61)]

## <a name="example"></a>例

次の例では、列挙型を反復処理します。 <xref:System.Enum.GetNames%2A> メソッドを使用して列挙型からメンバー名の配列を取得し、<xref:System.Enum.GetValues%2A> を使用してメンバー値の配列を取得します。

[!code-vb[VbEnumsTask#51](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#51)]

## <a name="see-also"></a>関連項目

- <xref:System.Enum>
- <xref:Microsoft.VisualBasic.Strings.AscW%2A>
- [Const ステートメント](const-statement.md)
- [Dim ステートメント](dim-statement.md)
- [暗黙の型変換と明示的な型変換](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [定数と列挙体](../constants-and-enumerations.md)
