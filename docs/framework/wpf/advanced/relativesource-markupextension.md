---
title: RelativeSource のマークアップ拡張機能
ms.date: 03/30/2017
f1_keywords:
- RelativeSource
helpviewer_keywords:
- RelativeSource markup extensions [WPF]
- XAML [WPF], RelativeSource markup extension
ms.assetid: 26be4721-49b5-4717-a92e-7d54ad0d3a81
ms.openlocfilehash: 7a9c9fe379f361dec0d65b71c4d883958be9ed2f
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834828"
---
# <a name="relativesource-markupextension"></a>RelativeSource のマークアップ拡張機能

[バインドマークアップ拡張機能](binding-markup-extension.md)内で使用されるか、XAML で確立される <xref:System.Windows.Data.Binding> 要素の @no__t プロパティを設定するときに、@no__t 0 バインディングソースのプロパティを指定します。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xml
<Binding RelativeSource="{RelativeSource modeEnumValue}" .../>
```

## <a name="xaml-attribute-usage-nested-within-binding-extension"></a>XAML 属性の使用方法 (バインディング拡張内で入れ子にした場合)

```xml
<object property="{Binding RelativeSource={RelativeSource modeEnumValue} ...}" .../>
```

## <a name="xaml-object-element-usage"></a>XAML オブジェクト要素の使用方法

```xml
<Binding>
  <Binding.RelativeSource>
    <RelativeSource Mode="modeEnumValue"/>
  </Binding.RelativeSource>
</Binding>
```

\- または -

```xml
<Binding>
  <Binding.RelativeSource>
    <RelativeSource
      Mode="FindAncestor"
      AncestorType="{x:Type typeName}"
      AncestorLevel="intLevel"
    />
  </Binding.RelativeSource>
</Binding>
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|`modeEnumValue`|次のいずれかです。<br /><br /> -文字列トークン `Self`;@no__t の2つのプロパティを <xref:System.Windows.Data.RelativeSourceMode.Self> に設定して作成された <xref:System.Windows.Data.RelativeSource> に対応します。<br />-文字列トークン `TemplatedParent`;@no__t の2つのプロパティを <xref:System.Windows.Data.RelativeSourceMode.TemplatedParent> に設定して作成された <xref:System.Windows.Data.RelativeSource> に対応します。<br />-文字列トークン `PreviousData`;@no__t の2つのプロパティを <xref:System.Windows.Data.RelativeSourceMode.PreviousData> に設定して作成された <xref:System.Windows.Data.RelativeSource> に対応します。<br />-@No__t 0 モードの詳細については、以下を参照してください。|
|`FindAncestor`|文字列トークン `FindAncestor`。 このトークンを使用すると、`RelativeSource` によって先祖の型およびオプションで先祖レベルを指定するモードになります。 これは、<xref:System.Windows.Data.RelativeSource> プロパティが <xref:System.Windows.Data.RelativeSource.Mode%2A> に設定された状態で作成された <xref:System.Windows.Data.RelativeSourceMode.FindAncestor> に対応します。|
|`typeName`|`FindAncestor` モードで必要です。 <xref:System.Windows.Data.RelativeSource.AncestorType%2A> プロパティに指定する型の名前。|
|`intLevel`|`FindAncestor` モードのオプションです。 論理ツリー内で親の方向に向けて数えた先祖レベル。|

## <a name="remarks"></a>コメント

`{RelativeSource TemplatedParent}` バインディングの使用は、コントロールの UI とコントロールのロジックを分離するという大きな概念に対処する重要な手法です。 これによって、テンプレートが適用される親 (テンプレートが適用されるランタイム オブジェクト インスタンス) へのバインディングをテンプレート定義内から行うことができます。 この場合、 [TemplateBinding マークアップ拡張機能](templatebinding-markup-extension.md)は、実際には次のバインド式の短縮形になります。 `{Binding RelativeSource={RelativeSource TemplatedParent}}`. `TemplateBinding` または `{RelativeSource TemplatedParent}` の使用は、どちらもテンプレートを定義する XAML 内でのみ関連します。 詳細については、「 [TemplateBinding Markup Extension](templatebinding-markup-extension.md)」を参照してください。

@no__t 0 は、コントロールテンプレートまたは予測可能な自己完結型 UI コンポジションで主に使用されます。この場合、コントロールは常に特定の先祖タイプのビジュアルツリー内にあることが想定されます。 たとえば、項目コントロールの各項目は `FindAncestor` を使用して、その項目コントロールの親先祖のプロパティにバインドすることができます。 または、テンプレート内のコントロール合成に参加している要素は、同じ合成体系の親要素に対して `FindAncestor` バインディングを使用できます。

XAML 構文のセクションに示した `FindAncestor` モードのオブジェクト要素構文では、2 番目のオブジェクト要素構文は `FindAncestor` モード向けに使用されます。 `FindAncestor` モードでは、<xref:System.Windows.Data.RelativeSource.AncestorType%2A> 値が必要です。 検索する先祖の型への[X:Type マークアップ拡張機能](../../xaml-services/x-type-markup-extension.md)の参照を使用して、属性として <xref:System.Windows.Data.RelativeSource.AncestorType%2A> を設定する必要があります。 <xref:System.Windows.Data.RelativeSource.AncestorType%2A> 値は、実行時にバインディング要求を処理する際に使用されます。

`FindAncestor` モードでは、オプションの <xref:System.Windows.Data.RelativeSource.AncestorLevel%2A> プロパティは、要素ツリー内に型の先祖が複数存在する可能性がある場合に、先祖の検索のあいまいさを解消するのに役立ちます。

`FindAncestor` モードの使用方法の詳細については、「<xref:System.Windows.Data.RelativeSource>」を参照してください。

`{RelativeSource Self}` は、インスタンスの1つのプロパティが同じインスタンスの別のプロパティの値に依存する必要があり、これら2つのプロパティ間には、一般的な依存関係プロパティの関係 (強制型変換など) が既に存在する場合に便利です。 1つのオブジェクトに2つのプロパティが存在することはめったにありませんが、値が文字どおり同じであり、同じように型指定されている場合もありますが、`{RelativeSource Self}` を持つバインディングに @no__t 0 パラメーターを適用し、コンバーターを使用してソースとターゲットの型の間で変換を行うことができます。 @No__t-0 のもう1つのシナリオは、<xref:System.Windows.MultiDataTrigger> の一部です。

たとえば、<xref:System.Windows.Shapes.Rectangle> という XAML は、<xref:System.Windows.FrameworkElement.Width%2A> 要素を定義します。<xref:System.Windows.Shapes.Rectangle> にどのような値が入力されても、`<Rectangle Width="200" Height="{Binding RelativeSource={RelativeSource Self}, Path=Width}" .../>` は常に正方形となります。

`{RelativeSource PreviousData}` は、データテンプレートで、またはバインディングがデータソースとしてコレクションを使用する場合に便利です。 @No__t-0 を使用すると、コレクション内の隣接するデータ項目間のリレーションシップを強調表示できます。 これと関連して、データ ソース内の現在の項目と直前の項目との間に <xref:System.Windows.Data.MultiBinding> を確立し、そのバインディング上のコンバーターを使用して、2 つの項目 (およびそれらのプロパティ) 間の相違を特定する手法もあります。

次の例の項目テンプレートに出現する 1 つ目の <xref:System.Windows.Controls.TextBlock> は、現在の数値を表示します。 2番目の <xref:System.Windows.Controls.TextBlock> バインド @no__t は、とに @no__t 2 つの構成要素があることを示します。これは、現在のレコードと、前のデータレコードを意図的に `{RelativeSource PreviousData}` を使用して使用するバインドです。 <xref:System.Windows.Data.MultiBinding> 上のコンバーターが、両者の差を計算し、バインディングに返します。

```xml
<ListBox Name="fibolist">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <StackPanel Orientation="Horizontal">
            <TextBlock Text="{Binding}"/>
            <TextBlock>, difference = </TextBlock>
                <TextBlock>
                    <TextBlock.Text>
                        <MultiBinding Converter="{StaticResource DiffConverter}">
                            <Binding/>
                            <Binding RelativeSource="{RelativeSource PreviousData}"/>
                        </MultiBinding>
                    </TextBlock.Text>
                </TextBlock>
            </StackPanel>
        </DataTemplate>
    </ListBox.ItemTemplate>
```

データバインディングの概念については、ここでは説明しません。「[データバインディングの概要](../data/data-binding-overview.md)」を参照してください。

@No__t 0 の XAML プロセッサ実装では、このマークアップ拡張機能の処理は、<xref:System.Windows.Data.RelativeSource> クラスによって定義されます。

`RelativeSource` はマークアップ拡張機能です。 一般にマークアップ拡張機能を実装するのは、属性値をリテラル値やハンドラー名以外にエスケープする要件が存在し、その要件の適用範囲がグローバルで、特定の型やプロパティに型コンバーターを適用するだけにとどまらない場合です。 XAML のすべてのマークアップ拡張は、属性構文で `{` および `}` 文字を使用します。これは、マークアップ拡張機能が属性を処理する必要があることを XAML プロセッサが認識する規則です。 詳細については、「[マークアップ拡張機能」および「WPF XAML](markup-extensions-and-wpf-xaml.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Data.Binding>
- [スタイルとテンプレート](../controls/styling-and-templating.md)
- [XAML の概要 (WPF)](xaml-overview-wpf.md)
- [マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)
- [データ バインディングの概要](../data/data-binding-overview.md)
- [バインディング宣言の概要](../data/binding-declarations-overview.md)
- [x:Type マークアップ拡張機能](../../xaml-services/x-type-markup-extension.md)
