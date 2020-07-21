---
ms.openlocfilehash: 9659068304eb208fd6a0a753273453bc669fbc56
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621272"
---
### <a name="keytips-behavior-improved-in-wpf"></a>WPF での KeyTip の動作が改良された

#### <a name="details"></a>説明

KeyTip の動作が、Microsoft Word やエクスプローラーでの動作と同等に変更されています。 <xref:System.Windows.Input.KeyEventArgs.SystemKey> (具体的には <xref:System.Windows.Input.Key> または <xref:System.Windows.Input.Key.F11>) が押された場合に KeyTip の状態が有効かどうかを調べることによって、WPF は KeyTip キーを適切に処理します。 メニューがマウスによって開かれている場合でも、KeyTip はメニューを閉じるようになっています。

#### <a name="suggestion"></a>提案される解決策

N/A

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.7.2|
|種類|ランタイム|
