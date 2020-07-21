---
ms.openlocfilehash: cef8096c971da8ae245ff974697022f350cb9195
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85616076"
---
### <a name="vbnet-no-longer-supports-partial-namespace-qualification-for-systemwindows-apis"></a>VB.NET は、System.Windows Api の部分的な名前空間の修飾をサポートしなくなりました

#### <a name="details"></a>説明

.NET Framework 4.5.2 以降では、VB.NET プロジェクトは、部分的に修飾された名前空間で System.Windows API を指定できません。 たとえば、`Windows.Forms.DialogResult` の参照は失敗します。 代わりに、コードは、完全修飾名 (<xref:System.Windows.Forms.DialogResult>) を参照するか、特定の名前空間をインポートして、<xref:System.Windows.Forms.DialogResult?displayProperty=fullName> を参照する必要があります。

#### <a name="suggestion"></a>提案される解決策

`System.Windows` API を単純な名前で参照するか (および関連する名前空間をインポートする)、完全修飾名で参照するように、コードを更新する必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.5.2       |
| 種類    | 再ターゲット中 |
