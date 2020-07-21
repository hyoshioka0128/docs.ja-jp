---
ms.openlocfilehash: 67e3ff5000ebd38064ed8a57e4fe561afa31f8d8
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614709"
---
### <a name="long-path-support"></a>長いパスのサポート

#### <a name="details"></a>説明

以降とするアプリをターゲットとする .NET Framework 4.6.2、長いパス (最大 32 K の文字) がサポートされている、および 260 文字 (または`MAX_PATH`) パスの長さの制限がなくなりました。 .NET Framework 4.6.2 を対象として再コンパイルされたアプリの場合は、コードをスローした以前のパス、 <xref:System.IO.PathTooLongException?displayProperty=fullName> 260 文字をスローがパスを超えたため、<xref:System.IO.PathTooLongException?displayProperty=fullName>次の条件下でのみ。

- パスの長さが <xref:System.Int16.MaxValue> (32,767) 文字を超えている。
- オペレーティング システムが `COR_E_PATHTOOLONG` またはそれと同等のものを返す。
.NET Framework 4.6.1 以前を対象とするアプリの場合、パスが 260 文字を超えるたびにランタイムで自動的に <xref:System.IO.PathTooLongException?displayProperty=fullName> がスローされます。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.6.2 を対象とするアプリケーションの場合、長いパスが望ましくないときは、`app.config` ファイルの `<runtime>` セクションに次を追加することで長いパスのサポートを無効にできます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.IO.BlockLongPaths=true" />
</runtime>
```

以前のバージョンの .NET Framework を対象とするが、.NET Framework 4.6.2 以降で実行するアプリの場合、`app.config` ファイルの `<runtime>` セクションに次を追加することで長いパスのサポートを選択できます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.IO.BlockLongPaths=false" />
</runtime>
```

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.6.2       |
| 種類    | 再ターゲット中 |
