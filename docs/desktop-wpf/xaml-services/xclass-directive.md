---
title: x:Class ディレクティブ
ms.date: 03/30/2017
f1_keywords:
- x:Class
- xClass
- Class
helpviewer_keywords:
- Class attribute in XAML [XAML Services]
- XAML [XAML Services], x:Class attribute
- x:Class attribute [XAML Services]
ms.assetid: bc4a3d8e-76e2-423e-a5d1-159a023e82ec
ms.openlocfilehash: f589fa70c2ee1c56544fa0f0152990478aa3761f
ms.sourcegitcommit: 99b153b93bf94d0fecf7c7bcecb58ac424dfa47c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2020
ms.locfileid: "81433278"
---
# <a name="xclass-directive"></a>x:Class ディレクティブ
マークアップと分離コードの間で部分クラスを結合するように XAML マークアップ コンパイルを構成します。 コード部分クラスは共通言語仕様 (CLS) 言語の個別のコード ファイルで定義されますが、マークアップ部分クラスは通常、XAML コンパイル時にコード生成によって作成されます。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<object x:Class="namespace.classname"...>
  ...
</object>
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|`namespace`|省略可能。 で識別される部分クラスを含む CLR`classname`名前空間を指定します。 指定`namespace`した場合、ドット (.) は`namespace`、`classname`と を区切ります。 「解説」を参照してください。|
|`classname`|必須。 読み込まれた XAML とその XAML の分離コードを接続する部分クラスの CLR 名を指定します。|

## <a name="dependencies"></a>依存関係

`x:Class`XAML の運用環境のルート要素でのみ指定できます。 `x:Class`は、XAML 運用環境で親を持つすべてのオブジェクトに対して無効です。 詳細については、 [ \[MS-XAML\]セクション 4.3.1.6](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))を参照してください。

## <a name="remarks"></a>解説

この`namespace`値には、関連する名前空間を名前階層に整理するための追加のドットが含まれる場合があります。 値の文字列`x:Class`の最後のドットのみが分離`namespace`に解釈され、`classname.`として使用されるクラスは入れ子`x:Class`になったクラスにすることはできません。 入れ子になったクラスが許可されている場合、文字列のドットの意味`x:Class`を判断することはあいまいであるため、入れ子になったクラスは許可されません。

を`x:Class``x:Class`使用する既存のプログラミング モデルでは、分離コードのない XAML ページを持つことは完全に有効であるという意味ではオプションです。 ただし、この機能は、XAML を使用するフレームワークによって実装されるビルド アクションと対話します。 `x:Class`また、アプリケーション モデルおよび対応するビルド アクションで、XAML で指定されたコンテンツのさまざまな分類が持つロールによっても影響を受けます。 XAML でイベント処理属性値を宣言する場合、または定義クラスが分離コード クラスにあるカスタム要素をインスタンス化する場合は、分離コードに対`x:Class`する適切なクラスにディレクティブ参照 (または[x:Subclass)](xsubclass-directive.md)を指定する必要があります。

ディレクティブの`x:Class`値は、アセンブリ情報を含まないクラスの完全修飾名を指定する文字列である必要があります ( と<xref:System.Type.FullName%2A?displayProperty=nameWithType>同じです)。 単純なアプリケーションでは、分離コードもその方法で構造化されている場合 (コード定義はクラス レベルで開始される) 場合は、CLR 名前空間情報を省略できます。

ページまたはアプリケーション定義の分離コード ファイルは、コンパイル済みアプリケーションを生成し、マークアップコンパイルを伴うプロジェクトの一部として含まれるコード ファイル内になければなりません。 CLR クラスの名前規則に従う必要があります。 詳細については、「[フレームワーク設計ガイドライン](../../../api/index.md)」を参照してください。 既定では、分離コード クラスは`public`;ただし[、x:ClassModifier ディレクティブ](xclassmodifier-directive.md)を使用して、異なるアクセス レベルで定義できます。

この属性の`x:Class`解釈は、CLR ベースの XAML 実装にのみ適用され、特に .NET XAML サービスに適用されます。 CLR に基づいておらず、.NET XAML サービスを使用しないその他の XAML 実装では、XAML マークアップを接続し、ランタイム コードをバッキングするために別の解決方法を使用する場合があります。 の一般的な解釈の`x:Class`詳細については、「 [ \[MS-XAML\]](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))」を参照してください。

アーキテクチャの特定のレベルでは、.NET `x:Class` XAML サービスでは、の意味は定義されていません。 これは、.NET XAML サービスでは、XAML マークアップとバッキング コードが接続されるプログラミング モデルが指定されないためです。 `x:Class`ディレクティブの追加の使用は、XAML マークアップと CLR ベースの分離コードを接続する方法を定義するプログラミング モデルまたはアプリケーション モデルを使用する特定のフレームワークによって実装される場合があります。 各フレームワークには、ビルド環境に含める必要がある動作または特定のコンポーネントの一部を有効にする独自のビルド アクションを持つことができます。 フレームワーク内では、ビルド アクションは分離コードに使用される特定の CLR 言語によっても異なる場合があります。

## <a name="xclass-in-the-wpf-programming-model"></a>x: WPF プログラミング モデルのクラス

WPF アプリケーションおよび WPF アプリケーション`x:Class`モデルでは、XAML ファイルのルートであり、コンパイルされる要素 (ビルド アクションを伴`Page`う WPF アプリケーション プロジェクトに XAML が含まれる)、またはコンパイルされた<xref:System.Windows.Application>WPF アプリケーションのアプリケーション定義のルートの属性として宣言できます。 ページ`x:Class`ルートまたはアプリケーション ルート以外の要素、またはコンパイルされていない WPF XAML ファイルで宣言すると、.NET Framework 3.0 および .NET Framework 3.5 WPF XAML コンパイラでコンパイル エラーが発生します。 WPF での処理の`x:Class`その他の側面については、「 WPF の[分離コードと XAML](../../framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)」を参照してください。

## <a name="xclass-for-windows-workflow-foundation"></a>x:Windows ワークフローファウンデーションのクラス
Windows ワークフロー ファン`x:Class`デーションの場合は、XAML で完全に構成されるカスタム アクティビティのクラスに名前を付けたり、分離コードを持つアクティビティ デザイナーの XAML ページの部分クラスに名前を付けます。

## <a name="silverlight-usage-notes"></a>Silverlight の使用上の注意

Silverlight 用の `x:Class` に関しては、別途ドキュメントが用意されています。 詳細については[、「XAML 名前空間 (x:)」を参照してください。言語機能 (シルバーライト)](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc188995(v=vs.95))

## <a name="see-also"></a>関連項目

- [x:Subclass ディレクティブ](xsubclass-directive.md)
- [WPF における XAML とカスタム クラス](../../framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)
- [x:ClassModifier ディレクティブ](xclassmodifier-directive.md)
- [WPF から System.Xaml に移行した型](../../framework/wpf/advanced/types-migrated-from-wpf-to-system.md)
