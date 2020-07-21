---
title: Implements 句
ms.date: 07/20/2015
f1_keywords:
- vb.ImplementsClause
helpviewer_keywords:
- interface implementation [Visual Basic], reimplementation
- interface members [Visual Basic], reimplementation
- interface members [Visual Basic], Implements keyword
- interface members
- members [Visual Basic], reimplementation
- interface implementation [Visual Basic], Implements keyword
- interface members [Visual Basic], implementing
- Implements keyword [Visual Basic]
- Implements statement [Visual Basic], about Implements
- members [Visual Basic], implementing
- members [Visual Basic], Implements keyword
- reimplementation
ms.assetid: 5252cdf9-964d-4fc6-af0f-0449b7126b5a
ms.openlocfilehash: 46ab1a1148e8d73d91293aedfc407e5efdc7cfb4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404564"
---
# <a name="implements-clause-visual-basic"></a>Implements 句 (Visual Basic)
クラスまたは構造体のメンバーがインターフェイスで定義されているメンバーの実装を提供していることを示します。  
  
## <a name="remarks"></a>Remarks  
`Implements` キーワードは、[Implements ステートメント](implements-statement.md)と同じではありません。 `Implements` ステートメントを使用して、クラスまたは構造体が 1 つ以上のインターフェイスを実装することを指定し、メンバーごとに `Implements` キーワードを使用して、実装するインターフェイスとメンバーを指定します。

クラスまたは構造体がインターフェイスを実装する場合は、[Class ステートメント](class-statement.md)または [Structure ステートメント](structure-statement.md)の直後に `Implements` ステートメントを含める必要があります。また、インターフェイスによって定義されたすべてのメンバーを実装する必要があります。

## <a name="reimplementation"></a>再実装  
派生クラスでは、基底クラスによって既に実装されているインターフェイス メンバーを再実装できます。 これは、基底クラスのメンバーのオーバーライドとは、次の点で異なります。

- 基底クラスのメンバーは、再実装するために [Overridable](../modifiers/overridable.md) である必要はありません。
- 別の名前を使用してメンバーを再実装できます。

`Implements` キーワードは、次のコンテキストで使用できます。

- [Event ステートメント](event-statement.md)
- [Function ステートメント](function-statement.md)
- [Property ステートメント](property-statement.md)
- [Sub ステートメント](sub-statement.md)  
  
## <a name="see-also"></a>関連項目

- [Implements ステートメント](implements-statement.md)
- [Interface ステートメント](interface-statement.md)
- [Class ステートメント](class-statement.md)
- [Structure ステートメント](structure-statement.md)
