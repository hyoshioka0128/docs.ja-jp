---
title: Declare Statement
ms.date: 07/20/2015
f1_keywords:
- vb.Declare
- vb.Lib
- vb.Any
helpviewer_keywords:
- Lib keyword [Visual Basic]
- declaring procedures [Visual Basic], Declare statement
- functions [Visual Basic], function procedures
- declarations [Visual Basic], procedures
- procedures [Visual Basic], declaration
- procedures [Visual Basic], external
- Alias keyword [Visual Basic]
- external references [Visual Basic], Visual Basic
- DLLs, declaring procedures
- Declare statement [Visual Basic]
- declarations [Visual Basic], external
- Visual Basic code, Function procedures
- As keyword [Visual Basic], in Declare statement
- resources [Visual Basic], declaring
- Public keyword [Visual Basic], Declare statement
- platform invoke, Visual Basic external references
- Sub procedures [Visual Basic], declarations
- APIs, declaring API functions
- Visual Basic code, Sub procedures
- Function procedures [Visual Basic], declaring
ms.assetid: d3f21fb0-b804-4c99-97ed-583b23894cf1
ms.openlocfilehash: 021805508a8a053ccc8fab6f1013109bece4b6f2
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404772"
---
# <a name="declare-statement"></a>Declare Statement

外部ファイルに実装されているプロシージャへの参照を宣言します。

## <a name="syntax"></a>構文

```vb
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ Overloads ] _
Declare [ charsetmodifier ] [ Sub ] name Lib "libname" _
[ Alias "aliasname" ] [ ([ parameterlist ]) ]
' -or-
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ Overloads ] _
Declare [ charsetmodifier ] [ Function ] name Lib "libname" _
[ Alias "aliasname" ] [ ([ parameterlist ]) ] [ As returntype ]
```

## <a name="parts"></a>指定項目

|用語|定義|
|---|---|
|`attributelist`|任意。 「[属性リスト](attribute-list.md)」を参照してください。|
|`accessmodifier`|任意。 次のいずれかの値を指定します。<br /><br /> -   [Public](../modifiers/public.md)<br />-   [Protected](../modifiers/protected.md)<br />-   [Friend](../modifiers/friend.md)<br />-   [Private](../modifiers/private.md)<br />- [Protected Friend](../modifiers/protected-friend.md)<br />- [Private Protected](../modifiers/private-protected.md)<br /><br /> 「 [Access levels in Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。|
|`Shadows`|任意。 「[Shadows](../modifiers/shadows.md)」を参照してください。|
|`charsetmodifier`|任意。 文字セットとファイル検索情報を指定します。 次のいずれかの値を指定します。<br /><br /> -   [Ansi](../modifiers/ansi.md) (既定値)<br />-   [Unicode](../modifiers/unicode.md)<br />-   [Auto](../modifiers/auto.md)|
|`Sub`|省略可能ですが、`Sub` または `Function` のいずれかを指定する必要があります。 外部プロシージャが値を返さないことを示します。|
|`Function`|省略可能ですが、`Sub` または `Function` のいずれかを指定する必要があります。 外部プロシージャが値を返すことを示します。|
|`name`|必須です。 この外部参照の名前。 詳細については、「[宣言された要素の名前](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。|
|`Lib`|必須です。 外部プロシージャを含む外部ファイル (DLL またはコード リソース) を識別する `Lib` 句を指定します。|
|`libname`|必須です。 宣言されるプロシージャが含まれているファイルの名前。|
|`Alias`|任意。 宣言されるプロシージャが、`name` に指定された名前によってファイル内で識別されないことを示します。 識別は `aliasname` で指定します。|
|`aliasname`|`Alias` キーワードを使用する場合は必須です。 次の 2 つの方法のいずれかでプロシージャを識別する文字列。<br /><br /> ファイル内のプロシージャのエントリ ポイント名 (引用符 (`""`) で囲む)<br /><br /> \- または -<br /><br /> 番号記号 (`#`) とそれに続く、ファイル内のプロシージャのエントリ ポイントの序数を指定する整数|
|`parameterlist`|プロシージャがパラメーターを受け取る場合は必須です。 「[パラメーターの一覧](parameter-list.md)」を参照してください。|
|`returntype`|`Function` が指定され、`Option Strict` が `On` の場合は必須です。 プロシージャによって返される値のデータ型。|

## <a name="remarks"></a>Remarks

プロジェクトの外部のファイル (DLL やコード リソースなど) で定義されたプロシージャを呼び出す必要がある場合があります。 これを行う場合、Visual Basic のコンパイラはプロシージャを正しく呼び出すために必要な情報 (プロシージャがある場所、その識別方法、呼び出しシーケンスと戻り値の型、使用する文字列の文字セットなど) にアクセスできません。 `Declare` ステートメントは、外部プロシージャへの参照を作成し、この必要な情報を提供します。

`Declare` は、モジュール レベルでのみ使用できます。 つまり、外部参照の*宣言コンテキスト*は、クラス、構造体、またはモジュールである必要があり、ソース ファイル、名前空間、インターフェイス、プロシージャ、またはブロックにすることはできません。 詳細については、「[宣言コンテキストと既定のアクセス レベル](declaration-contexts-and-default-access-levels.md)」を参照してください。

外部参照のアクセスは、既定で [Public](../modifiers/public.md) になります。 アクセス修飾子を使用してこれらのアクセス レベルを調整できます。

## <a name="rules"></a>ルール

- **属性。** 外部参照には属性を適用できます。 適用した属性は、プロジェクト内でのみ有効になり、外部ファイルには反映されません。

- **修飾子。** 外部プロシージャは、暗黙的に [Shared](../modifiers/shared.md) になります。 外部参照の宣言時に `Shared` キーワードを使用することはできません。また、共有ステータスを変更することもできません。

  外部プロシージャは、オーバーライド、インターフェイス メンバーの実装、またはイベントの処理に関与することはできません。 したがって、`Declare` ステートメントに `Overrides`、`Overridable`、`NotOverridable`、`MustOverride`、`Implements`、`Handles` キーワードを使用することはできません。

- **外部プロシージャ名。** 外部ファイル内のプロシージャのエントリ ポイント名 (`aliasname`) と同じ名前をこの外部参照 (`name`) に付ける必要はありません。 `Alias` 句を使用して、エントリ ポイント名を指定できます。 これは、外部プロシージャの名前が Visual Basic の予約済みの修飾子や変数、プロシージャ、または同じスコープ内のその他のプログラミング要素と同じである場合に便利です。

  > [!NOTE]
  > ほとんどの DLL のエントリ ポイント名では、大文字と小文字が区別されます。

- **外部プロシージャ番号。** または、`Alias` 句を使用して、外部ファイルのエクスポート テーブル内のエントリ ポイントの序数を指定することもできます。 これを行うには、`aliasname` を番号記号 (`#`) で開始します。 これは、Visual Basic で外部プロシージャ名に使用できない文字がある場合や、外部ファイルによってプロシージャが名前なしでエクスポートされた場合に便利です。

## <a name="data-type-rules"></a>データ型ルール

- **パラメーターのデータ型。** `Option Strict` が `On` の場合は、`parameterlist` に各パラメーターのデータ型を指定する必要があります。 任意のデータ型や、列挙、構造体、クラス、またはインターフェイスの名前を指定できます。 `parameterlist` 内で `As` 句を使用して、各パラメーターに渡される引数のデータ型を指定します。

  > [!NOTE]
  > 外部プロシージャが .NET Framework 用に記述されていない場合は、データ型が対応するようにする必要があります。 たとえば、`Integer` のパラメーター (Visual Basic 6.0 では 16 ビット) を持つ Visual Basic 6.0 のプロシージャへの外部参照を宣言する場合は、対応する引数を `Declare` ステートメントで `Short` として指定する必要があります。これが Visual Basic の 16 ビット整数型であるためです。 同様に、Visual Basic 6.0 では `Long` のデータ長が異なり、`Date` の実装方法も異なります。

- **戻り値のデータ型。** 外部プロシージャが `Function` で `Option Strict` が `On` の場合は、呼び出し元のコードに返される値のデータ型を指定する必要があります。 任意のデータ型や、列挙、構造体、クラス、またはインターフェイスの名前を指定できます。

  > [!NOTE]
  > Visual Basic のコンパイラでは、データ型が外部プロシージャのデータ型と互換性があるかどうかは検証されません。 不一致がある場合は、実行時に共通言語ランタイムによって <xref:System.Runtime.InteropServices.MarshalDirectiveException> 例外が生成されます。

- **既定のデータ型。** `Option Strict` が `Off` で、`parameterlist` にパラメーターのデータ型が指定されていない場合、Visual Basic コンパイラは、対応する引数を [Object データ型](../data-types/object-data-type.md)に変換します。 同様に、`returntype` が指定されていない場合、コンパイラは戻り値のデータ型を `Object` にします。

  > [!NOTE]
  > 別のプラットフォームで記述された可能性がある外部プロシージャを使用しようとしているため、データ型を想定したり、既定値を使用したりすることは危険です。 すべてのパラメーターのデータ型と戻り値 (存在する場合) を指定する方が、はるかに安全です。 これにより、コードも読みやすくなります。

## <a name="behavior"></a>動作

- **範囲**。 外部参照は、そのクラス、構造体、またはモジュール全体をスコープとします。

- **有効期間。** 外部参照の有効期間は、宣言されているクラス、構造体、またはモジュールと同じです。

- **外部プロシージャの呼び出し。** 外部プロシージャは、`Function` または `Sub` プロシージャを呼び出す場合と同じ方法で呼び出すことができます。値を返す場合は式で使用し、値を返さない場合は [Call ステートメント](call-statement.md)に指定します。

  引数は、`Declare` ステートメントの `parameterlist` に指定したとおりに、外部プロシージャに渡されます。 外部ファイル内でパラメーターが元々どのように宣言されたかは考慮されません。 同様に、戻り値がある場合は、`Declare` ステートメントの `returntype` に指定されたとおりに使用されます。

- **文字セット。** 外部プロシージャを呼び出すときに Visual Basic が文字列をマーシャリングする方法は `charsetmodifier` に指定できます。 `Ansi` 修飾子は、すべての文字列を ANSI 値にマーシャリングするように Visual Basic に指示し、`Unicode` 修飾子は、すべての文字列を Unicode 値にマーシャリングするように指示します。 `Auto` 修飾子は、外部参照の `name` (または、指定されている場合は `aliasname`) に基づいて .NET Framework の規則に従って文字列をマーシャリングするように Visual Basic に指示します。 既定値は `Ansi` です。

  `charsetmodifier` は外部ファイル内で Visual Basic が外部プロシージャを検索する方法も指定します。 `Ansi` と `Unicode` は、検索時に名前を変更せずに検索するように Visual Basic に指示し ます。 `Auto` は、実行時プラットフォームの基本文字セットを判別するように Visual Basic に指示します。また、場合によっては、次のように外部プロシージャ名を変更します。

  - Windows 95、Windows 98、または Windows Millennium Edition などの ANSI プラットフォームでは、最初に名前を変更せずに外部プロシージャを検索します。 失敗した場合は、外部プロシージャ名の末尾に "A" を付加して、もう一度検索します。

  - Windows NT、Windows 2000、Windows XP などの Unicode プラットフォームでは、最初に名前を変更せずに外部プロシージャを検索します。 失敗した場合は、外部プロシージャ名の末尾に "W" を付加して、もう一度検索します。

- **メカニズム。** Visual Basic は、.NET Framework の*プラットフォーム呼び出し* (PInvoke) メカニズムを使用して、外部プロシージャを解決し、アクセスします。 `Declare` ステートメントと <xref:System.Runtime.InteropServices.DllImportAttribute> クラスでは、このメカニズムが自動的に使用されため、PInvoke に関する知識は必要ありません。 詳細については、「[チュートリアル:Windows API の呼び出し](../../programming-guide/com-interop/walkthrough-calling-windows-apis.md)」を参照してください。

> [!IMPORTANT]
> 外部プロシージャが共通言語ランタイム (CLR) の外部で実行されている場合は、*アンマネージド コード*となります。 このようなプロシージャ (Windows API 関数や COM メソッドなど) を呼び出すと、アプリケーションがセキュリティ上のリスクにさらされる可能性があります。 詳細については、[アンマネージド コードの安全なコーディングのガイドライン](https://docs.microsoft.com/previous-versions/dotnet/framework/security/secure-coding-guidelines-for-unmanaged-code)に関するページを参照してください。

## <a name="example"></a>例

次の例では、現在のユーザー名を返す `Function` プロシージャへの外部参照を宣言しています。 その後、`getUser` プロシージャの一部として、外部プロシージャ `GetUserNameA` を呼び出します。

[!code-vb[VbVbalrStatements#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#15)]

## <a name="example"></a>例

<xref:System.Runtime.InteropServices.DllImportAttribute> には、アンマネージド コードで関数を使用するための別の方法が用意されています。 次の例では、`Declare` ステートメントを使用せずに、インポートされる関数を宣言しています。

[!code-vb[VbVbalrStatements#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#16)]

[!code-vb[VbVbalrStatements#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#1)]

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.ErrObject.LastDllError%2A>
- [Imports ステートメント (.NET 名前空間および型)](imports-statement-net-namespace-and-type.md)
- [AddressOf 演算子](../operators/addressof-operator.md)
- [Function ステートメント](function-statement.md)
- [Sub ステートメント](sub-statement.md)
- [パラメーター リスト](parameter-list.md)
- [Call ステートメント](call-statement.md)
- [チュートリアル: Windows API の呼び出し](../../programming-guide/com-interop/walkthrough-calling-windows-apis.md)
