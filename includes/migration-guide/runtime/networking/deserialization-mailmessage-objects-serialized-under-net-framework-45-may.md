---
ms.openlocfilehash: ad953a1562db407c04d7860c60eb5964fe6fe2ca
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620345"
---
### <a name="deserialization-of-mailmessage-objects-serialized-under-the-net-framework-45-may-fail"></a>.NET Framework 4.5 でシリアル化された MailMessage オブジェクトの逆シリアル化が失敗する可能性がある

#### <a name="details"></a>説明

.NET Framework 4.5 以降では、<xref:System.Web.Mail.MailMessage> オブジェクトに非 ASCII 文字を含めることができます。 .NET Framework 4 では、ASCII 文字しかサポートされていません。 非 ASCII 文字が含まれ、.NET Framework 4.5 以降でシリアル化された <xref:System.Web.Mail.MailMessage> オブジェクトは、.NET Framework 4 で逆シリアル化することはできません。

#### <a name="suggestion"></a>提案される解決策

<xref:System.Web.Mail.MailMessage> オブジェクトの逆シリアル化時に、コードで例外処理が提供されることを確認します。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Web.Mail.MailMessage?displayProperty=nameWithType></li></ul>|
