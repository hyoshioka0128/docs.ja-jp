---
ms.openlocfilehash: e66a5c2a33a4ab5cf35013c1843936ffd01f90a2
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614745"
---
### <a name="serialport-background-thread-exceptions"></a>SerialPort バックグラウンド スレッドの例外

#### <a name="details"></a>説明

OS 例外がスローされたとき、<xref:System.IO.Ports.SerialPort> ストリームで作成されたバックグラウンド スレッドによってプロセスが終了することがなくなりました。 <br/>.NET Framework 4.7 以前のバージョンを対象とするアプリケーションでは、<xref:System.IO.Ports.SerialPort> ストリームで作成されたバックグラウンド スレッドでオペレーティング システム例外がスローされたとき、プロセスが終了します。 <br/>.NET Framework 4.7.1 以降のバージョンを対象とするアプリケーションでは、バックグラウンド スレッドはアクティブなシリアル ポートに関連付けられている OS イベントを待ち、シリアル ポートが急に削除されるなどした場合にクラッシュすることがあります。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7.1 を対象とするアプリケーションの場合、例外処理が望ましくないときは、`app.config` ファイルの `<runtime>` セクションに次を追加することで例外処理を無効にできます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.IO.Ports.DoNotCatchSerialStreamThreadExceptions=true" />
</runtime>
```

以前のバージョンの .NET Framework を対象とするが、.NET Framework 4.7.1 以降で実行するアプリの場合、`app.config` ファイルの `<runtime>` セクションに次を追加することで例外処理を選択できます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.IO.Ports.DoNotCatchSerialStreamThreadExceptions=false" />
</runtime>
```

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.7.1       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.IO.Ports.SerialPort?displayProperty=nameWithType>
