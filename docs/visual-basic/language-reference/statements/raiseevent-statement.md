---
title: RaiseEvent ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.RaiseEventMethod
- vb.RaiseEvent
- RaiseEvent
helpviewer_keywords:
- raising events [Visual Basic], RaiseEvent statement
- RaiseEvent statement [Visual Basic]
- event handlers, connecting events to
ms.assetid: f82e380a-1e6b-4047-bea8-c853f4d2c742
ms.openlocfilehash: 46b93c060a12d82b34dafdf3aa4ea677df6f54cd
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404292"
---
# <a name="raiseevent-statement"></a>RaiseEvent ステートメント
クラス、フォーム、またはドキュメント内のモジュール レベルで宣言されたイベントをトリガーします。  
  
## <a name="syntax"></a>構文  
  
```vb  
RaiseEvent eventname[( argumentlist )]  
```  
  
## <a name="parts"></a>指定項目  
 `eventname`  
 必須です。 トリガーするイベントの名前です。  
  
 `argumentlist`  
 任意。 変数、配列、または式のコンマ区切りのリストです。 `argumentlist` 引数はかっこで囲む必要があります。 引数がない場合は、かっこを省略する必要があります。  
  
## <a name="remarks"></a>Remarks  
 必須の `eventname` は、モジュール内で宣言されたイベントの名前です。 Visual Basic 変数の名前付け規則に従います。  
  
 イベントが発生するモジュール内でそれが宣言されていない場合は、エラーが発生します。 次のコード フラグメントは、イベントの宣言と、イベントが発生するプロシージャを示しています。  
  
 [!code-vb[VbVbalrEvents#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#37)]  
  
 モジュール内で明示的に宣言されていないイベントを、`RaiseEvent` を使用して発生させることはできません。 たとえば、すべてのフォームが <xref:System.Windows.Forms.Form?displayProperty=nameWithType> から <xref:System.Windows.Forms.Control.Click> イベントを継承している場合、それを派生フォーム内の `RaiseEvent` を使用して発生させることはできません。 フォーム モジュール内で `Click` イベントを宣言すると、それによってフォーム独自の <xref:System.Windows.Forms.Control.Click> イベントはシャドウされます。 それでも、そのフォームの <xref:System.Windows.Forms.Control.Click> イベントは、<xref:System.Windows.Forms.Control.OnClick%2A> メソッドを呼び出すことで呼び出すことができます。  
  
 既定では、Visual Basic で定義されたイベントはそのイベント ハンドラーを、接続が確立された順に発生させます。 イベントには `ByRef` パラメーターを含めることができるため、遅れて接続するプロセスでは、先行するイベント ハンドラーによって変更されたパラメーターを受け取る場合があります。 イベント ハンドラーが実行されると、イベントを発生させたサブルーチンに制御が返されます。  
  
> [!NOTE]
> 非共有イベントは、それらが宣言されているクラスのコンストラクター内で発生させないでください。 このようなイベントが実行時エラーの原因となることはありませんが、関連付けられたイベント ハンドラーでキャッチされない場合があります。 コンストラクターからイベントを発生させる必要がある場合は、`Shared` 修飾子を使用して共有イベントを作成します。  
  
> [!NOTE]
> イベントの既定の動作を変更するには、カスタム イベントを定義します。 カスタム イベントの場合は、`RaiseEvent` ステートメントによってイベントの `RaiseEvent` アクセサーが呼び出されます。 カスタム イベントの詳細については、「[Event ステートメント](event-statement.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、イベントを使用して 10 秒から 0 秒までカウント ダウンします。 このコードは、イベント関連のいくつかのメソッド、プロパティ、およびステートメント (`RaiseEvent` など) の例を示しています。  
  
 イベントを発生させるクラスをイベント ソース、イベントを処理するメソッドをイベント ハンドラーと呼びます。 イベント ソースでは、生成されるイベントに対して複数のイベント ハンドラーを設定できます。 クラスでイベントが発生すると、そのイベントは、オブジェクトのインスタンスに対するイベントを処理するために選択されたすべてのクラスで発生します。  
  
 また、この例では、ボタン (`Button1`) とテキスト ボックス (`TextBox1`) を含んだフォーム (`Form1`) も使用しています。 ボタンをクリックすると、1 つ目のテキスト ボックスに 10 秒から 0 秒までのカウントダウンが表示されます。 カウントダウンが終わると (10 秒が経過すると)、1 つ目のテキスト ボックスに "Done" と表示されます。  
  
 `Form1` のコードでは、フォームの初期状態と終了状態を指定しています。 イベント発生時に実行されるコードも含まれています。  
  
 この例を使用するには、新しい Windows アプリケーション プロジェクトを開き、`Button1` という名前のボタンと、`TextBox1` という名前のテキスト ボックスを、`Form1` という名前のメイン フォームに追加します。 続いてフォームを右クリックし、 **[コードの表示]** をクリックしてコード エディターを開きます。  
  
 `Form1` クラスの宣言セクションに、`WithEvents` 変数を追加します。  
  
 [!code-vb[VbVbalrEvents#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#14)]  
  
## <a name="example"></a>例  
 `Form1` のコードに次のコードを追加します。 `Form_Load` や `Button_Click` など、重複して存在する可能性のあるプロシージャを置き換えます。  
  
 [!code-vb[VbVbalrEvents#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#15)]  
  
 F5 キーを押して上の例を実行し、**Start** というラベルのボタンをクリックします。 最初のテキスト ボックスで、秒のカウント ダウンが開始されます。 カウントダウンが終わると (10 秒が経過すると)、1 つ目のテキスト ボックスに "Done" と表示されます。  
  
> [!NOTE]
> `My.Application.DoEvents` メソッドがイベントを処理する方法は、フォームによる方法とは一部異なります。 フォームでイベントを直接処理できるようにするには、マルチスレッドを使用します。 詳細については、「[マネージド スレッド処理](../../../standard/threading/index.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [イベント](../../programming-guide/language-features/events/index.md)
- [Event ステートメント](event-statement.md)
- [AddHandler ステートメント](addhandler-statement.md)
- [RemoveHandler ステートメント](removehandler-statement.md)
- [Handles](handles-clause.md)
