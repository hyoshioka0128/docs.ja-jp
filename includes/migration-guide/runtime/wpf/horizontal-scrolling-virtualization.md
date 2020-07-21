---
ms.openlocfilehash: 14585b6de3ce02884f8be789930fc8610f73ba7d
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621267"
---
### <a name="horizontal-scrolling-and-virtualization"></a>水平方向スクロールと仮想化

#### <a name="details"></a>説明

この変更は、メインのスクロール方向と直交する方向で独自に仮想化を行う <xref:System.Windows.Controls.ItemsControl?displayProperty=fullName> に適用されます (代表的な例は、EnableColumnVirtualization=&quot;True&quot; である <xref:System.Windows.Controls.DataGrid?displayProperty=fullName> です)。  特定の水平方向スクロール操作の結果が変更され、比較可能な垂直操作の結果により類似した、より直感的な結果が生成されるようになりました。<p/>操作には &quot;ここにスクロール&quot; や &quot;右端&quot; などがあり、水平スクロール バーを右クリックすると表示されるメニューから名前を使用することができます。  これらの両方でオフセット候補が計算され、<xref:System.Windows.Controls.Primitives.IScrollInfo.SetHorizontalOffset(System.Double)> が呼び出されます。<p/>新しいオフセットにスクロールすると、&quot;ここ&quot; または &quot;右端&quot; の概念が変更されている場合があります。これは、新しく非仮想化されたコンテンツで <xref:System.Windows.Controls.Primitives.IScrollInfo.ExtentWidth?displayProperty=fullName> の値が変更されたためです。<p/>.NET Framework 4.6.2 より前では、もう &quot;ここ&quot; や &quot;右端&quot; にない場合でも、スクロール操作では単にオフセット候補を使用します。  その結果、スクロールつまみの &quot;バウンス&quot; などの効果が得られます。次に例を示します。 たとえば、<xref:System.Windows.Controls.DataGrid?displayProperty=fullName> で ExtentWidth=1000 および Width=200 であるものとします。  &quot;右端&quot; へのスクロールでは、1000 - 200 = 800 という候補オフセットを使用します。  そのオフセットへのスクロール時に、新しい列が非仮想化されます。これらの列が非常に広いため、<xref:System.Windows.Controls.Primitives.IScrollInfo.ExtentWidth?displayProperty=fullName> を 2000 に変更したとします。  スクロールは HorizontalOffset=800 で終了し、つまみはスクロールバーの中央付近 (正確には 800/2000 = 40%) に &quot;戻り&quot; ます。<p/>変更するには、この状況が発生したら新しいオフセット候補を再計算してやり直します (垂直方向スクロールの動作は既にこのようになっています)。 <p/>この変更により、エンド ユーザーにはより予測可能で直感的なエクスペリエンスが提供されるようになりますが、水平方向スクロール後の <xref:System.Windows.Controls.Primitives.IScrollInfo.HorizontalOffset?displayProperty=fullName> の正確な値に依存するアプリに影響する可能性もあります。これは、エンド ユーザーによる呼び出しであるか、<xref:System.Windows.Controls.Primitives.IScrollInfo.SetHorizontalOffset(System.Double)> の明示的な呼び出しであるかに関係ありません。

#### <a name="suggestion"></a>提案される解決策

<xref:System.Windows.Controls.Primitives.IScrollInfo.HorizontalOffset?displayProperty=fullName> の予測値を使用するアプリを、非仮想化により <xref:System.Windows.Controls.Primitives.IScrollInfo.ExtentWidth?displayProperty=fullName> が変更される可能性のある水平方向スクロール後の実際の値 (および <xref:System.Windows.Controls.Primitives.IScrollInfo.ExtentWidth?displayProperty=fullName> の値) を取得するように変更する必要があります。

| 名前    | 値       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.6.2|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.Controls.Primitives.IScrollInfo?displayProperty=nameWithType></li></ul>|
