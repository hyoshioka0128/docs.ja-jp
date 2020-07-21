---
title: スタイラスからの入力のインターセプト
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- 'architecture [WPF], '
- ', '
- ', '
- ', '
ms.assetid: 791bb2f0-4e5c-4569-ac3c-211996808d44
ms.openlocfilehash: 17cf42a9d6d94d6ea12399561af5647df3b4d8c2
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79181918"
---
# <a name="intercepting-input-from-the-stylus"></a>スタイラスからの入力のインターセプト
<xref:System.Windows.Input.StylusPlugIns> アーキテクチャには、<xref:System.Windows.Input.Stylus> の入力およびデジタル インクの <xref:System.Windows.Ink.Stroke> オブジェクトの作成に対する低レベルの制御を実装するためのメカニズムが用意されています。 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> クラスでは、パフォーマンスを最適にするために、カスタム動作を実装し、スタイラス デバイスから送信されるデータ ストリームにそれを適用するためのメカニズムが提供されています。  
  
 このトピックは、次の内容で構成されています。  
  
- [アーキテクチャ](#Architecture)  
  
- [スタイラス プラグインの実装](#ImplementingStylusPlugins)  
  
- [InkCanvas へのプラグインの追加](#AddingYourPluginToAnInkCanvas)  
  
- [まとめ](#Conclusion)  
  
<a name="Architecture"></a>
## <a name="architecture"></a>アーキテクチャ  
 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> は、「[ペン入力へのアクセスとその操作](https://docs.microsoft.com/previous-versions/ms818317(v%3dmsdn.10))」で説明されている [StylusInput](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms574861(v=vs.90)) API が進化したものです。  
  
 各 <xref:System.Windows.UIElement> には、<xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> である <xref:System.Windows.UIElement.StylusPlugIns%2A> プロパティがあります。 要素の <xref:System.Windows.UIElement.StylusPlugIns%2A> プロパティに <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> を追加して、生成時に <xref:System.Windows.Input.StylusPoint> のデータを操作できます。 <xref:System.Windows.Input.StylusPoint> のデータは、<xref:System.Windows.Input.StylusPoint.X%2A> および <xref:System.Windows.Input.StylusPoint.Y%2A> のポイント データや <xref:System.Windows.Input.StylusPoint.PressureFactor%2A> など、システム デジタイザーによってサポートされているすべてのプロパティで構成されます。  
  
 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> を <xref:System.Windows.UIElement.StylusPlugIns%2A> プロパティに追加すると、<xref:System.Windows.Input.Stylus> デバイスから送信されるデータ ストリームに、<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> オブジェクトが直接挿入されます。 プラグインが <xref:System.Windows.UIElement.StylusPlugIns%2A> コレクションに追加される順序によって、<xref:System.Windows.Input.StylusPoint> データを受信する順序が決まります。 たとえば、入力を特定の領域に制限するフィルター プラグインを追加した後、書き込まれたジェスチャを認識するプラグインを追加した場合、ジェスチャを認識するプラグインは、フィルター処理された <xref:System.Windows.Input.StylusPoint> データを受け取ります。  
  
<a name="ImplementingStylusPlugins"></a>
## <a name="implementing-stylus-plug-ins"></a>スタイラス プラグインの実装  
 プラグインを実装するには、<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> の派生クラスを作成します。 このクラスは、<xref:System.Windows.Input.Stylus> から送られてくるデータのストリームに適用されます。 このクラスでは、<xref:System.Windows.Input.StylusPoint> データの値を変更できます。  
  
> [!CAUTION]
> <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> で例外がスローされた場合、またはそれが例外の原因になった場合、アプリケーションは終了します。 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> を使用するコントロールを十分にテストし、<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> で例外がスローされないことが確実な場合にのみ、コントロールを使用する必要があります。  
  
 次の例では、<xref:System.Windows.Input.Stylus> デバイスから送られてきた <xref:System.Windows.Input.StylusPoint> データの <xref:System.Windows.Input.StylusPoint.X%2A> と <xref:System.Windows.Input.StylusPoint.Y%2A> の値を変更することによって、スタイラスの入力を制限するプラグインを示します。  
  
 [!code-csharp[AdvancedInkTopicsSamples#19](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#19)]
 [!code-vb[AdvancedInkTopicsSamples#19](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#19)]  
[!code-csharp[AdvancedInkTopicsSamples#3](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#3)]
[!code-vb[AdvancedInkTopicsSamples#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#3)]  
  
<a name="AddingYourPluginToAnInkCanvas"></a>
## <a name="adding-your-plug-in-to-an-inkcanvas"></a>InkCanvas へのプラグインの追加  
 カスタム プラグインを使用する最も簡単な方法は、InkCanvas から派生するクラスを実装し、それを <xref:System.Windows.UIElement.StylusPlugIns%2A> プロパティに追加することです。  
  
 次の例では、インクをフィルター処理するカスタム <xref:System.Windows.Controls.InkCanvas> を示します。  
  
 [!code-csharp[AdvancedInkTopicsSamples#4](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/Window1.xaml.cs#4)]  
  
 `FilterInkCanvas` をアプリケーションに追加して実行すると、ユーザーがストロークを完了するまで、インクの領域が限定されないことがわかります。 これは、<xref:System.Windows.Controls.InkCanvas> には <xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A> プロパティがありますが、それは <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> であり、既に <xref:System.Windows.UIElement.StylusPlugIns%2A> コレクションのメンバーになっているためです。 <xref:System.Windows.UIElement.StylusPlugIns%2A> コレクションに追加したカスタム <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> は、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> がデータを受け取った後で、<xref:System.Windows.Input.StylusPoint> データを受け取ります。 その結果、ユーザーがペンを上げてストロークを終了するまで、<xref:System.Windows.Input.StylusPoint> データはフィルター処理されません。 ユーザーが描画するのと同時にインクをフィルター処理するには、<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> の前に `FilterPlugin` を挿入する必要があります。  
  
 次の C# コードでは、描画と同時にインクをフィルター処理するカスタム <xref:System.Windows.Controls.InkCanvas> を示します。  
  
 [!code-csharp[AdvancedInkTopicsSamples#5](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/Window1.xaml.cs#5)]  
  
<a name="Conclusion"></a>
## <a name="conclusion"></a>まとめ  
 独自の <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> クラスを派生させて <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> コレクションに挿入することにより、デジタル インクの動作を大幅に拡張できます。 生成されている <xref:System.Windows.Input.StylusPoint> データにアクセスし、<xref:System.Windows.Input.Stylus> の入力をカスタマイズすることができます。 そのように低いレベルで <xref:System.Windows.Input.StylusPoint> のデータにアクセスできるため、アプリケーションに最適なパフォーマンスでインクのコレクションとレンダリングを実装できます。  
  
## <a name="see-also"></a>関連項目

- [高度なインク処理](advanced-ink-handling.md)
- [ペン入力へのアクセスとその操作](https://docs.microsoft.com/previous-versions/ms818317(v%3dmsdn.10))
