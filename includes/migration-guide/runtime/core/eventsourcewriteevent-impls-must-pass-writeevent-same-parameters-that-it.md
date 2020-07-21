---
ms.openlocfilehash: 662c140f019add66ff6605d47ad1f32c3f50d711
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620240"
---
### <a name="eventsourcewriteevent-impls-must-pass-writeevent-the-same-parameters-that-it-received-plus-id"></a>EventSource.WriteEvent impls は、受け取ったのと同じパラメーター (と ID) を WriteEvent に渡す必要がある

#### <a name="details"></a>説明

ランタイムは次の内容を指定するコントラクトを強制するようになりました。ETW イベント メソッドを定義する <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> から派生するクラスは、ETW イベント メソッドが渡された同じ引数が続くイベント ID の基底クラス <code>EventSource.WriteEvent</code> メソッドを呼び出す必要があります。

#### <a name="suggestion"></a>提案される解決策

<xref:System.IndexOutOfRangeException?displayProperty=fullName> 例外は、<xref:System.Diagnostics.Tracing.EventListener?displayProperty=fullName> がこのコントラクトに違反するイベント ソースのプロセスの <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> データを読み取るときに、スローされます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5.1|
|種類|ランタイム|
