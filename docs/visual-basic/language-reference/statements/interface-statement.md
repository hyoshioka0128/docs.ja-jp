---
title: Interface ステートメント
ms.date: 05/12/2018
f1_keywords:
- vb.Interface
helpviewer_keywords:
- interface statement [Visual Basic]
- interfaces [Visual Basic], interface definition
ms.assetid: 8997af73-bda3-4f79-bd41-ca396b610260
ms.openlocfilehash: 02d258084aaaa53dcc559cfaa0dec27556351037
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404487"
---
# <a name="interface-statement-visual-basic"></a>Interface ステートメント (Visual Basic)
インターフェイスの名前を宣言し、インターフェイスを構成しているメンバーの定義を取り込みます。  
  
## <a name="syntax"></a>構文  
  
```vb  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] _  
Interface name [ ( Of typelist ) ]  
    [ Inherits interfacenames ]  
    [ [ modifiers ] Property membername ]  
    [ [ modifiers ] Function membername ]  
    [ [ modifiers ] Sub membername ]  
    [ [ modifiers ] Event membername ]  
    [ [ modifiers ] Interface membername ]  
    [ [ modifiers ] Class membername ]  
    [ [ modifiers ] Structure membername ]  
End Interface  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`attributelist`|任意。 「[属性リスト](attribute-list.md)」を参照してください。|  
|`accessmodifier`|任意。 次のいずれかの値を指定します。<br /><br /> -   [Public](../modifiers/public.md)<br />-   [Protected](../modifiers/protected.md)<br />-   [Friend](../modifiers/friend.md)<br />-   [Private](../modifiers/private.md)<br />-  [Protected Friend](../modifiers/protected-friend.md)<br/>- [Private Protected](../modifiers/private-protected.md)<br /><br /> 「 [Access levels in Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。|  
|`Shadows`|任意。 「[Shadows](../modifiers/shadows.md)」を参照してください。|  
|`name`|必須です。 このインターフェイスの名前。 「 [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。|  
|`Of`|任意。 これがジェネリック インターフェイスであることを指定します。|  
|`typelist`|[Of](of-clause.md) キーワードを使用する場合は必須です。 このインターフェイスの型パラメーターの一覧。 必要に応じて、`In` および `Out` ジェネリック修飾子を使用して、各型パラメーターをバリアントとして宣言できます。 「[型リスト](type-list.md)」を参照してください。|  
|`Inherits`|任意。 このインターフェイスは、別のインターフェイス (複数のインターフェイスも含む) の属性とメンバーを継承することを示します。 「[Inherits ステートメント](inherits-statement.md)」を参照してください。|  
|`interfacenames`|`Inherits` ステートメントを使用する場合は必ず指定します。 このインターフェイスの派生元のインターフェイスの名前。|  
|`modifiers`|任意。 定義されているインターフェイス メンバーの適切な修飾子。|  
|`Property`|任意。 インターフェイスのメンバーであるプロパティを定義します。|  
|`Function`|任意。 インターフェイスのメンバーである `Function` プロシージャを定義します。|  
|`Sub`|任意。 インターフェイスのメンバーである `Sub` プロシージャを定義します。|  
|`Event`|任意。 インターフェイスのメンバーであるイベントを定義します。|  
|`Interface`|任意。 このインターフェイス内で入れ子になっているインターフェイスを定義します。 入れ子になったインターフェイスの定義は、`End Interface` ステートメントで終了する必要があります。|  
|`Class`|任意。 インターフェイスのメンバーであるクラスを定義します。 メンバー クラスの定義は、`End Class` ステートメントで終了する必要があります。|  
|`Structure`|任意。 インターフェイスのメンバーである構造体を定義します。 メンバー構造体の定義は、`End Structure` ステートメントで終了する必要があります。|  
|`membername`|インターフェイスのメンバーとして定義されているプロパティ、プロシージャ、イベント、インターフェイス、クラス、または構造体ごとに必須です。 メンバーの名前。|  
|`End Interface`|`Interface` の定義を終了します。|  
  
## <a name="remarks"></a>Remarks  
 *インターフェイス*では、クラスおよび構造体で実装できる、プロパティやプロシージャなどの一連のメンバーを定義します。 インターフェイスでは、メンバーのシグネチャのみを定義し、それらの内部動作は定義しません。  
  
 クラスまたは構造体では、インターフェイスで定義されているすべてのメンバーにコードを提供することによって、インターフェイスを実装します。 最後に、アプリケーションによって、そのクラスまたは構造体からインスタンスが作成されると、メモリ内にオブジェクトが存在し、実行されます。 詳細については、「[オブジェクトとクラス](../../programming-guide/language-features/objects-and-classes/index.md)」と「[インターフェイス](../../programming-guide/language-features/interfaces/index.md)」を参照してください。  
  
 `Interface` は、名前空間またはモジュール レベルでのみ使用できます。 つまり、インターフェイスの*宣言コンテキスト*は、ソース ファイル、名前空間、クラス、構造体、モジュール、またはインターフェイスである必要があり、プロシージャまたはブロックであってはいけません。 詳細については、「[宣言コンテキストと既定のアクセス レベル](declaration-contexts-and-default-access-levels.md)」を参照してください。  
  
 インターフェイスは、既定で [Friend](../modifiers/friend.md) アクセスに設定されます。 アクセス修飾子を使用してこれらのアクセス レベルを調整できます。 詳しくは、「[Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。  
  
## <a name="rules"></a>ルール  
  
- **インターフェイスの入れ子。** インターフェイスの内部に別のインターフェイスを定義できます。 外側のインターフェイスは、*包含インターフェイス*と呼ばれ、内側のインターフェイスは *入れ子になったインターフェイス*と呼ばれます。  
  
- **メンバー宣言。** インターフェイスのメンバーとしてプロパティまたはプロシージャを宣言する場合は、そのプロパティまたはプロシージャの*シグネチャ*のみを定義します。 これには、要素の型 (プロパティまたはプロシージャ)、そのパラメーターとパラメーターの型、およびその戻り値の型が含まれます。 このため、メンバー定義では、1 行だけのコードを使用し、インターフェイスでは `End Function` や `End Property` などの終了ステートメントは、有効ではありません。  
  
     これに対し、列挙型、構造体、または入れ子になったクラスやインターフェイスを定義する場合は、それらのデータ メンバーを含める必要があります。  
  
- **メンバー修飾子。** モジュール メンバーを定義するときにアクセス修飾子を使用することはできず、[Shared](../modifiers/shared.md) または [Overloads](../modifiers/overloads.md) を除く任意のプロシージャ修飾子を指定することもできません。 [Shadows](../modifiers/shadows.md) で任意のメンバーを宣言できます。また、プロパティを定義するときに [Default](../modifiers/default.md) のほか、[ReadOnly](../modifiers/readonly.md) や [WriteOnly](../modifiers/writeonly.md) を使用することもできます。  
  
- **継承。** インターフェイスで [Inherits ステートメント](inherits-statement.md)を使用する場合は、1 つまたは複数の基底インターフェイスを指定できます。 それぞれが同じ名前のメンバーを定義している場合でも、2 つのインターフェイスから継承できます。 その場合、実装するコードでは、実装するメンバーを指定するために名前の修飾を使用する必要があります。  
  
     インターフェイスは、より制限の厳しいアクセス レベルの別のインターフェイスから継承することはできません。 たとえば、`Public` インターフェイスは、`Friend` インターフェイスから継承することはできません。  
  
     インターフェイスは、その中に入れ子にされたインターフェイスから継承することはできません。  
  
- **実装。** クラスで [Implements](implements-clause.md) ステートメントを使用してこのインターフェイスを実装する場合は、インターフェイス内に定義されているすべてのメンバーを実装する必要があります。 さらに、実装するコード内の各シグネチャが、このインターフェイスで定義されている対応するシグネチャと正確に一致する必要があります。 ただし、実装するコード内のメンバーの名前が、インターフェイスで定義されているメンバー名と一致する必要はありません。  
  
     クラスでプロシージャを実装している場合、プロシージャを `Shared` として指定することはできません。  
  
- **既定のプロパティ。** インターフェイスでは、プロパティ名を使用せずに参照できる、*既定のプロパティ*として、最大で 1 つのプロパティを指定できます。 このようなプロパティを指定するには、[Default](../modifiers/default.md) 修飾子を使用して宣言します。  
  
     つまり、インターフェイスで何も継承しない場合にのみ、既定のプロパティを定義できます。  
  
## <a name="behavior"></a>動作  
  
- **アクセス レベル。** すべてのインターフェイス メンバーには、暗黙的に[Public](../modifiers/public.md) アクセス権が与えられます。 メンバーを定義するときに、アクセス修飾子を使用することはできません。 ただし、インターフェイスを実装するクラスでは、実装される各メンバーのアクセス レベルを宣言できます。  
  
     クラス インスタンスを変数に割り当てる場合、そのメンバーのアクセス レベルは、変数のデータ型が、基になるインターフェイスであるか、または実装しているクラスであるかによって異なります。 次に例を示します。  
  
     [!code-vb[VbVbalrStatements#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#39)]  
  
     `varAsInterface` によってクラス メンバーにアクセスする場合、それらすべてにパブリック アクセス権が与えられます。 ただし、`varAsClass` によってメンバーにアクセスする場合は、`Sub` プロシージャ `doSomething` にプライベート アクセス権が与えられます。  
  
- **範囲**。 インターフェイスは、その名前空間、クラス、構造体、またはモジュール全体をスコープとします。  
  
     すべてのインターフェイス メンバーのスコープは、インターフェイス全体になります。  
  
- **有効期間。** インターフェイス自体には、有効期間やメンバーがありません。 クラスでインターフェイスを実装し、そのクラスのインスタンスとしてオブジェクトが作成される場合、そのオブジェクトには、それが実行されているアプリケーション内での有効期間があります。 詳細については、「[Class ステートメント](class-statement.md)」の「有効期間」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`Interface` ステートメントを使用して、`thisInterface` という名前のインターフェイスを定義しています。これは、`Property` ステートメントと `Function` ステートメントで実装する必要があります。  
  
 [!code-vb[VbVbalrStatements#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#40)]  
  
 `Property` ステートメントと `Function` ステートメントでは、インターフェイス内に `End Property` および `End Function` で終わるブロックを取り込んでいないことに注意してください。 このインターフェイスでは、そのメンバーのシグネチャのみを定義しています。 完全な `Property` と `Function` のブロックは、`thisInterface` を実装するクラスに存在します。  
  
## <a name="see-also"></a>関連項目

- [インターフェイス](../../programming-guide/language-features/interfaces/index.md)
- [Class ステートメント](class-statement.md)
- [Module ステートメント](module-statement.md)
- [Structure ステートメント](structure-statement.md)
- [Property ステートメント](property-statement.md)
- [Function ステートメント](function-statement.md)
- [Sub ステートメント](sub-statement.md)
- [Generic Types in Visual Basic](../../programming-guide/language-features/data-types/generic-types.md)
- [ジェネリック インターフェイスの変性](../../programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)
- [In](../modifiers/in-generic-modifier.md)
- [Out](../modifiers/out-generic-modifier.md)
