---
title: Class ステートメント
ms.date: 05/12/2018
f1_keywords:
- vb.Class
helpviewer_keywords:
- class modules
- Class statement [Visual Basic]
- classes [Visual Basic], fields
- fields [Visual Basic], of classes
- class types [Visual Basic], class statements
- classes [Visual Basic], creating
- classes [Visual Basic], data members
- data members [Visual Basic], of classes
ms.assetid: f2664f38-eb5a-4d4b-a374-1d041521fb6c
ms.openlocfilehash: bdb73772dfe0e6d49d89a4ef006b1bceac14c8ee
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397156"
---
# <a name="class-statement-visual-basic"></a>Class ステートメント (Visual Basic)
クラスの名前を宣言し、クラスを構成する変数、プロパティ、イベント、およびプロシージャの定義を示します。  
  
## <a name="syntax"></a>構文  
  
```vb  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ MustInherit | NotInheritable ] [ Partial ] _  
Class name [ ( Of typelist ) ]  
    [ Inherits classname ]  
    [ Implements interfacenames ]  
    [ statements ]  
End Class  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`attributelist`|任意。 「[属性リスト](attribute-list.md)」を参照してください。|  
|`accessmodifier`|任意。 次のいずれかの値を指定します。<br /><br /> -   [Public](../modifiers/public.md)<br />-   [Protected](../modifiers/protected.md)<br />-   [Friend](../modifiers/friend.md)<br />-   [Private](../modifiers/private.md)<br />-   [Protected Friend](../modifiers/protected-friend.md)<br />- [Private Protected](../modifiers/private-protected.md)<br/><br/> 「 [Access levels in Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。|  
|`Shadows`|任意。 「[Shadows](../modifiers/shadows.md)」を参照してください。|  
|`MustInherit`|任意。 「[MustInherit](../modifiers/mustinherit.md)」を参照してください。|  
|`NotInheritable`|任意。 「[NotInheritable](../modifiers/notinheritable.md)」を参照してください。|  
|`Partial`|任意。 クラスの部分定義を示します。 「[Partial](../modifiers/partial.md)」を参照してください。|  
|`name`|必須です。 このクラスの名前です。 「 [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。|  
|`Of`|任意。 これがジェネリック クラスであることを指定します。|  
|`typelist`|[Of](of-clause.md) キーワードを使用する場合は必須です。 このクラスの型パラメーター リストを指定します。 「[型リスト](type-list.md)」を参照してください。|  
|`Inherits`|任意。 このクラスが別のクラスのメンバーを継承することを示します。 「[Inherits ステートメント](inherits-statement.md)」を参照してください。|  
|`classname`|`Inherits` ステートメントを使用する場合は必ず指定します。 このクラスの派生元のクラスの名前です。|  
|`Implements`|任意。 このクラスが 1 つ以上のインターフェイスのメンバーを実装していることを示します。 「[Implements ステートメント](implements-statement.md)」を参照してください。|  
|`interfacenames`|`Implements` ステートメントを使用する場合は必ず指定します。 このクラスが実装するインターフェイスの名前です。|  
|`statements`|任意。 このクラスのメンバーを定義するステートメントです。|  
|`End Class`|必須です。 `Class` の定義を終了します。|  
  
## <a name="remarks"></a>Remarks  
 `Class` ステートメントは新しいデータ型を定義します。 *クラス*は、オブジェクト指向プログラミング (OOP) の基本的な構成要素です。 詳細については、[オブジェクトとクラス](../../programming-guide/language-features/objects-and-classes/index.md)に関するページを参照してください。  
  
 `Class` は、名前空間またはモジュール レベルでのみ使用できます。 つまり、クラスの*宣言コンテキスト*は、ソース ファイル、名前空間、クラス、構造体、モジュール、またはインターフェイスのいずれかである必要があり、プロシージャまたはブロックでは宣言できません。 詳細については、「[宣言コンテキストと既定のアクセス レベル](declaration-contexts-and-default-access-levels.md)」を参照してください。  
  
 クラスの各インスタンスには、他のインスタンスに依存しない独自の有効期間があります。 この有効期間は、[New Operator](../operators/new-operator.md) 句によって、または <xref:Microsoft.VisualBasic.Interaction.CreateObject%2A> などの関数によって作成された時点で開始されます。 これは、インスタンスを指すすべての変数が、[Nothing](../nothing.md)、または他のクラスのインスタンスに設定された時点で終了します。  
  
 クラスは、既定で [Friend](../modifiers/friend.md) アクセスに設定されます。 アクセス修飾子を使用してこれらのアクセス レベルを調整できます。 詳しくは、「[Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。  
  
## <a name="rules"></a>ルール  
  
- **入れ子。** クラスの内部に別のクラスを定義できます。 外側のクラスは、*含まれているクラス*と呼ばれ、内側のクラスは*入れ子になったクラス*と呼ばれます。  
  
- **継承。** クラスが [Inherits ステートメント](inherits-statement.md)を使用する場合、指定できる基底クラスまたはインターフェイスは 1 つだけです。 クラスは複数の要素からは継承できません。  
  
     クラスは、より制限の厳しいアクセス レベルを持つ別のクラスから継承することはできません。 たとえば、`Public` クラスは `Friend` クラスから継承できません。  
  
     クラスは、その中の入れ子にされたクラスから継承できません。  
  
- **実装。** クラスで [Implements ステートメント](implements-statement.md)を使用する場合、`interfacenames` に指定するすべてのインターフェイスによって定義されたすべてのメンバーを実装する必要があります。 この例外は、基底クラスのメンバーの再実装です。 詳細については、[Implements](implements-clause.md) に関するページの「再実装」を参照してください。  
  
- **既定のプロパティ。** クラスは、その*既定のプロパティ*として、最大で 1 つのプロパティを指定できます。 詳細については、「[Default](../modifiers/default.md)」を参照してください。  
  
## <a name="behavior"></a>動作  
  
- **アクセス レベル。** クラスの内部では、各メンバーを独自のアクセス レベルで宣言できます。 クラス メンバーは、既定で [Private](../modifiers/private.md) アクセスに設定される変数と定数を除き、既定で [Public](../modifiers/public.md) アクセスに設定されます。 クラスがそのメンバーのいずれかよりもアクセスが制限されている場合は、クラスのアクセス レベルが優先されます。  
  
- **範囲**。 クラスは、そこに含まれる名前空間、クラス、構造体、またはモジュールをスコープとします。  
  
     すべてのクラス メンバーのスコープは、クラス全体になります。  
  
     **有効期間。** Visual Basic では、静的クラスをサポートしていません。 静的クラスに相当する機能は、モジュールによって提供されます。 詳細については、「[Module ステートメント](module-statement.md)」を参照してください。  
  
     クラス メンバーの有効期間は、それを宣言する方法と場所で決まります。 詳しくは、「[Visual Basic における有効期間](../../programming-guide/language-features/declared-elements/lifetime.md)」をご覧ください。  
  
- **修飾。** クラスの外側にあるコードでは、メンバーの名前をそのクラスの名前で修飾する必要があります。  
  
     入れ子になったクラスの内側のコードでプログラミング要素を修飾なしで参照した場合、Visual Basic はその要素をまず入れ子になったクラスの内側で探し、その次に含まれているクラスの内側で探します。この手順が、最も外側のコンテナー要素にまで繰り返されます。  
  
## <a name="classes-and-modules"></a>クラスとモジュール  
 これらの要素には多くの類似点がありますが、重要な相違点もいくつかあります。  
  
- **用語。** 以前のバージョンの Visual Basic は、*クラス モジュール* (.cls ファイル) と*標準モジュール* (.bas ファイル) の 2 種類のモジュールを認識します。 現在のバージョンでは、これらの*クラス*と*モジュール*をそれぞれ呼び出します。  
  
- **共有メンバー。** クラスのメンバーが共有メンバーかインスタンス メンバーかを制御できます。  
  
- **オブジェクト指向。** クラスはオブジェクト指向ですが、モジュールはそうではありません。 クラスの 1 つ以上のインスタンスを作成できます。 詳細については、[オブジェクトとクラス](../../programming-guide/language-features/objects-and-classes/index.md)に関するページを参照してください。  
  
## <a name="example"></a>例  
 次の例では、`Class` ステートメントを使用して 1 つのクラスといくつかのメンバーを定義します。  
  
 [!code-vb[VbVbalrStatements#62](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#62)]  
  
## <a name="see-also"></a>関連項目

- [クラスとオブジェクト](../../programming-guide/language-features/objects-and-classes/index.md)
- [構造体とクラス](../../programming-guide/language-features/data-types/structures-and-classes.md)
- [Interface ステートメント](interface-statement.md)
- [Module ステートメント](module-statement.md)
- [Property ステートメント](property-statement.md)
- [オブジェクトの有効期間: オブジェクトの作成と破棄](../../programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)
- [Generic Types in Visual Basic](../../programming-guide/language-features/data-types/generic-types.md)
- [方法: ジェネリック クラスを使用する](../../programming-guide/language-features/data-types/how-to-use-a-generic-class.md)
