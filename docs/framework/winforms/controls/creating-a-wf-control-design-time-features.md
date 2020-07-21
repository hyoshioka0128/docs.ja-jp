---
title: Visual Studio のデザイン時機能を利用するコントロールを作成する
description: デザイン時機能を利用する Windows フォームでカスタムコントロールのカスタムデザイナーを作成する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows Forms controls, creating
- design-time functionality [Windows Forms], Windows Forms
- DocumentDesigner class [Windows Forms]
- walkthroughs [Windows Forms], controls
ms.assetid: 6f487c59-cb38-4afa-ad2e-95edacb1d626
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 03c04578ecb01b689f58d41a46eef5793fb1182c
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85613911"
---
# <a name="walkthrough-create-a-control-that-takes-advantage-of-design-time-features"></a>チュートリアル: デザイン時機能を活用したコントロールの作成

カスタムコントロールのデザイン時のエクスペリエンスは、関連するカスタムデザイナーを作成することによって拡張できます。

この記事では、カスタムコントロールのカスタムデザイナーを作成する方法について説明します。 `MarqueeControl`型とという名前の関連付けられたデザイナークラスを実装し `MarqueeControlRootDesigner` ます。

この型は、アニメーション化さ `MarqueeControl` れたライトと点滅するテキストを含むシアターマーキーに似た表示を実装します。

このコントロールのデザイナーは、デザイン時のカスタムエクスペリエンスを提供するために、デザイン環境と対話します。 カスタムデザイナーを使用すると、アニメーション化さ `MarqueeControl` れたライトと、さまざまな組み合わせで点滅するテキストを使用して、カスタム実装を組み立てることができます。 アセンブルされたコントロールは、他の Windows フォームコントロールと同様に、フォーム上で使用できます。

このチュートリアルを終了すると、カスタムコントロールは次のようになります。

![テキストと [開始] および [停止] ボタンを示すマーキーを表示するアプリ。](./media/creating-a-wf-control-design-time-features/demo-marquee-control.gif)

完全なコードリストについては、「[方法: デザイン時機能を利用する Windows フォームコントロールを作成](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/307hck25(v=vs.120))する」を参照してください。

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、Visual Studio が必要です。

## <a name="create-the-project"></a>プロジェクトの作成

最初にアプリケーションのプロジェクトを作成します。 このプロジェクトは、カスタムコントロールをホストするアプリケーションをビルドするために使用します。

Visual Studio で、新しい Windows フォームアプリケーションプロジェクトを作成し、 **MarqueeControlTest**という名前を指定します。

## <a name="create-the-control-library-project"></a>コントロールライブラリプロジェクトを作成する

1. ソリューションに Windows フォームコントロールライブラリプロジェクトを追加します。 プロジェクトに**MarqueeControlLibrary**という名前を指定します。

2. **ソリューションエクスプローラー**を使用して、選択した言語に応じて、"UserControl1.cs" または "UserControl1" という名前のソースファイルを削除して、プロジェクトの既定のコントロールを削除します。

3. 新しい項目を <xref:System.Windows.Forms.UserControl> プロジェクトに追加 `MarqueeControlLibrary` します。 新しいソースファイルに**MarqueeControl**のベース名を指定します。

4. **ソリューションエクスプローラー**を使用して、プロジェクトに新しいフォルダーを作成し `MarqueeControlLibrary` ます。

5. **Design**フォルダーを右クリックし、新しいクラスを追加します。 **MarqueeControlRootDesigner**という名前を指定します。

6. System.string アセンブリの型を使用する必要があるため、この参照をプロジェクトに追加し `MarqueeControlLibrary` ます。

## <a name="reference-the-custom-control-project"></a>カスタムコントロールプロジェクトを参照する

`MarqueeControlTest`カスタムコントロールをテストするには、プロジェクトを使用します。 アセンブリにプロジェクト参照を追加すると、テストプロジェクトはカスタムコントロールを認識するようになり `MarqueeControlLibrary` ます。

プロジェクトで `MarqueeControlTest` 、アセンブリへのプロジェクト参照を追加し `MarqueeControlLibrary` ます。 アセンブリを直接参照するのではなく、[**参照の追加**] ダイアログボックスの [**プロジェクト**] タブを使用するようにしてください `MarqueeControlLibrary` 。

## <a name="define-a-custom-control-and-its-custom-designer"></a>カスタムコントロールとそのカスタムデザイナーを定義する

カスタムコントロールはクラスから派生 <xref:System.Windows.Forms.UserControl> します。 これにより、コントロールに他のコントロールを含めることができます。また、コントロールには、既定の機能が多数用意されています。

カスタムコントロールには、関連付けられたカスタムデザイナーがあります。 これにより、カスタムコントロール専用にカスタマイズされた独自のデザインエクスペリエンスを作成できます。

コントロールをデザイナーに関連付けるには、クラスを使用し <xref:System.ComponentModel.DesignerAttribute> ます。 カスタムコントロールのデザイン時動作全体を開発しているため、カスタムデザイナーはインターフェイスを実装し <xref:System.ComponentModel.Design.IRootDesigner> ます。

### <a name="to-define-a-custom-control-and-its-custom-designer"></a>カスタムコントロールとそのカスタムデザイナーを定義するには

1. `MarqueeControl`**コードエディター**でソースファイルを開きます。 ファイルの先頭に、次の名前空間をインポートします。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#220](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#220)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#220](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#220)]

2. を <xref:System.ComponentModel.DesignerAttribute> クラス宣言に追加し `MarqueeControl` ます。 これにより、カスタムコントロールがデザイナーに関連付けられます。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#240](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#240)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#240](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#240)]

3. `MarqueeControlRootDesigner`**コードエディター**でソースファイルを開きます。 ファイルの先頭に、次の名前空間をインポートします。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#520](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#520)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#520](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#520)]

4. `MarqueeControlRootDesigner`クラスを継承するようにの宣言を変更し <xref:System.Windows.Forms.Design.DocumentDesigner> ます。 を適用して、 <xref:System.ComponentModel.ToolboxItemFilterAttribute> デザイナーと**ツールボックス**の対話を指定します。

   > [!NOTE]
   > クラスの定義は、 `MarqueeControlRootDesigner` MarqueeControlLibrary という名前空間で囲まれています。 この宣言により、デザイン関連の型用に予約された特殊な名前空間にデザイナーが配置されます。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#530](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#530)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#530](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#530)]

5. クラスのコンストラクターを定義し `MarqueeControlRootDesigner` ます。 <xref:System.Diagnostics.Trace.WriteLine%2A>コンストラクター本体にステートメントを挿入します。 これはデバッグに役立ちます。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#540](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#540)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#540](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#540)]

## <a name="create-an-instance-of-your-custom-control"></a>カスタムコントロールのインスタンスを作成する

1. 新しい項目を <xref:System.Windows.Forms.UserControl> プロジェクトに追加 `MarqueeControlTest` します。 新しいソースファイルに**DemoMarqueeControl**のベース名を指定します。

2. `DemoMarqueeControl`**コードエディター**でファイルを開きます。 ファイルの先頭に、名前空間をインポートし `MarqueeControlLibrary` ます。

   ```vb
   Imports MarqueeControlLibrary
   ```

   ```csharp
   using MarqueeControlLibrary;
   ```

3. `DemoMarqueeControl`クラスを継承するようにの宣言を変更し `MarqueeControl` ます。

4. プロジェクトをビルドします。

5. Windows フォームデザイナーで Form1 を開きます。

6. **ツールボックス**の [ **MarqueeControlTest Components** ] タブを見つけて開きます。 `DemoMarqueeControl`**ツールボックス**からフォームにをドラッグします。

7. プロジェクトをビルドします。

## <a name="set-up-the-project-for-design-time-debugging"></a>デザイン時デバッグ用にプロジェクトを設定する

カスタムデザイン時のエクスペリエンスを開発している場合は、コントロールとコンポーネントをデバッグする必要があります。 デザイン時にデバッグを許可するようにプロジェクトを設定する簡単な方法があります。 詳細については、「[チュートリアル: デザイン時のカスタム Windows フォームコントロールのデバッグ](walkthrough-debugging-custom-windows-forms-controls-at-design-time.md)」を参照してください。

1. プロジェクトを右クリック `MarqueeControlLibrary` し、[**プロパティ**] を選択します。

2. [ **MarqueeControlLibrary プロパティページ**] ダイアログボックスで、[**デバッグ**] ページを選択します。

3. [**開始アクション**] セクションで、[**外部プログラムの開始**] を選択します。 Visual Studio の別のインスタンスをデバッグする場合は、[visual studio のプロパティウィンドウ] の省略記号ボタン ([...]) をクリックして、 ![ ](./media/visual-studio-ellipsis-button.png) VISUAL studio IDE を参照します。 実行可能ファイルの名前は devenv.exe であり、を既定の場所にインストールした場合、そのパスは *% ProgramFiles (x86)% \ Microsoft Visual Studio\2019 \\ \<edition>\Common7\IDE\devenv.exe*になります。

4. **[OK]** を選択してダイアログ ボックスを閉じます。

5. MarqueeControlLibrary プロジェクトを右クリックし、[**スタートアッププロジェクトに設定**] を選択して、このデバッグ構成を有効にします。

## <a name="checkpoint"></a>Checkpoint

これで、カスタムコントロールのデザイン時動作をデバッグする準備ができました。 デバッグ環境が正しく設定されていることを確認したら、カスタムコントロールとカスタムデザイナーの関連付けをテストします。

### <a name="to-test-the-debugging-environment-and-the-designer-association"></a>デバッグ環境とデザイナーの関連付けをテストするには

1. **コードエディター**で MarqueeControlRootDesigner ソースファイルを開き、ステートメントにブレークポイントを設定し <xref:System.Diagnostics.Trace.WriteLine%2A> ます。

2. **F5**キーを押してデバッグセッションを開始します。

   Visual Studio の新しいインスタンスが作成されます。

3. Visual Studio の新しいインスタンスで、MarqueeControlTest ソリューションを開きます。 [**ファイル**] メニューから [**最近使ったプロジェクト**] を選択すると、ソリューションを簡単に見つけることができます。 MarqueeControlTest ソリューションファイルは、最近使用したファイルとして一覧表示されます。

4. `DemoMarqueeControl`デザイナーでを開きます。

   Visual Studio のデバッグインスタンスによってフォーカスが取得され、ブレークポイントで実行が停止します。 **F5**キーを押してデバッグセッションを続行します。

この時点で、カスタムコントロールとそれに関連付けられているカスタムデザイナーを開発およびデバッグするために、すべてが準備されています。 この記事の残りの部分では、コントロールとデザイナーの機能を実装する方法の詳細について説明します。

## <a name="implement-the-custom-control"></a>カスタムコントロールを実装する

は、 `MarqueeControl` <xref:System.Windows.Forms.UserControl> カスタマイズが少ししかないです。 ここでは、2つのメソッドを公開しています。は `Start` 、マーキーアニメーションを開始し、はアニメーションを停止します。 `Stop` には、インターフェイスを実装する子コントロールが含まれているため、それぞれの子コントロールを列挙し、を `MarqueeControl` `IMarqueeWidget` `Start` `Stop` `StartMarquee` `StopMarquee` 実装する各子コントロールで、それぞれのメソッドとメソッドをそれぞれ呼び出し `IMarqueeWidget` ます。

`MarqueeBorder`コントロールとコントロールの外観 `MarqueeText` は、レイアウトに依存しているため、 `MarqueeControl` <xref:System.Windows.Forms.Control.OnLayout%2A> メソッドをオーバーライドし、 <xref:System.Windows.Forms.Control.PerformLayout%2A> この型の子コントロールに対してを呼び出します。

これはカスタマイズの範囲です `MarqueeControl` 。 実行時の機能はコントロールとコントロールによって実装され、 `MarqueeBorder` `MarqueeText` デザイン時の機能はクラスおよびクラスによって実装され `MarqueeBorderDesigner` `MarqueeControlRootDesigner` ます。

### <a name="to-implement-your-custom-control"></a>カスタムコントロールを実装するには

1. `MarqueeControl`**コードエディター**でソースファイルを開きます。 `Start`メソッドとメソッドを実装し `Stop` ます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#260](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#260)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#260](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#260)]

2. <xref:System.Windows.Forms.Control.OnLayout%2A> メソッドをオーバーライドします。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#270](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#270)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#270](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#270)]

## <a name="create-a-child-control-for-your-custom-control"></a>カスタムコントロールの子コントロールを作成する

は、 `MarqueeControl` `MarqueeBorder` コントロールとコントロールという2種類の子コントロールをホストします `MarqueeText` 。

- `MarqueeBorder`: このコントロールは、端の周りに "ライト" の境界線を描画します。 ライトが連続して点滅しているように見えます。 ライトフラッシュがというプロパティによって制御される速度 `UpdatePeriod` 。 他のいくつかのカスタムプロパティによって、コントロールの外観の他の側面が決まります。 と呼ばれる2つのメソッドは、 `StartMarquee` `StopMarquee` アニメーションの開始と停止を制御します。

- `MarqueeText`: このコントロールは、点滅する文字列を描画します。 コントロールと同様に、 `MarqueeBorder` テキストが点滅する速度は、プロパティによって制御され `UpdatePeriod` ます。 コントロールには、 `MarqueeText` `StartMarquee` `StopMarquee` コントロールに共通のメソッドとメソッドもあり `MarqueeBorder` ます。

デザイン時に、を使用すると、 `MarqueeControlRootDesigner` これら2つのコントロール型を任意の組み合わせでに追加でき `MarqueeControl` ます。

2つのコントロールの共通機能は、と呼ばれるインターフェイスに分けられてい `IMarqueeWidget` ます。 これにより、は、 `MarqueeControl` マーキーに関連する子コントロールを検出し、特別な処理を行うことができます。

定期的なアニメーション機能を実装するには、 <xref:System.ComponentModel.BackgroundWorker> 名前空間のオブジェクトを使用し <xref:System.ComponentModel?displayProperty=nameWithType> ます。 オブジェクトを使用することもでき <xref:System.Windows.Forms.Timer> ますが、多くの `IMarqueeWidget` オブジェクトが存在する場合、1つの UI スレッドがアニメーションを維持できないことがあります。

### <a name="to-create-a-child-control-for-your-custom-control"></a>カスタムコントロールの子コントロールを作成するには

1. 新しいクラス項目をプロジェクトに追加 `MarqueeControlLibrary` します。 新しいソースファイルに "IMarqueeWidget" のベース名を指定します。

2. `IMarqueeWidget`**コードエディター**でソースファイルを開き、宣言をからに変更 `class` し `interface` ます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/imarqueewidget.cs#2)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/imarqueewidget.vb#2)]

3. 次のコードをインターフェイスに追加して、 `IMarqueeWidget` 2 つのメソッドと、マーキーアニメーションを操作するプロパティを公開します。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/imarqueewidget.cs#3)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/imarqueewidget.vb#3)]

4. 新しい**カスタムコントロール**項目をプロジェクトに追加 `MarqueeControlLibrary` します。 新しいソースファイルに "MarqueeText" のベース名を指定します。

5. コンポーネントを <xref:System.ComponentModel.BackgroundWorker> **ツールボックス**からコントロールにドラッグし `MarqueeText` ます。 このコンポーネントを使用すると、 `MarqueeText` コントロール自体を非同期的に更新できます。

6. [**プロパティ**] ウィンドウで、 <xref:System.ComponentModel.BackgroundWorker> コンポーネントの `WorkerReportsProgress` プロパティと <xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A> プロパティを**true**に設定します。 これらの設定により、 <xref:System.ComponentModel.BackgroundWorker> コンポーネントは定期的にイベントを発生させ、非同期更新を取り消すことができ <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> ます。

   詳細については、「 [BackgroundWorker Component](backgroundworker-component.md)」を参照してください。

7. `MarqueeText`**コードエディター**でソースファイルを開きます。 ファイルの先頭に、次の名前空間をインポートします。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#120](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#120)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#120](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#120)]

8. を継承し、インターフェイスを実装するように、の宣言を変更 `MarqueeText` <xref:System.Windows.Forms.Label> し `IMarqueeWidget` ます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#130](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#130)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#130](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#130)]

9. 公開されたプロパティに対応するインスタンス変数を宣言し、コンストラクターで初期化します。 フィールドは、 `isLit` プロパティによって指定された色でテキストを描画するかどうかを決定し `LightColor` ます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#140](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#140)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#140](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#140)]

10. `IMarqueeWidget` インターフェイスを実装します。

    `StartMarquee`メソッドと `StopMarquee` メソッドは、 <xref:System.ComponentModel.BackgroundWorker> コンポーネントの <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> メソッドとメソッドを呼び出して、アニメーションを <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> 開始および停止します。

    <xref:System.ComponentModel.CategoryAttribute.Category%2A>属性と <xref:System.ComponentModel.BrowsableAttribute.Browsable%2A> 属性はプロパティに適用さ `UpdatePeriod` れるため、"Marquee" と呼ばれるプロパティウィンドウのカスタムセクションに表示されます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#150](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#150)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#150](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#150)]

11. プロパティアクセサーを実装します。 クライアントには `LightColor` 、との2つのプロパティを公開します。 `DarkColor` <xref:System.ComponentModel.CategoryAttribute.Category%2A>これらの <xref:System.ComponentModel.BrowsableAttribute.Browsable%2A> プロパティには属性と属性が適用されるので、プロパティは "Marquee" と呼ばれるプロパティウィンドウのカスタムセクションに表示されます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#160](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#160)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#160](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#160)]

12. コンポーネントとイベントのハンドラーを実装し <xref:System.ComponentModel.BackgroundWorker> <xref:System.ComponentModel.BackgroundWorker.DoWork> <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> ます。

    <xref:System.ComponentModel.BackgroundWorker.DoWork>イベントハンドラーは、によって指定されたミリ秒数の間スリープ状態に `UpdatePeriod` <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> なり、コードがを呼び出すことによってアニメーションを停止するまで、イベントを発生させ <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> ます。

    <xref:System.ComponentModel.BackgroundWorker.ProgressChanged>イベントハンドラーは、テキストを淡色と濃色の状態の間で切り替えて、点滅のようにします。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#180](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#180)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#180](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#180)]

13. アニメーションを <xref:System.Windows.Forms.Control.OnPaint%2A> 有効にするには、メソッドをオーバーライドします。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#170](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#170)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#170](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#170)]

14. **F6** キーを押してソリューションをビルドします。

## <a name="create-the-marqueeborder-child-control"></a>MarqueeBorder 子コントロールを作成する

コントロールは、 `MarqueeBorder` コントロールよりも少し洗練されてい `MarqueeText` ます。 これにはさらに多くのプロパティがあり、メソッドのアニメーションも複雑になり <xref:System.Windows.Forms.Control.OnPaint%2A> ます。 原則として、コントロールと非常によく似てい `MarqueeText` ます。

コントロールは `MarqueeBorder` 子コントロールを持つことができるため、イベントに注意する必要があり <xref:System.Windows.Forms.Control.Layout> ます。

### <a name="to-create-the-marqueeborder-control"></a>MarqueeBorder コントロールを作成するには

1. 新しい**カスタムコントロール**項目をプロジェクトに追加 `MarqueeControlLibrary` します。 新しいソースファイルに "MarqueeBorder" のベース名を指定します。

2. コンポーネントを <xref:System.ComponentModel.BackgroundWorker> **ツールボックス**からコントロールにドラッグし `MarqueeBorder` ます。 このコンポーネントを使用すると、 `MarqueeBorder` コントロール自体を非同期的に更新できます。

3. [**プロパティ**] ウィンドウで、 <xref:System.ComponentModel.BackgroundWorker> コンポーネントの `WorkerReportsProgress` プロパティと <xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A> プロパティを**true**に設定します。 これらの設定により、 <xref:System.ComponentModel.BackgroundWorker> コンポーネントは定期的にイベントを発生させ、非同期更新を取り消すことができ <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> ます。 詳細については、「 [BackgroundWorker Component](backgroundworker-component.md)」を参照してください。

4. **[プロパティ]** ウィンドウで、 **[イベント]** ボタンを選択します。 イベントおよびイベントのハンドラーをアタッチ <xref:System.ComponentModel.BackgroundWorker.DoWork> <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> します。

5. `MarqueeBorder`**コードエディター**でソースファイルを開きます。 ファイルの先頭に、次の名前空間をインポートします。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#20](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#20)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#20](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#20)]

6. から継承し、インターフェイスを実装するように、の宣言を変更 `MarqueeBorder` <xref:System.Windows.Forms.Panel> し `IMarqueeWidget` ます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#30](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#30)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#30](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#30)]

7. コントロールの状態を管理するための2つの列挙体を宣言 `MarqueeBorder` します。 `MarqueeSpinDirection` これは、ライトが境界の周りを "スピン" する方向を決定します。は、 `MarqueeLightShape` ライトの形状 (正方形または円形) を決定します。 これらの宣言は、クラス宣言の前に配置 `MarqueeBorder` します。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#97](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#97)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#97](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#97)]

8. 公開されたプロパティに対応するインスタンス変数を宣言し、コンストラクターで初期化します。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#40](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#40)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#40](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#40)]

9. `IMarqueeWidget` インターフェイスを実装します。

    `StartMarquee`メソッドと `StopMarquee` メソッドは、 <xref:System.ComponentModel.BackgroundWorker> コンポーネントの <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> メソッドとメソッドを呼び出して、アニメーションを <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> 開始および停止します。

    コントロールに `MarqueeBorder` 子コントロールを含めることができるため、メソッドは、 `StartMarquee` すべての子コントロールを列挙し、を `StartMarquee` 実装する子コントロールに対してを呼び出し `IMarqueeWidget` ます。 メソッドには `StopMarquee` 同様の実装があります。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#50](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#50)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#50](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#50)]

10. プロパティアクセサーを実装します。 `MarqueeBorder`コントロールには、外観を制御するためのプロパティがいくつかあります。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#60](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#60)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#60](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#60)]

11. コンポーネントとイベントのハンドラーを実装し <xref:System.ComponentModel.BackgroundWorker> <xref:System.ComponentModel.BackgroundWorker.DoWork> <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> ます。

    <xref:System.ComponentModel.BackgroundWorker.DoWork>イベントハンドラーは、によって指定されたミリ秒数の間スリープ状態に `UpdatePeriod` <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> なり、コードがを呼び出すことによってアニメーションを停止するまで、イベントを発生させ <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> ます。

    <xref:System.ComponentModel.BackgroundWorker.ProgressChanged>イベントハンドラーは、他のライトの明るい/暗い状態が決定される "基本" ライトの位置をインクリメントし、メソッドを呼び出して <xref:System.Windows.Forms.Control.Refresh%2A> 、コントロール自体を再描画します。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#90](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#90)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#90](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#90)]

12. ヘルパーメソッドとを実装 `IsLit` し `DrawLight` ます。

    メソッドは、 `IsLit` 指定された位置のライトの色を決定します。 "Lit" のライトは、プロパティによって指定された色で描画され `LightColor` ます。 "ダーク" は、プロパティによって指定された色で描画され `DarkColor` ます。

    メソッドは、 `DrawLight` 適切な色、形状、および位置を使用してライトを描画します。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#80](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#80)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#80](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#80)]

13. <xref:System.Windows.Forms.Control.OnLayout%2A> および <xref:System.Windows.Forms.Control.OnPaint%2A> メソッドをオーバーライドします。

    メソッドは、 <xref:System.Windows.Forms.Control.OnPaint%2A> コントロールの端に沿ってライトを描画し `MarqueeBorder` ます。

    メソッドは <xref:System.Windows.Forms.Control.OnPaint%2A> コントロールのディメンションに依存するため `MarqueeBorder` 、レイアウトが変更されるたびに呼び出す必要があります。 これを実現するには、 <xref:System.Windows.Forms.Control.OnLayout%2A> をオーバーライドし、を呼び出し <xref:System.Windows.Forms.Control.Refresh%2A> ます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#70](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#70)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#70](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#70)]

## <a name="create-a-custom-designer-to-shadow-and-filter-properties"></a>カスタムデザイナーを作成してプロパティをシャドウおよびフィルター処理する

クラスは、 `MarqueeControlRootDesigner` ルートデザイナーの実装を提供します。 で動作するこのデザイナーに加えて、 `MarqueeControl` コントロールに特に関連付けられたカスタムデザイナーが必要です `MarqueeBorder` 。 このデザイナーには、カスタムルートデザイナーのコンテキストに適したカスタム動作が用意されています。

具体的には、は、 `MarqueeBorderDesigner` コントロールの特定のプロパティを "シャドウ" してフィルター処理し `MarqueeBorder` 、デザイン環境との相互作用を変更します。

コンポーネントのプロパティアクセサーへの呼び出しのインターセプトは、"シャドウ処理" と呼ばれます。 これにより、デザイナーはユーザーが設定した値を追跡し、必要に応じてその値をデザイン対象のコンポーネントに渡すことができます。

この例では、 <xref:System.Windows.Forms.Control.Visible%2A> プロパティとプロパティがに <xref:System.Windows.Forms.Control.Enabled%2A> よってシャドウされます。これにより、 `MarqueeBorderDesigner` デザイン時にユーザーがコントロールを非表示にしたり無効にしたりすることができなくなり `MarqueeBorder` ます。

デザイナーでは、プロパティを追加および削除することもできます。 この例では、プロパティは <xref:System.Windows.Forms.Control.Padding%2A> デザイン時に削除され `MarqueeBorder` ます。コントロールはプログラムによって、プロパティによって指定されたライトのサイズに基づいて余白を設定し `LightSize` ます。

の基本クラス `MarqueeBorderDesigner` はです <xref:System.ComponentModel.Design.ComponentDesigner> 。これには、デザイン時にコントロールによって公開される属性、プロパティ、およびイベントを変更するためのメソッドがあります。

- <xref:System.ComponentModel.Design.ComponentDesigner.PreFilterProperties%2A>

- <xref:System.ComponentModel.Design.ComponentDesigner.PostFilterProperties%2A>

- <xref:System.ComponentModel.Design.ComponentDesigner.PreFilterAttributes%2A>

- <xref:System.ComponentModel.Design.ComponentDesigner.PostFilterAttributes%2A>

- <xref:System.ComponentModel.Design.ComponentDesigner.PreFilterEvents%2A>

- <xref:System.ComponentModel.Design.ComponentDesigner.PostFilterEvents%2A>

これらのメソッドを使用してコンポーネントのパブリックインターフェイスを変更する場合は、次の規則に従います。

- メソッドでのみ項目を追加または削除する `PreFilter`

- メソッド内の既存の項目のみを変更する `PostFilter`

- 常に基本実装をメソッドで呼び出す `PreFilter`

- メソッドの最後に基本実装を呼び出します。 `PostFilter`

これらの規則に従うことで、デザイン時環境のすべてのデザイナーが、デザインされているすべてのコンポーネントの一貫したビューを確実に表示できるようになります。

クラスは、 <xref:System.ComponentModel.Design.ComponentDesigner> シャドウプロパティの値を管理するためのディクショナリを提供します。これにより、特定のインスタンス変数を作成する必要がなくなります。

### <a name="to-create-a-custom-designer-to-shadow-and-filter-properties"></a>プロパティをシャドウおよびフィルター処理するためのカスタムデザイナーを作成するには

1. **Design**フォルダーを右クリックし、新しいクラスを追加します。 ソースファイルに**MarqueeBorderDesigner**のベース名を指定します。

2. **コードエディター**で MarqueeBorderDesigner ソースファイルを開きます。 ファイルの先頭に、次の名前空間をインポートします。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#420](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#420)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#420](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#420)]

3. を `MarqueeBorderDesigner` 継承するようにの宣言を変更 <xref:System.Windows.Forms.Design.ParentControlDesigner> します。

    コントロールに `MarqueeBorder` 子コントロールを含めることができるため、はを `MarqueeBorderDesigner` 継承し <xref:System.Windows.Forms.Design.ParentControlDesigner> ます。これは、親子の相互作用を処理します。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#430](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#430)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#430](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#430)]

4. の基本実装をオーバーライド <xref:System.ComponentModel.Design.ComponentDesigner.PreFilterProperties%2A> します。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#450](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#450)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#450](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#450)]

5. <xref:System.Windows.Forms.Control.Enabled%2A> プロパティと <xref:System.Windows.Forms.Control.Visible%2A> プロパティを実装します。 これらの実装は、コントロールのプロパティをシャドウします。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#440](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#440)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#440](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#440)]

## <a name="handle-component-changes"></a>コンポーネントの変更を処理する

クラスは、 `MarqueeControlRootDesigner` インスタンスのカスタムデザイン時エクスペリエンスを提供し `MarqueeControl` ます。 デザイン時の機能のほとんどは、クラスから継承され <xref:System.Windows.Forms.Design.DocumentDesigner> ます。 コードには、コンポーネントの変更の処理とデザイナー動詞の追加という2つのカスタマイズのカスタマイズが実装されます。

ユーザーが `MarqueeControl` インスタンスをデザインすると、ルートデザイナーはとその子コントロールに対する変更を追跡し `MarqueeControl` ます。 デザイン時環境には、コンポーネントの状態に対する変更を追跡するための便利なサービスが用意されて <xref:System.ComponentModel.Design.IComponentChangeService> います。

このサービスへの参照を取得するには、メソッドを使用して環境に対してクエリを実行し <xref:System.ComponentModel.Design.ComponentDesigner.GetService%2A> ます。 クエリが成功した場合、デザイナーはイベントのハンドラーをアタッチ <xref:System.ComponentModel.Design.IComponentChangeService.ComponentChanged> し、デザイン時に一貫性のある状態を維持するために必要なすべてのタスクを実行できます。

クラスの場合は `MarqueeControlRootDesigner` 、に格納され <xref:System.Windows.Forms.Control.Refresh%2A> ている各オブジェクトに対してメソッドを呼び出し `IMarqueeWidget` `MarqueeControl` ます。 これにより、 `IMarqueeWidget` 親のようなプロパティが変更されたときに、オブジェクトが適切に再描画され <xref:System.Windows.Forms.Control.Size%2A> ます。

### <a name="to-handle-component-changes"></a>コンポーネントの変更を処理するには

1. `MarqueeControlRootDesigner`**コードエディター**でソースファイルを開き、メソッドをオーバーライドし <xref:System.Windows.Forms.Design.DocumentDesigner.Initialize%2A> ます。 の基本実装を呼び出し、に対してクエリを実行し <xref:System.Windows.Forms.Design.DocumentDesigner.Initialize%2A> <xref:System.ComponentModel.Design.IComponentChangeService> ます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#580](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#580)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#580](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#580)]

2. <xref:System.ComponentModel.Design.IComponentChangeService.OnComponentChanged%2A>イベントハンドラーを実装します。 送信コンポーネントの型をテストし、がの場合は `IMarqueeWidget` 、そのメソッドを呼び出し <xref:System.Windows.Forms.Control.Refresh%2A> ます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#560](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#560)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#560](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#560)]

## <a name="add-designer-verbs-to-your-custom-designer"></a>デザイナー動詞をカスタムデザイナーに追加する

デザイナー動詞は、イベント ハンドラーにリンクされたメニュー コマンドです。 デザイナー動詞は、デザイン時にコンポーネントのショートカットメニューに追加されます。 詳細については、「<xref:System.ComponentModel.Design.DesignerVerb>」を参照してください。

デザイナーに2つのデザイナー動詞を追加します。**テストを実行**し、**テストを停止**します。 これらの動詞を使用すると、デザイン時にの実行時の動作を表示でき `MarqueeControl` ます。 これらの動詞はに追加され `MarqueeControlRootDesigner` ます。

**実行テスト**が呼び出されると、動詞イベントハンドラーは `StartMarquee` に対してメソッドを呼び出し `MarqueeControl` ます。 **停止テスト**が呼び出されると、動詞イベントハンドラーは `StopMarquee` に対してメソッドを呼び出し `MarqueeControl` ます。 メソッドとメソッドの実装では `StartMarquee` `StopMarquee` 、を実装する含まれるコントロールに対してこれらのメソッドを呼び出し `IMarqueeWidget` ます。これにより、含まれる `IMarqueeWidget` コントロールもテストに参加します。

### <a name="to-add-designer-verbs-to-your-custom-designers"></a>デザイナー動詞をカスタムデザイナーに追加するには

1. クラスで、 `MarqueeControlRootDesigner` およびという名前のイベントハンドラーを追加し `OnVerbRunTest` `OnVerbStopTest` ます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#570](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#570)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#570](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#570)]

2. これらのイベントハンドラーを、対応するデザイナー動詞に接続します。 `MarqueeControlRootDesigner`<xref:System.ComponentModel.Design.DesignerVerbCollection>基底クラスからを継承します。 2つの新しいオブジェクトを作成 <xref:System.ComponentModel.Design.DesignerVerb> し、メソッドでこのコレクションに追加し <xref:System.Windows.Forms.Design.DocumentDesigner.Initialize%2A> ます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#590](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#590)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#590](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#590)]

## <a name="create-a-custom-uitypeeditor"></a>カスタム UITypeEditor を作成する

ユーザーに対してカスタムのデザイン時エクスペリエンスを作成する場合、多くの場合、プロパティウィンドウとのカスタム操作を作成することをお勧めします。 これを行うには、を作成し <xref:System.Drawing.Design.UITypeEditor> ます。

`MarqueeBorder`コントロールは、プロパティウィンドウ内のいくつかのプロパティを公開します。 これらのプロパティのうちの2つ `MarqueeSpinDirection` `MarqueeLightShape` は、列挙体によって表されます。 UI 型エディターの使用方法を示すために、 `MarqueeLightShape` プロパティにはクラスが関連付けられてい <xref:System.Drawing.Design.UITypeEditor> ます。

### <a name="to-create-a-custom-ui-type-editor"></a>カスタム UI 型エディターを作成するには

1. `MarqueeBorder`**コードエディター**でソースファイルを開きます。

2. クラスの定義で `MarqueeBorder` 、から派生するというクラスを宣言し `LightShapeEditor` <xref:System.Drawing.Design.UITypeEditor> ます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#96](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#96)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#96](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#96)]

3. <xref:System.Windows.Forms.Design.IWindowsFormsEditorService>という名前のインスタンス変数を宣言 `editorService` します。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#92](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#92)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#92](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#92)]

4. <xref:System.Drawing.Design.UITypeEditor.GetEditStyle%2A> メソッドをオーバーライドします。 この実装はを返し <xref:System.Drawing.Design.UITypeEditorEditStyle.DropDown> ます。これは、を表示する方法をデザイン環境に指示し `LightShapeEditor` ます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#93](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#93)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#93](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#93)]

5. <xref:System.Drawing.Design.UITypeEditor.EditValue%2A> メソッドをオーバーライドします。 この実装は、オブジェクトのデザイン環境に対してクエリを <xref:System.Windows.Forms.Design.IWindowsFormsEditorService> 行います。 成功した場合は、が作成さ `LightShapeSelectionControl` れます。 を <xref:System.Windows.Forms.Design.IWindowsFormsEditorService.DropDownControl%2A> 開始するためにメソッドが呼び出され `LightShapeEditor` ます。 この呼び出しからの戻り値がデザイン環境に返されます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#94](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#94)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#94](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#94)]

## <a name="create-a-view-control-for-your-custom-uitypeeditor"></a>カスタム UITypeEditor のビューコントロールを作成する

プロパティは、 `MarqueeLightShape` との2種類のライトシェイプをサポートしてい `Square` `Circle` ます。 プロパティウィンドウでこれらの値をグラフィカルに表示する目的でのみ使用されるカスタムコントロールを作成します。 このカスタムコントロールは、 <xref:System.Drawing.Design.UITypeEditor> プロパティウィンドウと対話するためにによって使用されます。

### <a name="to-create-a-view-control-for-your-custom-ui-type-editor"></a>カスタム UI 型エディターのビューコントロールを作成するには

1. 新しい項目を <xref:System.Windows.Forms.UserControl> プロジェクトに追加 `MarqueeControlLibrary` します。 新しいソースファイルに**LightShapeSelectionControl**のベース名を指定します。

2. ツールボックスからに2つのコントロールをドラッグし <xref:System.Windows.Forms.Panel> **Toolbox** `LightShapeSelectionControl` ます。 とという名前を指定し `squarePanel` `circlePanel` ます。 それらを並べて配置します。 <xref:System.Windows.Forms.Control.Size%2A>両方のコントロールのプロパティ <xref:System.Windows.Forms.Panel> を **(60, 60)** に設定します。 <xref:System.Windows.Forms.Control.Location%2A>コントロールのプロパティ `squarePanel` を **(8, 10)** に設定します。 <xref:System.Windows.Forms.Control.Location%2A>コントロールのプロパティ `circlePanel` を **(80, 10)** に設定します。 最後に、 <xref:System.Windows.Forms.Control.Size%2A> のプロパティ `LightShapeSelectionControl` を **(150, 80)** に設定します。

3. `LightShapeSelectionControl`**コードエディター**でソースファイルを開きます。 ファイルの先頭に、名前空間をインポートし <xref:System.Windows.Forms.Design?displayProperty=nameWithType> ます。

   ```vb
   Imports System.Windows.Forms.Design
   ```

   ```csharp
   using System.Windows.Forms.Design;
   ```

4. <xref:System.Windows.Forms.Control.Click>コントロールとコントロールのイベントハンドラーを実装 `squarePanel` `circlePanel` します。 これらのメソッド <xref:System.Windows.Forms.Design.IWindowsFormsEditorService.CloseDropDown%2A> は、カスタム編集セッションを終了するためにを呼び出し <xref:System.Drawing.Design.UITypeEditor> ます。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#390](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#390)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#390](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#390)]

5. <xref:System.Windows.Forms.Design.IWindowsFormsEditorService>という名前のインスタンス変数を宣言 `editorService` します。

   ```vb
   Private editorService As IWindowsFormsEditorService
   ```

   ```csharp
   private IWindowsFormsEditorService editorService;
   ```

6. `MarqueeLightShape`という名前のインスタンス変数を宣言 `lightShapeValue` します。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#330](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#330)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#330](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#330)]

7. コンストラクターで、 `LightShapeSelectionControl` <xref:System.Windows.Forms.Control.Click> イベントハンドラーをとコントロールのイベントにアタッチし `squarePanel` `circlePanel` <xref:System.Windows.Forms.Control.Click> ます。 また、 `MarqueeLightShape` デザイン環境からフィールドに値を割り当てるコンストラクターのオーバーロードを定義し `lightShapeValue` ます。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#340](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#340)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#340](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#340)]

8. メソッドで <xref:System.ComponentModel.Component.Dispose%2A> 、イベントハンドラーをデタッチし <xref:System.Windows.Forms.Control.Click> ます。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#350](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#350)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#350](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#350)]

9. **ソリューション エクスプローラー**で、**[すべてのファイルを表示]** ボタンをクリックします。 LightShapeSelectionControl.Designer.cs または LightShapeSelectionControl ファイルを開き、メソッドの既定の定義を削除し <xref:System.ComponentModel.Component.Dispose%2A> ます。

10. `LightShape` プロパティを実装します。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#360](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#360)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#360](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#360)]

11. <xref:System.Windows.Forms.Control.OnPaint%2A> メソッドをオーバーライドします。 この実装では、塗りつぶされた正方形と円を描画します。 また、1つの図形の周りに境界線を描画して、選択された値を強調表示します。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#380](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#380)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#380](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#380)]

## <a name="test-your-custom-control-in-the-designer"></a>デザイナーでカスタムコントロールをテストする

この時点で、プロジェクトをビルドでき `MarqueeControlLibrary` ます。 クラスを継承し、フォームで使用するコントロールを作成して、実装をテスト `MarqueeControl` します。

### <a name="to-create-a-custom-marqueecontrol-implementation"></a>カスタムの MarqueeControl 実装を作成するには

1. Windows フォーム デザイナーで `DemoMarqueeControl` を開きます。 これにより、型のインスタンスが作成さ `DemoMarqueeControl` れ、型のインスタンスに表示され `MarqueeControlRootDesigner` ます。

2. **ツールボックス**で、[ **MarqueeControlLibrary Components** ] タブを開きます。`MarqueeBorder`選択できるコントロールとコントロールが表示され `MarqueeText` ます。

3. コントロールのインスタンスを `MarqueeBorder` デザインサーフェイスにドラッグし `DemoMarqueeControl` ます。 この `MarqueeBorder` コントロールを親コントロールにドッキングします。

4. コントロールのインスタンスを `MarqueeText` デザインサーフェイスにドラッグし `DemoMarqueeControl` ます。

5. ソリューションをビルドします。

6. を右クリックし、 `DemoMarqueeControl` ショートカットメニューの [**テストの実行**] オプションを選択してアニメーションを開始します。 アニメーションを停止するには、[**テストの停止**] をクリックします。

7. デザイン ビューで **[Form1]** を開きます。

8. フォームに2つの <xref:System.Windows.Forms.Button> コントロールを配置します。 それらに `startButton` とという名前を設定 `stopButton` し、 <xref:System.Windows.Forms.Control.Text%2A> プロパティ値をそれぞれ**Start**および**Stop**に変更します。

9. <xref:System.Windows.Forms.Control.Click>両方のコントロールにイベントハンドラーを実装 <xref:System.Windows.Forms.Button> します。

10. **ツールボックス**で、[ **MarqueeControlTest Components** ] タブを開きます。選択できるが表示され `DemoMarqueeControl` ます。

11. のインスタンスを `DemoMarqueeControl` **Form1**デザインサーフェイスにドラッグします。

12. <xref:System.Windows.Forms.Control.Click>イベントハンドラーで、 `Start` `Stop` でメソッドとメソッドを呼び出し `DemoMarqueeControl` ます。

    ```vb
    Private Sub startButton_Click(sender As Object, e As System.EventArgs)
        Me.demoMarqueeControl1.Start()
    End Sub 'startButton_Click

    Private Sub stopButton_Click(sender As Object, e As System.EventArgs)
    Me.demoMarqueeControl1.Stop()
    End Sub 'stopButton_Click
    ```

    ```csharp
    private void startButton_Click(object sender, System.EventArgs e)
    {
        this.demoMarqueeControl1.Start();
    }

    private void stopButton_Click(object sender, System.EventArgs e)
    {
        this.demoMarqueeControl1.Stop();
    }
    ```

13. プロジェクトを `MarqueeControlTest` スタートアッププロジェクトとして設定し、実行します。 というフォームが表示され `DemoMarqueeControl` ます。 [**開始**] ボタンを選択して、アニメーションを開始します。 テキストが点滅し、ライトが境界内を移動していることを確認します。

## <a name="next-steps"></a>次のステップ

は、 `MarqueeControlLibrary` カスタムコントロールおよび関連するデザイナーの単純な実装を示しています。 このサンプルは、いくつかの方法でより高度なものにすることができます。

- デザイナーでのプロパティの値を変更し `DemoMarqueeControl` ます。 `MarqueBorder`コントロールを追加し、親インスタンス内にドッキングして、入れ子になった効果を作成します。 と light 関連のプロパティについて、さまざまな設定を試してみて `UpdatePeriod` ください。

- の独自の実装を作成 `IMarqueeWidget` します。 たとえば、点滅する "ネオンサイン" や、複数のイメージを使用したアニメーション化された記号を作成することができます。

- デザイン時のエクスペリエンスをさらにカスタマイズします。 とより多くのプロパティをシャドウすることもでき <xref:System.Windows.Forms.Control.Enabled%2A> <xref:System.Windows.Forms.Control.Visible%2A> ます。また、新しいプロパティを追加することもできます。 新しいデザイナー動詞を追加して、子コントロールのドッキングなどの一般的なタスクを簡略化します。

- をライセンス `MarqueeControl` します。

- コントロールのシリアル化方法とコードの生成方法を制御します。 詳細については、「[動的なソースコードの生成とコンパイル](../../reflection-and-codedom/dynamic-source-code-generation-and-compilation.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.UserControl>
- <xref:System.Windows.Forms.Design.ParentControlDesigner>
- <xref:System.Windows.Forms.Design.DocumentDesigner>
- <xref:System.ComponentModel.Design.IRootDesigner>
- <xref:System.ComponentModel.Design.DesignerVerb>
- <xref:System.Drawing.Design.UITypeEditor>
- <xref:System.ComponentModel.BackgroundWorker>
