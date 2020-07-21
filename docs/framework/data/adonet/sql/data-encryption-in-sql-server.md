---
title: SQL Server でのデータの暗号化
ms.date: 03/30/2017
ms.assetid: 83b992f7-b351-4678-b4b9-f4ffd58134cc
ms.openlocfilehash: 1d185dd121336b62bd66a11bf0cc4253b45ae47e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794247"
---
# <a name="data-encryption-in-sql-server"></a>SQL Server でのデータの暗号化
SQL Server には、証明書、非対称キー、対称キーのいずれかを使ってデータを暗号化したり、復号化したりできる関数が用意されています。 これらはすべて内部の証明書ストアで管理されます。 証明書ストアは、1 つ上の層がその下の層を保護する暗号化階層を使用することによって、証明書およびキーを保護します。 SQL Server では、この機能領域をシークレット ストレージと呼びます。  
  
 暗号化関数によってサポートされる最速の暗号化方式は対称キーによる暗号化です。 この方法は大量のデータを処理する場合に適しています。 対称キーは、証明書、パスワードまたは他の対称キーで暗号化できます。  
  
## <a name="keys-and-algorithms"></a>キーとアルゴリズム  
 SQL Server は、DES、Triple DES、RC2、RC4、128 ビット RC4、DESX、128 ビット AES、192 ビット AES、256 ビット AES など、複数の対称キー暗号化アルゴリズムをサポートしています。 アルゴリズムは Windows Crypto API を使って実装されています。  
  
 SQL Server は、オープンする対称キーをデータベース接続のスコープ内で複数管理できます。 オープンするキーは証明書ストアから取得でき、データを復号化する際に使用できます。 データの一部が復号化されていれば、使用する対称キーを指定する必要はありません。 暗号化された各値は、どのキーを使って暗号化されたかを示すキー識別子 (キー GUID) を保持します。 正しいキーが復号化されてオープンされた場合、暗号化されたバイト ストリームとオープンする対称キーとがエンジンによって照合されます。 次に、このキーを使って復号化が実行されて、データが返されます。 正しいキーがオープンされなかった場合は NULL が返されます。  
  
 データベース内の暗号化されたデータを使用する方法がわかる例については、「[データの列の暗号化](/sql/relational-databases/security/encryption/encrypt-a-column-of-data)」をご覧ください。
  
## <a name="external-resources"></a>外部リソース  
 データの暗号化の詳細については、次のリソースを参照してください。  
  
|リソース|説明|  
|-|-|  
|[SQL Server の暗号化](/sql/relational-databases/security/encryption/sql-server-encryption)|SQL Server における暗号化の概要を説明します。 このトピックには、他の記事へのリンクが含まれます。|  
|[暗号化階層](/sql/relational-databases/security/encryption/encryption-hierarchy)|SQL Server における暗号化の概要を説明します。 このトピックでは、他の記事へのリンクが提供されています。|  
  
## <a name="see-also"></a>関連項目

- [ADO.NET アプリケーションのセキュリティ保護](../securing-ado-net-applications.md)
- [SQL Server におけるアプリケーション セキュリティのシナリオ](application-security-scenarios-in-sql-server.md)
- [SQL Server での認証](authentication-in-sql-server.md)
- [SQL Server のサーバー ロールとデータベース ロール](server-and-database-roles-in-sql-server.md)
- [SQL Server における所有権とユーザーとスキーマの分離](ownership-and-user-schema-separation-in-sql-server.md)
- [SQL Server の承認とアクセス許可](authorization-and-permissions-in-sql-server.md)
- [ADO.NET の概要](../ado-net-overview.md)
