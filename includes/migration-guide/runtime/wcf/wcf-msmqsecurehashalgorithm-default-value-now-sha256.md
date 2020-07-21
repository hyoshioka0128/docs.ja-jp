---
ms.openlocfilehash: ccdf232d743c9e270b6ed21f698998eb95a97399
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621219"
---
### <a name="wcf-msmqsecurehashalgorithm-default-value-is-now-sha256"></a>WCF MsmqSecureHashAlgorithm の既定値が SHA256 になった

#### <a name="details"></a>説明

.NET Framework 4.7.1 以降では、Msmq メッセージの WCF での既定のメッセージ署名アルゴリズムは SHA256 です。 .NET Framework 4.7 以前のバージョンでは、既定のメッセージ署名アルゴリズムは SHA1 です。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7.1 以降でこの変更に関する互換性の問題が発生した場合は、次の行を app.config ファイルの <code>&lt;runtime&gt;</code> セクションに追加することで、変更を無効にできます。<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.ServiceModel.UseSha1InMsmqEncryptionAlgorithm=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| 名前    | 値       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.7.1|
|種類|ランタイム|
