---
title: SQL Server セキュリティの概要
description: 既知の脅威に対抗するための機能を理解し、将来の脅威を予測するうえで必要な、SQL Server のセキュリティ アーキテクチャについて説明します。
ms.date: 03/30/2017
ms.assetid: ae66dd75-5c16-4cc0-9e12-774dd26d3fb9
ms.openlocfilehash: c423a408e607c51c048ad08b91122a1fe06e31b2
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286276"
---
# <a name="overview-of-sql-server-security"></a>SQL Server セキュリティの概要
セキュリティを幾重にも重ねて講じる多層防御は、セキュリティ上の脅威に対抗する最も有効な手段です。 SQL Server のセキュリティ アーキテクチャは、データベースの管理者および開発者が安全なデータベース アプリケーションを作成して脅威に対応できるように設計されています。 SQL Server は、前のバージョンに新しい機能を導入することによって絶えず進化してきました。 しかし、セキュリティを箱詰めして出荷することはできません。 アプリケーションには、それぞれ固有のセキュリティ要件があります。 開発者は、既知の脅威に対してどのような機能を組み合わせるのが最も効果的かを理解し、将来発生する可能性のある脅威を予測する必要があります。  
  
 SQL Server のインスタンスは、サーバーを頂点とする階層形式のエンティティのコレクションを持ちます。 各サーバーには複数のデータベースが存在し、各データベースには、セキュリティ保護可能なオブジェクトのコレクションが存在します。 SQL Server へのアクセスが許可されたユーザー、グループ、またはプロセスを "*プリンシパル*" と呼び、SQL Server のセキュリティ保護可能なリソースにはすべて、プリンシパルに対して付与することのできる "*権限*" が関連付けられています。 SQL Server セキュリティ フレームワークでは、"*認証*" および "*承認*" を使用して、セキュリティ保護可能なエンティティへのアクセスを管理します。  
  
- 認証は SQL Server にログオンするプロセスです。プリンシパルは、サーバーによって評価される資格情報を送信することによってアクセスを要求します。 認証対象となるユーザーまたはプロセスの ID は、認証によって確立されます。  
  
- 承認は、プリンシパルがアクセスできる、セキュリティ保護可能なリソースと、これらのリソースに対して許可された操作を特定するプロセスです。  
  
 このセクションの各トピックでは、SQL Server のセキュリティの基礎を取り上げています。より詳細な情報を確認できるように、該当するバージョンの SQL Server オンライン ブックへのリンクも用意されています。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [SQL Server での認証](authentication-in-sql-server.md)  
 SQL Server のログインと認証の説明のほか、各種リソースへのリンクが記載されています。  
  
 [SQL Server のサーバー ロールとデータベース ロール](server-and-database-roles-in-sql-server.md)  
 固定サーバー ロールと固定データベース ロール、カスタム データベース ロール、組み込みアカウントの説明のほか、各種リソースへのリンクが記載されています。  
  
 [SQL Server における所有権とユーザーとスキーマの分離](ownership-and-user-schema-separation-in-sql-server.md)  
 オブジェクトの所有権とユーザーとスキーマの分離の説明のほか、各種リソースへのリンクが記載されています。  
  
 [SQL Server の承認とアクセス許可](authorization-and-permissions-in-sql-server.md)  
 最小特権の原則に基づく権限の付与について説明しているほか、各種リソースへのリンクが記載されています。  
  
 [SQL Server でのデータの暗号化](data-encryption-in-sql-server.md)  
 SQL Server におけるデータの暗号化オプションの説明のほか、各種リソースへのリンクが記載されています。  
  
 [SQL Server の CLR 統合セキュリティ](clr-integration-security-in-sql-server.md)  
 CLR 統合セキュリティ関連リソースへのリンクが記載されています。  
  
## <a name="see-also"></a>関連項目

- [ADO.NET アプリケーションのセキュリティ保護](../securing-ado-net-applications.md)
- [SQL Server のセキュリティ](sql-server-security.md)
- [SQL Server におけるアプリケーション セキュリティのシナリオ](application-security-scenarios-in-sql-server.md)
- [ADO.NET の概要](../ado-net-overview.md)
