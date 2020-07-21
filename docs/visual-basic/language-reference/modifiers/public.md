---
title: Public
ms.date: 07/20/2015
f1_keywords:
- vb.Public
helpviewer_keywords:
- Public keyword [Visual Basic]
- Public keyword [Visual Basic], syntax
- Public access modifier
ms.assetid: 284c9e1b-ed23-499b-9bc9-ad87c11485a5
ms.openlocfilehash: 35332e50227cdef6386362df17c10b5b2cdaa689
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415350"
---
# <a name="public-visual-basic"></a>Public (Visual Basic)
1 つ以上の宣言されたプログラミング要素にアクセス制限がないことを示します。  
  
## <a name="remarks"></a>Remarks  
 クラス ライブラリなどのコンポーネントまたはコンポーネントのセットを公開する場合は、通常、アセンブリと相互運用できるコードでプログラミング要素にアクセスできるようにする必要があります。 要素に対してこのような無制限のアクセス権を付与するには、`Public` で宣言します。  
  
 パブリック アクセスは、プログラミング要素へのアクセスを制限する必要がない場合の通常のレベルです。 インターフェイス、モジュール、クラス、または構造体で宣言されている要素のアクセス レベルは、宣言しない場合、既定では `Public` になることに注意してください。  
  
## <a name="rules"></a>ルール  
  
- **宣言コンテキスト。** `Public` は、モジュール、インターフェイス、または名前空間レベルでのみ使用できます。 つまり、`Public` 要素の宣言コンテキストは、ソース ファイル、名前空間、インターフェイス、モジュール、クラス、または構造体にする必要があり、プロシージャにすることはできません。  
  
## <a name="behavior"></a>動作  
  
- **アクセス レベル。** モジュール、クラス、または構造体にアクセスできるすべてのコードは、その `Public` 要素にアクセスできます。  
  
- **既定のアクセス。** プロシージャ内のローカル変数は、既定でパブリック アクセスに設定されていて、それらでアクセス修飾子を使用することはできません。  
  
- **アクセス修飾子。** アクセス レベルを指定するキーワードは、*アクセス修飾子*と呼ばれます。 アクセス修飾子の比較については、「[Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。  
  
 `Public` 修飾子は、次のコンテキストで使用できます。  
  
 [Class ステートメント](../statements/class-statement.md)  
  
 [Const ステートメント](../statements/const-statement.md)  
  
 [Declare ステートメント](../statements/declare-statement.md)  
  
 [Delegate ステートメント](../statements/delegate-statement.md)  
  
 [Dim ステートメント](../statements/dim-statement.md)  
  
 [Enum ステートメント](../statements/enum-statement.md)  
  
 [Event ステートメント](../statements/event-statement.md)  
  
 [Function ステートメント](../statements/function-statement.md)  
  
 [Interface ステートメント](../statements/interface-statement.md)  
  
 [Module ステートメント](../statements/module-statement.md)  
  
 [Operator ステートメント](../statements/operator-statement.md)  
  
 [Property ステートメント](../statements/property-statement.md)  
  
 [Structure ステートメント](../statements/structure-statement.md)  
  
 [Sub ステートメント](../statements/sub-statement.md)  
  
## <a name="see-also"></a>関連項目

- [Protected](protected.md)
- [Friend](friend.md)
- [Private](private.md)
- [Private Protected](private-protected.md)
- [Protected Friend](protected-friend.md)
- [Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)
- [手順](../../programming-guide/language-features/procedures/index.md)
- [構造体](../../programming-guide/language-features/data-types/structures.md)
- [クラスとオブジェクト](../../programming-guide/language-features/objects-and-classes/index.md)
