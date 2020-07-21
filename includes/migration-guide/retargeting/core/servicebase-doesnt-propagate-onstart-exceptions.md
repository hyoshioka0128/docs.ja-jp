---
ms.openlocfilehash: 519de92ca4201d199941afe6382ddf9fc480fbbd
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614780"
---
### <a name="servicebase-doesnt-propagate-onstart-exceptions"></a>ServiceBase で OnStart 例外を伝達させない

#### <a name="details"></a>説明

.NET Framework 4.7 以前のバージョンでは、サービス起動時にスローされた例外は <xref:System.ServiceProcess.ServiceBase.Run%2A?displayProperty=nameWithType> の呼び出し元に伝達されません。<br/>.NET Framework 4.7.1 を対象とするアプリケーション以降では、起動できなかったサービスに関して、ランタイムによって例外が <xref:System.ServiceProcess.ServiceBase.Run%2A?displayProperty=nameWithType> に伝達されます。

#### <a name="suggestion"></a>提案される解決策

サービスの起動時、例外が存在する場合、その例外は伝達されます。 サービスを起動できなかったとき、診断に役立ちます。 <br/>この動作が望ましくない場合、アプリケーション構成ファイルの &lt;runtime&gt; セクションに次の &lt;AppContextSwitchOverrides&gt; 要素を追加することで無効化できます。

```xml
<AppContextSwitchOverrides value="Switch.System.ServiceProcess.DontThrowExceptionsOnStart=true" />
```

4.7.1 より前のバージョンを対象とするアプリケーションでこの動作を望む場合、アプリケーション構成ファイルの &lt;runtime&gt; セクションに次の &lt;AppContextSwitchOverrides&gt; 要素を追加してください。

```xml
<AppContextSwitchOverrides value="Switch.System.ServiceProcess.DontThrowExceptionsOnStart=false" />
```

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.7.1       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.ServiceProcess.ServiceBase.Run(System.ServiceProcess.ServiceBase)?displayProperty=nameWithType>
- <xref:System.ServiceProcess.ServiceBase.Run(System.ServiceProcess.ServiceBase[])?displayProperty=nameWithType>
