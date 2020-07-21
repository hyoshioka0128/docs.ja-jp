---
title: ベース <typename> のアクセスをアセンブリの外側に展開しているため、'<type>' は <basetypename> '<type>' から継承できません。
ms.date: 07/20/2015
f1_keywords:
- vbc30910
- bc30910
helpviewer_keywords:
- BC30910
ms.assetid: 68fc05c5-5d55-4742-9a3b-ea04312594f4
ms.openlocfilehash: aa04c558abbcc4259c2821cdcbdc1669b91ffee0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402773"
---
# <a name="typename-cannot-inherit-from-type-basetypename-because-it-expands-the-access-of-the-base-type-outside-the-assembly"></a>ベース \<typename> のアクセスをアセンブリの外側に展開しているため、'\<type>' は \<basetypename> '\<type>' から継承できません。
クラスまたはインターフェイスは、基底クラスまたはインターフェイスから継承されますが、アクセス レベルの制限が緩くなります。  
  
 たとえば、`Public` インターフェイスは `Friend` インターフェイスから継承し、または `Protected` クラスは、`Private` クラスから継承します。 これにより、目的のレベルを超えてアクセスする基底クラスまたはインターフェイスが公開されます。  
  
 **エラー ID:** BC30910  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 派生クラスまたはインターフェイスのアクセス レベルを、少なくとも基底クラスまたはインターフェイスのアクセス レベルの制限になるように変更します。  
  
     \- または -  
  
- 制限の緩いアクセス レベルが必要な場合は、`Inherits` ステートメントを削除します。 より制限の厳しい基底クラスまたはインターフェイスから継承することはできません。  
  
## <a name="see-also"></a>関連項目

- [Class ステートメント](../statements/class-statement.md)
- [Interface ステートメント](../statements/interface-statement.md)
- [Inherits ステートメント](../statements/inherits-statement.md)
- [Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)
