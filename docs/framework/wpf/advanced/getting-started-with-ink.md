---
title: Visual Studio で InkCanvas を作成する
ms.date: 08/15/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- procedural code in lieu of XAML [WPF]
- XAML [WPF], procedural code in lieu of
- InkCanvas (WPF)
ms.assetid: 760332dd-594a-475d-865b-01659db8cab7
ms.openlocfilehash: b8087d6db04f7024b9ee48f28002bee04045a14b
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76737888"
---
# <a name="get-started-with-ink-in-wpf"></a>WPF でのインクの概要

Windows Presentation Foundation (WPF) には、デジタル インクをアプリに簡単に組み込むことができるインク機能があります。

## <a name="prerequisites"></a>必須コンポーネント

次の例を使用するには、まず [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) をインストールします。 また、基本的な WPF アプリの作成方法を理解するためにも役立ちます。 WPF の概要については、「[チュートリアル: 初めての WPF デスクトップ アプリケーション](../getting-started/walkthrough-my-first-wpf-desktop-application.md)」を参照してください。

## <a name="quick-start"></a>クイック スタート

このセクションは、インクを収集する簡単な WPF アプリケーションを作成するために役立ちます。

### <a name="got-ink"></a>インクを用意できたら

インクをサポートする WPF アプリを作成するには:

1. Visual Studio を開きます。

2. 新しい **WPF アプリ**を作成します。

   **[新しいプロジェクト]** ダイアログで、 **[インストール済み]**  >  **[Visual C#]** または **[Visual Basic]**  >  **[Windows デスクトップ]** カテゴリを展開します。 次に、 **[WPF アプリ (.NET Framework)]** アプリ テンプレートを選択します。 名前を入力し、 **[OK]** を選択します。

   Visual Studio によってプロジェクトが作成され、デザイナーで *MainWindow.xaml* が開きます。

3. `<Grid>` タグの間に「`<InkCanvas/>`」と入力します。

   ![InkCanvas タグを使用する XAML デザイナー](./media/getting-started-with-ink/inkcanvas-xaml.png)

4. **F5** キーを押して、デバッガーでアプリケーションを起動します。

5. スタイラスまたはマウスを使用して、ウィンドウに「**hello world**」と入力します。

これで、わずか 12 回のキーストロークで "hello world" アプリケーションに相当するインクを作成できました。

### <a name="spice-up-your-app"></a>アプリにスパイスを加える

WPF のいくつかの機能を活用してみましょう。 開始と終了の \<Window> タグの間にあるすべてを次のマークアップに置き換えます。

```xaml
<Page>
  <InkCanvas Name="myInkCanvas" MouseRightButtonUp="RightMouseUpHandler">
    <InkCanvas.Background>
      <LinearGradientBrush>
        <GradientStop Color="Yellow" Offset="0.0" />
          <GradientStop Color="Blue" Offset="0.5" />
            <GradientStop Color="HotPink" Offset="1.0" />
              </LinearGradientBrush>
    </InkCanvas.Background>
  </InkCanvas>
</Page>
```

この XAML によって、インク サーフェイスにグラデーション ブラシの背景が作成されます。

![WPF アプリのインク サーフェイスのグラデーション カラー](./media/getting-started-with-ink/gradient-colors.png)

### <a name="add-some-code-behind-the-xaml"></a>XAML の背後にコードを追加する

XAML を使用すると、ユーザー インターフェイスの設計がとても簡単になりますが、実際のアプリケーションでは、イベントを処理するためのコードを追加する必要があります。 マウスの右クリックに応じてインクを拡大する簡単な例を次に示します。

1. XAML で `MouseRightButtonUp` ハンドラーを設定します。

   [!code-xaml[DigitalInkTopics#3](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#3)]

1. **ソリューション エクスプローラー** で、MainWindow.xaml を展開し、分離コード ファイル (MainWindow.xaml.cs または MainWindow.xaml.vb) を開きます。 次のイベント ハンドラー コードを追加します。

   [!code-csharp[DigitalInkTopics#4](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml.cs#4)]
   [!code-vb[DigitalInkTopics#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window2.xaml.vb#4)]

1. アプリケーションを実行します。 何らかのインクを追加してから、マウスで右クリックするか、スタイラスで同等の長押しを実行します。

   マウスの右ボタンでクリックするたびにディスプレイが拡大されます。

### <a name="use-procedural-code-instead-of-xaml"></a>XAML ではなく手続き型コードを使用する

手続き型コードからすべての WPF 機能にアクセスできます。 XAML をまったく使用しない WPF 用の "Hello Ink World" アプリケーションを作成するには、次の手順を実行します。

1. Visual Studio で新しいコンソール アプリケーション プロジェクトを作成します。

   **[新しいプロジェクト]** ダイアログで、 **[インストール済み]**  >  **[Visual C#]** または **[Visual Basic]**  >  **[Windows デスクトップ]** カテゴリを展開します。 次に、 **[コンソール アプリ (.NET Framework)]** アプリ テンプレートを選択します。 名前を入力し、 **[OK]** を選択します。

1. 次のコードを Program.cs または Program.vb ファイルに貼り付けます。

   [!code-csharp[InkCanvasConsoleApp#1](~/samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasConsoleApp/CSharp/Program.cs#1)]
   [!code-vb[InkCanvasConsoleApp#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/InkCanvasConsoleApp/VisualBasic/Module1.vb#1)]

1. **ソリューション エクスプローラー**で **[参照]** を右クリックし、 **[参照の追加]** を選択して、PresentationCore、PresentationFramework、および WindowsBase アセンブリへの参照を追加します。

   ![PresentationCore および PresentationFramework を示す参照マネージャー](./media/getting-started-with-ink/reference-manager-presentationcore-presentationframework.png)

1. **F5** キーを押してアプリケーションをビルドします。

## <a name="see-also"></a>関連項目

- [デジタル インク](digital-ink.md)
- [インクの収集](collecting-ink.md)
- [手書き認識](handwriting-recognition.md)
- [インクの格納](storing-ink.md)
