---
title: 'チュートリアル: COM オブジェクトによる継承の実装'
ms.date: 07/20/2015
helpviewer_keywords:
- inheritance [Visual Basic], COM reusability
- base classes [Visual Basic], COM reusability
- inheritance [Visual Basic], walkthroughs
- derived classes [Visual Basic], COM reusability
ms.assetid: f8e7263a-de13-48d1-b67c-ca1adf3544d9
ms.openlocfilehash: bdb891e1a150f0d7b79aefcc3db1f18dc8e84be4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396728"
---
# <a name="walkthrough-implementing-inheritance-with-com-objects-visual-basic"></a>チュートリアル: COM オブジェクトによる継承の実装 (Visual Basic)

以前のバージョンの Visual Basic で作成されたものでも、COM オブジェクトの `Public` クラスから Visual Basic クラスを派生させることができます。 COM オブジェクトから継承されたクラスのプロパティとメソッドは、他の基底クラスのプロパティとメソッドがオーバーライドまたはオーバーロードできるのと同様に、オーバーライドまたはオーバーロードできます。 COM オブジェクトからの継承は、再コンパイルしたくない既存のクラス ライブラリがある場合に便利です。

次の手順では、Visual Basic 6.0 を使用してクラスを含む COM オブジェクトを作成してから、それを基底クラスとして使用する方法を示します。

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-build-the-com-object-that-is-used-in-this-walkthrough"></a>このチュートリアルで使用する COM オブジェクトをビルドするには

1. Visual Basic 6.0 で、新しい ActiveX DLL プロジェクトを開きます。 `Project1` という名前のプロジェクトが作成されます。 これには `Class1` という名前のクラスが含まれています。

2. **プロジェクト エクスプローラー**で **[Project1]** を右クリックし、 **[Project1 Properties] (Project1 のプロパティ)** をクリックします。 **[プロジェクトのプロパティ]** ダイアログ ボックスが表示されます。

3. **[プロジェクトのプロパティ]** ダイアログ ボックスの **[全般]** タブで、 **[プロジェクト名]** フィールドに「`ComObject1`」と入力してプロジェクト名を変更します。

4. **プロジェクト エクスプローラー**で `Class1` を右クリックし、 **[プロパティ]** をクリックします。 クラスの **[プロパティ]** ウィンドウが表示されます。

5. `Name` プロパティを `MathFunctions` に変更します。

6. **プロジェクト エクスプローラー**で `MathFunctions` を右クリックし、 **[コードの表示]** をクリックします。 **[コード エディター]** が表示されます。

7. プロパティ値を保持するためにローカル変数を追加します。

    ```vb
    ' Local variable to hold property value
    Private mvarProp1 As Integer
    ```

8. Property `Let` と Property `Get` のプロパティ プロシージャを追加します。

    ```vb
    Public Property Let Prop1(ByVal vData As Integer)
       'Used when assigning a value to the property.
       mvarProp1 = vData
    End Property
    Public Property Get Prop1() As Integer
       'Used when retrieving a property's value.
       Prop1 = mvarProp1
    End Property
    ```

9. 関数を追加します。

    ```vb
    Function AddNumbers(
       ByVal SomeNumber As Integer,
       ByVal AnotherNumber As Integer) As Integer

       AddNumbers = SomeNumber + AnotherNumber
    End Function
    ```

10. **[ファイル]** メニューの **[Make ComObject1.dll] (ComObject1 の作成)** をクリックして、COM オブジェクトを作成して登録します。

    > [!NOTE]
    > Visual Basic で作成されたクラスを COM オブジェクトとして公開することもできますが、これは真の COM オブジェクトではなく、このチュートリアルでは使用できません。 詳細については、「[.NET Framework アプリケーションにおける COM 相互運用性](com-interoperability-in-net-framework-applications.md)」を参照してください。

## <a name="interop-assemblies"></a>相互運用機能アセンブリ

次の手順では、アンマネージ コード (COM オブジェクトなど) と Visual Studio で使用されるマネージド コードの間のブリッジとして機能する相互運用機能アセンブリを作成します。 Visual Basic で作成される相互運用機能アセンブリは、COM オブジェクトの操作の多くの詳細情報を処理します。たとえば、*相互運用マーシャリング*、COM オブジェクトとの間で移動するときに、パラメーターと戻り値を同等のデータ型にパッケージ化するプロセスなどです。 Visual Basic アプリケーション内の参照は、実際の COM オブジェクトではなく、相互運用機能アセンブリを指します。

### <a name="to-use-a-com-object-with-visual-basic-2005-and-later-versions"></a>Visual Basic 2005 以降のバージョンで COM オブジェクトを使用するには

1. 新しい Visual Basic Windows アプリケーション プロジェクトを開きます。

2. **[プロジェクト]** メニューの **[参照の追加]** をクリックします。

     **[参照の追加]** ダイアログ ボックスが表示されます。

3. **[COM]** タブで、 **[コンポーネント名]** の一覧で `ComObject1` をダブルクリックし、 **[OK]** をクリックします。

4. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

     **[新しい項目の追加]** ダイアログ ボックスが表示されます。

5. **[テンプレート]** ウィンドウで **[クラス]** をクリックします。

     `Class1.vb`[名前]**フィールドに既定のファイル名** が表示されます。 このフィールドを MathClass.vb に変更し、 **[追加]** をクリックします。 これにより `MathClass` という名前のクラスが作成され、そのコードが表示されます。

6. COM クラスを継承するために、`MathClass` の先頭に次のコードを追加します。

     [!code-vb[VbVbalrInterop#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#31)]

7. `MathClass` に次のコードを追加して、基底クラスのパブリック メソッドをオーバーロードします。

     [!code-vb[VbVbalrInterop#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#32)]

8. 次のコードを `MathClass` に追加して、継承されたクラスを拡張します。

     [!code-vb[VbVbalrInterop#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#33)]

新しいクラスは、COM オブジェクトの基底クラスのプロパティを継承し、メソッドをオーバーロードして、クラスを拡張する新しいメソッドを定義します。

### <a name="to-test-the-inherited-class"></a>継承されたクラスをテストするには

1. スタートアップ フォームにボタンを追加し、それをダブルクリックしてコードを表示します。

2. ボタンの `Click` イベント ハンドラー プロシージャに次のコードを追加して、`MathClass` のインスタンスを作成し、オーバーロードされたメソッドを呼び出します。

     [!code-vb[VbVbalrInterop#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#34)]

3. F5 キーを押して、プロジェクトを実行します。

フォームのボタンをクリックすると、`AddNumbers` メソッドが最初に `Short` データ型の数値で呼び出され、Visual Basic で基底クラスから適切なメソッドが選択されます。 `AddNumbers` の 2 回目の呼び出しは `MathClass` からのオーバーロード メソッドに送られます。 3 回目の呼び出しは、クラスを拡張する `SubtractNumbers` メソッドを呼び出します。 基底クラスのプロパティが設定され、値が表示されます。

## <a name="next-steps"></a>次の手順

オーバーロードされた `AddNumbers` 関数が、COM オブジェクトの基底クラスから継承されたメソッドと同じデータ型を持つように見えることに気付いたかもしれません。 これは、基底クラスのメソッドの引数とパラメーターが Visual Basic 6.0 では 16 ビット整数として定義されているのに対し、以降のバージョンの Visual Basic では型 `Short` の 16 ビット整数として公開されているためです。 新しい関数は、32 ビットの整数を受け入れ、基底クラスの関数をオーバーロードします。

COM オブジェクトを使用する場合は、パラメーターのサイズとデータ型を必ず確認してください。 たとえば、引数として Visual Basic 6.0 コレクション オブジェクトを受け入れる COM オブジェクトを使用している場合、以降のバージョンの Visual Basic のコレクションを指定することはできません。

COM クラスから継承されたプロパティとメソッドは、オーバーライドすることができます。つまり、基底の COM クラスから継承されたプロパティまたはメソッドを置き換えるローカル プロパティまたはメソッドを宣言できます。 継承された COM プロパティをオーバーライドするためのルールは、次の例外を除き、他のプロパティおよびメソッドをオーバーライドするためのルールに似ています。

- COM クラスから継承されたプロパティまたはメソッドをオーバーライドする場合は、継承された他のすべてのプロパティとメソッドをオーバーライドする必要があります。

- `ByRef` パラメーターを使用するプロパティをオーバーライドすることはできません。

## <a name="see-also"></a>関連項目

- [.NET Framework アプリケーションにおける COM 相互運用性](com-interoperability-in-net-framework-applications.md)
- [Inherits ステートメント](../../language-reference/statements/inherits-statement.md)
- [Short データ型](../../language-reference/data-types/short-data-type.md)
