---
title: グローバリゼーション
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [WPF], international user interface
- XAML [WPF], globalization
- international user interface [WPF], XAML
- globalization [WPF]
ms.assetid: 4571ccfe-8a60-4f06-9b37-7ac0b1c2d10f
ms.openlocfilehash: 95c0368889dfa4e69b5e40b32ea19ba845aa5c30
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76747058"
---
# <a name="globalization-for-wpf"></a>WPF のグローバリゼーション
このトピックでは、グローバル市場向けに [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションを開発するときに注意するべき問題を紹介します。 グローバリゼーション プログラミング要素は、.NET の <xref:System.Globalization> 名前空間に定義されています。

<a name="xaml_globalization"></a>
## <a name="xaml-globalization"></a>XAML グローバリゼーション
 Extensible Application Markup Language (XAML) は XML に基づいており、XML 仕様で定義されているグローバリゼーション サポートが利用されます。 以下のセクションでは、注意するべき [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 機能についていくつか説明します。

<a name="char_reference"></a>
### <a name="character-references"></a>文字参照
文字参照は、特定の Unicode 文字の UTF16 コード ユニットを、10 進数または 16 進数で表したものです。 次の例は、コプト語の大文字のホリ (つまり 'Ϩ') の 10 進の文字参照を示しています。

```
&#1000;
```

次は、16 進数の文字参照の例です。 16 進数の前には **x** が付くことに注意してください。

```
&#x3E8;
```

<a name="encoding"></a>
### <a name="encoding"></a>エンコード
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] でサポートされているエンコードは、ASCII、Unicode UTF-16、および UTF-8 です。 エンコード ステートメントは [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文書の最初に配置されます。 エンコーディング属性が存在せず、バイト順もない場合、パーサーでは既定として UTF-8 が使用されます。 UTF-8 と UTF-16 は優先エンコードです。 UTF-7 には対応していません。 次の例は、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルで UTF-8 エンコードを指定する方法を示しています。

```xaml
?xml encoding="UTF-8"?
```

<a name="lang_attrib"></a>
### <a name="language-attribute"></a>言語属性
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] は [xml:lang](../../../desktop-wpf/xaml-services/xml-language-handling.md) を利用し、要素の言語属性を表します。  <xref:System.Globalization.CultureInfo> クラスを利用するには、言語属性値が <xref:System.Globalization.CultureInfo> で事前定義されたカルチャ名のいずれかである必要があります。 [xml:lang](../../../desktop-wpf/xaml-services/xml-language-handling.md) は要素ツリーで継承可能であり (XML ルールによる継承であり、必ずしも依存関係プロパティの継承によるものではありません)、その既定値は、明示的に割り当てられていない場合、空の文字列になります。

 言語属性は、方言を指定するときに非常に役立ちます。 たとえば、フランス語であれば、フランス、ケベック、ベルギー、スイスでスペル、語彙、発音が異なります。 また、中国語、日本語、韓国語は Unicode のコード ポイントを共有していますが、表意文字の形が異なり、まったく別のフォントが使用されます。

 次の [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 例では、`fr-CA` 言語属性を利用し、カナダのフランス語を指定します。

```xaml
<TextBlock xml:lang="fr-CA">Découvrir la France</TextBlock>
```

<a name="unicode"></a>
### <a name="unicode"></a>Unicode
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] は、サロゲートを含むすべての Unicode 機能をサポートしています。 文字セットを Unicode にマッピングできるのであればサポートされます。 たとえば、GB18030 では、一部の文字が中国語、日本語、韓国語 (CFK) の拡張 A および B とサロゲート ペアにマッピングされているため、完全に対応しています。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションでは、<xref:System.Globalization.StringInfo> を使用して、サロゲート ペアまたは結合文字があるかどうかを知らなくても文字列を操作できます。

<a name="design_intl_ui_with_xaml"></a>
## <a name="designing-an-international-user-interface-with-xaml"></a>XAML で各国対応ユーザー インターフェイスを設計する
 このセクションでは、アプリケーションの開発時に考慮するべき [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 機能について説明します。

<a name="intl_text"></a>
### <a name="international-text"></a>国際対応テキスト
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、Microsoft .NET Framework でサポートされているすべての書記体系の組み込み処理が含まれています。

 現在、次の書体がサポートされています。

- アラビア語

- ベンガル語

- デバナガリ

- キリル言語

- ギリシャ語

- グジャラート語

- グルムキー

- ヘブライ語

- 表意文字スクリプト

- カナラ語

- ラオス語

- ラテン語

- マラヤーラム語

- モンゴル語

- オディア語

- シリア語

- タミール語

- テルグ語

- ターナ

- タイ語*

- チベット語

 \* このリリースでは、タイ語テキストを表示し、編集できますが、単語を分割することはできません。

 現在、次のスクリプトはサポートされていません。

- クメール語

- 韓国語の古いハングル

- ミャンマー

- シンハラ語

 すべての書記体系エンジンは OpenType フォントをサポートしています。 OpenType フォントには、OpenType レイアウト テーブルを追加できます。このテーブルを追加すると、フォントの作成時、洗練された国際対応の印刷フォントの設計能力が上がります。 OpenType フォント レイアウト テーブルには、グリフ代用、グリフ配置、位置揃え、基線配置に関する情報が含まれています。テキスト処理アプリケーションでテキスト レイアウトを改善できます。

 OpenType フォントでは、Unicode エンコードを使用して大きなグリフ セットを処理できます。 このようなエンコードにより、広範な国際対応が可能になり、さまざまなグリフを印刷できます。

 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のテキスト レンダリングには、解像度に依存しない Microsoft ClearType サブピクセル テクノロジが採用されています。 これにより読みやすさが大幅に向上し、あらゆる書体で高品質の雑誌スタイルの書面を作成できます。

<a name="intl_layout"></a>
### <a name="international-layout"></a>国際対応レイアウト
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では非常に便利な方法で横書きレイアウト、双方向レイアウト、縦書きレイアウトを作成できます。 プレゼンテーション フレームワークでは、<xref:System.Windows.FrameworkElement.FlowDirection%2A> プロパティを使用してレイアウトを定義できます。 フローの方向パターン:

- *LeftToRight* - ラテン語や東アジア言語などのための横書きレイアウト。

- *RightToLeft* - アラビア語やヘブライ語などのための双方向レイアウト。

<a name="developing_localizable_apps"></a>
## <a name="developing-localizable-applications"></a>ローカライズ可能なアプリケーションの開発
 世界中で利用されるアプリケーションを開発するときは、アプリケーションをローカライズ可能にすることを忘れてはなりません。 後続のトピックで、考慮事項を指摘します。

<a name="mui"></a>
### <a name="multilingual-user-interface"></a>多言語ユーザー インターフェイス
 多言語ユーザー インターフェイス (MUI) は、UI をある言語から別の言語に切り替えるための Microsoft サポートです。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションはアセンブリ モデルを利用して MUI をサポートします。 1 つのアプリケーションに言語に依存しないアセンブリと言語に依存するサテライト リソース アセンブリが含まれます。 エントリ ポイントはメイン アセンブリのマネージド .EXE です。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] リソース ローダーは、Framework のリソース マネージャーを利用し、リソースのルックアップとフォールバックをサポートします。 多言語サテライト アセンブリは同じメイン アセンブリと連動します。 読み込まれるリソース アセンブリは、現在のスレッドの <xref:System.Globalization.CultureInfo.CurrentUICulture%2A> によって変わります。

<a name="localizable_ui"></a>
### <a name="localizable-user-interface"></a>ローカライズ可能なユーザー インターフェイス
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションでは [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] を利用して [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を定義します。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で開発すると、オブジェクトの階層に一連のプロパティとロジックを指定できます。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の主な用途は [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションの開発ですが、共通言語ランタイム (CLR) オブジェクトの階層を指定するために使用できます。 ほとんどの開発者は [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] を利用してアプリケーションの [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を指定し、C# などのプログラミング言語を利用してユーザーの操作に応答します。

 リソースの観点からは、言語依存の [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を表すように設計された [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルはリソース要素であり、そのため、その最終的な配布形式はローカライズ可能にして外国の言語に対応できるようにする必要があります。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] はイベントを処理できないため、多くの [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] アプリケーションにはコード ブロックが含まれ、イベントを処理します。 詳細については、「[XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)」を参照してください。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルがトークン化され、XAML の BAML 形式になるとき、コードは分解され、異なるバイナリにコンパイルされます。 XAML ファイル、画像、その他の種類の管理対象リソース オブジェクトの BAML 形式はサテライト リソース アセンブリに組み込まれます。サテライト リソース アセンブリに組み込むことで、他の言語にローカライズできます。ローカライズが必要なければ、メイン アセンブリに組み込まれます。

> [!NOTE]
> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションは、文字列テーブルやイメージなど、あらゆる FrameworkCLR リソースに対応しています。

<a name="building_localizable_apps"></a>
### <a name="building-localizable-applications"></a>ローカライズ可能なアプリケーションの構築
 ローカリゼーションとは、異なる文化に合わせて [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を調整することです。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションをローカライズ可能にするには、開発者はローカライズ可能なすべてのリソースでリソース アセンブリを構築する必要があります。 リソース アセンブリはさまざまな言語にローカライズされ、コードビハインドでリソース管理 API が使用されて読み込まれます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションに必要なファイルの 1 つは、プロジェクト ファイル (.proj) です。 アプリケーションで使用するすべてのリソースをプロジェクト ファイルに含める必要があります。 その方法を .csproj ファイルからの次の例で示します。

```xml
<Resource Include="data\picture1.jpg"/>
<EmbeddedResource Include="data\stringtable.en-US.restext"/>
```

 アプリケーションでリソースを使用するには、<xref:System.Resources.ResourceManager> をインスタンス化し、使用するリソースを読み込みます。 この方法を次の例に示します。

 [!code-csharp[LocalizationResources#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationResources/CSharp/page1.xaml.cs#2)]

<a name="using_clickonce"></a>
## <a name="using-clickonce-with-localized-applications"></a>ローカライズされたアプリケーションで ClickOnce を使用する
 ClickOnce は Visual Studio 2005 に付属する Windows フォームの新しい展開技術です。 アプリケーションをインストールしたり、Web アプリケーションをアップグレードしたりできます。 ClickOnce で展開されたアプリケーションがローカライズされると、ローカライズされたカルチャでのみ表示できます。 たとえば、展開されたアプリケーションが日本語にローカライズされている場合、日本語の Microsoft Windows でのみ表示できます。英語の Windows では表示できません。 これは問題になります。日本のユーザーが英語版の Windows を実行することは珍しくないためです。

 この問題の解決策は、非依存言語フォールバック属性を設定することです。 アプリケーション開発者はメイン アセンブリからリソースを任意で削除し、特定のカルチャに対応するサテライト アセンブリでそのリソースを見つけられるように指定できます。 このプロセスを制御するには、<xref:System.Resources.NeutralResourcesLanguageAttribute> を使用します。 <xref:System.Resources.NeutralResourcesLanguageAttribute> クラスのコンストラクターには 2 つのシグネチャがあります。1 つは、<xref:System.Resources.UltimateResourceFallbackLocation> パラメーターを受け取り、<xref:System.Resources.ResourceManager> でフォールバック リソースを抽出する場所 (メイン アセンブリまたはサテライト アセンブリ) を指定するものです。 この属性を使用する方法の例を次に示します。 最終的なフォールバックの場所の場合、コードにより、<xref:System.Resources.ResourceManager> は現在実行中のアセンブリのディレクトリの "de" サブディレクトリ内のリソースが検索されます。

```csharp
[assembly: NeutralResourcesLanguageAttribute(
    "de" , UltimateResourceFallbackLocation.Satellite)]
```

## <a name="see-also"></a>関連項目

- [WPF のグローバリゼーションおよびローカリゼーションの概要](wpf-globalization-and-localization-overview.md)
