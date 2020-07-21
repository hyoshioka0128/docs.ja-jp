---
ms.openlocfilehash: fc6066fd0b23d299158114cb397934041b99ba47
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620462"
---
### <a name="wpf-dispatchersynchronizationcontextcreatecopy-now-returns-a-new-copy-instead-of-the-current-instance"></a>WPF DispatcherSynchronizationContext.CreateCopy は、現在のインスタンスの代わりに新しいコピーを返すようになった

#### <a name="details"></a>説明

.NET Framework 4 では、<xref:System.Windows.Threading.DispatcherSynchronizationContext.CreateCopy> は、主にパフォーマンスの最適化として、現在のインスタンスへの参照を返しました。 .NET Framework 4.5 では、これが新しいインスタンスになり、参照が等しければ、実行中のスレッドが正しい同期コンテキストにあると結論付けることが初めて可能になりました。  これらの参照の ID をチェックするコードが影響を受ける可能性は低いですが、この変更により、<xref:System.Windows.Threading.DispatcherSynchronizationContext.CreateCopy> を呼び出すコードは、.NET Framework 4.5 以降への移行の一部としてテストする必要があります。

#### <a name="suggestion"></a>提案される解決策

<xref:System.Windows.Threading.DispatcherSynchronizationContext.CreateCopy> が新しい <xref:System.Threading.SynchronizationContext?displayProperty=fullName> オブジェクトを返すようになったことに注意してください。 以前は、このように生成された参照の等価性を使用するコードは、実際には、正しいコンテキストにあるかどうかを確認していませんでしたが、.NET Framework 4.5 以降でのビルド時には確認を行います。  問題になる可能性は低いですが、影響を受けるコードのパスをよく調べて、何か問題が生じないかどうか確認する必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.Threading.DispatcherSynchronizationContext.CreateCopy?displayProperty=nameWithType></li></ul>|
