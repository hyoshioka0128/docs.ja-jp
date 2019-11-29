---
title: プライベート
ms.date: 07/20/2015
f1_keywords:
- vb.Private
helpviewer_keywords:
- Private keyword [Visual Basic]
- Private keyword [Visual Basic], syntax
ms.assetid: aba74a2e-5824-4613-bf63-b9ec7787f4e6
ms.openlocfilehash: 5600744aeca79a54f51a1f9ecd0ef00fed4b00fd
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74351331"
---
# <a name="private-visual-basic"></a>Private (Visual Basic)
1つ以上の宣言されたプログラミング要素が、含まれている型の中からを含め、宣言コンテキスト内からのみアクセス可能であることを指定します。  
  
## <a name="remarks"></a>コメント  
 プログラミング要素が独自の機能を表している場合、または機密データが含まれている場合は、通常、できるだけ厳密にアクセスを制限することをお勧めします。 最大の制限を達成するには、それを定義するモジュール、クラス、または構造体だけがアクセスできるようにします。 この方法で要素へのアクセスを制限するには、`Private`で要素を宣言します。  

> [!NOTE]
> [プライベート Protected](private-protected.md)アクセス修飾子を使用することもできます。これにより、メンバーは、そのクラス内から、およびそれを含むアセンブリに配置されている派生クラスからアクセスできるようになります。

## <a name="rules"></a>ルール  

- **宣言コンテキスト。** `Private` は、モジュール レベルでのみ使用できます。 つまり、`Private` 要素の宣言コンテキストは、モジュール、クラス、または構造体である必要があり、ソースファイル、名前空間、インターフェイス、またはプロシージャにすることはできません。  
  
## <a name="behavior"></a>動作  
  
- **アクセスレベル。** 宣言コンテキスト内のすべてのコードは、その `Private` 要素にアクセスできます。 これには、入れ子になったクラスや列挙体の代入式など、含まれている型内のコードが含まれます。 宣言コンテキストの外部のコードは、その `Private` 要素にアクセスできません。  
  
- **アクセス修飾子。** アクセスレベルを指定するキーワードは、*アクセス修飾子*と呼ばれます。 アクセス修飾子の比較については、「 [Visual Basic のアクセスレベル](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。  
  
 `Private` 修飾子は、次のコンテキストで使用できます。  
  
 [Class ステートメント](../../../visual-basic/language-reference/statements/class-statement.md)  
  
 [Const ステートメント](../../../visual-basic/language-reference/statements/const-statement.md)  
  
 [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Delegate ステートメント](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
 [Dim ステートメント](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Enum ステートメント](../../../visual-basic/language-reference/statements/enum-statement.md)  
  
 [Event ステートメント](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Function ステートメント](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Interface ステートメント](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 [Property ステートメント](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Structure ステートメント](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Sub ステートメント](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>関連項目

- [Public](../../../visual-basic/language-reference/modifiers/public.md)
- [Protected](../../../visual-basic/language-reference/modifiers/protected.md)
- [Friend](../../../visual-basic/language-reference/modifiers/friend.md)
- [Private Protected](./private-protected.md)
- Visual Basic の[保護されたフレンド](./protected-friend.md)[アクセスレベル](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [手順](../../../visual-basic/programming-guide/language-features/procedures/index.md)
- [構造体](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [クラスとオブジェクト](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
