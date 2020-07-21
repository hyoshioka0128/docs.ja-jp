---
title: 宣言された要素の特性
ms.date: 07/20/2015
helpviewer_keywords:
- declared elements [Visual Basic], lifetime
- access levels, declared elements
- declared elements [Visual Basic], scope
- visibility [Visual Basic], declared elements
- elements [Visual Basic], programming
- scope [Visual Basic], declared elements
- lifetime [Visual Basic], declared elements
- declared elements [Visual Basic], access level
- data types [Visual Basic], declared elements
- declared elements [Visual Basic], visibility
ms.assetid: 1bc40fb8-b67c-4428-90a4-76b630ae2583
ms.openlocfilehash: 9d1e327c25689bed1405ea9a627da6232abb707b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84392949"
---
# <a name="declared-element-characteristics-visual-basic"></a>宣言された要素の特性 (Visual Basic)
宣言された要素の "*特性*" は、その要素の側面の 1 つで、コードが要素とやり取りする方法に影響を与えます。 宣言されたすべての要素には、次の 1 つ以上の特性が関連付けられています。  
  
- *データ型*: 要素で保持できる値と、その値を格納する方法。 詳細については、「[Data Types](../../../language-reference/data-types/index.md)」(データ型) を参照してください。  
  
- *有効期間*: 要素で使用可能な実行時間。 詳しくは、「[Visual Basic における有効期間](lifetime.md)」をご覧ください。  
  
- *スコープ*: 名前を修飾せずに要素を参照できるすべてのコードのセット。 詳細については、「[方法:方法: 変数のスコープを制御する](how-to-control-the-scope-of-a-variable.md)」を参照してください。  
  
- *アクセス レベル*: 要素を使用するコードのアクセス許可。 詳細については、「[方法:方法: 変数の可用性を制御する](how-to-control-the-availability-of-a-variable.md)」を参照してください。  
  
## <a name="characteristics-of-the-elements"></a>要素の特性  
 次の表に、宣言された要素と、それぞれに適用される特性を示します。  
  
|要素|データの種類|有効期間|スコープ <sup>1</sup>|アクセス レベル|  
|-------------|---------------|--------------|------------------------|------------------|  
|変数|はい|はい|はい|はい|  
|定数|はい|×|はい|はい|  
|列挙|はい|×|はい|はい|  
|構造体|いいえ|いいえ|はい|はい|  
|プロパティ|はい|はい|はい|はい|  
|メソッド|いいえ|はい|はい|はい|  
|プロシージャ (`Sub` または `Function`)|いいえ|はい|はい|はい|  
|プロシージャ パラメーター|はい|はい|はい|いいえ|  
|関数の戻り値|はい|はい|はい|いいえ|  
|演算子|はい|×|はい|はい|  
|Interface|いいえ|いいえ|はい|はい|  
|クラス|いいえ|いいえ|はい|はい|  
|event|いいえ|いいえ|はい|はい|  
|Delegate|いいえ|いいえ|はい|はい|  
  
 <sup>1</sup> スコープは、"*可視性*" と呼ばれることもあります。  
  
## <a name="see-also"></a>関連項目

- [宣言された要素](index.md)
- [宣言された要素の名前](declared-element-names.md)
- [宣言された要素の参照](references-to-declared-elements.md)
- [Visual Basic における有効期間](lifetime.md)
- [Visual Basic におけるスコープ](scope.md)
- [Visual Basic でのアクセス レベル](access-levels.md)
- [データの種類](../data-types/index.md)
- [変数宣言](../variables/variable-declaration.md)
