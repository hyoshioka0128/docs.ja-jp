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
ms.openlocfilehash: d6baa6d8eb3a6d3520fb1549e2182f27ca52c36a
ms.sourcegitcommit: a4f9b754059f0210e29ae0578363a27b9ba84b64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74837247"
---
# <a name="xclass-directive"></a>x:Class ディレクティブ
マークアップと分離コードの間で部分クラスを結合するように、XAML マークアップのコンパイルを構成します。 コード部分クラスは、共通言語仕様 (CLS) 言語の個別のコードファイルで定義されます。一方、マークアップ部分クラスは、通常、XAML のコンパイル時にコード生成によって作成されます。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性の使用  
  
```xaml  
<object x:Class="namespace.classname"...>  
  ...  
</object>  
```  
  
## <a name="xaml-values"></a>XAML の値  
  
|||  
|-|-|  
|`namespace`|省略可。 `classname`によって識別される部分クラスを含む CLR 名前空間を指定します。 `namespace` が指定されている場合、ドット (.) は `namespace` と `classname`を分離します。 「解説」を参照してください。|  
|`classname`|必須です。 読み込まれた XAML とその XAML の分離コードを接続する部分クラスの CLR 名を指定します。|  
  
## <a name="dependencies"></a>の依存関係  
 `x:Class` は、XAML 運用のルート要素でのみ指定できます。 `x:Class` は、XAML 運用環境で親を持つオブジェクトでは無効です。 詳細については、「 [\[\]」セクション 4.3.1.6](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))を参照してください。  
  
## <a name="remarks"></a>Remarks  
 `namespace` 値には、関連する名前空間を名前階層に編成するための追加のドットを含めることができます。これは、.NET Framework プログラミングの一般的な手法です。 `x:Class` 値の文字列の最後のドットだけが `classname.` `namespace` を分離するように解釈され、`x:Class` として使用されるクラスは、入れ子になったクラスにはできません。 入れ子になったクラスが許可されている場合、`x:Class` 文字列のドットの意味を判断するのは、入れ子になったクラスを使用できません。  
  
 `x:Class`を使用する既存のプログラミングモデルでは、コードビハインドのない XAML ページを持つことが完全に有効であるという意味で、`x:Class` は省略可能です。 ただし、この機能は、XAML を使用するフレームワークによって実装されるビルドアクションと対話します。 `x:Class` 機能は、XAML によって指定されたコンテンツのさまざまな分類がアプリケーションモデルとそれに対応するビルドアクションに存在するロールの影響も受けます。 XAML でイベント処理属性値が宣言されている場合、または定義するクラスが分離コードクラスに含まれるカスタム要素をインスタンス化する場合は、分離コードのために適切なクラスに `x:Class` ディレクティブ参照 (または[x:Subclass](x-subclass-directive.md)) を提供する必要があります。  
  
 `x:Class` ディレクティブの値は、クラスの完全修飾名を指定する文字列である必要があります。ただし、アセンブリ情報は含まれません (<xref:System.Type.FullName%2A?displayProperty=nameWithType>と同じです)。 単純なアプリケーションの場合、分離コードがその方法でも構造化されている場合は、CLR 名前空間の情報を省略できます (コード定義はクラスレベルで開始されます)。  
  
 ページまたはアプリケーション定義の分離コードファイルは、コンパイルされたアプリケーションを生成するプロジェクトの一部として含まれているコードファイル内に存在する必要があります。また、マークアップコンパイルも関係します。 CLR クラスの名前の規則に従う必要があります。 詳細については、「[フレームワークのデザインガイドライン](../../standard/design-guidelines/index.md)」を参照してください。 既定では、分離コードクラスは `public`である必要があります。ただし、 [X:ClassModifier ディレクティブ](x-classmodifier-directive.md)を使用して、別のアクセスレベルで定義することもできます。  
  
 この `x:Class` 属性の解釈は CLR ベースの XAML 実装にのみ適用されます。特に、.NET Framework XAML サービスに適用されます。 CLR に基づいていない、.NET Framework XAML サービスを使用していないその他の XAML 実装は、XAML マークアップの接続や実行時コードのバックアップに別の解決式を使用する場合があります。 `x:Class`の一般的な解釈の詳細については、「 [\[MS XAML\]](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))」を参照してください。  
  
 特定のレベルのアーキテクチャでは、`x:Class` の意味は、.NET Framework の XAML サービスでは定義されていません。 これは .NET Framework XAML サービスで、XAML マークアップとバッキングコードの接続に使用するプログラミングモデルが指定されていないためです。 `x:Class` ディレクティブのその他の使用方法は、プログラミングモデルまたはアプリケーションモデルを使用して XAML マークアップと CLR ベースの分離コードを接続する方法を定義する特定のフレームワークによって実装される場合があります。 各フレームワークは独自のビルドアクションを持つことができ、ビルド環境に含まれる必要がある動作または特定のコンポーネントの一部を有効にすることができます。 フレームワーク内では、ビルドアクションは、分離コードに使用されている特定の CLR 言語によって異なる場合もあります。  
  
## <a name="xclass-in-the-wpf-programming-model"></a>WPF プログラミングモデルにおける x:Class  
 WPF アプリケーションと WPF アプリケーションモデルでは、`x:Class` を XAML ファイルのルートである任意の要素の属性として宣言し、コンパイルする (XAML が `Page` ビルドアクションを使用する WPF アプリケーションプロジェクトに含まれる) か、またはコンパイルされた WPF アプリケーションのアプリケーション定義の <xref:System.Windows.Application> ルートにすることができます。 ページルートまたはアプリケーションルート以外の要素、またはコンパイルされていない WPF XAML ファイル上で `x:Class` を宣言すると、.NET Framework 3.0 および .NET Framework 3.5 WPF XAML コンパイラでコンパイル時エラーが発生します。 WPF での `x:Class` 処理のその他の側面については、「 [wpf の分離コードと XAML](../wpf/advanced/code-behind-and-xaml-in-wpf.md)」を参照してください。  
  
## <a name="xclass-for-windows-workflow-foundation"></a>Windows Workflow Foundation の x:Class  
 Windows Workflow Foundation の場合 `x:Class`、は、XAML で完全に構成されたカスタムアクティビティのクラスに名前を付けたり、分離コードを使用してアクティビティデザイナーの XAML ページの部分クラスに名前を付けたりします。  
  
## <a name="silverlight-usage-notes"></a>Silverlight の使用上の注意  
 Silverlight 用の `x:Class` に関しては、別途ドキュメントが用意されています。 詳細については、「 [XAML 名前空間 (x:)」を参照してください。言語機能 (Silverlight)](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc188995(v=vs.95))。  
  
## <a name="see-also"></a>参照

- [x:Subclass ディレクティブ](x-subclass-directive.md)
- [WPF における XAML とカスタム クラス](../wpf/advanced/xaml-and-custom-classes-for-wpf.md)
- [x:ClassModifier ディレクティブ](x-classmodifier-directive.md)
- [WPF から System.Xaml に移行した型](types-migrated-from-wpf-to-system-xaml.md)
