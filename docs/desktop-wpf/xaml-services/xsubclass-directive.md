---
title: x:Subclass ディレクティブ
ms.date: 03/30/2017
f1_keywords:
- Subclass
- xSubclass
- x:Subclass
helpviewer_keywords:
- x:Subclass attribute [XAML Services]
- XAML [XAML Services], x:Subclass attribute
- Subclass attribute in XAML [XAML Services]
ms.assetid: 99f66072-8107-4362-ab99-8171dc83b469
ms.openlocfilehash: e85e0fb5a0e1a865ed84a93767f8152a115bbe5f
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432642"
---
# <a name="xsubclass-directive"></a>x:Subclass ディレクティブ

XAML マークアップ コンパイル動作を`x:Class`変更します ( 指定されている場合 ) 。 に`x:Class`基づく部分クラスを作成する代わりに、提供`x:Class`されるクラスは中間クラスとして作成され、指定された派生クラスは に基`x:Class`づくと想定されます。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<object x:Class="namespace.classname" x:Subclass="subclassNamespace.subclassName">
   ...
</object>
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|`namespace`|省略可能。 を含む`classname`CLR 名前空間を指定します。 指定`namespace`した場合、ドット (.) は`namespace`、`classname`と を区切ります。|
|`classname`|必須。 読み込まれた XAML とその XAML の分離コードを接続する部分クラスの CLR 名を指定します。 「解説」を参照してください。|
|`subclassNamespace`|省略可能。 各名前空間が他`namespace`の名前空間を解決できる場合とは異なる場合があります。 を含む`subclassName`CLR 名前空間を指定します。 指定`subclassName`した場合、ドット (.) は`subclassNamespace`、`subclassName`と を区切ります。|
|`subclassName`|必須。 サブクラスの CLR 名を指定します。|

## <a name="dependencies"></a>依存関係

[x: Class ディレクティブ](xclass-directive.md)も同じオブジェクトに提供する必要があり、そのオブジェクトは XAML 運用環境のルート要素である必要があります。

## <a name="remarks"></a>解説

`x:Subclass`使用法は、主に部分クラス宣言をサポートしない言語を対象としています。

として`x:Subclass`使用されるクラスは、入れ子になったクラスにすることはできません`x:Subclass`。

それ以外の場合、概`x:Subclass`念的な意味は .NET XAML サービスの実装によって定義されていません。 これは、.NET XAML サービスの動作では、XAML マークアップとバッキング コードが接続される全体的なプログラミング モデルが指定されないためです。 プログラミング モデルまたはアプリケーション モデル`x:Class`を`x:Subclass`使用して、XAML マークアップ、コンパイル済みマークアップ、および CLR ベースの分離コードを接続する方法を定義する特定のフレームワークによって、さらに概念の実装が実行されます。 各フレームワークには、動作の一部を有効にする独自のビルド アクション、またはビルド環境に含める必要がある特定のコンポーネントを持つ場合があります。 フレームワーク内では、ビルド アクションは分離コードに使用される特定の CLR 言語によって異なる場合もあります。

## <a name="wpf-usage-notes"></a>WPF の使用上の注意

`x:Subclass`ページ ルートまたはアプリケーション定義の<xref:System.Windows.Application>ルートに指定できます。 `x:Class` ページ`x:Subclass`またはアプリケーション ルート以外の要素で宣言するか、存在しない`x:Class`場所で指定すると、コンパイル エラーが発生します。

シナリオに対して正しく機能する`x:Subclass`派生クラスの作成は、非常に複雑です。 中間ファイル (マークアップ コンパイルによってプロジェクトの obj フォルダーに作成される .g ファイルと、.xaml ファイル名を組み込んだ名前) を調べる必要があります。 これらの中間ファイルは、コンパイル済みアプリケーションの結合部分クラス内の特定のプログラミング構成要素の起点を判別するのに役立ちます。

コンパイル時に中間クラスで作成された`internal override`ハンドラー`Friend Overrides`のスタブをオーバーライドするには、派生クラスのイベント ハンドラーが ( Microsoft Visual Basic で ) 必要があります。 それ以外の場合、派生クラスの実装は、中間クラスの実装と中間クラス ハンドラーを非表示 (シャドウ) にします。

と の`x:Class``x:Subclass`両方を定義する場合は、 で`x:Class`参照されるクラスの実装を提供する必要はありません。 コンパイラが中間ファイルで作成するクラスに対`x:Class`して何らかのガイダンスを持つため、属性を使用して名前を付けるだけで済みます (この場合、コンパイラは既定の名前を選択しません)。 クラスに実装を`x:Class`与えることができます。ただし、これは、 と の`x:Class``x:Subclass`両方を使用する一般的なシナリオではありません。

## <a name="see-also"></a>関連項目

- [x:Class ディレクティブ](xclass-directive.md)
- [WPF における XAML とカスタム クラス](../../framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)
