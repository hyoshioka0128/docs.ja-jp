---
title: Declare ステートメント (Visual Basic)
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
ms.openlocfilehash: 186238d8e823f028caaed2e2618d882d21e1358f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54548951"
---
# <a name="declare-statement"></a>Declare Statement
外部のファイルに実装されているプロシージャへの参照を宣言します。  
  
## <a name="syntax"></a>構文  
  
```  
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
|`attributelist`|任意。 参照してください[属性一覧](../../../visual-basic/language-reference/statements/attribute-list.md)します。|  
|`accessmodifier`|任意。 次のいずれかの値を指定します。<br /><br /> -   [パブリック](../../../visual-basic/language-reference/modifiers/public.md)<br />-   [保護されています。](../../../visual-basic/language-reference/modifiers/protected.md)<br />-   [friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [Private](../../../visual-basic/language-reference/modifiers/private.md)<br />- [保護されたフレンド](../../language-reference/modifiers/protected-friend.md)<br />- [Private Protected](../../language-reference/modifiers/private-protected.md)<br /><br /> 「 [Access levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。|  
|`Shadows`|任意。 参照してください[Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)します。|  
|`charsetmodifier`|任意。 文字セットとファイルを指定の情報を検索します。 次のいずれかの値を指定します。<br /><br /> -   [Ansi](../../../visual-basic/language-reference/modifiers/ansi.md) (既定値)<br />-   [Unicode](../../../visual-basic/language-reference/modifiers/unicode.md)<br />-   [自動](../../../visual-basic/language-reference/modifiers/auto.md)|  
|`Sub`|省略可能、ただしか`Sub`または`Function`表示する必要があります。 外部プロシージャが値を返さないことを示します。|  
|`Function`|省略可能、ただしか`Sub`または`Function`表示する必要があります。 外部プロシージャが値を返すことを示します。|  
|`name`|必須。 この外部参照の名前です。 詳細については、次を参照してください。 [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)します。|  
|`Lib`|必須。 紹介を`Lib`句は、外部プロシージャを含む外部ファイル (DLL またはコード リソース) を識別します。|  
|`libname`|必須。 宣言されたプロシージャを含むファイルの名前。|  
|`Alias`|任意。 指定された名前でファイルの内部で宣言されているプロシージャを識別できないことを示します`name`します。 その id を指定する`aliasname`します。|  
|`aliasname`|使用するかどうかは必ず、`Alias`キーワード。 2 つの方法のいずれかでプロシージャを識別する文字列。<br /><br /> 引用符で囲んで、ファイルの内部でプロシージャのエントリ ポイント名 (`""`)<br /><br /> - または -<br /><br /> シャープ記号 (`#`) 後にファイルの内部でプロシージャのエントリ ポイントの序数を指定する整数|  
|`parameterlist`|かどうか、プロシージャがパラメーターが必要です。 参照してください[パラメーター リスト](../../../visual-basic/language-reference/statements/parameter-list.md)します。|  
|`returntype`|必要な場合`Function`が指定されて、`Option Strict`は`On`します。 プロシージャによって返される値のデータ型。|  
  
## <a name="remarks"></a>Remarks  
 場合があります (DLL またはコード リソース) などのファイルをプロジェクト外で定義されているプロシージャを呼び出す必要があります。 これを行うときに、Visual Basic コンパイラには、プロシージャがある場所は、識別方法、その呼び出し元のシーケンスと戻り値の型およびを使用して、文字列の文字セットなど、正しくプロシージャを呼び出すために必要な情報へのアクセスはありません。 `Declare`ステートメントが外部プロシージャへの参照を作成し、このために必要な情報を提供します。  
  
 `Declare` は、モジュール レベルでのみ使用できます。 つまり、*宣言コンテキスト*外部参照は、クラス、構造体、またはモジュールである必要があり、ソース ファイル、名前空間、インターフェイス、プロシージャ、またはブロックすることはできません。 詳細については、「[宣言コンテキストと既定のアクセス レベル](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)」を参照してください。  
  
 外部参照の既定値は[パブリック](../../../visual-basic/language-reference/modifiers/public.md)アクセスします。 アクセス修飾子を使用してこれらのアクセス レベルを調整できます。  
  
## <a name="rules"></a>ルール  
  
-   **属性。** 外部参照に属性を適用することができます。 プロジェクトでのみ、外部のファイルではなくを適用するすべての属性を持ちません。  
  
-   **修飾子。** 外部プロシージャは暗黙的に[Shared](../../../visual-basic/language-reference/modifiers/shared.md)します。 使用することはできません、`Shared`キーワードと、その共有状態を変更して、外部参照を宣言することはできません。  
  
     外部プロシージャでは、オーバーライドに参加したり、インターフェイス メンバーを実装、またはイベントを処理できません。 したがって、使用することはできません、 `Overrides`、 `Overridable`、 `NotOverridable`、 `MustOverride`、 `Implements`、または`Handles`キーワード、`Declare`ステートメント。  
  
-   **外部プロシージャの名前。** この外部参照に同じ名前を指定する必要はありません (で`name`) 外部ファイルの内部でプロシージャのエントリ ポイント名として (`aliasname`)。 使用することができます、`Alias`エントリ ポイント名を指定する句。 これは、外部プロシージャが同じスコープ内で予約済みの Visual Basic の修飾子または変数、プロシージャ、またはその他のプログラミング要素と同じ名前を持つ場合に役立ちます。 ことができます。  
  
    > [!NOTE]
    >  ほとんどの Dll のエントリ ポイント名は大文字小文字を区別します。  
  
-   **外部プロシージャの数。** また、使用することができます、`Alias`句を外部ファイルのエクスポート テーブル内のエントリ ポイントの序数を指定します。 開始するには、`aliasname`に番号記号 (`#`)。 Visual basic では、外部プロシージャ名の任意の文字は許可されていない場合、または外部のファイル名を指定せず、プロシージャをエクスポートする場合は便利にできます。  
  
## <a name="data-type-rules"></a>データ型のルール  
  
-   **パラメーターのデータ型。** 場合`Option Strict`は`On`、内の各パラメーターのデータ型を指定する必要があります`parameterlist`します。 これには、任意のデータ型または列挙型、構造体、クラス、インターフェイスの名前を指定できます。 内で`parameterlist`を使用する、`As`句の各パラメーターに渡される引数のデータ型を指定します。  
  
    > [!NOTE]
    >  外部プロシージャが .NET Framework の書き込まれないため場合、必要があります注意するデータ型の対応します。 Visual Basic 6.0 プロシージャへの外部参照を宣言する場合など、`Integer`パラメーター (Visual Basic 6.0 では 16 ビット) として、対応する引数を識別する必要があります`Short`で、`Declare`ステートメントでは、16 ビットであるためですVisual Basic では、整数型をビットです。 同様に、`Long`別のデータ幅が、Visual Basic 6.0、および`Date`の実装は異なります。  
  
-   **データ型を返します。** 外部プロシージャがある場合、`Function`と`Option Strict`は`On`、呼び出し元のコードに返される値のデータ型を指定する必要があります。 これには、任意のデータ型または列挙型、構造体、クラス、インターフェイスの名前を指定できます。  
  
    > [!NOTE]
    >  Visual Basic コンパイラでは、ユーザーのデータ型が外部プロシージャのものと互換性があるは検証しません。 不一致がある場合、共通言語ランタイムを生成、<xref:System.Runtime.InteropServices.MarshalDirectiveException>実行時に例外。  
  
-   **既定のデータ型。** 場合`Option Strict`は`Off`内のパラメーターのデータ型を指定しないと`parameterlist`、Visual Basic コンパイラに対応する引数の変換、 [Object Data Type](../../../visual-basic/language-reference/data-types/object-data-type.md)。 同様に、指定しない場合`returntype`、コンパイラは、戻り値のデータ型を受け取る`Object`します。  
  
    > [!NOTE]
    >  別のプラットフォームで書き込まれた外部プロシージャを扱うため、これについてのデータ型を推測したりすると、既定値には危険です。 存在する場合は安全にすべてのパラメーターと戻り値のデータ型を指定します。 これは、コードの読みやすさも向上します。  
  
## <a name="behavior"></a>動作  
  
-   **スコープ。** 外部参照では、そのクラス、構造体、またはモジュール全体にわたってスコープ内で。  
  
-   **有効期間。** 外部参照では、クラス、構造体、またはそれが宣言されているモジュールと同じ有効期間があります。  
  
-   **外部プロシージャの呼び出し。** 呼び出すのと同じ方法で外部プロシージャを呼び出す、`Function`または`Sub`プロシージャ: またはを指定することで、値を返す場合、式の中で使用することによって、 [Call ステートメント](../../../visual-basic/language-reference/statements/call-statement.md)値を返さない場合。  
  
     指定されているとおり、外部プロシージャに引数を渡す`parameterlist`で、`Declare`ステートメント。 考慮されない方法パラメーターは、外部のファイルで宣言されていた。 同様に、戻り値がある場合を使用して、これによって指定されているとおり`returntype`で、`Declare`ステートメント。  
  
-   **文字を設定します。** 指定できる`charsetmodifier`方法 Visual Basic は文字列をマーシャ リングしている外部プロシージャを呼び出すときにします。 `Ansi`修飾子に指示を ANSI 値のすべての文字列をマーシャ リングする Visual Basic、および`Unicode`を Unicode 値にすべての文字列をマーシャ リングすることです。 `Auto`修飾子は、Visual Basic .NET フレームワークに従って文字列をマーシャ リングにルールが外部参照に基づくように指示`name`、または`aliasname`指定されている場合。 既定値は `Ansi` です。  
  
     `charsetmodifier` また、外部ファイル内で外部プロシージャが Visual Basic を検索する方法を指定します。 `Ansi` `Unicode`両方を検索中にその名前を変更することがなく調べる Visual Basic に指示します。 `Auto` Visual Basic ランタイム プラットフォームの基本文字セットを決定し、次のように、外部プロシージャ名を変更するように指示します。  
  
    -   Windows 95、Windows 98、または Windows Millennium Edition などの ANSI プラットフォームでは、名前変更していない場合、外部の手順をまず検索します。 失敗した場合は、外部プロシージャ名の末尾に"A"を追加し、もう一度検索します。  
  
    -   Windows NT、Windows 2000、Windows XP などの Unicode プラットフォームでは、名前変更していない場合、外部の手順をまず検索します。 失敗した場合、追加している外部プロシージャの末尾に"W"名前を指定し、もう一度検索します。  
  
-   **メカニズムです。** Visual Basic、.NET Framework を使用して*プラットフォーム呼び出し*(PInvoke) メカニズムを解決し、外部プロシージャにアクセスします。 `Declare`ステートメントと<xref:System.Runtime.InteropServices.DllImportAttribute>両方のクラスが自動的に、このメカニズムを使用して、PInvoke を認識する必要はありません。 詳細については、「[チュートリアル:Windows Api を呼び出す](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)します。  
  
> [!IMPORTANT]
>  共通言語ランタイム (CLR) の外部で実行している外部プロシージャ、ある*アンマネージ コード*します。 このようなプロシージャ、Win32 API 関数または COM メソッドの場合は、たとえばを呼び出すときに、セキュリティ リスクにアプリケーションを公開する可能性があります。 詳細については、次を参照してください。[アンマネージ コードのコーディング ガイドラインをセキュリティで保護された](../../../framework/security/secure-coding-guidelines-for-unmanaged-code.md)します。  
  
## <a name="example"></a>例  
 次の例への外部参照の宣言を`Function`を現在のユーザー名を返すプロシージャです。 外部プロシージャを呼び出して`GetUserNameA`の一部として、`getUser`プロシージャ。  
  
 [!code-vb[VbVbalrStatements#15](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/declare-statement_1.vb)]  
  
## <a name="example"></a>例  
 <xref:System.Runtime.InteropServices.DllImportAttribute>アンマネージ コードで関数を使用する別の方法を提供します。 次の例では、インポートした関数を宣言を使用せず、`Declare`ステートメント。  
  
 [!code-vb[VbVbalrStatements#16](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/declare-statement_2.vb)]  
  
 [!code-vb[VbVbalrStatements#1](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/declare-statement_3.vb)]  
  
## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualBasic.ErrObject.LastDllError%2A>
- [Imports ステートメント (.NET 名前空間および型)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
- [AddressOf 演算子](../../../visual-basic/language-reference/operators/addressof-operator.md)
- [Function ステートメント](../../../visual-basic/language-reference/statements/function-statement.md)
- [Sub ステートメント](../../../visual-basic/language-reference/statements/sub-statement.md)
- [パラメーター リスト](../../../visual-basic/language-reference/statements/parameter-list.md)
- [Call ステートメント](../../../visual-basic/language-reference/statements/call-statement.md)
- [チュートリアル: Windows API の呼び出し](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)
