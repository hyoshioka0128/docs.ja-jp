---
title: Property Statement
ms.date: 05/12/2018
f1_keywords:
- vb.PropertySet
- vb.Property
- vb.PropertyGet
helpviewer_keywords:
- Property statement [Visual Basic]
- default modifier
- property procedures [Visual Basic], Property statements
- Property keyword [Visual Basic]
ms.assetid: 3155edaf-8ebd-45c6-9cef-11d5d2dc8d38
ms.openlocfilehash: 80bce2442d96ecb9c548a88c8e5ee44c6258473b
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74346758"
---
# <a name="property-statement"></a>Property Statement

プロパティの名前、およびプロパティの値を格納して取得するために使用されるプロパティ プロシージャを宣言します。

## <a name="syntax"></a>構文

```vb
[ <attributelist> ] [ Default ] [ accessmodifier ]
[ propertymodifiers ] [ Shared ] [ Shadows ] [ ReadOnly | WriteOnly ] [ Iterator ]
Property name ( [ parameterlist ] ) [ As returntype ] [ Implements implementslist ]
    [ <attributelist> ] [ accessmodifier ] Get
        [ statements ]
    End Get
    [ <attributelist> ] [ accessmodifier ] Set ( ByVal value As returntype [, parameterlist ] )
        [ statements ]
    End Set
End Property
- or -
[ <attributelist> ] [ Default ] [ accessmodifier ]
[ propertymodifiers ] [ Shared ] [ Shadows ] [ ReadOnly | WriteOnly ]
Property name ( [ parameterlist ] ) [ As returntype ] [ Implements implementslist ]
```

## <a name="parts"></a>指定項目

- `attributelist`

  任意。 このプロパティか、`Get` または `Set` プロシージャに適用される属性の一覧です。 「[属性リスト](attribute-list.md)」を参照してください。

- `Default`

  任意。 このプロパティが、定義されているクラスまたは構造体の既定のプロパティであることを指定します。 既定のプロパティはパラメーターを受け取る必要があり、プロパティ名を指定せずに設定および取得できます。 プロパティを `Default` として宣言する場合、プロパティで、またはそのプロパティ プロシージャのいずれかで `Private` を使用することはできません。

- `accessmodifier`

  `Property` ステートメントで、および `Get` ステートメントと `Set` ステートメントのうちのいずれかで省略可能です。 次のいずれかの値を指定します。

  - [Public](../modifiers/public.md)

  - [Protected](../modifiers/protected.md)

  - [Friend](../modifiers/friend.md)

  - [Private](../modifiers/private.md)

  - [Protected Friend](../modifiers/protected-friend.md)

  - [Private Protected](../modifiers/private-protected.md)

  「 [Access levels in Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。

- `propertymodifiers`

  任意。 次のいずれかの値を指定します。

  - [Overloads](../modifiers/overloads.md)

  - [Overrides](../modifiers/overrides.md)

  - [Overridable](../modifiers/overridable.md)

  - [NotOverridable](../modifiers/notoverridable.md)

  - [MustOverride](../modifiers/mustoverride.md)

  - `MustOverride Overrides`

  - `NotOverridable Overrides`

- `Shared`

  任意。 「[Shared](../modifiers/shared.md)」を参照してください。

- `Shadows`

  任意。 「[Shadows](../modifiers/shadows.md)」を参照してください。

- `ReadOnly`

  任意。 「[ReadOnly](../modifiers/readonly.md)」を参照してください。

- `WriteOnly`

  任意。 「[WriteOnly](../modifiers/writeonly.md)」を参照してください。

- `Iterator`

  任意。 「[反復子](../modifiers/iterator.md)」を参照してください。

- `name`

  必須です。 プロパティ名。 「 [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。

- `parameterlist`

  任意。 このプロパティのパラメーターと、`Set` プロシージャの指定できるその他のパラメーターを表すローカル変数名の一覧です。 [パラメーター リスト](parameter-list.md)に関するページを参照してください。

- `returntype`

  `Option Strict` が `On` の場合は必ず指定します。 このプロパティによって返される値のデータ型。

- `Implements`

  任意。 このプロパティが、それぞれがこのプロパティの含まれているクラスまたは構造体によって実装されたインターフェイスに定義されている、1 つ以上のプロパティを実装することを示します。 「[Implements ステートメント](implements-statement.md)」を参照してください。

- `implementslist`

  `Implements` を指定する場合は、必ず指定します。 実装されるプロパティの一覧です。

  `implementedproperty [ , implementedproperty ... ]`

  `implementedproperty` の構文と指定項目は次のとおりです。

  `interface.definedname`

  |パーツ|説明|
  |---|---|
  |`interface`|必須です。 このプロパティの含まれているクラスまたは構造体によって実装されたインターフェイスの名前です。|
  |`definedname`|必須です。 `interface` の中でプロパティを定義するために使用する名前です。|

- `Get`

  任意。 プロパティが `ReadOnly` とマークされている場合は、必ず指定します。 プロパティの値を返すために使用される `Get` プロパティ プロシージャを開始します。  `Get` ステートメントは、[自動実装プロパティ](../../programming-guide/language-features/procedures/auto-implemented-properties.md)と一緒には使用されません。

- `statements`

  任意。 `Get` または `Set` プロシージャ内で実行するためのステートメントのブロック。

- `End Get`

  `Get` プロパティ プロシージャを終了します。

- `Set`

  任意。 プロパティが `WriteOnly` とマークされている場合は、必ず指定します。 プロパティの値を格納するために使用される `Set` プロパティ プロシージャを開始します。  `Set` ステートメントは、[自動実装プロパティ](../../programming-guide/language-features/procedures/auto-implemented-properties.md)と一緒には使用されません。

- `End Set`

  `Set` プロパティ プロシージャを終了します。

- `End Property`

  このプロパティの定義を終了します。

## <a name="remarks"></a>Remarks

`Property` ステートメントは、プロパティの宣言を導入します。 プロパティには `Get` プロシージャ (読み取り専用)、`Set` プロシージャ (書き込み専用)、またはその両方 (読み取り/書き込み) を指定できます。 自動実装プロパティを使用する場合は、`Get` プロシージャと `Set` プロシージャを省略できます。 詳細については、「[自動実装プロパティ](../../programming-guide/language-features/procedures/auto-implemented-properties.md)」を参照してください。

`Property` は、クラス レベルでのみ使用できます。 つまり、プロパティの*宣言コンテキスト*は、クラス、構造体、モジュール、またはインターフェイスであることが必要で、ソース ファイル、名前空間、プロシージャ、ブロックでは宣言できません。 詳細については、「[宣言コンテキストと既定のアクセス レベル](declaration-contexts-and-default-access-levels.md)」を参照してください。

既定では、プロパティはパブリック アクセスを使用します。 `Property` ステートメントでアクセス修飾子を使用してプロパティのアクセス レベルを調整できます。また、必要に応じて、そのプロパティ プロシージャの 1 つをより制限の厳しいアクセス レベルに調整することもできます。

Visual Basic は、プロパティの割り当て時に `Set` プロシージャにパラメーターを渡します。 `Set` のパラメーターを指定しない場合、統合開発環境 (IDE) では `value` という名前の暗黙的なパラメーターが使用されます。 このパラメーターは、プロパティに割り当てられる値を保持します。 通常はこの値をプライベート ローカル変数に格納し、これは `Get` プロシージャが呼び出されるたびに返されます。

## <a name="rules"></a>ルール

- **混合アクセス レベル。** 読み取り/書き込みプロパティを定義する場合は、必要に応じて、`Get` または `Set` のいずれかのプロシージャに対して異なるアクセス レベルを指定できますが、両方に対して指定することはできません。 この場合、プロシージャのアクセス レベルは、プロパティのアクセス レベルよりも制限されている必要があります。 たとえば、プロパティが `Friend` として宣言されている場合は、`Set` プロシージャを、`Public` ではなく `Private` として宣言できます。

  `ReadOnly` または `WriteOnly` プロパティを定義する場合、1 つのプロパティ プロシージャ (それぞれ `Get` または `Set`) がプロパティのすべてを表します。 このようなプロシージャに対して異なるアクセス レベルを宣言することはできません。これは、プロパティに 2 つのアクセス レベルが設定されるためです。

- **戻り値の型。** `Property` ステートメントは、返される値のデータ型を宣言できます。 任意のデータ型や、列挙、構造体、クラス、またはインターフェイスの名前を指定できます。

  `returntype` を指定しない場合、プロパティは `Object` を返します。

- **実装。** このプロパティで `Implements` キーワードが使用されている場合、含まれているクラスまたは構造体には、その `Class` または `Structure` ステートメントの直後に `Implements` ステートメントが必要です。 `Implements` ステートメントには、`implementslist` で指定された各インターフェイスを含める必要があります。 ただし、インターフェイスが `Property` を定義するときに使用する名前 (`definedname`) は、このプロパティの名前と同じである必要はありません (`name`)。

## <a name="behavior"></a>動作

- **プロパティ プロシージャからの復帰。** `Get` または `Set` プロシージャから呼び出し元のコードに返されると、実行は、それを呼び出したステートメントの後のステートメントを使用して続行されます。

  `Exit Property` および `Return` ステートメントでは、プロパティ プロシージャがすぐに終了します。 任意の数の `Exit Property` および `Return` ステートメントをプロシージャ内の任意の場所に記述でき、`Exit Property` ステートメントと `Return` ステートメントを混在させることができます。

- **戻り値。** `Get` プロシージャから値を返すには、プロパティ名に値を割り当てるか、`Return` ステートメントに値を含めることができます。 次の例では、プロパティ名 `quoteForTheDay` に戻り値を割り当ててから、`Exit Property` ステートメントを使用して返します。

  [!code-vb[VbVbalrStatements#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#27)]

  [!code-vb[VbVbalrStatements#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#28)]

  `name` に値を割り当てずに `Exit Property` を使用すると、`Get` プロシージャは、プロパティのデータ型の既定値を返します。

  同時に、`Return` ステートメントによって `Get` プロシージャの戻り値が割り当てられ、プロシージャが終了します。 次に例を示します。

  [!code-vb[VbVbalrStatements#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#27)]

  [!code-vb[VbVbalrStatements#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#29)]

## <a name="example"></a>例

次の例では、クラス内にプロパティを宣言しています。

[!code-vb[VbVbalrStatements#51](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#51)]

## <a name="see-also"></a>関連項目

- [自動実装プロパティ](../../programming-guide/language-features/procedures/auto-implemented-properties.md)
- [クラスとオブジェクト](../../programming-guide/language-features/objects-and-classes/index.md)
- [Get ステートメント](get-statement.md)
- [Set ステートメント](set-statement.md)
- [パラメーター リスト](parameter-list.md)
- [default](../modifiers/default.md)
