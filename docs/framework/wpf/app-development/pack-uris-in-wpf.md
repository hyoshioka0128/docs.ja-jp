---
title: パック URI
description: Uniform Resource Identifier (URI) を使用して Windows Presentation Foundation (WPF) でファイルを識別して読み込む多くの方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- pack URI scheme [WPF]
- loading embedded resources [WPF]
- URIs (Uniform Resource Identifiers)
- Uniform Resource Identifiers (URIs)
- loading non-resource files
- application management [WPF]
ms.assetid: 43adb517-21a7-4df3-98e8-09e9cdf764c4
ms.openlocfilehash: 1d19dec0d846659f8de6ed518a7f98d224354a82
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621692"
---
# <a name="pack-uris-in-wpf"></a>WPF におけるパッケージの URI

Windows Presentation Foundation (WPF) では、Uniform Resource Identifier (URI) は、次のようなさまざまな用途でファイルを識別し、読み込むために使用されます。

- アプリケーションが初めて起動するときに表示する [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] の指定。

- イメージの読み込み。

- ページへの移動。

- 実行可能でないデータ ファイルの読み込み。

さらに、URI は、次のようなさまざまな場所からファイルを識別し、読み込むために使用できます。

- 現在のアセンブリ。

- 参照アセンブリ。

- アセンブリに対して相対的な位置。

- アプリケーションの起点サイト。

これらの位置からこれらの種類のファイルを識別し、読み込むための一貫性のあるメカニズムを提供するために、WPF では "*パック URI スキーム*" の拡張性が利用されます。 このトピックでは、このスキームの概要を説明し、さまざまなシナリオに応じたパック URI を構築する方法を述べ、絶対および相対 URI と URI の解決について説明した後、マークアップとコードの両方からパック URI を使用する方法を示します。

<a name="The_Pack_URI_Scheme"></a>

## <a name="the-pack-uri-scheme"></a>パック URI スキーム

パック URI スキームは、[Open Packaging Conventions](https://www.ecma-international.org/publications/standards/Ecma-376.htm) (OPC) 仕様によって使用されます。この仕様は、コンテンツを編成し、識別するためのモデルを規定しています。 このモデルの主な要素は、パッケージとパーツであり、"*パッケージ*" は、1 つ以上の論理 "*パーツ*" の論理的なコンテナーです。 この概念を次の図に示します。

![パッケージとパーツのダイアグラム](./media/pack-uris-in-wpf/wpf-package-parts-diagram.png)

パーツを識別するために、OPC 仕様では、RFC 2396 (Uniform Resource Identifier (URI): 一般構文) の拡張性を利用して、パック URI スキームが定義されます。

URI によって指定されるスキームは、そのプレフィックスによって定義されます。http、ftp、および file は、よく知られている例です。 パック URI スキームでは、スキームとして "pack" が使用され、オーソリティとパスの 2 つのコンポーネントが含まれます。 パック URI の形式は、次のとおりです。

pack://*authority*/*path*

*authority* は、パーツが含まれるパッケージの種類を指定し、*path* は、パッケージ内のパーツの位置を指定します。

この概念を次の図に示します。

![パッケージ、権限、およびパスの間のリレーションシップ](./media/pack-uris-in-wpf/wpf-relationship-diagram.png)

パッケージとパーツは、アプリケーションとファイルに似ています。つまり、アプリケーション (パッケージ) は、次のような 1 つ以上のファイル (パーツ) を含むことができます。

- ローカル アセンブリにコンパイルされるリソース ファイル。

- 参照センブリにコンパイルされるリソース ファイル。

- 参照元センブリにコンパイルされるリソース ファイル。

- コンテンツ ファイル。

- 起点サイト ファイル。

これらの種類のファイルにアクセスするために、WPF では、application:/// と siteoforigin:/// という 2 つのオーソリティがサポートされます。 application:/// オーソリティは、リソース ファイルやコンテンツ ファイルなど、コンパイル時に既知のアプリケーション データ ファイルを識別します。 siteoforigin:/// オーソリティは、起点サイト ファイルを識別します。 各オーソリティのスコープを次の図に示します。

![Pack URI のダイアグラム](./media/pack-uris-in-wpf/wpf-pack-uri-scheme.png)

> [!NOTE]
> パック URI のオーソリティ コンポーネントは、パッケージを指す埋め込み URI であり、RFC 2396 に準拠する必要があります。 さらに、"/" 文字は "," 文字に置き換える必要があり、"%" や "?" などの予約文字はエスケープする必要があります。 詳細については、OPC を参照してください。

以下のセクションでは、この 2 つのオーソリティと、リソース ファイル、コンテンツ ファイル、および起点サイト ファイルを識別する適切なパスとを組み合わせてパック URI を構築する方法について説明します。

<a name="Resource_File_Pack_URIs___Local_Assembly"></a>

## <a name="resource-file-pack-uris"></a>リソース ファイルのパック URI

リソース ファイルは、MSBuild の`Resource` 項目として構成され、アセンブリにコンパイルされます。 WPF では、ローカル アセンブリにコンパイルされるか、ローカル アセンブリから参照されるアセンブリにコンパイルされるリソース ファイルを識別するために使用できるパック URI の構築がサポートされています。

<a name="Local_Assembly_Resource_File"></a>

### <a name="local-assembly-resource-file"></a>ローカル アセンブリ リソース ファイル

ローカル アセンブリにコンパイルされるリソース ファイルのパック URI では、次のオーソリティとパスを使用します。

- **オーソリティ**: application:///。

- **パス**:ローカル アセンブリのプロジェクト フォルダーのルートに対して相対的なパスを含むリソース ファイルの名前。

次の例では、ローカル アセンブリのプロジェクト フォルダーのルートにある [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] リソース ファイルのパック URI を示します。

`pack://application:,,,/ResourceFile.xaml`

次の例では、ローカル アセンブリのプロジェクト フォルダーのサブフォルダーにある [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] リソース ファイルのパック URI を示します。

`pack://application:,,,/Subfolder/ResourceFile.xaml`

<a name="Resource_File_Pack_URIs___Referenced_Assembly"></a>

### <a name="referenced-assembly-resource-file"></a>参照アセンブリ リソース ファイル

参照アセンブリにコンパイルされるリソース ファイルのパック URI では、次のオーソリティとパスを使用します。

- **オーソリティ**: application:///。

- **パス**:参照アセンブリにコンパイルされるリソース ファイルの名前。 パスは、次の書式に従う必要があります。

  *AssemblyShortName*{ *;Version*]{ *;PublicKey*];component/*Path*

  - **AssemblyShortName**: 参照アセンブリの短い名前。

  - **;Version** (省略可能): リソース ファイルを含む参照アセンブリのバージョン。 これは、同じ短い名前を持つ 2 つ以上の参照アセンブリが読み込まれるときに使用されます。

  - **;PublicKey** (省略可能): 参照アセンブリの署名に使用された公開鍵。 これは、同じ短い名前を持つ 2 つ以上の参照アセンブリが読み込まれるときに使用されます。

  - **;component**: 参照されるアセンブリが、ローカル アセンブリから参照されることを指定します。

  - **/Path**: 参照アセンブリのプロジェクト フォルダーのルートに対して相対的なパスを含むリソース ファイルの名前。

次の例では、参照アセンブリのプロジェクト フォルダーのルートにある [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] リソース ファイルのパック URI を示します。

`pack://application:,,,/ReferencedAssembly;component/ResourceFile.xaml`

次の例では、参照アセンブリのプロジェクト フォルダーのサブフォルダーにある [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] リソース ファイルのパック URI を示します。

`pack://application:,,,/ReferencedAssembly;component/Subfolder/ResourceFile.xaml`

次の例では、バージョン固有の参照アセンブリのプロジェクト フォルダーのルートにある [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] リソース ファイルのパック URI を示します。

`pack://application:,,,/ReferencedAssembly;v1.0.0.1;component/ResourceFile.xaml`

参照アセンブリ リソース ファイルのパック URI 構文は、application:/// オーソリティでのみ使用できます。 たとえば、WPF では、次はサポートされません。

`pack://siteoforigin:,,,/SomeAssembly;component/ResourceFile.xaml`

<a name="Content_File_Pack_URIs"></a>

## <a name="content-file-pack-uris"></a>コンテンツ ファイルのパック URI

コンテンツ ファイルのパック URI では、次のオーソリティとパスを使用します。

- **オーソリティ**: application:///。

- **パス**:アプリケーションのメインの実行可能アセンブリのファイル システム位置に対して相対的なパスを含む、コンテンツ ファイルの名前。

次の例では、実行可能アセンブリと同じフォルダーにある [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] コンテンツ ファイルのパック URI を示します。

`pack://application:,,,/ContentFile.xaml`

次の例では、アプリケーションの実行可能アセンブリに対して相対的なサブフォルダーにある [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] コンテンツ ファイルのパック URI を示します。

`pack://application:,,,/Subfolder/ContentFile.xaml`

> [!NOTE]
> HTML コンテンツ ファイルにナビゲートすることはできません。 URI スキームでは、起点サイトにある HTML ファイルへのナビゲーションのみがサポートされます。

<a name="The_siteoforigin_____Authority"></a>

## <a name="site-of-origin-pack-uris"></a>起点サイトのパック URI

起点サイト ファイルのパック URI では、次のオーソリティとパスを使用します。

- **オーソリティ**: siteoforigin:///。

- **パス**:実行可能アセンブリの起動元の位置に対して相対的なパスを含む起点サイト ファイルの名前。

次の例では、実行可能アセンブリの起動元の位置に格納された [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 起点サイト ファイルのパック URI を示します。

`pack://siteoforigin:,,,/SiteOfOriginFile.xaml`

次の例では、アプリケーションの実行可能アセンブリの起動元の位置に対して相対的なサブフォルダーに格納された [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 起点サイト ファイルのパック URI を示します。

`pack://siteoforigin:,,,/Subfolder/SiteOfOriginFile.xaml`

<a name="Page_Files"></a>

## <a name="page-files"></a>ページ ファイル

MSBuild の `Page` 項目として構成される XAML ファイルは、リソース ファイルと同じようにアセンブリにコンパイルされます。 したがって、MSBuild の`Page` 項目は、リソース ファイルのパック URI を使用して識別できます。

一般に MSBuild の `Page` 項目として構成される [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルの種類は、次のいずれかをルート要素として持ちます。

- <xref:System.Windows.Window?displayProperty=nameWithType>

- <xref:System.Windows.Controls.Page?displayProperty=nameWithType>

- <xref:System.Windows.Navigation.PageFunction%601?displayProperty=nameWithType>

- <xref:System.Windows.ResourceDictionary?displayProperty=nameWithType>

- <xref:System.Windows.Documents.FlowDocument?displayProperty=nameWithType>

- <xref:System.Windows.Controls.UserControl?displayProperty=nameWithType>

<a name="Absolute_vs_Relative_Pack_URIs"></a>

## <a name="absolute-vs-relative-pack-uris"></a>絶対および相対パック URI

完全修飾されたパック URI は、スキーム、オーソリティ、およびパスを含み、絶対パック URI とみなされます。 開発者にとっての簡便さを考慮して、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 要素では、一般に、パスのみを含む相対パック URI で適切な属性を設定できます。

たとえば、ローカル アセンブリ内のリソース ファイルに対する次のような絶対パック URI を考えてみます。

`pack://application:,,,/ResourceFile.xaml`

このリソース ファイルを参照する相対パック URI は、次のようになります。

`/ResourceFile.xaml`

> [!NOTE]
> 起点サイト ファイルはアセンブリに関連付けられていないため、絶対パック URI でのみ参照できます。

既定では、相対パック URI は、参照を含んでいるマークアップまたはコードの位置に対して相対的とみなされます。 ただし、先頭にバック スラッシュが使用された場合、相対パック URI 参照は、アプリケーションのルートに対して相対的とみなされます。 たとえば、次のようなプロジェクト構造を考えてみます。

`App.xaml`

`Page2.xaml`

`\SubFolder`

`+ Page1.xaml`

`+ Page2.xaml`

Page1.xaml に、*Root*\SubFolder\Page2.xaml を参照する URI が含まれる場合、参照で次のような相対パック URI を使用することができます。

`Page2.xaml`

Page1.xaml に、*Root*\Page2.xaml を参照する URI が含まれる場合、参照で次のような相対パック URI を使用することができます。

`/Page2.xaml`

<a name="Pack_URI_Resolution"></a>

## <a name="pack-uri-resolution"></a>パック URI の解決

パック URI の書式では、異なる種類のファイルのパック URI が同じに見えることがあります。 たとえば、次のような絶対パック URI を考えてみます。

`pack://application:,,,/ResourceOrContentFile.xaml`

この絶対パック URI では、ローカル アセンブリ内のリソース ファイルまたはコンテンツ ファイルが参照されている可能性があります。 次の相対 URI も同様です。

`/ResourceOrContentFile.xaml`

パック URI で参照されているファイルの種類を判断するため、WPF では、次のヒューリスティックを使用して、ローカル アセンブリ内のリソース ファイルとコンテンツ ファイルの URI が解決されます。

1. アセンブリ メタデータに、パック URI に一致する <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 属性があるかどうかを調べます。

2. <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 属性が見つかった場合、パック URI ではコンテンツ ファイルが参照されています。

3. <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 属性が見つからなかった場合は、ローカル アセンブリにコンパイルされる設定リソース ファイルを調べます。

4. パック URI のパスに一致するリソース ファイルが見つかった場合、パック URI のパスではリソース ファイルが参照されています。

5. リソースが見つからなかった場合、内部で作成された <xref:System.Uri> は無効です。

URI 解決は、次を参照する URI には適用されません。

- 参照アセンブリ内のコンテンツ ファイル: この種類のファイルは、WPF ではサポートされません。

- 参照アセンブリ内の埋め込みファイル: これらは参照アセンブリの名前と `;component` サフィックスの両方を含むため、これらを示す URI は一意です。

- 起点サイト ファイル: これらは siteoforigin:/// オーソリティを含むパック URI によって識別できる唯一のファイルであるため、これらを示す URI は一意です。

パック URI の解決によってもたらされる単純化の 1 つは、コードがリソース ファイルやコンテンツ ファイルの位置にあまり依存しなくなることです。 たとえば、ローカル アセンブリ内のリソース ファイルがコンテンツ ファイルに再構成される場合、リソースのパック URI は同じままであり、パック URI を使用するコードも変わりません。

<a name="Programming_with_Pack_URIs"></a>

## <a name="programming-with-pack-uris"></a>パック URI を使用したプログラミング

多くの WPF クラスでは、次のように、パック URI で設定できるプロパティが実装されます。

- <xref:System.Windows.Application.StartupUri%2A?displayProperty=nameWithType>

- <xref:System.Windows.Controls.Frame.Source%2A?displayProperty=nameWithType>

- <xref:System.Windows.Navigation.NavigationWindow.Source%2A?displayProperty=nameWithType>

- <xref:System.Windows.Documents.Hyperlink.NavigateUri%2A?displayProperty=nameWithType>

- <xref:System.Windows.Window.Icon%2A?displayProperty=nameWithType>

- <xref:System.Windows.Controls.Image.Source%2A?displayProperty=nameWithType>

これらのプロパティは、マークアップとコードのどちらからでも設定できます。 このセクションでは、両方の基本構造について説明してから、一般的なシナリオの例を示します。

<a name="Using_Pack_URIs_in_Markup"></a>

### <a name="using-pack-uris-in-markup"></a>マークアップでのパック URI の使用

パック URI は、マークアップでは、属性の要素にパック URI を設定することによって指定されます。 次に例を示します。

`<element attribute="pack://application:,,,/File.xaml" />`

表 1 では、マークアップで指定できるさまざまな絶対パック URI を示します。

表 1:マークアップでの絶対パック URI

|ファイル|絶対パック URI|
|----------|-------------------------------------------------------------------------------------------------------------------------|
|リソース ファイル - ローカル アセンブリ|`"pack://application:,,,/ResourceFile.xaml"`|
|サブフォルダー内のリソース ファイル - ローカル アセンブリ|`"pack://application:,,,/Subfolder/ResourceFile.xaml"`|
|リソース ファイル - 参照アセンブリ|`"pack://application:,,,/ReferencedAssembly;component/ResourceFile.xaml"`|
|参照アセンブリのサブフォルダー内のリソース ファイル|`"pack://application:,,,/ReferencedAssembly;component/Subfolder/ResourceFile.xaml"`|
|バージョン管理された参照アセンブリ内のリソース ファイル|`"pack://application:,,,/ReferencedAssembly;v1.0.0.0;component/ResourceFile.xaml"`|
|コンテンツ ファイル|`"pack://application:,,,/ContentFile.xaml"`|
|サブフォルダー内のコンテンツ ファイル|`"pack://application:,,,/Subfolder/ContentFile.xaml"`|
|起点サイト ファイル|`"pack://siteoforigin:,,,/SOOFile.xaml"`|
|サブフォルダー内の起点サイト ファイル|`"pack://siteoforigin:,,,/Subfolder/SOOFile.xaml"`|

表 2 では、マークアップで指定できるさまざまな相対パック URI を示します。

表 2:マークアップでの相対パック URI

|ファイル|相対パック URI|
|----------|-------------------------------------------------------------------------------------------------------------------------|
|ローカル アセンブリ内のリソース ファイル|`"/ResourceFile.xaml"`|
|ローカル アセンブリのサブフォルダー内のリソース ファイル|`"/Subfolder/ResourceFile.xaml"`|
|参照アセンブリ内のリソース ファイル|`"/ReferencedAssembly;component/ResourceFile.xaml"`|
|参照アセンブリのサブフォルダー内のリソース ファイル|`"/ReferencedAssembly;component/Subfolder/ResourceFile.xaml"`|
|コンテンツ ファイル|`"/ContentFile.xaml"`|
|サブフォルダー内のコンテンツ ファイル|`"/Subfolder/ContentFile.xaml"`|

<a name="Using_Pack_URIs_in_Code"></a>

### <a name="using-pack-uris-in-code"></a>コードでのパック URI の使用

コードでパック URI を指定するには、<xref:System.Uri> クラスをインスタンス化して、コンストラクターのパラメーターとしてパック URI を渡します。 このコード例を次に示します。

```csharp
Uri uri = new Uri("pack://application:,,,/File.xaml");
```

既定では、<xref:System.Uri> クラスではパック URI は絶対とみなされます。 そのため、相対パック URI で <xref:System.Uri> クラスのインスタンスが作成されると、例外が発生します。

```csharp
Uri uri = new Uri("/File.xaml");
```

幸いにも、<xref:System.Uri> クラス コンストラクターの <xref:System.Uri.%23ctor%28System.String%2CSystem.UriKind%29> オーバーロードでは、<xref:System.UriKind> 型のパラメーターを受け入れるため、パック URI が絶対か相対かを指定できます。

```csharp
// Absolute URI (default)
Uri absoluteUri = new Uri("pack://application:,,,/File.xaml", UriKind.Absolute);
// Relative URI
Uri relativeUri = new Uri("/File.xaml",
                        UriKind.Relative);
```

提供されたパック URI がどちらであるかわかっているときには、<xref:System.UriKind.Absolute> または <xref:System.UriKind.Relative> のみを指定する必要があります。 ユーザーが実行時にパック URI を入力するときなど、使用されるパック URI の種類がわからない場合は、代わりに <xref:System.UriKind.RelativeOrAbsolute> を使用します。

```csharp
// Relative or Absolute URI provided by user via a text box
TextBox userProvidedUriTextBox = new TextBox();
Uri uri = new Uri(userProvidedUriTextBox.Text, UriKind.RelativeOrAbsolute);
```

表 3 では、<xref:System.Uri?displayProperty=nameWithType> を使用してコードで指定できるさまざまな相対パック URI を示します。

表 3:コードでの絶対パック URI

|ファイル|絶対パック URI|
|----------|-------------------------------------------------------------------------------------------------------------------------|
|リソース ファイル - ローカル アセンブリ|`Uri uri = new Uri("pack://application:,,,/ResourceFile.xaml", UriKind.Absolute);`|
|サブフォルダー内のリソース ファイル - ローカル アセンブリ|`Uri uri = new Uri("pack://application:,,,/Subfolder/ResourceFile.xaml", UriKind.Absolute);`|
|リソース ファイル - 参照アセンブリ|`Uri uri = new Uri("pack://application:,,,/ReferencedAssembly;component/ResourceFile.xaml", UriKind.Absolute);`|
|参照アセンブリのサブフォルダー内のリソース ファイル|`Uri uri = new Uri("pack://application:,,,/ReferencedAssembly;component/Subfolder/ResourceFile.xaml", UriKind.Absolute);`|
|バージョン管理された参照アセンブリ内のリソース ファイル|`Uri uri = new Uri("pack://application:,,,/ReferencedAssembly;v1.0.0.0;component/ResourceFile.xaml", UriKind.Absolute);`|
|コンテンツ ファイル|`Uri uri = new Uri("pack://application:,,,/ContentFile.xaml", UriKind.Absolute);`|
|サブフォルダー内のコンテンツ ファイル|`Uri uri = new Uri("pack://application:,,,/Subfolder/ContentFile.xaml", UriKind.Absolute);`|
|起点サイト ファイル|`Uri uri = new Uri("pack://siteoforigin:,,,/SOOFile.xaml", UriKind.Absolute);`|
|サブフォルダー内の起点サイト ファイル|`Uri uri = new Uri("pack://siteoforigin:,,,/Subfolder/SOOFile.xaml", UriKind.Absolute);`|

表 4 では、<xref:System.Uri?displayProperty=nameWithType> を使用してコードで指定できるさまざまな相対パック URI を示します。

表 4:コードでの相対パック URI

|ファイル|相対パック URI|
|----------|-------------------------------------------------------------------------------------------------------------------------|
|リソース ファイル - ローカル アセンブリ|`Uri uri = new Uri("/ResourceFile.xaml", UriKind.Relative);`|
|サブフォルダー内のリソース ファイル - ローカル アセンブリ|`Uri uri = new Uri("/Subfolder/ResourceFile.xaml", UriKind.Relative);`|
|リソース ファイル - 参照アセンブリ|`Uri uri = new Uri("/ReferencedAssembly;component/ResourceFile.xaml", UriKind.Relative);`|
|サブフォルダー内のリソース ファイル - 参照アセンブリ|`Uri uri = new Uri("/ReferencedAssembly;component/Subfolder/ResourceFile.xaml", UriKind.Relative);`|
|コンテンツ ファイル|`Uri uri = new Uri("/ContentFile.xaml", UriKind.Relative);`|
|サブフォルダー内のコンテンツ ファイル|`Uri uri = new Uri("/Subfolder/ContentFile.xaml", UriKind.Relative);`|

<a name="Common_Pack_URI_Scenarios"></a>

### <a name="common-pack-uri-scenarios"></a>一般的なパック URI のシナリオ

以前のセクションでは、パック URI を構築して、リソース ファイル、コンテンツ ファイル、および起点サイト ファイルを識別する方法を説明しました。 WPF では、このような構築はさまざまな方法で使用されますが、以下のセクションでは、いくつかの一般的な用途について説明します。

<a name="Specifying_the_UI_to_Show_when_an_Application_Starts"></a>

#### <a name="specifying-the-ui-to-show-when-an-application-starts"></a>アプリケーションの起動時に表示する UI の指定

<xref:System.Windows.Application.StartupUri%2A> では、WPF アプリケーションの起動時に表示する最初の [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を指定します。 スタンドアロン アプリケーションの場合、次の例に示されているように、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] としてウィンドウを使用できます。

[!code-xaml[PackURIOverviewSnippets#StartupUriWindow](~/samples/snippets/csharp/VS_Snippets_Wpf/PackURIOverviewSnippets/CS/Copy of App.xaml#startupuriwindow)]

スタンドアロン アプリケーションと XAML ブラウザー アプリケーション (XBAP) では、次の例に示されているように、最初の UI としてページを指定することもできます。

[!code-xaml[PackURIOverviewSnippets#StartupUriPage](~/samples/snippets/csharp/VS_Snippets_Wpf/PackURIOverviewSnippets/CS/App.xaml#startupuripage)]

アプリケーションがスタンドアロン アプリケーションであり、ページが <xref:System.Windows.Application.StartupUri%2A> で指定されている場合、WPF は <xref:System.Windows.Navigation.NavigationWindow> を開いて、ページをホストします。 XBAP の場合、ページはホスト ブラウザーに表示されます。

<a name="Navigating_to_a_Page"></a>

#### <a name="navigating-to-a-page"></a>ページへのナビゲート

次の例は、ページにナビゲートする方法を示しています。

[!code-xaml[NavigationOverviewSnippets#HyperlinkXAML1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithHyperlink.xaml#hyperlinkxaml1)]
[!code-xaml[NavigationOverviewSnippets#HyperlinkXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithHyperlink.xaml#hyperlinkxaml2)]
[!code-xaml[NavigationOverviewSnippets#HyperlinkXAML3](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithHyperlink.xaml#hyperlinkxaml3)]

WPF でのさまざまなナビゲートの方法については、「[ナビゲーションの概要](navigation-overview.md)」を参照してください。

<a name="Specifying_a_Window_Icon"></a>

#### <a name="specifying-a-window-icon"></a>ウィンドウ アイコンの指定

次の例は、URI を使用してウィンドウのアイコンを指定する方法を示しています。

[!code-xaml[WindowIconSnippets#WindowIconSetXAML](~/samples/snippets/xaml/VS_Snippets_Wpf/WindowIconSnippets/XAML/MainWindow.xaml#windowiconsetxaml)]

詳細については、「<xref:System.Windows.Window.Icon%2A>」を参照してください。

<a name="Loading_Image__Audio__and_Video_Files"></a>

#### <a name="loading-image-audio-and-video-files"></a>イメージ ファイル、オーディオ ファイル、およびビデオ ファイルの読み込み

WPF では、アプリケーションはさまざまな種類のメディアを使用でき、次の例に示されているように、そのすべてをパック URI で示して、読み込むことができます。

[!code-xaml[MediaPlayerVideoSample#VideoPackURIAtSOO](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaPlayerVideoSample/CS/HomePage.xaml#videopackuriatsoo)]

[!code-xaml[MediaPlayerAudioSample#AudioPackURIAtSOO](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaPlayerAudioSample/CS/HomePage.xaml#audiopackuriatsoo)]

[!code-xaml[ImageSample#ImagePackURIContent](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageSample/CS/HomePage.xaml#imagepackuricontent)]

メディア コンテンツの操作方法の詳細については、「[グラフィックスとマルチ メディア](../graphics-multimedia/index.md)」を参照してください。

<a name="Loading_a_Resource_Dictionary_from_the_Site_of_Origin"></a>

#### <a name="loading-a-resource-dictionary-from-the-site-of-origin"></a>起点サイトからのリソース ディクショナリの読み込み

リソース ディクショナリ (<xref:System.Windows.ResourceDictionary>) を使用して、アプリケーションのテーマをサポートできます。 テーマを作成し、管理する方法の 1 つは、複数のテーマをリソース ディクショナリとして作成して、アプリケーションの起点サイトに配置することです。 これにより、アプリケーションを再コンパイルして再配置しなくても、テーマの追加と交信が可能です。 これらのリソース ディクショナリは、次の例に示されているように、パック URI を使用して示し、読み込むことができます。

[!code-xaml[ResourceDictionarySnippets#ResourceDictionaryPackURI](~/samples/snippets/csharp/VS_Snippets_Wpf/ResourceDictionarySnippets/CS/App.xaml#resourcedictionarypackuri)]

WPF でのテーマの概要については、「[スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [WPF アプリケーションのリソース ファイル、コンテンツ ファイル、およびデータ ファイル](wpf-application-resource-content-and-data-files.md)
