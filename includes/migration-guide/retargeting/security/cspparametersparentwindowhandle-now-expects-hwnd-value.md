---
ms.openlocfilehash: 4b5c886ad35afbbf0a68e03b3174ab9ea1f5524f
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614768"
---
### <a name="cspparametersparentwindowhandle-now-expects-hwnd-value"></a>CspParameters.ParentWindowHandle が HWND 値を受け取るようになる

#### <a name="details"></a>説明

.NET Framework 2.0 で導入された <xref:System.Security.Cryptography.CspParameters.ParentWindowHandle> 値をアプリケーションに使用すると、親ウィンドウのハンドル値を登録できます。これを利用して、キーにアクセスする必要がある UI (PIN プロンプトや同意を求めるダイアログなど) を、指定したウィンドウの子のモーダルとして開くことができます。 .NET Framework 4.7 を対象とするアプリ以降では、Windows フォーム アプリケーションは、次のようなコードを使用して、<xref:System.Security.Cryptography.CspParameters.ParentWindowHandle> プロパティを設定できます。

```csharp
cspParameters.ParentWindowHandle = form.Handle;
```

以前のバージョンの .NET Framework では、[HWND](https://docs.microsoft.com/windows/desktop/WinProg/windows-data-types#HWND) 値が置かれているメモリ内の場所を表す <xref:System.IntPtr?displayProperty=fullName> が値として必要でした。 Windows 7 以前のバージョンでこのプロパティを form.Handle に設定しても影響はありませんでしたが、Windows 8 以降のバージョンでは、&quot;<xref:System.Security.Cryptography.CryptographicException?displayProperty=fullName>:パラメーターが正しくありません&quot; が表示されます。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7 以降をターゲットとするアプリケーションで親ウィンドウの関係を登録する場合、次のように単純な形式を使用することをお勧めします。

```csharp
cspParameters.ParentWindowHandle = form.Handle;
```

渡すべき正しい値は、値 `form.Handle` が保持されているメモリ内の場所のアドレスであることがわかっていた場合は、AppContext スイッチ `Switch.System.Security.Cryptography.DoNotAddrOfCspParentWindowHandle` を `true` に設定して、動作変更を無効にできます。

- プログラムで AppContext の互換性スイッチを設定する (説明は[こちらに](https://devblogs.microsoft.com/dotnet/net-announcements-at-build-2015/#dotnet46)あります)。
- app.config ファイルの `<runtime>` セクションに以下の行を追加する:

```xml
<runtime>
 <AppContextSwitchOverrides value="Switch.System.Security.Cryptography.DoNotAddrOfCspParentWindowHandle=true"/>
</runtime>
```

逆に、アプリケーションが以前のバージョンの .NET Framework の下で読み込むとき、.NET Framework 4.7 ランタイムで新しい動作を選択する場合、AppContext スイッチを `false` に設定できます。

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.7         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Security.Cryptography.CspParameters.ParentWindowHandle?displayProperty=nameWithType>
