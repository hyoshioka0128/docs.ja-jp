---
title: x:Shared 属性
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], x:Shared attribute
- x:Shared attribute [XAML Services]
- Shared attribute in XAML [XAML Services]
ms.assetid: c8cff434-2785-405f-9f95-16deb34c9e64
ms.openlocfilehash: e1cd1d9db5c19decd840b433f986e0ba53557a8b
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432648"
---
# <a name="xshared-attribute"></a>x:Shared 属性

に`false`設定すると、WPF リソース取得動作が変更され、属性付きリソースに対する要求がすべての要求に対して同じインスタンスを共有するのではなく、要求ごとに新しいインスタンスが作成されるようにします。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<ResourceDictionary>
  <object x:Shared="false".../>
</ResourceDictionary>
```

## <a name="remarks"></a>解説

`x:Shared`XAML 言語 XAML 名前空間にマップされ、.NET XAML サービスとその XAML リーダーによって有効な XAML 言語要素として認識されます。 ただし、上記の`x:Shared`機能は、WPF アプリケーションと WPF XAML パーサーにのみ関連します。 WPF では`x:Shared`、属性が WPF<xref:System.Windows.ResourceDictionary>内に存在するオブジェクトに適用される場合にのみ、属性として役立ちます。 その他の使用法では、解析例外やその他のエラーはスローされませんが、影響はありません。

の`x:Shared`意味は XAML 言語仕様では指定されていません。 .NET XAML サービスをベースに構築する XAML 実装など、他の XAML 実装では、リソース共有のサポートが必ずしも提供されるとは限りません。 このような XAML 実装は、同様の動作をサポートフレームワークで提供`x:Shared`し、同様に値を使用する場合があります。

WPF では、リソース`x:Shared`の既定の条件`true`は です。 この条件は、特定のリソース要求が常に同じインスタンスを返すということを意味します。

などの<xref:System.Windows.FrameworkElement.FindResource%2A>リソース API を通じて返されるオブジェクトを変更したり、 内で<xref:System.Windows.ResourceDictionary>直接オブジェクトを変更したりすると、元のリソースが変更されます。 そのリソースへの参照が動的リソース参照である場合、そのリソースのコンシューマーは変更されたリソースを取得します。

リソースへの参照が静的リソース参照であった場合、処理時間の経過後[!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)]のリソースへの変更は関係ありません。 静的リソース参照と動的リソース参照の詳細については[、「XAML リソース](../fundamentals/xaml-resources-define.md)」を参照してください。

明示的な指定`x:Shared="true"`は、すでにデフォルトであるため、めったに行われません。 WPF オブジェクト モデルに相当`x:Shared`する直接のコードはありません。このメソッドは XAML の使用法でのみ指定でき、.NET XAML サービスとその XAML リーダーを使用して処理される場合は、既定の WPF 動作または読み込みパスの中間 XAML ノード ストリームで処理する必要があります。

シナリオ`x:Shared="false"`としては、 または<xref:System.Windows.FrameworkElement><xref:System.Windows.FrameworkContentElement>派生クラスをリソースとして定義し、その要素リソースをコンテンツ モデルに導入する場合です。 `x:Shared="false"`では、同じコレクション (a など) で要素リソースを複数回<xref:System.Windows.Controls.UIElementCollection>導入できます。 コレクション`x:Shared="false"`は、その内容の一意性を強制するため、この値を指定しない場合は無効です。 ただし、この`x:Shared="false"`動作では、同じインスタンスを返すのではなく、リソースの別の同一のインスタンスが作成されます。

もう 1`x:Shared="false"`つのシナリオは、<xref:System.Windows.Freezable>アニメーション値にリソースを使用するが、アニメーションごとにリソースを変更する場合です。

の文字列処理`false`では、大文字と小文字は区別されません。

WPF では`x:Shared`、次の条件でのみ有効です。

- と<xref:System.Windows.ResourceDictionary>の`x:Shared`アイテムを含む をコンパイルする必要があります。 緩<xref:System.Windows.ResourceDictionary>い XAML 内に含めたり、テーマに使用したりすることはできません。

- アイテム<xref:System.Windows.ResourceDictionary>を含む は、別<xref:System.Windows.ResourceDictionary>の . たとえば、 内のアイテム`x:Shared`が既に<xref:System.Windows.ResourceDictionary><xref:System.Windows.Style><xref:System.Windows.ResourceDictionary>アイテムである場合は使用できません。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.ResourceDictionary>
- [XAML リソース](../fundamentals/xaml-resources-define.md)
- [基本要素](../../framework/wpf/advanced/base-elements.md)
