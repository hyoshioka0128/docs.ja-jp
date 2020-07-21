---
title: インターフェイスの作成と実装
ms.date: 07/20/2015
helpviewer_keywords:
- interfaces [Visual Basic], walkthroughs
- interfaces [Visual Basic], testing
- interface implementation [Visual Basic], walkthrough
- interfaces [Visual Basic], creating
ms.assetid: ded82af2-9f52-4232-98ef-fe458180f112
ms.openlocfilehash: 89e8f91a04b25b84bc783d5c4f4b91cf12426f72
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405068"
---
# <a name="walkthrough-creating-and-implementing-interfaces-visual-basic"></a>チュートリアル: インターフェイスの作成と実装 (Visual Basic)

インターフェイスには、プロパティ、メソッド、およびイベントの特性が記述されていますが、実装の詳細は構造体またはクラスに委ねられています。  
  
 このチュートリアルでは、インターフェイスを宣言し、実装する方法について説明します。  
  
> [!NOTE]
> このチュートリアルでは、ユーザー インターフェイスの作成方法については説明しません。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="to-define-an-interface"></a>インターフェイスを定義するには
  
1. 新しい Visual Basic Windows アプリケーション プロジェクトを開きます。  
  
2. **[プロジェクト]** メニューの **[モジュールの追加]** をクリックして、プロジェクトに新しいモジュールを追加します。  
  
3. 新しいモジュールに `Module1.vb` という名前を付け、 **[追加]** をクリックします。 新しいモジュールのコードが表示されます。  
  
4. `Module` ステートメントと `End Module` ステートメントの間に `Interface TestInterface` と入力し、ENTER キーを押して、`Module1` 内に `TestInterface` という名前のインターフェイスを定義します。 **コード エディター**によって `Interface` キーワードがインデントされ、`End Interface` ステートメントが追加されて、コード ブロックが形成されます。  
  
5. `Interface` ステートメントと `End Interface` ステートメントの間に次のコードを配置して、インターフェイスのプロパティ、メソッド、およびイベントを定義します。  
  
     [!code-vb[VbVbalrOOP#98](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#98)]
  
## <a name="implementation"></a>実装

 インターフェイス メンバーを宣言するために使用する構文は、クラス メンバーを宣言するために使用する構文とは異なるので注意してください。 この差異は、インターフェイスに実装コードを含めることができないという事実を反映しています。  
  
### <a name="to-implement-the-interface"></a>インターフェイスを実装するには
  
1. `Module1` に次のステートメントを追加し、ENTER キーを押して、`ImplementationClass` という名前のクラスを追加します。追加する場所は、`End Interface` ステートメントの後で、`End Module` ステートメントの前です。  
  
     [!code-vb[VbVbalrOOP#99](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#99)]
  
     統合開発環境内で作業している場合は、ENTER キーを押すと、**コード エディター**によって対応する `End Class` ステートメントが提供されます。  
  
2. 次の `Implements` ステートメントを `ImplementationClass` に追加します。これにより、クラスで実装するインターフェイスに名前が付けられます。  
  
     [!code-vb[VbVbalrOOP#100](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#100)]
  
     `Implements` ステートメントが、クラスまたは構造体の先頭にある他の項目とは別にリストされている場合、そのステートメントは、クラスまたは構造体がインターフェイスを実装していることを示します。  
  
     統合開発環境内で作業している場合は、ENTER キーを押すと、**コード エディター**によって `TestInterface` に必要なクラス メンバーが実装され、次の手順をスキップできます。  
  
3. 統合開発環境内で作業していない場合は、`MyInterface` インターフェイスのすべてのメンバーを実装する必要があります。 次のコードを `ImplementationClass` に追加して、`Event1`、`Method1`、および `Prop1` を実装します。  
  
     [!code-vb[VbVbalrOOP#101](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#101)]
  
     `Implements` ステートメントで、実装するインターフェイスとインターフェイス メンバーの名前を指定します。  
  
4. プロパティ値を格納したプライベート フィールドをクラスに追加して、`Prop1` の定義を完了します。  
  
     [!code-vb[VbVbalrOOP#102](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#102)]
  
     プロパティの get アクセサーで `pval` の値を取得します。  
  
     [!code-vb[VbVbalrOOP#103](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#103)]
  
     プロパティの set アクセサーで `pval` の値を設定します。  
  
     [!code-vb[VbVbalrOOP#104](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#104)]
  
5. 次のコードを追加して、`Method1` の定義を完了します。  
  
     [!code-vb[VbVbalrOOP#105](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#105)]
  
### <a name="to-test-the-implementation-of-the-interface"></a>インターフェイスの実装をテストするには
  
1. **ソリューション エクスプローラー**でプロジェクトのスタートアップ フォームを右クリックし、 **[コードの表示]** をクリックします。 エディターにスタートアップ フォームのクラスが表示されます。 既定では、スタートアップ フォームは `Form1` という名前です。  
  
2. 次の `testInstance` フィールドを `Form1` クラスに追加します。  
  
     [!code-vb[VbVbalrOOP#120](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#120)]
  
     `testInstance` を `WithEvents` として宣言することで、`Form1` クラスがそのイベントを処理できるようになります。  
  
3. `testInstance` によって発生するイベントを処理するために、次のイベント ハンドラーを `Form1` クラスに追加します。  
  
     [!code-vb[VbVbalrOOP#106](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#106)]
  
4. 実装クラスをテストするために、`Test` という名前のサブルーチンを `Form1` クラスに追加します。  
  
     [!code-vb[VbVbalrOOP#107](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#107)]
  
     `Test` プロシージャは、`MyInterface` を実装するクラスのインスタンスを作成し、そのインスタンスを `testInstance` フィールドに割り当て、プロパティを設定し、インターフェイスを介してメソッドを実行します。  
  
5. スタートアップ フォームの `Form1 Load` プロシージャから `Test` プロシージャを呼び出すコードを追加します。  
  
     [!code-vb[VbVbalrOOP#108](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#108)]
  
6. F5 キーを押して、`Test` プロシージャを実行します。 "Prop1 が 9 に設定されました" というメッセージが表示されます。 [OK] をクリックします。クリック後、"The X parameter for Method1 is 5 (Method1 の X パラメーターは 5 です)" というメッセージが表示されます。 [OK] をクリックします。"The event handler caught the event (イベント ハンドラーがイベントをキャッチしました)" というメッセージが表示されます。  
  
## <a name="see-also"></a>関連項目

- [Implements ステートメント](../../../language-reference/statements/implements-statement.md)
- [インターフェイス](index.md)
- [Interface ステートメント](../../../language-reference/statements/interface-statement.md)
- [Event ステートメント](../../../language-reference/statements/event-statement.md)
