---
ms.openlocfilehash: f980c8029375074889505a8eb7e8a65aaa8d74e4
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614769"
---
### <a name="resgen-refuses-to-load-content-from-the-web"></a>resgen で Web からのコンテンツの読み込みが拒否される

#### <a name="details"></a>説明

.resx ファイルには、バイナリ形式の入力が含まれている場合があります。 resgen を使用して、信頼されていない場所からダウンロードされたファイルを読み込もうとすると、既定で入力の読み込みに失敗します。

#### <a name="suggestion"></a>提案される解決策

信頼されていない場所からのバイナリ形式の入力を読み込む必要がある resgen ユーザーは、入力ファイルから Web のマークを削除するか、オプトアウト特性を適用できます。次のレジストリ設定を追加して、マシン全体のオプトアウト特性を適用します: [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft.NETFramework\SDK] &quot;AllowProcessOfUntrustedResourceFiles&quot;=&quot;true&quot;

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.7.2       |
| 種類    | 再ターゲット中 |
