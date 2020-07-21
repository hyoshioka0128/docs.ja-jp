---
ms.openlocfilehash: 83d3f24680531d1e447f047151a28c98ce0da04b
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620400"
---
### <a name="managed-browser-hosting-controls-from-the-net-framework-11-and-20-are-blocked"></a>.NET Framework 1.1 および 2.0 からのマネージド ブラウザーでのコントロールのホストがブロックされる

#### <a name="details"></a>説明

これらのコントロールのホストは、Internet Explorer でブロックされます。

#### <a name="suggestion"></a>提案される解決策

Internet Explorer では、マネージド ブラウザーを使用してコントロールをホストするアプリケーションは起動できません。 以前の動作を復元するには、レジストリ サブキー <code>HKLM/SOFTWARE/MICROSOFT/.NETFramework</code> の EnableIEHosting 値を、x86 システム用および x64 システム上の 32 ビット プロセス用に <code>1</code> に設定し、レジストリ サブキー <code>HKLM/SOFTWARE/Wow6432Node/Microsoft/.NETFramework</code> の <code>EnableIEHosting</code> 値を x64 システム上の 64 ビット プロセス用に <code>1</code> に設定します。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム|
