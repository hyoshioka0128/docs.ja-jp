---
title: LINQ to SQL におけるセキュリティ
ms.date: 03/30/2017
ms.assetid: d49787f7-414e-4c71-aa33-80a5895536b1
ms.openlocfilehash: f1ebf2f72fbfe3b27b9fbfd41f0dd65c70103620
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781187"
---
# <a name="security-in-linq-to-sql"></a>LINQ to SQL におけるセキュリティ
データベースに接続するときは、常にセキュリティのリスクがあります。 LINQ to SQL には SQL Server のデータを操作する新しい方法が含まれていますが、セキュリティ メカニズムは追加されていません。  
  
## <a name="access-control-and-authentication"></a>アクセス制御と認証  
 LINQ to SQL には独自のユーザー モデルや認証メカニズムがありません。 オブジェクト モデルにマッピングされるデータベース、データベースのテーブル、ビュー、ストアド プロシージャなどへのアクセス制御には SQL Server のセキュリティを使用します。 ユーザーには必要最小限のアクセス権を与え、ユーザー認証には強力なパスワードを要求してください。  
  
## <a name="mapping-and-schema-information"></a>マッピングとスキーマ情報  
 オブジェクト モデルまたは外部マッピング ファイルにある、SQL-CLR 型マッピングとデータベース スキーマ情報は、ファイル システムでこれらのファイルに対してアクセス権を持つ全ユーザーに公開されます。 オブジェクト モデルまたは外部マッピング ファイルにアクセスできるすべてのユーザーがスキーマ情報を使用できることを前提としています。 より広範囲にスキーマ情報をアクセス可能にするには、ファイル セキュリティ メカニズムを使用して、ソース ファイルとマッピング ファイルをセキュリティで保護します。  
  
## <a name="connection-strings"></a>接続文字列  
 接続文字列にパスワードを使用することは、できるだけ避けてください。 接続文字列自体がセキュリティのリスクであるうえに、接続文字列はオブジェクト リレーショナル デザイナーまたは SQLMetal コマンド ライン ツールの使用時にオブジェクト モデルや外部マッピング ファイルにクリア テキストで追加できます。 ファイル システムでオブジェクト モデルまたは外部マッピング ファイルに対してアクセス権があれば、どのユーザーでも接続パスワードを見ることができます (パスワードが接続文字列に含まれている場合)。  
  
 このようなリスクを最小限に抑えるには、統合セキュリティを使用して SQL Server との信頼関係接続を作成します。 この方法を使用すると、接続文字列にパスワードを含める必要がなくなります。 詳細については、「[SQL Server のセキュリティ](../sql-server-security.md)」をご覧ください。  
  
 統合セキュリティがない場合は、接続文字列にクリア テキストのパスワードが必要になります。 以下は、接続文字列のセキュリティ保護に最も有効な手段です。  
  
- 統合セキュリティを使用します。  
  
- 接続文字列をパスワードで保護し、接続文字列の配布を最小限にします。  
  
- 接続文字列の代わりに、表示時間に制限のある <xref:System.Data.SqlClient.SqlConnection?displayProperty=nameWithType> クラスを使用します。 LINQ to SQL の <xref:System.Data.Linq.DataContext?displayProperty=nameWithType> クラスは <xref:System.Data.SqlClient.SqlConnection> を使用してインスタンス化できます。  
  
- すべての接続文字列の期限と接触点を最小限にします。  
  
## <a name="see-also"></a>関連項目

- [背景情報](background-information.md)
- [よく寄せられる質問](frequently-asked-questions.md)
