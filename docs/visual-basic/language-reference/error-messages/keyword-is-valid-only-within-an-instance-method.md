---
title: "'<keyword>' は、インスタンス メソッド内でのみ有効です。"
ms.date: 07/20/2015
f1_keywords:
- bc30043
- vbc30043
helpviewer_keywords:
- BC30043
ms.assetid: 7973aa82-a681-440c-9bca-242627d7ba86
ms.openlocfilehash: 537689405ea30bdd7c075320eba58a8723a93cdb
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397403"
---
# <a name="keyword-is-valid-only-within-an-instance-method"></a>'\<keyword>' は、インスタンス メソッド内でのみ有効です。
`Me`、`MyClass`、および `MyBase` キーワードは、特定のクラス インスタンスを参照します。 それらを共有の `Function` または `Sub` プロシージャ内で使用することはできません。  
  
 **エラー ID:** BC30043  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- プロシージャからキーワードを削除するか、プロシージャ宣言から `Shared` キーワードを削除します。  
  
## <a name="see-also"></a>関連項目

- [オブジェクト変数の代入](../../programming-guide/language-features/variables/object-variable-assignment.md)
- [Me、My、MyBase、および MyClass](../../programming-guide/program-structure/me-my-mybase-and-myclass.md)
- [継承の基本](../../programming-guide/language-features/objects-and-classes/inheritance-basics.md)
