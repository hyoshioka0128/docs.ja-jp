---
ms.openlocfilehash: 09fb7a54fccd5cf37800483c64e2fa6a54681f11
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621327"
---
### <a name="the-net-framework-46-does-not-use-a-45xx-version-when-registering-itself-in-the-registry"></a>.NET Framework 4.6 は、自分自身をレジストリに登録するときに 4.5.x.x バージョンを使用しない

#### <a name="details"></a>説明

予想されるように、.NET Framework 4.6 に対してレジストリ (<code>HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\NET Framework Setup\NDP\v4\Full</code>) に設定されるバージョン キーは、"4.5" ではなく "4.6" で始まります。 これらのレジストリ キーに依存してコンピューターにインストールされている .NET Framework のバージョンを特定するアプリは、4.6 が可能な新しいバージョンであり、前の 4.5.x リリースと互換性があることを認識するように、更新する必要があります。

#### <a name="suggestion"></a>提案される解決策

4\.5 のレジストリ キーを検索することによって .NET Framework 4.5 のインストールを調べるアプリを、4.6 も受け付けるように更新します。

| 名前    | 値       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.6|
|種類|ランタイム|
