---
title: CLR ユーザー定義型
ms.date: 03/30/2017
ms.assetid: 9f70e0b0-3a0d-4eb1-b914-07a5d0c167c2
ms.openlocfilehash: e3b087124773db592b349e07cd022b0f642bdbe3
ms.sourcegitcommit: e08b319358a8025cc6aa38737854f7bdb87183d6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2019
ms.locfileid: "64910729"
---
# <a name="clr-user-defined-types"></a>CLR ユーザー定義型
Microsoft SQL Server では、Microsoft .NET Framework 共通言語ランタイム (CLR) を使用して実装されるユーザー定義型 (UDT) をサポートしています。 CLR は SQL Server に統合されており、この機構を利用すると、データベースの型システムを拡張できます。 UDT を利用すれば、SQL Server データ型システムのユーザー拡張が可能であり、複雑な構造化型を定義することもできます。  
  
 UDT は、アプリケーション アーキテクチャの観点から見て 2 つの重要な利点を備えています。  
  
- 内部状態と外部動作の間の (クライアントとサーバーの両方での) 強力なカプセル化。  
  
- 他の関連するサーバー機能との緊密な統合。 独自の UDT を定義すると、列定義、変数、パラメーター、関数の結果、カーソル、トリガー、およびレプリケーションなど、SQL Server のシステム型を利用できるすべてのコンテキストでその UDT を使用できます。  
  
 詳細については、ご使用中の SQL Server のバージョンに対応する [SQL Server ドキュメント](/sql)を参照してください。
  
 **SQL Server のドキュメント**
  
1. [CLR ユーザー定義型](/sql/relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types)  
  
## <a name="see-also"></a>関連項目

- [ADO.NET の概要](../ado-net-overview.md)
