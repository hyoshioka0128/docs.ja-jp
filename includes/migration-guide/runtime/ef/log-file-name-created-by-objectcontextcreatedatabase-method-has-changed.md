---
ms.openlocfilehash: 768a948849064cedb38110f5ed271717442325c0
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620315"
---
### <a name="log-file-name-created-by-the-objectcontextcreatedatabase-method-has-changed-to-match-sql-server-specifications"></a>ObjectContext.CreateDatabase メソッドによって作成されたログ ファイル名が、SQL Server の仕様に一致するように変更された

#### <a name="details"></a>説明

<xref:System.Data.Objects.ObjectContext.CreateDatabase?displayProperty=fullName> メソッドが、直接、または SqlClient プロバイダーと共に Code First と接続文字列の AttachDBFilename 値を使用して呼び出されると、filename.ldf (filename は AttachDBFilename 値によって指定されたファイルの名前) ではなく、filename_log.ldf という名前のログ ファイルを作成します。 この変更により、SQL Server の仕様に従ってログ ファイル名が提供されるため、デバッグ機能が向上します。

#### <a name="suggestion"></a>提案される解決策

ログ ファイル名がアプリケーションにとって重要な場合、標準の _log.ldf ファイル名形式を予期するように、アプリケーションを更新する必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Data.Objects.ObjectContext.CreateDatabase?displayProperty=nameWithType></li></ul>|
