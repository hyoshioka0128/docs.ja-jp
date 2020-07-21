---
ms.openlocfilehash: 92c03328414410d56a2ff5f445639757367b42c7
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420430"
---
### <a name="processstartinfo-throws-invalidoperationexception-for-processes-you-didnt-start"></a>開始されなかったプロセスについて Process.StartInfo が InvalidOperationException をスローする

コードで開始されなかったプロセスの <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> プロパティの読み取りによって、<xref:System.InvalidOperationException> がスローされます。

#### <a name="change-description"></a>変更の説明

.NET Framework では、コードで開始されなかったプロセスの <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> プロパティにアクセスすると、ダミーの <xref:System.Diagnostics.ProcessStartInfo> オブジェクトが返されます。 ダミー オブジェクトには、<xref:System.Diagnostics.ProcessStartInfo.EnvironmentVariables> を除くすべてのプロパティの既定値が含まれています。

.NET Core 1.0 以降では、開始されなかった (<xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType> が呼びされなかった) プロセスの <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> プロパティを読み取ると、<xref:System.InvalidOperationException> がスローされます。

#### <a name="version-introduced"></a>導入されたバージョン

1

#### <a name="recommended-action"></a>推奨アクション

コードで開始されなかったプロセスの <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> プロパティにアクセスしません。 たとえば、<xref:System.Diagnostics.Process.GetProcesses%2A?displayProperty=nameWithType> によって返されるプロセスについて、このプロパティは読み取らないでください。

#### <a name="category"></a>カテゴリ

Core .NET ライブラリ

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Diagnostics.Process.StartInfo?displayProperty=fullName>

<!--

#### Affected APIs

- `P:System.Diagnostics.Process.StartInfo`

-->
