---
title: 'チュートリアル: Microsoft Expression Blend を使用してボタンを作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- buttons [WPF]
- converting [WPF], shape to button
- Expression Blend [WPF Designer]
ms.assetid: ff5037c2-bba7-4cae-8abb-6475b686c48e
ms.openlocfilehash: 10d049288cf560dadedf7bc5e624deb7c42aae81
ms.sourcegitcommit: 7bc6887ab658550baa78f1520ea735838249345e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75636173"
---
# <a name="walkthrough-create-a-button-by-using-microsoft-expression-blend"></a>チュートリアル: Microsoft Expression Blend を使用してボタンを作成する

このチュートリアルでは、Microsoft Expression Blend を使用して WPF のカスタマイズされたボタンを作成する手順について説明します。

> [!IMPORTANT]
> Microsoft Expression Blend は、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を生成することによって機能し、これがコンパイルされて実行可能プログラムが作成されます。 XAML を直接操作する場合は、Blend ではなく Visual Studio で XAML を使用して、これと同じアプリケーションを作成するもう 1 つのチュートリアルが用意されています。 詳細については、[XAML を使用したボタンの作成](walkthrough-create-a-button-by-using-xaml.md)に関する記事をご覧ください。

次の図は、作成するカスタマイズされたボタンを示しています。

![作成するカスタマイズされたボタン](./media/custom-button-blend-intro.jpg)

## <a name="convert-a-shape-to-a-button"></a>シェイプをボタンに変換する

このチュートリアルの最初の部分では、カスタム ボタンの外観を独自に作成します。 これを行うには、最初に四角形をボタンに変換します。 次に、ボタンのテンプレートにその他のシェイプを追加して、より複雑な外観のボタンを作成します。 通常のボタンから始めてそれをカスタマイズしないのはなぜでしょうか。 それは、ボタンには、不要な組み込みの機能が含まれるためです。カスタム ボタンの場合は、四角形から始める方が簡単です。

### <a name="to-create-a-new-project-in-expression-blend"></a>Expression Blend で新しいプロジェクトを作成するには

1. Expression Blend を起動します。 ( **[スタート]** をクリックし、 **[すべてのプログラム]** 、 **[Microsoft Expression]** の順にポイントして、 **[Microsoft Expression Blend]** をクリックします。)

2. 必要に応じて、アプリケーションを最大化します。

3. **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。

4. **[標準アプリケーション (.exe)]** を選択します。

5. プロジェクトに `CustomButton` という名前を指定し、 **[OK]** を押します。

この時点で、空の WPF プロジェクトが作成されます。 F5 キーを押してアプリケーションを実行できます。 ご想像のとおり、アプリケーションは空白のウィンドウだけで構成されています。 次に、角丸四角形を作成してボタンに変換します。

### <a name="to-convert-a-rectangle-to-a-button"></a>四角形をボタンに変換するには

1. **Window の Background プロパティを黒に設定する:** Window を選択し、 **[プロパティ] タブ**をクリックして、<xref:System.Windows.Controls.Control.Background%2A> プロパティを `Black` に設定します。

    ![ボタンの背景を黒に設定する方法](./media/custom-button-blend-changebackground.png)

2. **Window のボタンとほぼ同じサイズになる四角形を描画する:** 左側のツール パネルで四角形のツールを選択し、Window 上に四角形をドラッグします。

    ![四角形を描画する方法](./media/custom-button-blend-drawrect.png)

3. **四角形の角を丸める:** 四角形のコントロール ポイントをドラッグするか、<xref:System.Windows.Shapes.Rectangle.RadiusX%2A> と <xref:System.Windows.Shapes.Rectangle.RadiusY%2A> のプロパティを直接設定します。 <xref:System.Windows.Shapes.Rectangle.RadiusX%2A> と <xref:System.Windows.Shapes.Rectangle.RadiusY%2A> の値を 20 に設定します。

    ![四角形の角を丸くする方法](./media/custom-button-blend-roundcorners.png)

4. **四角形をボタンに変更する:** 四角形を選択します。 **[ツール]** メニューで **[ボタンの作成]** をクリックします。

    ![シェイプをボタンにする方法](./media/custom-button-blend-makebutton.png)

5. **スタイルまたはテンプレートの範囲を指定する:** 次のようなダイアログ ボックスが表示されます。

    ![[スタイル リソースの作成] ダイアログ ボックス](./media/custom-button-blend-makebutton2.gif)

    **[リソース名 (キー)]** には、 **[すべてに適用]** を選択します。  これにより、生成されるスタイルとボタン テンプレートが、ボタンであるすべてのオブジェクトに適用されます。 **[定義先]** には、 **[アプリケーション]** を選択します。 これにより、生成されるスタイルとボタン テンプレートの対象範囲がアプリケーション全体になります。 これらの 2 つのボックスの値を設定すると、ボタンのスタイルとテンプレートはアプリケーション全体のすべてのボタンに適用されます。また、アプリケーションで作成したすべてのボタンで、既定でこのテンプレートが使用されます。

## <a name="edit-the-button-template"></a>ボタン テンプレートを編集する

これで、ボタンに変更された四角形ができました。 このセクションでは、ボタンのテンプレートを変更し、その外観をさらにカスタマイズします。

### <a name="to-edit-the-button-template-to-change-the-button-appearance"></a>ボタン テンプレートを編集してボタンの外観を変更するには

1. **テンプレートの編集ビューに移動する:** ボタンの外観をさらにカスタマイズするには、ボタン テンプレートを編集する必要があります。 このテンプレートは、四角形をボタンに変換したときに作成されたものです。 ボタン テンプレートを編集するには、ボタンを右クリックして **[コントロール パーツ (テンプレート) の編集]** を選択し、 **[テンプレートの編集]** を選択します。

    ![テンプレートを編集する方法](./media/custom-button-blend-edittemplate.jpg)

    テンプレート エディターでは、現在、ボタンが <xref:System.Windows.Shapes.Rectangle> と <xref:System.Windows.Controls.ContentPresenter> に分割されていることがわかります。 <xref:System.Windows.Controls.ContentPresenter> は、ボタン内に内容を表示するために使用されます (たとえば、文字列 "Button")。 Rectangle と <xref:System.Windows.Controls.ContentPresenter> はどちらも <xref:System.Windows.Controls.Grid> 内にレイアウトされます。

    ![四角形に表示されるコンポーネント](./media/custom-button-blend-templatepanel.png)

2. **テンプレート コンポーネントの名前を変更する:** テンプレート インベントリ内の四角形を右クリックして、<xref:System.Windows.Shapes.Rectangle> の名前を "[Rectangle]" から "outerRectangle" に変更し、"[ContentPresenter]" を "myContentPresenter" に変更します。

    ![テンプレートのコンポーネント名を変更する方法](./media/custom-button-blend-renamecomponents.png)

3. **(ドーナツのように) 内側が空白になるように四角形を変更する:** **outerRectangle** を選択して、<xref:System.Windows.Shapes.Shape.Fill%2A> を "Transparent" に、<xref:System.Windows.Shapes.Shape.StrokeThickness%2A> を 5 に設定します。

    ![四角形を空白にする方法](./media/custom-button-blend-changerectproperties.png)

    次に、<xref:System.Windows.Shapes.Shape.Stroke%2A> を、テンプレートに設定する任意の色に設定します。 これを行うには、 **[ストローク]** の横にある小さな白いボックスをクリックし、 **[CustomExpression]** を選択して、ダイアログ ボックスに「{TemplateBinding Background}」と入力します。

    ![テンプレートの色の使用を設定する方法](./media/custom-button-blend-templatestroke.png)

4. **内部の四角形を作成する:** 次に、別の四角形を作成し ("innerRectangle" という名前を付けます)、**outerRectangle** の内部の上に対称的に配置します。 このような作業では、ズームして、編集領域のボタンのサイズを大きくすることをお勧めします。

    > [!NOTE]
    > 四角形の外観は、次の図のものとは異なる場合があります (たとえば、角が丸い場合があります)。

    ![別の四角形の中に四角形を作成する方法](./media/custom-button-blend-innerrectangleproperties.png)

5. **ContentPresenter を一番上に移動する:** この時点で、テキスト "Button" が表示されなくなる可能性があります。 そのような場合は、**innerRectangle** が **myContentPresenter** の上にあることが原因です。 これを修正するには、**myContentPresenter** を **innerRectangle** の下にドラッグします。 以下のように、四角形と **myContentPresenter** の位置を変更します。

    > [!NOTE]
    > または、**myContentPresenter** を右クリックして **[Send Forward]\(前に送る\)** を押すことで、それを一番上に配置することもできます。

    ![別のボタンの上にボタンを移動する方法](./media/custom-button-blend-innerrectangle2.png)

6. **innerRectangle の外観を変更する:** <xref:System.Windows.Shapes.Rectangle.RadiusX%2A>、<xref:System.Windows.Shapes.Rectangle.RadiusY%2A>、および <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> の値を 20 に設定します。 さらに、カスタム式 "{TemplateBinding Background}" ) を使用して <xref:System.Windows.Shapes.Shape.Fill%2A> をテンプレートの背景に設定し、<xref:System.Windows.Shapes.Shape.Stroke%2A> を "transparent" に設定します。 **innerRectangle** の <xref:System.Windows.Shapes.Shape.Fill%2A> と <xref:System.Windows.Shapes.Shape.Stroke%2A> の設定は、**outerRectangle** の設定とは逆になっていることがわかります。

    ![四角形の外観を変更する方法](./media/custom-button-blend-glassrectangleproperties1.png)

7. **上部にグラス レイヤーを追加する:** ボタンの外観をカスタマイズする最後の手順は、上部にグラス レイヤーを追加することです。 このグラス レイヤーは、3 つ目の四角形で構成されます。 グラスによってボタン全体が覆われるため、グラスの四角形のディメンションは **outerRectangle** と似たものになります。 したがって、**outerRectangle** のコピーを作成するだけで、四角形を作成できます。 **outerRectangle** を強調表示し、Ctrl + C キーと Ctrl + V キーを使用してコピーを作成します。 この新しい四角形に "glassCube" という名前を指定します。

8. **必要に応じて glassCube の位置を変更する:** **glassCube** がまだボタン全体を覆うように配置されていない場合は、その位置にドラッグします。

9. **glassCube に outerRectangle とは少し異なるシェイプを指定する:** **glassCube** のプロパティを変更します。 まず、<xref:System.Windows.Shapes.Rectangle.RadiusX%2A> と <xref:System.Windows.Shapes.Rectangle.RadiusY%2A> のプロパティを 10 に変更し、<xref:System.Windows.Shapes.Shape.StrokeThickness%2A> を 2 に変更します。

    ![glassCube の外観設定](./media/custom-button-blend-glasscubeappearance.gif)

10. **glassCube をグラスのように表示する:** <xref:System.Windows.Shapes.Shape.Fill%2A> をグラスのような外観に設定するには、75% 不透明な線状グラデーションを使用して、白色と透明を大体均等な間隔で 6 回交互に配置します。 グラデーション境界に設定するものを次に示します。

    - グラデーション境界 1:アルファ値が 75% の白

    - グラデーション境界 2:透明

    - グラデーション境界 3:アルファ値が 75% の白

    - グラデーション境界 4:透明

    - グラデーション境界 5:アルファ値が 75% の白

    - グラデーション境界 6:透明

    これにより、"波形" グラスの外観が作成されます。

    ![グラスのような四角形](./media/custom-button-blend-glassrectangleproperties2.png)

11. **グラス レイヤーを非表示にする:** グラス レイヤーの外観を確認したので、 **[プロパティ] パネル**の **[外観] ペイン**に移動し、不透明度を 0% に設定して非表示にします。 この後のセクションでは、プロパティ トリガーとイベントを使用して、グラス レイヤーの表示と操作を行います。

    ![グラス四角形を非表示にする方法](./media/custom-button-glassrectangleproperties3.gif)

## <a name="customize-the-button-behavior"></a>ボタンの動作をカスタマイズする

これまではテンプレートを編集することでボタンの表示をカスタマイズしましたが、このボタンは、通常のボタンのようにユーザーのアクションに応答することはありません (たとえば、マウスによるポイント、フォーカスの受け取り、クリックなどで外観を変更する場合)。次の 2 つの手順では、これらのような動作をカスタム ボタンに構築する方法を示します。 まずシンプルなプロパティ トリガーから始めて、次にイベント トリガーとアニメーションを追加します。

### <a name="to-set-property-triggers"></a>プロパティ トリガーを設定するには

1. **新しいプロパティ トリガーを作成する:** **glassCube** を選択した状態で、 **[トリガー]** パネルの **[+ プロパティ]** をクリックします (次の手順の後の図を参照)。 これにより、既定のプロパティ トリガーでプロパティ トリガーが作成されます。

2. **IsMouseOver をトリガーによって使用されるプロパティにする:** プロパティを <xref:System.Windows.UIElement.IsMouseOver%2A> に変更します。 これにより、<xref:System.Windows.UIElement.IsMouseOver%2A> プロパティが `true` のとき (ユーザーがマウスでボタンをポイントしたとき) にプロパティ トリガーがアクティブになります。

    ![プロパティでトリガーを設定する方法](./media/custom-button-blend-ismousedoverpropertytrigger.png)

3. **IsMouseOver で glassCube の 100% の不透明度をトリガーする:** **[Trigger recording is on]\(トリガーの記録オン\)** が表示されます (前の図を参照)。 これは、記録がオンであるときに **glassCube** のプロパティ値に加えた変更が、<xref:System.Windows.UIElement.IsMouseOver%2A> が `true` のときに行われるアクションになることを意味します。 記録中に、**glassCube** の <xref:System.Windows.UIElement.Opacity%2A> を 100% に変更します。

    ![ボタンの不透明度を設定する方法](./media/custom-button-blend-ismousedoverpropertytrigger2.gif)

    これで、最初のプロパティ トリガーを作成できました。 エディターの **[トリガー] パネル**によって、100% に変更される <xref:System.Windows.UIElement.Opacity%2A> が記録されたことがわかります。

    ![[トリガー] パネル](./media/custom-button-blend-propertytriggerinfo.png)

    F5 キーを押してアプリケーションを実行し、マウス ポインターをボタンの上と外部に移動します。 ボタンをマウスでポイントするとグラス レイヤーが表示され、ポインターが離れると消えるはずです。

4. **IsMouseOver でストローク値の変更をトリガーする:** 他のいくつかのアクションを <xref:System.Windows.UIElement.IsMouseOver%2A> トリガーに関連付けてみましょう。 記録が続いている間に、**glassCube** から **outerRectangle** に選択を切り替えます。 次に、**outerRectangle** の <xref:System.Windows.Shapes.Shape.Stroke%2A> をカスタム式 "{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" に設定します。 これにより、<xref:System.Windows.Shapes.Shape.Stroke%2A> が、ボタンによって使用される一般的な強調表示色に設定されます。 F5 キーを押して、ボタンにマウスをポイントしたときの効果を確認します。

    ![ストロークを強調表示色に設定する方法](./media/custom-button-blend-ismousedoverpropertytrigger3.png)

5. **IsMouseOver でぼやけたテキストをトリガーする:** もう 1 つのアクションを <xref:System.Windows.UIElement.IsMouseOver%2A> プロパティ トリガーに関連付けてみましょう。 ボタンの上にグラスが表示されているときに、ボタンの内容が少しぼやけて表示されるようにします。 これを行うには、ぼかしの <xref:System.Windows.Media.Effects.BitmapEffect> を <xref:System.Windows.Controls.ContentPresenter> (**myContentPresenter**) に適用します。

    ![ボタンの内容をぼかす方法](./media/custom-button-blend-propertytriggerwithbitmapeffect.png)

    > [!NOTE]
    > **[プロパティ] パネル**を <xref:System.Windows.Media.Effects.BitmapEffect> の検索を行う前の状態に戻すには、**検索ボックス**のテキストをクリアします。

    これまでに、いくつかのアクションが関連付けられたプロパティ トリガーを使用して、マウス ポインターがボタン領域に出入りするときの強調表示の動作を作成しました。 ボタンのもう 1 つの一般的な動作は、フォーカスがあるときに強調表示することです (クリックされた後など)。 このような動作を追加するには、<xref:System.Windows.UIElement.IsFocused%2A> プロパティに対するもう 1 つのプロパティ トリガーを追加します。

6. **IsFocused のプロパティ トリガーを作成する:** <xref:System.Windows.UIElement.IsMouseOver%2A> の場合と同じ手順 (このセクションの最初の手順を参照) を使用して、<xref:System.Windows.UIElement.IsFocused%2A> プロパティに対するもう 1 つのプロパティ トリガーを作成します。 **[Trigger recording is on]\(トリガーの記録オン\)** の状態で、次のアクションをトリガーに追加します。

    - **glassCube** の <xref:System.Windows.UIElement.Opacity%2A> を 100% にする。

    - **outerRectangle** の <xref:System.Windows.Shapes.Shape.Stroke%2A> カスタム式の値を "{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" にする。

このチュートリアルの最後の手順として、ボタンにアニメーションを追加します。 これらのアニメーションは、イベント (具体的には、<xref:System.Windows.UIElement.MouseEnter> イベントと <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント) によってトリガーされます。

### <a name="to-use-event-triggers-and-animations-to-add-interactivity"></a>イベント トリガーとアニメーションを使用してインタラクティビティを追加するには

1. **MouseEnter イベント トリガーを作成する:** 新しいイベント トリガーを追加し、トリガーで使用するイベントとして [<xref:System.Windows.UIElement.MouseEnter>] を選択します。

     ![MouseEnter イベント トリガーを作成する方法](./media/custom-button-blend-mouseovereventtrigger.png)

2. **アニメーション タイムラインを作成する:** 次に、アニメーション タイムラインを <xref:System.Windows.UIElement.MouseEnter> イベントに関連付けます。

    ![アニメーション タイムラインをイベントに追加する方法](./media/custom-button-blend-mouseovereventtrigger2.png)

    **[OK]** を押して新しいタイムラインを作成すると、**タイムライン パネル**が表示され、デザインパネルに [Timeline recording is on]\(タイムラインの記録オン\) が表示されます。 これは、タイムラインでプロパティの変更の記録を開始できることを意味します (プロパティの変更をアニメーション化)。

    > [!NOTE]
    > 表示内容を確認するために、ウィンドウやパネルのサイズを変更する必要がある場合があります。

    ![タイムライン パネル](./media/custom-button-blend-mouseovereventtrigger3.png)

3. **キーフレームを作成する:** アニメーションを作成するには、アニメーション化するオブジェクトを選択し、タイムライン上に複数のキーフレームを作成します。また、これらのキーフレームの間には、アニメーションで補間するプロパティ値を設定します。 次の図は、キーフレームを作成する手順を示しています。

    ![キーフレームを作成する方法](./media/custom-button-blend-mouseovereventtrigger4.png)

4. **このキーフレームで glassCube を縮小する:** 2 番目のキーフレームを選択した状態で、**サイズ変換**を使用して、**glassCube** のサイズをフル サイズの 90% に縮小します。

    ![ボタンのサイズを縮小する方法](./media/custom-button-blend-sizetransform.png)

    F5 キーを押してアプリケーションを実行します。 マウス ポインターをボタンの上に移動します。 ボタンの上のグラス レイヤーが縮小されることがわかります。

5. **もう 1 つのイベント トリガーを作成し、別のアニメーションを関連付ける:** もう 1 つアニメーションを追加してみましょう。 前のイベント トリガー アニメーションの作成に使用したものと同様の手順を使用します。

    1. <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントを使用して、新しいイベント トリガーを作成します。

    2. 新しいタイムラインを <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントに関連付けます。

        ![新しいタイムラインを作成する方法](./media/custom-button-blend-clickeventtrigger1.png)

    3. このタイムラインに対して、2 つのキーフレームを作成します。1 つ目は 0.0 秒、2 つ目は 0.3 秒にします。ｌ

    4. 0\.3 秒のキーフレームが強調表示されている状態で、**回転変換の角度**を 360 度に設定します。

        ![回転変換を作成する方法](./media/custom-button-blend-rotatetransform.gif)

    5. F5 キーを押してアプリケーションを実行します。 ボタンをクリックします。 グラス レイヤーが回転することがわかります。

## <a name="conclusion"></a>まとめ

これでカスタマイズしたボタンが完成しました。 これを行うためにボタン テンプレートを使用しました。これは、アプリケーション内のすべてのボタンに適用されました。 テンプレート編集モードを終了して (次の図を参照) さらにボタンを作成すると、それらは既定のボタンではなく、カスタム ボタンのような外観と動作を持つことが確認できます。

![カスタム ボタン テンプレート](./media/custom-button-blend-scopeup.gif)

![同じテンプレートを使用する複数のボタン](./media/custom-button-blend-createmultiplebuttons.png)

F5 キーを押してアプリケーションを実行します。 ボタンをクリックして、すべての動作が同じであることを確認します。

テンプレートをカスタマイズしている間に、**innerRectangle** の <xref:System.Windows.Shapes.Shape.Fill%2A> プロパティと **outerRectangle** の <xref:System.Windows.Shapes.Shape.Stroke%2A> プロパティをテンプレートの背景 ({TemplateBinding Background}) に設定したことを思い出してください。 このため、個々のボタンの背景色を設定すると、設定した背景がそのそれぞれのプロパティに使用されます。 今すぐ背景を変更してみてください。 次の図では、さまざまなグラデーションが使用されています。 したがって、テンプレートはボタンのようなコントロールを全体的にカスタマイズする場合に便利ですが、テンプレートを使用したコントロールは互いに異なる外観に変更される可能性があります。

![外観が異なる、同じテンプレートを使用したボタン](./media/custom-button-blend-blendconclusion.jpg "custom_button_blend_BlendConclusion")

結論として、ボタン テンプレートをカスタマイズするプロセスを通じて、Microsoft Expression Blend で次の操作を行う方法を学習しました。

- コントロールの外観をカスタマイズする。

- プロパティ トリガーを設定する。 プロパティ トリガーは、コントロールだけでなく、ほとんどのオブジェクトで使用できるため、非常に便利です。

- イベント トリガーを設定する。 イベント トリガーは、コントロールだけでなく、ほとんどのオブジェクトで使用できるため、非常に便利です。

- アニメーションを作成する。

- その他: グラデーションの作成、BitmapEffects の追加、変換の使用、オブジェクトの基本プロパティの設定。

## <a name="see-also"></a>関連項目

- [XAML を使用したボタンの作成](walkthrough-create-a-button-by-using-xaml.md)
- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [アニメーションの概要](../graphics-multimedia/animation-overview.md)
- [純色およびグラデーションによる塗りつぶしの概要](../graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)
- [ビットマップ効果の概要](../graphics-multimedia/bitmap-effects-overview.md)
