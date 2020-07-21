---
title: Module ステートメント
ms.date: 07/20/2015
f1_keywords:
- Module
- vb.Module
helpviewer_keywords:
- modules, classes
- modules
- Module statement [Visual Basic]
- modules, declaring
- standard modules
- classes [Visual Basic], vs. modules
- declarations [Visual Basic], modules
ms.assetid: a1243afc-14a5-45df-95d5-51118aeac362
ms.openlocfilehash: 24a27ba41f5ac889f2f2725a2852368a4292a6fb
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404458"
---
# <a name="module-statement"></a>Module ステートメント

モジュールの名前を宣言し、モジュールを構成する変数、プロパティ、イベント、およびプロシージャの定義を提供します。

## <a name="syntax"></a>構文

```vb
[ <attributelist> ] [ accessmodifier ]  Module name
    [ statements ]
End Module
```

## <a name="parts"></a>指定項目

`attributelist`  
任意。 「[属性リスト](attribute-list.md)」を参照してください。

`accessmodifier`  
任意。 次のいずれかの値を指定します。

- [Public](../modifiers/public.md)

- [Friend](../modifiers/friend.md)

「 [Access levels in Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。

`name`  
必須です。 このモジュールの名前です。 「 [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。

`statements`  
任意。 このモジュールの変数、プロパティ、イベント、プロシージャ、および入れ子にされた型を定義するステートメントです。

`End Module`  
`Module` の定義を終了します。

## <a name="remarks"></a>Remarks

`Module` ステートメントは、名前空間全体で使用できる参照型を定義します。 *モジュール* (*標準モジュール*と呼ばれることもあります) はクラスに似ていますが、いくつかの重要な違いがあります。 すべてのモジュールにはインスタンスが 1 つだけあり、変数を作成したり、変数に割り当てたりする必要はありません。 モジュールは、継承をサポートしたり、インターフェイスを実装したりしません。 モジュールはクラスまたは構造体の意味で*型*ではないことに注意してください。モジュールのデータ型を持つようにプログラミング要素を宣言することはできません。

`Module` は、名前空間レベルでのみ使用できます。 つまり、モジュールの*宣言コンテキスト*は、ソース ファイルまたは名前空間である必要があり、クラス、構造体、モジュール、インターフェイス、プロシージャ、またはブロックにすることはできません。 モジュールは、別のモジュール内、または任意の型の中で入れ子にすることはできません。 詳細については、「[宣言コンテキストと既定のアクセス レベル](declaration-contexts-and-default-access-levels.md)」を参照してください。

モジュールの有効期間はプログラムと同じです。 そのメンバーはすべて `Shared` であるため、有効期間もプログラムと同じになります。

モジュールは、既定で [Friend](../modifiers/friend.md) アクセスに設定されます。 アクセス修飾子を使用してこれらのアクセス レベルを調整できます。 詳しくは、「[Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。

モジュールのすべてのメンバーは、暗黙的に `Shared` です。

## <a name="classes-and-modules"></a>クラスとモジュール

これらの要素には多くの類似点がありますが、重要な相違点もいくつかあります。

- **用語。** 以前のバージョンの Visual Basic では、*クラス モジュール* (.cls ファイル) と*標準モジュール* (.bas ファイル) の 2 種類のモジュールを認識します。 現在のバージョンでは、これらの*クラス*と*モジュール*をそれぞれ呼び出します。

- **共有メンバー。** クラスのメンバーが共有メンバーかインスタンス メンバーかを制御できます。

- **オブジェクト指向。** クラスはオブジェクト指向ですが、モジュールはそうではありません。 そのため、オブジェクトとしてインスタンス化できるのはクラスだけです。 詳細については、[オブジェクトとクラス](../../programming-guide/language-features/objects-and-classes/index.md)に関するページを参照してください。

## <a name="rules"></a>ルール

- **修飾子。** すべてのモジュール メンバーは、暗黙的に [Shared](../modifiers/shared.md) です。 メンバーを宣言するときに `Shared` キーワードを使用することはできません。また、メンバーの共有ステータスを変更することもできません。

- **継承。** モジュールは、<xref:System.Object> 以外の型を継承できません。すべてのモジュールが、この型を継承します。 特に、モジュールは別のモジュールからは継承できません。

  <xref:System.Object> を指定する場合でも、モジュールの定義で [Inherits ステートメント](inherits-statement.md)を使用することはできません。

- **既定のプロパティ。** モジュールでは、既定のプロパティを定義することはできません。 詳細については、「[Default](../modifiers/default.md)」を参照してください。

## <a name="behavior"></a>動作

- **アクセス レベル。** モジュールの内部では、各メンバーを独自のアクセス レベルで宣言できます。 モジュール メンバーは、既定で [Private](../modifiers/private.md) アクセスに設定される変数と定数を除き、既定で [Public](../modifiers/public.md) アクセスに設定されます。 モジュールがそのメンバーのいずれかよりもアクセスが制限されている場合は、指定されたモジュールのアクセス レベルが優先されます。

- **範囲**。 モジュールは、その名前空間全体をスコープとします。

  すべてのモジュール メンバーのスコープは、モジュール全体になります。 すべてのメンバーで*型の上位変換*が行われることに注意してください。これにより、そのスコープがモジュールを含む名前空間に昇格します。 詳細については、「[型の上位変換](../../programming-guide/language-features/declared-elements/type-promotion.md)」を参照してください。

- **修飾。** プロジェクトには複数のモジュールを含めることができ、2 つ以上のモジュールで同じ名前のメンバーを宣言できます。 ただし、このようなメンバーへの参照は、そのモジュールの外部から参照されている場合は、適切なモジュール名で修飾する必要があります。 詳細については、「 [References to Declared Elements](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)」を参照してください。

## <a name="example"></a>例

[!code-vb[VbVbalrStatements#69](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#69)]

## <a name="see-also"></a>関連項目

- [Class ステートメント](class-statement.md)
- [Namespace ステートメント](namespace-statement.md)
- [Structure ステートメント](structure-statement.md)
- [Interface ステートメント](interface-statement.md)
- [Property ステートメント](property-statement.md)
- [型の上位変換](../../programming-guide/language-features/declared-elements/type-promotion.md)
