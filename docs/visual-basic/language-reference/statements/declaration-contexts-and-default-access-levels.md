---
title: 宣言コンテキストと既定のアクセス レベル
ms.date: 07/20/2015
helpviewer_keywords:
- module level, defined
- declaration contexts, Visual Basic
- procedure level, defined
- namespace level, defined
- access levels, Visual Basic
- access levels, default levels
ms.assetid: bf63b96e-e825-4745-88c8-5dae222728db
ms.openlocfilehash: b5bb943a062ac648f88645fb6de1acb42213071c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404798"
---
# <a name="declaration-contexts-and-default-access-levels-visual-basic"></a>宣言コンテキストと既定のアクセス レベル (Visual Basic)
このトピックでは、どの Visual Basic の型を他のどの型内に宣言できるか、およびそれらのアクセス レベルが指定されていない場合の既定値について説明します。  
  
## <a name="declaration-context-levels"></a>宣言コンテキスト レベル  
 プログラミング要素の*宣言コンテキスト*は、それが宣言されているコードの領域です。 これは、多くの場合、別のプログラミング要素であり、そのために*親要素*と呼ばれます。  
  
 宣言コンテキストのレベルは次のとおりです。  
  
- *名前空間レベル* - ソースファイルまたは名前空間内であり、クラス、構造体、モジュール、またはインターフェイス内ではありません  
  
- *モジュール レベル* - クラス、構造体、モジュール、またはインターフェイス内であり、プロシージャまたはブロック内ではありません  
  
- *プロシージャ レベル* - プロシージャまたはブロック (`If` や `For` など) 内です  
  
 次の表に、宣言コンテキストに応じて、宣言されたさまざまなプログラミング要素の既定のアクセス レベルを示します。  
  
|宣言された要素|名前空間レベル|モジュール レベル|プロシージャ レベル|  
|----------------------|---------------------|------------------|---------------------|  
|変数 ([Dim ステートメント](dim-statement.md))|使用できません|`Private` (`Structure` 内の `Public`、`Interface` では使用できません)|`Public`|  
|定数 ([Const ステートメント](const-statement.md))|使用できません|`Private` (`Structure` 内の `Public`、`Interface` では使用できません)|`Public`|  
|列挙型 ([Enum ステートメント](enum-statement.md))|`Friend`|`Public`|使用できません|  
|クラス ([Class ステートメント](class-statement.md))|`Friend`|`Public`|使用できません|  
|構造体 ([Structure ステートメント](structure-statement.md))|`Friend`|`Public`|使用できません|  
|モジュール ([Module ステートメント](module-statement.md))|`Friend`|使用できません|使用できません|  
|インターフェイス ([Interface ステートメント](interface-statement.md))|`Friend`|`Public`|使用できません|  
|プロシージャ ([Function ステートメント](function-statement.md)、[Sub ステートメント](sub-statement.md))|使用できません|`Public`|使用できません|  
|外部参照 ([Declare ステートメント](declare-statement.md))|使用できません|`Public` (`Interface` では使用できません)|使用できません|  
|演算子 ([Operator ステートメント](operator-statement.md))|使用できません|`Public` (`Interface` または `Module` では使用できません)|使用できません|  
|プロパティ ([Property ステートメント](property-statement.md))|使用できません|`Public`|使用できません|  
|既定のプロパティ ([Default](../modifiers/default.md))|使用できません|`Public` (`Module` では使用できません)|使用できません|  
|イベント ([Event ステートメント](event-statement.md))|使用できません|`Public`|使用できません|  
|委任 ([Delegate ステートメント](delegate-statement.md))|`Friend`|`Public`|使用できません|  
  
 詳しくは、「[Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [Friend](../modifiers/friend.md)
- [Private](../modifiers/private.md)
- [Public](../modifiers/public.md)
