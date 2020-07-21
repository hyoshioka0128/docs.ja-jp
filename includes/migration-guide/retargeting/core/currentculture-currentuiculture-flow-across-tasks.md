---
ms.openlocfilehash: 78faa5f4008b41bac75c94ce09a58c8227e5b485
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614672"
---
### <a name="currentculture-and-currentuiculture-flow-across-tasks"></a>タスク全体の CurrentCulture と CurrentUICulture のフロー

#### <a name="details"></a>説明

.NET Framework 4.6 より、非同期操作全体をフローする、スレッドの <xref:System.Threading.ExecutionContext?displayProperty=fullName> に <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=fullName> と <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=fullName> が格納されます。その結果、<xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=fullName> または <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=fullName> に対する変更は、後で非同期実行されるタスクで反映されます。 これは、すべての非同期タスクで <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=fullName> と <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=fullName> がリセットされていた、以前のバージョンの .NET Framework の動作とは異なります。

#### <a name="suggestion"></a>提案される解決策

この変更の影響を受けるアプリでは、非同期タスクの最初の操作として任意の <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=fullName> または <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=fullName> を明示的に設定することで問題を回避できます。 あるいは、次の互換性スイッチを設定することで、<xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=fullName>/<xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=fullName> をフローしない以前の動作を選択できます。

```csharp
AppContext.SetSwitch("Switch.System.Globalization.NoAsyncCurrentCulture", true);
```

この問題は、.NET Framework 4.6.2 の WPF で修正されました。 また、.NET Frameworks 4.6、4.6.1 では [KB 3139549](https://support.microsoft.com/kb/3139549) を通じて修正されました。 .NET Framework 4.6 以降を対象とするアプリケーションでは WPF アプリケーション (<xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=fullName>/<xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=fullName>) の正しい動作が自動的に取得されます。これは、ディスパッチャー操作にわたって維持されます。

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.6         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=nameWithType>
- <xref:System.Threading.Thread.CurrentCulture?displayProperty=nameWithType>
- <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=nameWithType>
- <xref:System.Threading.Thread.CurrentUICulture?displayProperty=nameWithType>
