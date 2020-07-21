---
title: クラスの定義
ms.date: 07/20/2015
helpviewer_keywords:
- execution [Visual Basic], ending
- objects [Visual Basic], initializing
- Initialize event [Visual Basic]
- files [Visual Basic], closing
- programs [Visual Basic], quitting
- code, exiting
- objects [Visual Basic], creating
- program termination
- classes [Visual Basic], walkthroughs
- class modules, walkthroughs
- Terminate event [Visual Basic]
- execution [Visual Basic], stopping
ms.assetid: 07018828-2d49-4cf5-a44b-19fb15d9efea
ms.openlocfilehash: 646c6ce307131f3edba194af19920eade9c1753c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84389115"
---
# <a name="walkthrough-defining-classes-visual-basic"></a>チュートリアル: クラスの定義 (Visual Basic)

このチュートリアルでは、クラスを定義する方法について説明します。このクラスを使用してオブジェクトを作成できます。 また、新しいクラスにプロパティとメソッドを追加する方法と、オブジェクトを初期化する方法についても説明します。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="to-define-a-class"></a>クラスを定義するには
  
1. **[ファイル]** メニューの **[新しいプロジェクト]** をクリックして、プロジェクトを作成します。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2. Visual Basic プロジェクト テンプレートの一覧から [Windows アプリケーション] を選択して、新しいプロジェクトを表示します。  
  
3. **[プロジェクト]** メニューの **[クラスの追加]** をクリックして、プロジェクトに新しいクラスを追加します。 **[新しい項目の追加]** ダイアログ ボックスが表示されます。  
  
4. **[クラス]** テンプレートを選択します。  
  
5. 新しいクラスに `UserNameInfo.vb` という名前を指定し、 **[追加]** をクリックして新しいクラスのコードを表示します。  
  
     [!code-vb[VbVbalrOOP#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#5)]
  
    > [!NOTE]
    > Visual Basic **コード エディター**を使用すると、`Class` キーワードに続けて新しいクラスの名前を入力することで、クラスをスタートアップ フォームに追加できます。 **コードエディター**には、対応する `End Class` ステートメントが用意されています。  
  
6. `Class` ステートメントと `End Class` ステートメントの間に次のコードを追加して、クラスのプライベート フィールドを定義します。  
  
     [!code-vb[VbVbalrOOP#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#7)]
  
     フィールドを `Private` として宣言すると、そのクラス内でのみ使用できます。 より多くのアクセスを提供する `Public` などのアクセス修飾子を使用すると、クラスの外部からフィールドを使用できるようにすることができます。 詳しくは、「[Visual Basic でのアクセス レベル](../declared-elements/access-levels.md)」を参照してください。  
  
7. 次のコードを追加して、クラスのプロパティを定義します。  
  
     [!code-vb[VbVbalrOOP#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#8)]
  
8. 次のコードを追加して、クラスのメソッドを定義します。  
  
     [!code-vb[VbVbalrOOP#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#9)]
  
9. `Sub New` という名前のプロシージャを追加して、新しいクラスのパラメーター化されたコンストラクターを定義します。  
  
     [!code-vb[VbVbalrOOP#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#10)]
  
     このクラスに基づくオブジェクトが作成されると、`Sub New` コンストラクターが自動的に呼び出されます。 このコンストラクターは、ユーザー名を保持するフィールドの値を設定します。  
  
## <a name="to-create-a-button-to-test-the-class"></a>クラスをテストするボタンを作成するには
  
1. **ソリューション エクスプローラー**で名前を右クリックし、 **[ビュー デザイナー]** をクリックして、スタートアップ フォームをデザイン モードに変更します。 既定では、Windows アプリケーション プロジェクトのスタートアップ フォームには、Form1.vb という名前が付けられています。 メイン フォームが表示されます。  
  
2. メイン フォームにボタンを追加し、それをダブルクリックして、`Button1_Click` イベント ハンドラーのコードを表示します。 テスト プロシージャを呼び出す次のコードを追加します。  
  
     [!code-vb[VbVbalrOOP#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#12)]
  
## <a name="to-run-your-application"></a>アプリケーションを実行するには
  
1. F5 キーを押してアプリケーションを実行します。 フォーム上のボタンをクリックして、テスト プロシージャを呼び出します。 元の `UserName` が "MOORE, BOBBY" であることを示すメッセージが表示されます。これは、プロシージャがオブジェクトの `Capitalize` メソッドを呼び出したためです。  
  
2. **[OK]** をクリックしてメッセージ ボックスを閉じます。 `Button1 Click` プロシージャによって `UserName` プロパティの値が変更され、`UserName` の新しい値が "Worden, Joe" であることを示すメッセージが表示されます。  
  
## <a name="see-also"></a>関連項目

- [オブジェクト指向プログラミング (Visual Basic)](../../concepts/object-oriented-programming.md)
- [クラスとオブジェクト](index.md)
