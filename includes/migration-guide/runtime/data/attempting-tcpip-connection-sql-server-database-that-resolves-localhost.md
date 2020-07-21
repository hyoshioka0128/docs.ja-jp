---
ms.openlocfilehash: 87cb2570d3d47a2acb85b5557141c0fef885516a
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621806"
---
### <a name="attempting-a-tcpip-connection-to-a-sql-server-database-that-resolves-to-localhost-fails"></a>`localhost` に解決される SQL Server データベースへの TCP/IP 接続の試みが失敗します

#### <a name="details"></a>説明

.NET Framework 4.6 および 4.6.1 で、<code>localhost</code> に解決される SQL Server データベースへの TCP/IP 接続の試みが次のエラーで失敗していました: &quot;SQL Server への接続を確立しているときにネットワーク関連またはインスタンス固有のエラーが発生しました。 サーバーが見つからないかアクセスできません。 インスタンス名が正しいこと、および SQL Server がリモート接続を許可するように構成されていることを確認してください。 (プロバイダー:SQL ネットワーク インターフェイス、エラー:26 - 指定されたサーバーまたはインスタンスの位置を特定しているときにエラーが発生しました)&quot;

#### <a name="suggestion"></a>提案される解決策

この問題は修正済みであり、.NET Framework 4.6.2 では以前の動作に戻っています。 <code>localhost</code> に解決される SQL Server データベースに接続するには、.NET Framework 4.6.2 にアップグレードします。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.6|
|種類|ランタイム|
