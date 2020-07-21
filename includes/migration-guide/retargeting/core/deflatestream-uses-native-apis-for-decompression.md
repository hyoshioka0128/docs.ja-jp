---
ms.openlocfilehash: 7e42a294b151d07a6fdc61308cdf92df7a31a1d6
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614721"
---
### <a name="deflatestream-uses-native-apis-for-decompression"></a>DeflateStream で圧縮解除のためにネイティブ API が使用される

#### <a name="details"></a>説明

.NET Framework 4.7.2 以降では、`T:System.IO.Compression.DeflateStream` クラスの圧縮解除の実装の際に、既定でネイティブの Windows API を使用するように変更されました。 通常は、これによりパフォーマンスが大幅に改善されます。 .NET Framework バージョン 4.7.2 以降を対象とするすべての .NET アプリケーションでは、ネイティブ実装が使用されます。この変更により、次のように動作にいくつか違いが生じる場合があります。

- 例外メッセージが異なる場合があります。 ただし、スローされる例外の種類は変わりません。
- 操作を完了するのに十分なメモリがないなど、いくつかの特殊な状況が異なる方法で処理される場合があります。
- gzip ヘッダーの解析には、次のような違いが確認されています (注: 圧縮解除のために設定されている `GZipStream` のみが影響します)。
- 無効なヘッダーの解析時の例外がさまざまなタイミングでスローされる場合があります。
- ネイティブ実装では、gzip ヘッダー内で予約されているいくつかのフラグの値 (つまり、[FLG](http://www.zlib.org/rfc-gzip.html#header-trailer)) が、仕様に基づいて設定されるように強制されます。これにより、以前は無効な値が無視されていた例外がスローされる可能性があります。

#### <a name="suggestion"></a>提案される解決策

ネイティブ API での圧縮解除がアプリの動作に悪影響を与えている場合は、app.config ファイルの `runtime` セクションに `Switch.System.IO.Compression.DoNotUseNativeZipLibraryForDecompression` スイッチを追加して `true` に設定することで、この機能の選択を解除できます。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <runtime>
    <AppContextSwitchOverrides value="Switch.System.IO.Compression.DoNotUseNativeZipLibraryForDecompression=true" />
  </runtime>
</configuration>
```

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.7.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.IO.Compression.DeflateStream?displayProperty=nameWithType>
- <xref:System.IO.Compression.GZipStream?displayProperty=nameWithType>
