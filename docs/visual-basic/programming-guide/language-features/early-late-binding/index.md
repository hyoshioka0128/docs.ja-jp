---
title: 事前バインディングと遅延バインディング (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- early binding [Visual Basic]
- objects [Visual Basic], late-bound
- objects [Visual Basic], early-bound
- objects [Visual Basic], late bound
- early binding [Visual Basic], Visual Basic compiler
- binding [Visual Basic], late and early
- objects [Visual Basic], early bound
- Visual Basic compiler, early and late binding
- late binding [Visual Basic]
- late binding [Visual Basic], Visual Basic compiler
ms.assetid: d6ff7f1e-b94f-4205-ab8d-5cfa91758724
ms.openlocfilehash: 8426899b0c0d3649f47cbd6ad5383dd3c95b9499
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33647254"
---
# <a name="early-and-late-binding-visual-basic"></a>事前バインディングと遅延バインディング (Visual Basic)
Visual Basic コンパイラの実行と呼ばれるプロセス`binding`オブジェクトが、オブジェクト変数に割り当てられている場合。 オブジェクトが特定のオブジェクト型として宣言された変数に代入される場合、オブジェクトは*事前バインディング*されます。 事前バインディングされたオブジェクトを使用すると、コンパイラは、アプリケーションを実行する前に、メモリの割り当てとその他の最適化を実行することができます。 たとえば、次のコードは、<xref:System.IO.FileStream> 型の変数を宣言します。  
  
 [!code-vb[VbVbalrOOP#90](../../../../visual-basic/misc/codesnippet/VisualBasic/early-and-late-binding_1.vb)]  
  
 <xref:System.IO.FileStream> は特定のオブジェクト型であるため、`FS` に代入されるインスタンスは事前バインディングされます。  
  
 対照的に、オブジェクトが `Object` 型として宣言された変数に代入される場合、オブジェクトは*遅延バインディング*されます。 この型のオブジェクトは、任意のオブジェクトへの参照を保持できますが、事前バインディングされたオブジェクトが持っている多くの利点を欠いています。 たとえば、次のコードは、`CreateObject` 関数によって返されたオブジェクトを保持するオブジェクト変数を宣言します。  
  
 [!code-vb[VbVbalrOOP#91](../../../../visual-basic/misc/codesnippet/VisualBasic/early-and-late-binding_2.vb)]  
  
## <a name="advantages-of-early-binding"></a>事前バインディングの利点  
 コンパイラが効率の高いアプリケーションを生成するための重要な最適化を行うことができるため、可能であれば、事前バインディングされたオブジェクトを使用する必要があります。 事前バインディングされたオブジェクトは遅延バインディング オブジェクトよりもはるかに高速であり、使用されるオブジェクトの種類を正確に記述することでコードを読みやすくして管理を容易にします。 事前バインディングをもう 1 つの利点は、Visual Studio 統合開発環境 (IDE) に正確にどのようなオブジェクトの型を扱うを編集すると判断できるので自動コード補完機能とダイナミック ヘルプなどの便利な機能を使用できること、コードです。 事前バインディングを使用すると、コンパイラがプログラムのコンパイル時にエラーを報告できるため、ランタイム エラーの数が減少し、重大度が低下します。  
  
> [!NOTE]
>  遅延バインディングは、`Public` として宣言されている型メンバーにアクセスするためにのみ使用できます。 `Friend` または `Protected Friend` として宣言されているメンバーにアクセスすると、ランタイム エラーが発生します。  
  
## <a name="see-also"></a>関連項目  
 <xref:Microsoft.VisualBasic.Interaction.CreateObject%2A>  
 [オブジェクトの有効期間 : オブジェクトの作成と破棄](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)  
 [Object 型](../../../../visual-basic/language-reference/data-types/object-data-type.md)
