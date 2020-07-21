---
ms.openlocfilehash: af10716fe5f4c07091e8605cdf620e4a499fb1e8
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620180"
---
### <a name="ipad-should-not-be-used-in-custom-capabilities-file-because-it-is-now-a-browser-capability"></a>iPad はブラウザー機能になったため、カスタム機能ファイルでは使用できない

#### <a name="details"></a>説明

.NET Framework 4.5 以降では、iPad は既定の ASP.NET ブラウザー機能ファイルの識別子であるため、カスタム機能ファイルでは使用できません

#### <a name="suggestion"></a>提案される解決策

iPad 固有の機能が必要な場合は、ユーザー エージェントのマッチングで新しい &quot;IPad&quot; ID を生成するのではなく、定義済みのゲートウェイ refID &quot;IPad&quot; で機能を設定して、iPad の動作を変更する必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム|
