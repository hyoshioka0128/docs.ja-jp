---
ms.openlocfilehash: 87013a04f7ff975e40a3c49c41c1c5acc2374066
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620410"
---
### <a name="wf-serializes-expressionsliterallttgt-datetimes-differently-now-breaks-custom-xaml-parsers"></a>WF による Expressions.Literal&lt;T&gt; DateTimes のシリアル化の方法が変わった (カスタム XAML パーサーが機能しなくなる)

#### <a name="details"></a>説明

関連する <xref:System.Windows.Markup.ValueSerializer> オブジェクトは、Second コンポーネントと <xref:System.DateTime.Millisecond?displayProperty=fullName> コンポーネントが非ゼロで (<xref:System.DateTime?displayProperty=fullName> 値の場合)、<xref:System.DateTime.Kind> プロパティが Unspecified ではない <xref:System.DateTime?displayProperty=fullName> オブジェクトまたは <xref:System.DateTimeOffset?displayProperty=fullName> オブジェクトを文字列ではなくプロパティ要素構文に変換します。 この変更により、<xref:System.DateTime?displayProperty=fullName> 値と <xref:System.DateTimeOffset?displayProperty=fullName> 値を往復させることができるようになります。 入力 XAML が属性構文であると想定するカスタム XAML パーサーは正しく機能しません。

#### <a name="suggestion"></a>提案される解決策

この変更により、<xref:System.DateTime?displayProperty=fullName> 値と <xref:System.DateTimeOffset?displayProperty=fullName> 値を往復させることができるようになります。 入力 XAML が属性構文であると想定するカスタム XAML パーサーは正しく機能しません。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム|
