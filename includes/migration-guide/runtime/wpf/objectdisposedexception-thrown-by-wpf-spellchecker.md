---
ms.openlocfilehash: b836b26f3f52e9d0cc78feb764629bd2fa306657
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621809"
---
### <a name="objectdisposedexception-thrown-by-wpf-spellchecker"></a>ObjectDisposedException が WPF スペルチェックでスローされる

#### <a name="details"></a>説明

スペルチェックで <xref:System.ObjectDisposedException?displayProperty=fullName> がスローされ、WPF アプリケーションがシャットダウン時にクラッシュする場合があります。 これは .NET Framework 4.7 WPF で修正されます。例外は正しく処理されるため、アプリケーションが悪影響を受けることはなくなります。 ただし、デバッグ時に実行中のアプリケーションで初回例外が見られる場合があるので注意してください。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7 にアップグレードします

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.6.1|
|種類|ランタイム|
