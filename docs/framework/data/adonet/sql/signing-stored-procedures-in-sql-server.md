---
title: SQL Server でのストアド プロシージャの署名
ms.date: 01/05/2018
ms.assetid: eeed752c-0084-48e5-9dca-381353007a0d
ms.openlocfilehash: 0131655d06a6ef543ea460d04739401538cac04b
ms.sourcegitcommit: 700ea803fb06c5ce98de017c7f76463ba33ff4a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77452358"
---
# <a name="signing-stored-procedures-in-sql-server"></a>SQL Server でのストアド プロシージャの署名

デジタル署名は、署名者の秘密キーで暗号化されたデータ ダイジェストです。 秘密キーにより、デジタル署名がその保持者または所有者に固有であることが保証されます。 ストアド プロシージャ、関数 (インライン テーブル値関数を除く)、トリガー、アセンブリに署名できます。

証明書や非対称キーを使用してストアド プロシージャに署名することができます。 この機能は、動的 SQL などのように、組み合わせ所有権によって権限を継承できない場合や、組み合わせ所有権が壊れている場合を想定して用意されています。 証明書にマップされたユーザーを作成し、その証明書ユーザーに、ストアド プロシージャがアクセスする必要があるオブジェクトへのアクセス許可を与えることができます。

同じ証明書にマップされたログインを作成し、必要なサーバー レベルのアクセス許可をそのログインに付与したり、1 つ以上の固定サーバー ロールにログインを追加したりすることもできます。 これは、高いレベルのアクセス許可が必要なシナリオで、`TRUSTWORTHY` のデータベース設定を有効にしなくて済むように設計されています。

ストアド プロシージャが実行されるときに、SQL Server によって証明書ユーザーやログインのアクセス許可が、呼び出し元のアクセス許可と組み合わされます。 `EXECUTE AS` 句とは異なり、プロシージャの実行コンテキストは変更されません。 ログイン名とユーザー名を返す組み込み関数を実行すると、証明書ユーザーの名前ではなく、呼び出し元の名前が返されます。

## <a name="creating-certificates"></a>証明書の作成

証明書または非対称キーを使用してストアド プロシージャに署名すると、ストアド プロシージャのコードの暗号化ハッシュで構成されたデータ ダイジェストが、実行ユーザーと共に、秘密キーを使用して作成されます。 実行時に、このデータ ダイジェストが公開キーを使用して復号化され、ストアド プロシージャのハッシュ値と比較されます。 実行ユーザーを変更するとハッシュ値が無効になり、デジタル署名が一致しなくなります。 ストアド プロシージャを変更すると、署名が完全に削除され、これにより、秘密キーへのアクセス権を持たないユーザーは、ストアド プロシージャのコードを変更できなくなります。 どちらの場合も、コードまたは実行ユーザーを変更するたびに、プロシージャに再署名する必要があります。

モジュールに署名するには、次の 2 つのステップを実行する必要があります。

1. Transact-SQL ステートメント `CREATE CERTIFICATE [certificateName]` を使用して、証明書を作成します。 このステートメントには、開始日、終了日、パスワードを設定するためのオプションがあります。 既定の有効期限は 1 年間です。

1. Transact-SQL ステートメント `ADD SIGNATURE TO [procedureName] BY CERTIFICATE [certificateName]` を使用して、証明書によってプロシージャに署名します。

モジュールに署名したら、証明書に関連付ける必要がある追加のアクセス許可を保持するため、1 つ以上のプリンシパルを作成する必要があります。

モジュールにデータベース レベルのアクセス許可を追加する必要がある場合:

1. Transact-SQL ステートメント `CREATE USER [userName] FROM CERTIFICATE [certificateName]` を使用して、証明書に関連付けられたデータベース ユーザーを作成します。 このユーザーはデータベースにのみ存在し、ログインも同じ証明書から作成されている場合を除き、ログインには関連付けられません。

1. 証明書ユーザーに、必要なデータベース レベルのアクセス許可を与えます。

モジュールにサーバー レベルのアクセス許可を追加する必要がある場合:

1. 証明書を `master` データベースにコピーします。

1. Transact-SQL のステートメント `CREATE LOGIN [userName] FROM CERTIFICATE [certificateName]` を使用して、その証明書に関連付けられたログインを作成します。

1. 証明書ログインに、必要なサーバー レベルのアクセス許可を与えます。

> [!NOTE]
> 証明書では、DENY ステートメントを使用して権限が取り消されているユーザーに権限を与えることはできません。 DENY は常に GRANT よりも優先されるため、証明書ユーザーに許可された権限を呼び出し元が継承することはできません。

## <a name="external-resources"></a>外部リソース

詳細については、次のリソースを参照してください。

|リソース|説明|
|--------------|-----------------|
|[モジュール署名](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/ms345102(v=sql.100))|モジュールの署名について説明し、サンプル シナリオと、関連する Transact-SQL の記事へのリンクを示します。|
|[証明書を使用したストアド プロシージャへの署名](/sql/relational-databases/tutorial-signing-stored-procedures-with-a-certificate)|証明書を使用したストアド プロシージャの署名のチュートリアルです。|

## <a name="see-also"></a>関連項目

- [ADO.NET アプリケーションのセキュリティ保護](../securing-ado-net-applications.md)
- [SQL Server セキュリティの概要](overview-of-sql-server-security.md)
- [SQL Server におけるアプリケーション セキュリティのシナリオ](application-security-scenarios-in-sql-server.md)
- [SQL Server でのストアド プロシージャを使用したアクセス許可の管理](managing-permissions-with-stored-procedures-in-sql-server.md)
- [SQL Server での安全な動的 SQL の作成](writing-secure-dynamic-sql-in-sql-server.md)
- [SQL Server での借用を使用したアクセス許可のカスタマイズ](customizing-permissions-with-impersonation-in-sql-server.md)
- [ストアド プロシージャでのデータの変更](../modifying-data-with-stored-procedures.md)
- [ADO.NET の概要](../ado-net-overview.md)
