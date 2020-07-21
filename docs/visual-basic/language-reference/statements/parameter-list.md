---
title: パラメーター リスト
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- parameters [Visual Basic], Visual Basic
- parameters [Visual Basic], lists
- parameter lists [Visual Basic]
- Visual Basic code, parameter lists
- arguments [Visual Basic], Visual Basic
- procedures [Visual Basic], parameter lists
ms.assetid: 5d737319-0c34-4df9-a23d-188fc840becd
ms.openlocfilehash: 706fc2414806db5608cce410bf4156839ec2d83e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404318"
---
# <a name="parameter-list-visual-basic"></a>パラメーターの一覧 (Visual Basic)

プロシージャが呼び出されるときに、プロシージャで期待するパラメーターを指定します。 複数のパラメーターはコンマで区切ります。 次に 1 つのパラメーターの構文を示します。

## <a name="syntax"></a>構文

```vb
[ <attributelist> ] [ Optional ] [{ ByVal | ByRef }] [ ParamArray ]
parametername[( )] [ As parametertype ] [ = defaultvalue ]
```

## <a name="parts"></a>指定項目

`attributelist`  
任意。 このパラメーターに適用される属性の一覧。 [属性リスト](attribute-list.md)は山かっこ ("`<`" および "`>`") で囲む必要があります。

`Optional`  
任意。 プロシージャが呼び出されるときに、このパラメーターが必須でないことを指定します。

`ByVal`  
任意。 プロシージャで、呼び出し元のコード内の対応する引数の基になる変数要素を置換または再代入できないことを指定します。

`ByRef`  
任意。 プロシージャで、呼び出し元のコード自体で可能な同じ方法で、呼び出し元のコード内の基になる変数要素を変更できることを指定します。

`ParamArray`  
任意。 パラメーター リストの最後のパラメーターが、指定したデータ型の要素の省略可能な配列であることを指定します。 これにより、呼び出し元のコードで、プロシージャに任意の数の引数を渡すことができます。

`parametername`  
必須です。 パラメーターを表すローカル変数の名前。

`parametertype`  
`Option Strict` が `On` の場合は必須です。 パラメーターを表すローカル変数のデータ型。

`defaultvalue`  
`Optional` パラメーターに必須です。 パラメーターのデータ型に評価される定数または定数式。 型が `Object`、クラス、インターフェイス、配列、または構造体の場合、既定値は `Nothing` のみ指定できます。

## <a name="remarks"></a>Remarks

パラメーターは、かっこで囲み、コンマで区切ります。 パラメーターは任意のデータ型で宣言できます。 `parametertype` を指定しない場合、既定で `Object` が設定されます。

呼び出し元のコードでプロシージャを呼び出すと、各必須パラメーターに*引数*が渡されます。 詳細については、「[パラメーターと引数の違い](../../programming-guide/language-features/procedures/differences-between-parameters-and-arguments.md)」を参照してください。

呼び出し元のコードから各パラメーターに渡される引数は、呼び出し元のコード内の基になる要素へのポインターです。 この要素が*変数でない* (定数、リテラル、列挙型、または式) 場合、どのコードでもそれを変更することはできません。 それが*変数*要素 (宣言された変数、フィールド、プロパティ、配列要素、または構造体要素) の場合は、呼び出し元のコードでそれを変更できます。 詳細については、「[変更できる引数と変更できない引数の違い](../../programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md)」を参照してください。

変数要素が `ByRef` で渡された場合は、プロシージャでそれを変更できます。 詳細については、「[引数の値渡しと参照渡しの違い](../../programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md)」を参照してください。

## <a name="rules"></a>ルール

- **かっこ。** パラメーター リストを指定する場合は、かっこで囲む必要があります。 パラメーターがない場合でも、空のリストを囲むかっこを使用できます。 これにより、要素がプロシージャであることを明確にすることで、コードの読みやすさが向上します。

- **省略可能なパラメーター。** パラメーターで `Optional` 修飾子を使用する場合、リスト内の後続のすべてのパラメーターも省略可能で、`Optional` 修飾子を使用して宣言されている必要があります。

     省略可能なすべてのパラメーター宣言で、`defaultvalue` 句を指定する必要があります。

     詳細については、「[省略可能なパラメーター](../../programming-guide/language-features/procedures/optional-parameters.md)」を参照してください。

- **パラメーター配列。** `ParamArray` パラメーターには `ByVal` を指定する必要があります。

     同じパラメーター リストで `Optional` と `ParamArray` の両方を使用することはできません。

     詳細については、「[パラメーター配列](../../programming-guide/language-features/procedures/parameter-arrays.md)」を参照してください。

- **引渡し方法。** すべての引数の既定の方法は `ByVal` です。これは、プロシージャで基になる変数要素を変更できないことを意味します。 ただし、要素が参照型の場合、プロシージャで、オブジェクト自体の置換や再代入ができなくても、基になるオブジェクトの内容やメンバーを変更できます。

- **パラメーター名。** パラメーターのデータ型が配列である場合は、`parametername` の直後にかっこで指定します。 パラメーター名の詳細については、「[宣言された要素の名前](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。

## <a name="example"></a>例

次の例では、2 つのパラメーターを定義する `Function` プロシージャを示しています。

[!code-vb[VbVbalrStatements#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#2)]

## <a name="see-also"></a>関連項目

- <xref:System.Runtime.InteropServices.DllImportAttribute>
- [Function ステートメント](function-statement.md)
- [Sub ステートメント](sub-statement.md)
- [Declare ステートメント](declare-statement.md)
- [Structure ステートメント](structure-statement.md)
- [Option Strict ステートメント](option-strict-statement.md)
- [属性の概要](../../programming-guide/concepts/attributes/index.md)
- [方法: コード内でステートメントを分割および連結する](../../programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
