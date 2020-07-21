---
ms.openlocfilehash: a44458484ea09c566defeabc9b604bd55d994e93
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617539"
---
### <a name="calls-to-systemwindowsinputpencontextdisable-on-touch-enabled-systems-may-throw-an-argumentexception"></a>タッチ対応システムで System.Windows.Input.PenContext.Disable を呼び出すと ArgumentException がスローされることがある

#### <a name="details"></a>説明

一部の状況では、タッチ対応システムで内部 **System.Windows.Intput.PenContext.Disable** メソッドを呼び出すと、再入に起因して未処理の `T:System.ArgumentException` がスローされることがあります。

#### <a name="suggestion"></a>提案される解決策

この問題は、.NET Framework 4.7 では対処済みです。 例外を防ぐには、.NET Framework 4.7 以降のバージョンの .NET Framework にアップグレードします。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.6.1       |
| 種類    | 再ターゲット中 |
