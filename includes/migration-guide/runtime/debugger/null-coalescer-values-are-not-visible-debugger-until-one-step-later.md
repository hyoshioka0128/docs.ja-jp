---
ms.openlocfilehash: 907c4aa5573c392a68afad0a4d937eadcd556440
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620295"
---
### <a name="null-coalescer-values-are-not-visible-in-debugger-until-one-step-later"></a>デバッガーですぐに null コアレッサー値が表示されない

#### <a name="details"></a>説明

.NET Framework 4.5 のバグにより、64 ビット版の Framework で実行中に代入演算が実行された直後に、デバッガーで null 合体演算で設定された値が表示されません。

#### <a name="suggestion"></a>提案される解決策

デバッガーでの操作に時間がかかると、ローカル/フィールドの値が正しく更新されなくなります。 この問題は .NET Framework 4.6 で修正されました。このバージョンの .NET Framework にアップグレードすれば、問題は解決します。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム|
