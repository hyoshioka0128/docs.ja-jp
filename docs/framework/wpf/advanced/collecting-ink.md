---
title: デジタル インクを収集する
ms.date: 08/15/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ink [WPF], collecting
- InkCanvas element [WPF]
- properties [WPF], DrawingAttributes
- collecting digital ink [WPF]
- digital ink [WPF], collecting
- properties [WPF], DefaultDrawingAttributes
- DefaultDrawingAttributes property [WPF]
ms.assetid: 66a3129d-9577-43eb-acbd-56c147282016
ms.openlocfilehash: 813a5313a6fbf83c36cdbed1f64ce69a217ad788
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76747027"
---
# <a name="collect-ink"></a>インクを収集する

[Windows Presentation Foundation](../index.md) プラットフォームでは、その機能の中核としてデジタル インクが収集されます。 このトピックでは、Windows Presentation Foundation (WPF) でインクを収集する方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント

次の例を使用するには、まず Visual Studio と Windows SDK をインストールする必要があります。 また、WPF に対応するアプリケーションの作成方法も理解しておく必要があります。 WPF の概要については、「[チュートリアル: 初めての WPF デスクトップ アプリケーション](../getting-started/walkthrough-my-first-wpf-desktop-application.md)」を参照してください。

## <a name="use-the-inkcanvas-element"></a>InkCanvas 要素を使用する

<xref:System.Windows.Controls.InkCanvas?displayProperty=fullName> 要素を使用すると、最も簡単に WPF でインクを収集できます。 <xref:System.Windows.Controls.InkCanvas> 要素を使用して、インク入力を受け取って表示します。 インクは一般的に、スタイラスを使用して入力します。スタイラスはデジタイザーとの対話により、インク ストロークを生成します。 また、スタイラスの代わりにマウスを使用することもできます。 作成されたストロークは <xref:System.Windows.Ink.Stroke> オブジェクトとして表され、プログラムとユーザー入力の両方で操作できます。 <xref:System.Windows.Controls.InkCanvas> を使用すると、ユーザーは既存の <xref:System.Windows.Ink.Stroke> を選択、変更、または削除できます。

XAML を使用して、**InkCanvas** 要素をツリーに追加するだけで簡単にインク収集を設定できます。 次の例では、Visual Studio で作成された既定の WPF プロジェクトに <xref:System.Windows.Controls.InkCanvas> を追加します。

[!code-xaml[DigitalInkTopics#6](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#6)]

**InkCanvas** 要素には子要素を含めることもできます。これにより、ほとんどすべての XAML 要素にインク注釈機能を追加できます。 たとえば、テキスト要素にインク機能を追加するには、単にそれを <xref:System.Windows.Controls.InkCanvas> の子にします。

[!code-xaml[DigitalInkTopics#5](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#5)]

インクを使用したイメージのマークアップのサポートも、簡単に追加できます。

[!code-xaml[DigitalInkTopics#7](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#7)]

### <a name="inkcollection-modes"></a>InkCollection モード

<xref:System.Windows.Controls.InkCanvas> は、<xref:System.Windows.Controls.InkCanvas.EditingMode%2A> プロパティを介したさまざまな入力モードをサポートしています。

### <a name="manipulate-ink"></a>インクを操作する

<xref:System.Windows.Controls.InkCanvas> は、多くのインク編集操作をサポートしています。 たとえば、<xref:System.Windows.Controls.InkCanvas> は消しゴム付きペンの機能をサポートしており、この機能を要素に追加するために追加のコードは必要ありません。

#### <a name="selection"></a>選択ツール

選択モードの設定は、<xref:System.Windows.Controls.InkCanvasEditingMode> プロパティを **Select** に設定する場合と同じくらい簡単です。

次のコードでは、<xref:System.Windows.Forms.CheckBox> の値に基づいて編集モードを設定します。

[!code-csharp[DigitalInkTopics#8](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#8)]
[!code-vb[DigitalInkTopics#8](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#8)]

#### <a name="drawingattributes"></a>DrawingAttributes

インク ストロークの外観を変更するには、<xref:System.Windows.Ink.Stroke.DrawingAttributes%2A> プロパティを使用します。 たとえば、<xref:System.Windows.Ink.DrawingAttributes> の <xref:System.Windows.Ink.DrawingAttributes.Color%2A> メンバーを使用して、レンダリングされた <xref:System.Windows.Ink.Stroke> の色を設定できます。

次の例では、選択されたストロークの色を赤に変更します。

[!code-csharp[DigitalInkTopics#9](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#9)]
[!code-vb[DigitalInkTopics#9](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#9)]

### <a name="defaultdrawingattributes"></a>DefaultDrawingAttributes

<xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> プロパティを使用すると、<xref:System.Windows.Controls.InkCanvas> で作成されるストロークの高さ、幅、色などのプロパティにアクセスできます。 <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> を変更すると、以降、<xref:System.Windows.Controls.InkCanvas> に入力されるすべてのストロークは、新しいプロパティ値でレンダリングされます。

分離コード ファイルの <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> を変更するだけでなく、XAML 構文を使用して <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> プロパティを指定できます。

次の例は、<xref:System.Windows.Ink.DrawingAttributes.Color%2A> プロパティを設定する方法を示しています。 このコードを使用するには、Visual Studio で "HelloInkCanvas" という新しい WPF プロジェクトを作成します。 *MainWindow.xaml* ファイル内のコードを次のコードに置き換えます。

[!code-xaml[HelloInkCanvas#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HelloInkCanvas/CSharp/Window1.xaml#1)]

次に、以下のボタン イベント ハンドラーを、分離コード ファイルの MainWindow クラス内に追加します。

[!code-csharp[HelloInkCanvas#2](~/samples/snippets/csharp/VS_Snippets_Wpf/HelloInkCanvas/CSharp/Window1.xaml.cs#2)]

このコードをコピーしたら、Visual Studio で **F5** キーを押して、デバッガーでプログラムを実行します。

<xref:System.Windows.Controls.StackPanel> によってボタンが <xref:System.Windows.Controls.InkCanvas> の上に配置されていることに注意してください。 ボタンの上にインクを塗ろうとすると、<xref:System.Windows.Controls.InkCanvas> によってボタンの背後にインクが収集され、レンダリングされます。 これは、ボタンが <xref:System.Windows.Controls.InkCanvas> の子ではなく兄弟であるためです。 また、ボタンは z オーダーの上位に位置するため、インクはその背後で描画されます。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Ink.DrawingAttributes>
- <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>
- <xref:System.Windows.Ink>
