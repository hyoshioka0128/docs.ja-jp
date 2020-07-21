---
ms.openlocfilehash: c967a5b09b5e9ffeee7bff046f0c96469bc7fb02
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85615655"
---
### <a name="clickonce-supports-sha-256-on-40-targeted-apps"></a>4\.0 を対象とするアプリの ClickOnce が SHA-256 に対応

#### <a name="details"></a>説明

以前は、SHA-256 で署名された証明書が与えられた ClickOnce アプリには、アプリの対象が 4.0 の場合でも、.NET Framework 4.5 以降が必要でした。 それが今では、SHA-256 で署名されている場合でも、.NET Framework 4.0 を対象とする ClickOnce アプリを .NET Framework 4.0 で実行できるようになりました。

#### <a name="suggestion"></a>提案される解決策

この変更により、その依存関係がなくなったので、.NET Framework 4 以前のバージョンを対象とする ClickOnce アプリの署名に SAH-256 証明書が使用できるようになりました。

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.6         |
| 種類    | 再ターゲット中 |
