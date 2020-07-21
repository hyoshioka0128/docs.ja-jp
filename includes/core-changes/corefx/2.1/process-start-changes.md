---
ms.openlocfilehash: 9544b65f31772d0f4cee918528a73171fec4de99
ms.sourcegitcommit: 348bb052d5cef109a61a3d5253faa5d7167d55ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "82021809"
---
### <a name="change-in-default-value-of-useshellexecute"></a>UseShellExecute の既定値の変更

<xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> の .NET Core での既定値は `false` です。 .NET Framework での既定値は `true` です。

#### <a name="change-description"></a>変更の説明

<xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType> では、たとえば、ペイントを起動する `Process.Start("mspaint.exe")` などのコードを使用して、アプリケーションを直接起動することができます。 また、<xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> が `true` に設定されている場合、関連付けられているアプリケーションを間接的に起動することもできます。 .NET Framework では、<xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> の既定値は `true` です。つまり、 *.txt* ファイルをメモ帳に関連付けていれば、`Process.Start("mytextfile.txt")` のようなコードではそのエディターが起動されます。 .NET Framework でアプリケーションを間接的に起動しないようにするには、明示的に <xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> を `false` に設定する必要があります。 .NET Core で、<xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> の既定値は `false` です。 つまり、既定では、`Process.Start` を呼び出したとき、関連付けられているアプリケーションは起動されません。

この変更は、パフォーマンス上の理由で .NET Core に導入されました。 通常、<xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType> は、アプリケーションを直接起動するために使用されます。 アプリケーションを直接起動するのに、Windows シェルを使用して、関連するパフォーマンス コストを生じさせる必要はありません。 この既定のケースを高速化するために、.NET Core では、<xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> の既定値を `false` に変更します。 必要に応じて、低速パスを選択できます。

#### <a name="version-introduced"></a>導入されたバージョン

2.1

> [!NOTE]
> .NET Core の以前のバージョンでは、Windows に対して `UseShellExecute` は実装されていませんでした。

#### <a name="recommended-action"></a>推奨アクション

アプリが古い動作に依存している場合は、<xref:System.Diagnostics.ProcessStartInfo> オブジェクトで <xref:System.Diagnostics.ProcessStartInfo.UseShellExecute> を `true` に設定して <xref:System.Diagnostics.Process.Start(System.Diagnostics.ProcessStartInfo)?displayProperty=nameWithType> を呼び出します。

#### <a name="category"></a>カテゴリ

Core .NET ライブラリ

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType>
- <xref:System.Diagnostics.ProcessStartInfo?displayProperty=nameWithType>

<!--

#### Affected APIs

- `Overload:System.Diagnostics.Process.Start`
- `M:System.Diagnostics.ProcessStartInfo`

-->
