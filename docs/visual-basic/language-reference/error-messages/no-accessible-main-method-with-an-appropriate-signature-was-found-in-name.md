---
title: 正しいシグネチャを持つ、アクセス可能な 'Main' メソッドは、'<name>' に見つかりませんでした。
ms.date: 07/20/2015
f1_keywords:
- bc30737
- vbc30737
helpviewer_keywords:
- BC30737
ms.assetid: 3f40bacd-3fac-4741-b204-852f693d4340
ms.openlocfilehash: 6760b931ceb2ad5c2c04169d664da8629badc487
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409414"
---
# <a name="no-accessible-main-method-with-an-appropriate-signature-was-found-in-name"></a>正しいシグネチャを持つ、アクセス可能な 'Main' メソッドは、'\<name>' に見つかりませんでした。
コマンドライン アプリケーションには `Sub Main` が定義されている必要があります。 `Main` は、クラスで定義されている場合は `Public Shared` として、またはモジュールで定義されている場合は `Public` として宣言する必要があります。  
  
 **エラー ID:** BC30737  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- プロジェクトに `Public Sub Main` プロシージャを定義します。 それをクラス内で定義する場合、かつその場合にのみ、`Shared` として宣言します。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic プログラムの構造](../../programming-guide/program-structure/structure-of-a-visual-basic-program.md)
- [手順](../../programming-guide/language-features/procedures/index.md)
