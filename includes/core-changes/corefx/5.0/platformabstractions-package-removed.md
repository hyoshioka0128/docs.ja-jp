---
ms.openlocfilehash: d85fb8df7afdc5f4c3faecebcd24d11677798bc9
ms.sourcegitcommit: 63bb83322814f5e5e5c5b69939b14a3139a6ca7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2020
ms.locfileid: "85365617"
---
### <a name="microsoftdotnetplatformabstractions-package-removed"></a>Microsoft.DotNet.PlatformAbstractions パッケージの削除

新しいバージョンの [Microsoft.DotNet.PlatformAbstractions NuGet パッケージ](https://www.nuget.org/packages/Microsoft.DotNet.PlatformAbstractions/)は生成されなくなります。

#### <a name="change-description"></a>変更の説明

これまで、新しいバージョンの <xref:Microsoft.DotNet.PlatformAbstractions?displayProperty=fullName> ライブラリは、新しいバージョンの .NET Core と共に生成されていました。 今後は、ライブラリに新機能が追加されなくなり、新しいメジャー バージョンはリリースされなくなります。 しかし、既存のバージョンのライブラリは引き続き動作し、サービスが提供されます。

<xref:Microsoft.DotNet.PlatformAbstractions?displayProperty=fullName> ライブラリは、System.\* 名前空間に既に確立されている API と重複します。 また、一部の <xref:Microsoft.DotNet.PlatformAbstractions> API は、System.\*API の他の部分と同じレベルの監視と長期的なサポートを考慮して設計されていませんでした。 たとえば、<xref:Microsoft.DotNet.PlatformAbstractions> では、`Platform` 列挙型を使用して、現在のオペレーティング システムのプラットフォームを記述します。 この列挙型の設計は、新しいプラットフォームおよび今後の柔軟性に対応できるように、<xref:System.Runtime.InteropServices.RuntimeInformation.IsOSPlatform(System.Runtime.InteropServices.OSPlatform)?displayProperty=nameWithType> API が設計されたときに明示的に拒否されました。

<xref:Microsoft.DotNet.PlatformAbstractions?displayProperty=fullName> ライブラリで有効にされたシナリオは、それがなくても実現できるようになりました。 既存のバージョンは、.NET 5.0 以降でも引き続き動作し、以前のバージョンの .NET Core と共にサービスが提供されます。 しかし、新機能はライブラリに追加されなくなります。 代わりに、他のライブラリと API に新機能が追加されるようになります。

#### <a name="version-introduced"></a>導入されたバージョン

5.0 Preview 6

#### <a name="recommended-action"></a>推奨アクション

- 要件が満たされている場合は、古いバージョンのライブラリを引き続き使用することができます。

- 以前のバージョンで要件が満たされていない場合は、`PlatformAbstractions` API の代わりに推奨される代替を使用してください。

  | `PlatformAbstractions` API | 推奨代替 |
  |-|-|
  | `ApplicationEnvironment.ApplicationBasePath` | <xref:System.AppContext.BaseDirectory?displayProperty=nameWithType> |
  | <xref:Microsoft.DotNet.PlatformAbstractions.HashCodeCombiner> | <xref:System.HashCode?displayProperty=nameWithType> |
  | `RuntimeEnvironment.GetRuntimeIdentifier()` | <xref:System.Runtime.InteropServices.RuntimeInformation.RuntimeIdentifier?displayProperty=nameWithType> |
  | `RuntimeEnvironment.OperatingSystemPlatform` | <xref:System.Runtime.InteropServices.RuntimeInformation.IsOSPlatform(System.Runtime.InteropServices.OSPlatform)?displayProperty=nameWithType> |
  | `RuntimeEnvironment.RuntimeArchitecture` | <xref:System.Runtime.InteropServices.RuntimeInformation.ProcessArchitecture?displayProperty=nameWithType> |
  | `RuntimeEnvironment.OperatingSystem` | <xref:System.Runtime.InteropServices.RuntimeInformation.OSDescription?displayProperty=nameWithType> |
  | `RuntimeEnvironment.OperatingSystemVersion` | <xref:System.Runtime.InteropServices.RuntimeInformation.OSDescription?displayProperty=nameWithType> および <xref:System.Environment.OSVersion?displayProperty=nameWithType> |

  > [!NOTE]
  > `RuntimeEnvironment.OperatingSystem` と `RuntimeEnvironment.OperatingSystemVersion` のほとんどのユース ケースは、表示目的で使用されます。たとえば、ユーザー、ログ記録、テレメトリに表示するためのものです。 オペレーティング システム (OS) のバージョンに基づいて、実行時の決定を行うことはお勧めできません。 <xref:System.Environment.OSVersion?displayProperty=nameWithType> では、Windows および macOS オペレーティング システムの正しいバージョンが返されるようになりました。 しかし、ほとんどの Unix ディストリビューションでは、どのようなものを "OS バージョン" と見なすかは簡単ではありません。 たとえば、Linux カーネル バージョンの場合もあれば、ディストリビューション バージョンの場合もあります。 ほとんどの Unix プラットフォームでは、<xref:System.Environment.OSVersion?displayProperty=nameWithType> と <xref:System.Runtime.InteropServices.RuntimeInformation.OSDescription?displayProperty=nameWithType> から、`uname` で返されるバージョンが返されます。 Linux ディストリビューションの名前とバージョン情報を取得する場合は、 */etc/os-release* ファイルを読み取ることをお勧めします。

#### <a name="category"></a>カテゴリ

Core .NET ライブラリ

#### <a name="affected-apis"></a>影響を受ける API

- `Microsoft.DotNet.PlatformAbstractions.ApplicationEnvironment.ApplicationBasePath`
- <xref:Microsoft.DotNet.PlatformAbstractions.HashCodeCombiner?displayProperty=fullName>
- `Microsoft.DotNet.PlatformAbstractions.RuntimeEnvironment.GetRuntimeIdentifier()`
- `Microsoft.DotNet.PlatformAbstractions.RuntimeEnvironment.OperatingSystem`
- `Microsoft.DotNet.PlatformAbstractions.RuntimeEnvironment.OperatingSystemPlatform`
- `Microsoft.DotNet.PlatformAbstractions.RuntimeEnvironment.OperatingSystemVersion`
- `Microsoft.DotNet.PlatformAbstractions.RuntimeEnvironment.RuntimeArchitecture`

<!--

#### Affected APIs

- `P:Microsoft.DotNet.PlatformAbstractions.ApplicationEnvironment.ApplicationBasePath`
- `T:Microsoft.DotNet.PlatformAbstractions.HashCodeCombiner`
- `M:Microsoft.DotNet.PlatformAbstractions.RuntimeEnvironment.GetRuntimeIdentifier`
- `P:Microsoft.DotNet.PlatformAbstractions.RuntimeEnvironment.OperatingSystem`
- `P:Microsoft.DotNet.PlatformAbstractions.RuntimeEnvironment.OperatingSystemPlatform`
- `P:Microsoft.DotNet.PlatformAbstractions.RuntimeEnvironment.OperatingSystemVersion`
- `P:Microsoft.DotNet.PlatformAbstractions.RuntimeEnvironment.RuntimeArchitecture`

-->
