---
title: Freezable オブジェクトの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Freezable objects [WPF], description
- unfreezing Freezable objects [WPF]
- classes [WPF], Freezable
ms.assetid: 89c71692-4f43-4057-b611-67c6a8a863a2
ms.openlocfilehash: b1887afd19407898d8de1d92252e29778899fb89
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2020
ms.locfileid: "77095191"
---
# <a name="freezable-objects-overview"></a>Freezable オブジェクトの概要

このトピックでは、アプリケーションのパフォーマンス向上に役立つ特殊な機能を提供する <xref:System.Windows.Freezable> オブジェクトを効果的に使用し、作成する方法について説明します。 freezable オブジェクトの例として、ブラシ、ペン、変換、ジオメトリ、アニメーションなどがあります。

<a name="whatisafreezable"></a>

## <a name="what-is-a-freezable"></a>Freezable とは

<xref:System.Windows.Freezable> は、非固定と固定という 2 つの状態を持つ特殊な型のオブジェクトです。 非固定の場合、<xref:System.Windows.Freezable> は他のオブジェクトと同じように動作します。 固定されると、<xref:System.Windows.Freezable> を変更できなくなります。

<xref:System.Windows.Freezable> には、オブジェクトに対する変更をオブザーバーに通知する <xref:System.Windows.Freezable.Changed> イベントが用意されています。 <xref:System.Windows.Freezable> を固定すると、変更通知にリソースを費やす必要がなくなるため、パフォーマンスが向上します。 固定された <xref:System.Windows.Freezable> は複数のスレッドで共有できますが、非固定の <xref:System.Windows.Freezable> はできません。

<xref:System.Windows.Freezable> クラスには多くのアプリケーションがありますが、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] のほとんどの <xref:System.Windows.Freezable> オブジェクトはグラフィックス サブシステムに関連しています。

<xref:System.Windows.Freezable> クラスによって、特定のグラフィックス システム オブジェクトを簡単に使用できるようになり、アプリケーションのパフォーマンス向上に役立ちます。 <xref:System.Windows.Freezable> から継承される型の例として、<xref:System.Windows.Media.Brush>、<xref:System.Windows.Media.Transform>、<xref:System.Windows.Media.Geometry> クラスなどがあります。 アンマネージ リソースが含まれているため、システムでこれらのオブジェクトの変更を監視し、元のオブジェクトに変更があった場合は対応するアンマネージ リソースを更新する必要があります。 グラフィックス システム オブジェクトを実際に変更していなくても、変更を実行する場合に備えて、システムではオブジェクトの監視にリソースの一部を費やす必要があります。

たとえば、<xref:System.Windows.Media.SolidColorBrush> ブラシを作成し、それを使用してボタンの背景を描画するとします。

[!code-csharp[freezablesample_procedural#FrozenExamplePart1](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#frozenexamplepart1)]
[!code-vb[freezablesample_procedural#FrozenExamplePart1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#frozenexamplepart1)]

ボタンがレンダリングされると、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] グラフィックス サブシステムでは、提供された情報を使用してピクセルのグループが描画され、ボタンの外観が作成されます。 ボタンの描画方法を説明するために単色ブラシを使用しましたが、この単色ブラシでは実際には描画を行いません。 グラフィックス システムによって、ボタンとブラシ用の高速で低レベルのオブジェクトが生成されます。実際に画面に表示されるのはこれらのオブジェクトです。

ブラシを変更する場合、それらの低レベル オブジェクトを再生成する必要があります。 freezable クラスは、生成された低レベルの対応するオブジェクトを見つけて、変更時にそれらを更新する機能をブラシに付与するものです。 この機能が有効な場合、ブラシは "非固定" と呼ばれます。

freezable の <xref:System.Windows.Freezable.Freeze%2A> メソッドを使用すると、この自己更新機能を無効にすることができます。 この方法を使用して、ブラシを "固定"、つまり変更不可にすることができます。

> [!NOTE]
> すべての Freezable オブジェクトを固定できるわけではありません。 <xref:System.InvalidOperationException> がスローされないようにするには、固定する前に、Freezable オブジェクトの <xref:System.Windows.Freezable.CanFreeze%2A> プロパティの値を確認して固定できるかどうかを判断します。

[!code-csharp[freezablesample_procedural#FrozenExamplePart2](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#frozenexamplepart2)]
[!code-vb[freezablesample_procedural#FrozenExamplePart2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#frozenexamplepart2)]

freezable を変更する必要がなくなった場合は、固定するとパフォーマンスが向上します。 この例のブラシを固定した場合、グラフィックス システムでブラシの変更を監視する必要がなくなります。 また、ブラシが変更されないことがわかっているため、グラフィックス システムで他の最適化を行うこともできます。

> [!NOTE]
> 便宜上、明示的に固定しない限り、freezable オブジェクトは固定されないままです。

<a name="frozenfreezables"></a>

## <a name="using-freezables"></a>Freezable の使用

固定されていない freezable の使用は、他の種類のオブジェクトの使用と同様です。 次の例では、<xref:System.Windows.Media.SolidColorBrush> の色は、ボタンの背景の描画に使用された後、黄色から赤に変更されます。 グラフィックス システムはバックグラウンドで動作しており、次に画面が更新されたときにボタンは自動的に黄色から赤に変更されます。

[!code-csharp[freezablesample_procedural#UnFrozenExampleShort](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#unfrozenexampleshort)]
[!code-vb[freezablesample_procedural#UnFrozenExampleShort](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#unfrozenexampleshort)]

### <a name="freezing-a-freezable"></a>Freezable の固定

<xref:System.Windows.Freezable> を変更不可にするには、その <xref:System.Windows.Freezable.Freeze%2A> メソッドを呼び出します。 freezable オブジェクトを含むオブジェクトを固定すると、それらのオブジェクトも固定されます。 たとえば、<xref:System.Windows.Media.PathGeometry> を固定すると、それに含まれる図とセグメントも固定されます。

次のいずれかに該当する場合、Freezable を固定**できません**。

- アニメーション化された、またはデータ バインドされたプロパティがあります。

- 動的リソースによって設定されるプロパティがあります (動的リソースの詳細については、[XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)に関する記事を参照してください)。

- 凍結できない <xref:System.Windows.Freezable> サブオブジェクトが含まれています。

これらの条件が false であり、<xref:System.Windows.Freezable> を変更する予定がない場合は、前述したように、固定してパフォーマンスを向上させることをお勧めします。

freezable の <xref:System.Windows.Freezable.Freeze%2A> メソッドを呼び出すと、変更できなくなります。 固定されたオブジェクトを変更しようとすると、<xref:System.InvalidOperationException> がスローされます。 次のコードでは、固定後にブラシを変更しようとしているため、例外がスローされます。

[!code-csharp[freezablesample_procedural#ExceptionExample](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#exceptionexample)]
[!code-vb[freezablesample_procedural#ExceptionExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#exceptionexample)]

この例外がスローされないようにするには、<xref:System.Windows.Freezable.IsFrozen%2A> メソッドを使用して、<xref:System.Windows.Freezable> が固定されているかどうかを確認します。

[!code-csharp[freezablesample_procedural#CheckIsFrozenExample](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#checkisfrozenexample)]
[!code-vb[freezablesample_procedural#CheckIsFrozenExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#checkisfrozenexample)]

前のコード例では、<xref:System.Windows.Freezable.Clone%2A> メソッドを使用して、固定されたオブジェクトから変更可能なコピーが作成されました。 次のセクションでは、複製について詳しく説明します。

> [!NOTE]
> 固定された freezable オブジェクトはアニメーション化できないため、<xref:System.Windows.Media.Animation.Storyboard> でアニメーション化しようとすると、アニメーション システムによって、固定された <xref:System.Windows.Freezable> オブジェクトの変更可能なクローンが自動的に作成されます。 複製によるパフォーマンスのオーバーヘッドをなくすには、アニメーション化する場合にオブジェクトを固定しないでください。 アニメーション化とストーリーボードの詳細については、「[ストーリーボードの概要](../graphics-multimedia/storyboards-overview.md)」を参照してください。

### <a name="freezing-from-markup"></a>マークアップからの固定

マークアップで宣言された <xref:System.Windows.Freezable> オブジェクトを固定するには、`PresentationOptions:Freeze` 属性を使用します。 次の例では、<xref:System.Windows.Media.SolidColorBrush> がページ リソースとして宣言され、固定されています。 これは、ボタンの背景を設定するために使用されます。

[!code-xaml[FreezableSample#FreezeFromMarkupWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FreezableSample/CS/FreezeFromMarkupExample.xaml#freezefrommarkupwholepage)]

`Freeze` 属性を使用するには、プレゼンテーション オプション名前空間 `http://schemas.microsoft.com/winfx/2006/xaml/presentation/options` にマップする必要があります。 `PresentationOptions` は、この名前空間のマッピングに推奨されるプレフィックスです。

```xaml
xmlns:PresentationOptions="http://schemas.microsoft.com/winfx/2006/xaml/presentation/options"
```

すべての XAML リーダーでこの属性が認識されるわけではないため、[mc:Ignorable 属性](mc-ignorable-attribute.md)を使用して、`Presentation:Freeze` 属性を無視できるものとしてマークすることをお勧めします。

```xaml
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="PresentationOptions"
```

詳細については、「[mc:Ignorable 属性](mc-ignorable-attribute.md)」ページを参照してください。

### <a name="unfreezing-a-freezable"></a>Freezable の "固定解除"

固定された後に、<xref:System.Windows.Freezable> を変更または固定解除することはできなくなります。ただし、<xref:System.Windows.Freezable.Clone%2A> または <xref:System.Windows.Freezable.CloneCurrentValue%2A> メソッドを使用して、固定されていない複製を作成できます。

次の例では、ボタンの背景にブラシを設定し、そのブラシを固定しています。 固定されていないコピーは、<xref:System.Windows.Freezable.Clone%2A> メソッドを使用してブラシから作成されます。 ボタンの背景を黄色から赤色に変更するために、複製が変更され、使用されます。

[!code-csharp[freezablesample_procedural#CloneExample](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#cloneexample)]
[!code-vb[freezablesample_procedural#CloneExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#cloneexample)]

> [!NOTE]
> 使用する複製方法に関係なく、アニメーションが新しい <xref:System.Windows.Freezable> にコピーされることはありません。

<xref:System.Windows.Freezable.Clone%2A> および <xref:System.Windows.Freezable.CloneCurrentValue%2A> メソッドを使用すると、freezable のディープ コピーが生成されます。 freezable に他の固定された freezable オブジェクトが含まれている場合は、それらも複製され、変更可能になります。 たとえば、固定された <xref:System.Windows.Media.PathGeometry> を複製して変更可能にすると、そこに含まれる図形とセグメントもコピーされ、変更可能になります。

<a name="createyourownfreezableclass"></a>

## <a name="creating-your-own-freezable-class"></a>独自の Freezable クラスの作成

<xref:System.Windows.Freezable> から派生するクラスには、次の機能があります。

- 特別な状態: 読み取り専用 (固定) および書き込み可能な状態。

- スレッド セーフ: 固定された <xref:System.Windows.Freezable> はスレッド間で共有できます。

- 詳細な変更通知:他の <xref:System.Windows.DependencyObject> とは異なり、Freezable オブジェクトからは、サブプロパティ値が変更されたときに変更通知が提供されます。

- 簡単な複製: Freezable クラスには、ディープ クローンを生成するいくつかのメソッドが既に実装されています。

<xref:System.Windows.Freezable> は <xref:System.Windows.DependencyObject> の一種であるため、依存関係プロパティ システムが使用されます。 クラスのプロパティは必ずしも依存関係プロパティではありません。ただし、依存関係プロパティを使用する場合、<xref:System.Windows.Freezable> クラスは依存関係プロパティを考慮して設計されているため、記述しなければならないコードの量が減ります。 依存関係プロパティ システムの詳細については、「[依存関係プロパティの概要](dependency-properties-overview.md)」を参照してください。

すべての <xref:System.Windows.Freezable> サブクラスで <xref:System.Windows.Freezable.CreateInstanceCore%2A> メソッドをオーバーライドする必要があります。 クラスで、すべてのデータに依存関係プロパティが使用されている場合は、これで完了です。

クラスに非依存関係プロパティ データ メンバーが含まれている場合は、次のメソッドもオーバーライドする必要があります。

- <xref:System.Windows.Freezable.CloneCore%2A>

- <xref:System.Windows.Freezable.CloneCurrentValueCore%2A>

- <xref:System.Windows.Freezable.GetAsFrozenCore%2A>

- <xref:System.Windows.Freezable.GetCurrentValueAsFrozenCore%2A>

- <xref:System.Windows.Freezable.FreezeCore%2A>

また、依存関係プロパティではないデータ メンバーへのアクセスと書き込みについては、次の規則に従う必要があります。

- 非依存関係プロパティ データ メンバーを読み取る API の先頭で、<xref:System.Windows.Freezable.ReadPreamble%2A> メソッドを呼び出します。

- 非依存関係プロパティ データ メンバーを書き込む API の先頭で、<xref:System.Windows.Freezable.WritePreamble%2A> メソッドを呼び出します (API で <xref:System.Windows.Freezable.WritePreamble%2A> を呼び出した後に、非依存関係プロパティ データ メンバーも読み取る場合、<xref:System.Windows.Freezable.ReadPreamble%2A> をさらに呼び出す必要はありません)。

- 非依存関係プロパティ データ メンバーに書き込むメソッドを終了する前に、<xref:System.Windows.Freezable.WritePostscript%2A> メソッドを呼び出します。

クラスに <xref:System.Windows.DependencyObject> オブジェクトである非依存関係プロパティ データ メンバーが含まれている場合、メンバーを `null` に設定している場合でも、いずれかの値を変更するたびに <xref:System.Windows.Freezable.OnFreezablePropertyChanged%2A> メソッドも呼び出す必要があります。

> [!NOTE]
> 基本実装を呼び出すことで、オーバーライドする各 <xref:System.Windows.Freezable> メソッドを開始することが非常に重要です。

カスタムの <xref:System.Windows.Freezable> クラスの例については、[カスタム アニメーションのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/CustomAnimation)を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Freezable>
- [カスタム アニメーションのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/CustomAnimation)
- [依存関係プロパティの概要](dependency-properties-overview.md)
- [カスタム依存関係プロパティ](custom-dependency-properties.md)
