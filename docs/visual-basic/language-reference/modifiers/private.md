---
title: Private
ms.date: 07/20/2015
f1_keywords:
- vb.Private
helpviewer_keywords:
- Private keyword [Visual Basic]
- Private keyword [Visual Basic], syntax
ms.assetid: aba74a2e-5824-4613-bf63-b9ec7787f4e6
ms.openlocfilehash: 524f03e77e075bef08a1b41b563985de41baacb6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404811"
---
# <a name="private-visual-basic"></a>Private (Visual Basic)
1 つ以上の宣言されたプログラミング要素が、含まれている型の中からを含め、その宣言コンテキスト内からのみアクセス可能であることを示します。  
  
## <a name="remarks"></a>Remarks  
 プログラミング要素が独自の機能を表している場合、または機密データが含まれている場合は、通常、できるだけ厳密にアクセスを制限することをお勧めします。 最大の制限を達成するには、それを定義するモジュール、クラス、または構造体だけがアクセスできるようにします。 この方法で要素へのアクセスを制限するには、`Private` を使用して宣言できます。  

> [!NOTE]
> また、[Private Protected](private-protected.md) アクセス修飾子を使用することもできます。これにより、メンバーには、クラス内から、および包含アセンブリにある派生クラスからアクセスできます。

## <a name="rules"></a>ルール  

- **宣言コンテキスト。** `Private` は、モジュール レベルでのみ使用できます。 つまり、`Private` 要素の宣言コンテキストは、モジュール、クラス、または構造体にする必要があり、ソース ファイル、名前空間、インターフェイス、またはプロシージャにすることはできません。  
  
## <a name="behavior"></a>動作  
  
- **アクセス レベル。** 宣言コンテキスト内のすべてのコードは、その `Private` 要素にアクセスできます。 これには、入れ子になったクラスや列挙内の代入式など、含まれている型内のコードが含まれます。 宣言コンテキストの外側のコードは、その `Private` 要素にアクセスすることはできません。  
  
- **アクセス修飾子。** アクセス レベルを指定するキーワードは、*アクセス修飾子*と呼ばれます。 アクセス修飾子の比較については、「[Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。  
  
 `Private` 修飾子は、次のコンテキストで使用できます。  
  
 [Class ステートメント](../statements/class-statement.md)  
  
 [Const ステートメント](../statements/const-statement.md)  
  
 [Declare ステートメント](../statements/declare-statement.md)  
  
 [Delegate ステートメント](../statements/delegate-statement.md)  
  
 [Dim ステートメント](../statements/dim-statement.md)  
  
 [Enum ステートメント](../statements/enum-statement.md)  
  
 [Event ステートメント](../statements/event-statement.md)  
  
 [Function ステートメント](../statements/function-statement.md)  
  
 [Interface ステートメント](../statements/interface-statement.md)  
  
 [Property ステートメント](../statements/property-statement.md)  
  
 [Structure ステートメント](../statements/structure-statement.md)  
  
 [Sub ステートメント](../statements/sub-statement.md)  
  
## <a name="see-also"></a>関連項目

- [Public](public.md)
- [Protected](protected.md)
- [Friend](friend.md)
- [Private Protected](./private-protected.md)
- [Protected Friend](./protected-friend.md)
- [Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)
- [手順](../../programming-guide/language-features/procedures/index.md)
- [構造体](../../programming-guide/language-features/data-types/structures.md)
- [クラスとオブジェクト](../../programming-guide/language-features/objects-and-classes/index.md)
