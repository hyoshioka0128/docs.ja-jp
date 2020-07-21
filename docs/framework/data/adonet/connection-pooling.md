---
title: 接続プール
description: データ ソースへの接続を開くコストを最小限にするために ADO.NET で使用される、接続プールと呼ばれる最適化の手法について説明します。
ms.date: 03/30/2017
ms.assetid: 955c057f-aea8-4ba8-aa6d-e3dfa18ba8d5
ms.openlocfilehash: b8f89dfda7edbde14dbb5945f10f2284ac43c3d8
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287091"
---
# <a name="connection-pooling"></a>接続プール
データ ソースへの接続は時間のかかる処理です。 接続を開くコストを最小限にするため、ADO.NET では、"*接続プール*" と呼ばれる最適化の手法が使われています。接続プールを使うことで、接続を開いて閉じるという処理の繰り返しによって生じるコストを、最小限に抑えることができます。 接続プールは、.NET Framework データ プロバイダーに応じて異なる処理が行われます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [SQL Server の接続プール (ADO.NET)](sql-server-connection-pooling.md)  
 接続プールの概要および SQL Server における接続プールの動作を説明します。  
  
 [OLE DB、ODBC、および Oracle 接続プール](ole-db-odbc-and-oracle-connection-pooling.md)  
 .NET Framework Data Provider for OLE DB、.NET Framework Data Provider for ODBC、および .NET Framework Data Provider for Oracle の接続プールについて説明します。  
  
## <a name="see-also"></a>関連項目

- [ADO.NET でのデータの取得および変更](retrieving-and-modifying-data.md)
- [ADO.NET の概要](ado-net-overview.md)
