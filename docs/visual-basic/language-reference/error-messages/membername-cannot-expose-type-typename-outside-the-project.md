---
title: ''<membername>' は、型 '<typename>' を <containertype> '<containertypename>' 経由でプロジェクトの外側に公開できません。'
ms.date: 07/20/2015
f1_keywords:
- bc30909
- vbc30909
helpviewer_keywords:
- BC30909
ms.assetid: ffa7395d-e182-4087-8ce8-079810fdae54
ms.openlocfilehash: 36add48ebee2d1804921eeeec0b59cdd4cbafecc
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33588094"
---
# <a name="39ltmembernamegt39-cannot-expose-type-39lttypenamegt39-outside-the-project-through-ltcontainertypegt-39ltcontainertypenamegt39"></a>'<membername>' は、型 '<typename>' を <containertype> '<containertypename>' 経由でプロジェクトの外側に公開できません。
変数、プロシージャのパラメーター、または関数の戻り値は、そのコンテナーでは、外部に公開されるが、コンテナーの外部公開してはならないを型として宣言されています。  
  
 次のスケルトン コードは、このエラーが発生する状況を示しています。  
  
```  
Private Class privateClass  
End Class  
Public Class mainClass  
    Public exposedVar As New privateClass  
End Class  
```  
  
 宣言されている型`Protected`、 `Friend`、 `Protected Friend`、または`Private`宣言コンテキストの外部アクセスを制限するためのものでは、します。 データとして使用する制限の少ない方のアクセス権を持つ変数の型に反しますこの目的。 上記のスケルトン コード`exposedVar`は`Public`公開と`privateClass`へのアクセス権のないコードにします。  
  
 **エラー ID:** BC30909  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
-   変数、プロシージャのパラメーター、または関数のアクセス レベルの変更は、少なくとも最小限にそのデータ型のアクセス レベルに戻ります。  
  
## <a name="see-also"></a>関連項目  
 [Visual Basic でのアクセス レベル](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
