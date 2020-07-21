---
ms.openlocfilehash: f87d0dbeda6094bd745f5b580772b1161f30d0d5
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86218175"
---
### <a name="change-in-path-separator-character-in-fullname-property-of-ziparchiveentry-objects"></a>ZipArchiveEntry オブジェクトの FullName プロパティのパス区切り文字の変更

#### <a name="details"></a>説明

.NET Framework 4.6.1 以降のバージョンを対象とするアプリでは、<xref:System.IO.Compression.ZipFile.CreateFromDirectory%2A> メソッドのオーバーロードによって作成された <xref:System.IO.Compression.ZipArchiveEntry> オブジェクトの <xref:System.IO.Compression.ZipArchiveEntry.FullName> プロパティで、パスの区切り文字が円記号 ("\\") からスラッシュ ("/") に変更されています。 この変更によって、.NET の実装が [.ZIP ファイル形式の仕様](https://pkware.cachefly.net/webdocs/casestudies/APPNOTE.TXT)のセクション 4.4.17.1 に準拠するようになったほか、Windows 以外のシステムで ZIP アーカイブを圧縮解除できるようになりました。<br />Macintosh などの Windows 以外のオペレーティング システムで以前のバージョンの .NET Framework を対象とするアプリで作成された zip ファイルを圧縮解除すると、ディレクトリ構造を保持できません。 たとえば、Macintosh で、ディレクトリ パスとファイル名が円記号 ("\\") 文字で連結された名前を持つ一連のファイルを作成するとします。 その場合、圧縮解除されたファイルのディレクトリ構造は保持されません。

#### <a name="suggestion"></a>提案される解決策

.NET Framework <xref:System.IO?displayProperty=nameWithType> 名前空間の API によって Windows オペレーティング システム上に展開される .zip ファイルでは、この変更の影響は最小限になるはずです。これらの API では、パスの区切り文字としてスラッシュ ("/") または円記号 ("\\") をシームレスに処理できるためです。<br />この変更が望ましくない場合、アプリケーション構成ファイルの [`<runtime>`](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) セクションに構成設定を追加して、無効にすることができます。 次の例では、`<runtime>` セクションと無効に切り替える処理 `Switch.System.IO.Compression.ZipFile.UseBackslash` の両方を確認できます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.IO.Compression.ZipFile.UseBackslash=true" />
</runtime>
```

また、以前のバージョンの .NET Framework を対象とするものの、.NET Framework 4.6.1 以降のバージョンで実行されているアプリでは、アプリケーション構成ファイルの [`<runtime>`](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) セクションに構成設定を追加して、この動作を有効にすることができます。 次では、`<runtime>` セクションと有効に切り替える処理 `Switch.System.IO.Compression.ZipFile.UseBackslash` の両方を確認できます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.IO.Compression.ZipFile.UseBackslash=false" />
</runtime>
```

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.6.1       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.IO.Compression.ZipFile.CreateFromDirectory(System.String,System.String)?displayProperty=nameWithType>
- <xref:System.IO.Compression.ZipFile.CreateFromDirectory(System.String,System.String,System.IO.Compression.CompressionLevel,System.Boolean)?displayProperty=nameWithType>
- <xref:System.IO.Compression.ZipFile.CreateFromDirectory(System.String,System.String,System.IO.Compression.CompressionLevel,System.Boolean,System.Text.Encoding)?displayProperty=nameWithType>
