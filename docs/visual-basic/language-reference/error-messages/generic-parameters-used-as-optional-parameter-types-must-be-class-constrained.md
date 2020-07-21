---
title: 省略可能なパラメーター型として使用されるジェネリック パラメーターは、クラスの制約がある型でなければなりません。
ms.date: 07/20/2015
f1_keywords:
- vbc32124
- bc32124
helpviewer_keywords:
- BC32124
ms.assetid: 55aa8b2a-9ce3-4620-a710-2f9b0feb6143
ms.openlocfilehash: 273ea592e73be5d76a4ffef077e691014a108347
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402928"
---
# <a name="generic-parameters-used-as-optional-parameter-types-must-be-class-constrained"></a>省略可能なパラメーター型として使用されるジェネリック パラメーターは、クラスの制約がある型でなければなりません。
プロシージャは、参照型に制限されていない型パラメーターを使用する省略可能なパラメーターで、宣言します。  
  
 省略可能な各パラメーターには、常に既定値を指定する必要があります。 パラメーターが参照型の場合、省略可能な値は `Nothing` である必要があります。これはすべての参照型に有効な値です。 ただし、パラメーターが値型の場合、その型は Visual Basic によって事前に定義された基本データ型である必要があります。 これは、ユーザー定義構造体などの複合値型に有効な既定値がないためです。  
  
 省略可能なパラメーターに型パラメーターを使用する場合は、有効な既定値を持たない値型の可能性を回避するために、それが参照型であることを保証する必要があります。 つまり、`Class` キーワードまたは特定のクラスの名前のいずれかによって、型パラメーターを制約する必要があります。  
  
 **エラー ID:** BC32124  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 参照型のみを受け入れるように型パラメーターを制約するか、または省略可能なパラメーターにそれを使用しないでください。  
  
## <a name="see-also"></a>関連項目

- [Generic Types in Visual Basic](../../programming-guide/language-features/data-types/generic-types.md)
- [型リスト](../statements/type-list.md)
- [Class ステートメント](../statements/class-statement.md)
- [省略可能なパラメーター](../../programming-guide/language-features/procedures/optional-parameters.md)
- [構造体](../../programming-guide/language-features/data-types/structures.md)
- [Nothing](../nothing.md)
