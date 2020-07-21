---
ms.openlocfilehash: 150b98255b3075a8fe8cad60ce234206b788a5f5
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617186"
---
### <a name="multi-line-aspnet-textbox-spacing-changed-when-using-antixssencoder"></a>AntiXSSEncoder を使用するときの複数行の ASP.Net TextBox の間隔が変更

#### <a name="details"></a>説明

.NET Framework 4.0 では、<xref:System.Web.Security.AntiXss.AntiXssEncoder?displayProperty=fullName> を使用する場合、ポストバックの複数行テキスト ボックスの行間に余分な行が挿入されました。 .NET Framework 4.5 では、これらの余分な改行は含まれませんが、web アプリが .NET Framework 4.5 を対象としている場合に限ります。

#### <a name="suggestion"></a>提案される解決策

4\.0 の Web アプリの対象を .NET Framework 4.5 に変更すると、複数行テキスト ボックスが改善され、余分な改行が挿入されなくなります。 これが望ましくない場合は、.NET Framework 4.0 を対象とすることによって、アプリを .NET Framework 4.5 で実行するときにも以前の動作が可能です。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.5         |
| 種類    | 再ターゲット中 |
