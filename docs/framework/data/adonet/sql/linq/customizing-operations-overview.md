---
title: 操作のカスタマイズ:概要
ms.date: 03/30/2017
ms.assetid: a3546296-1443-4b88-aa6e-d41011041ba7
ms.openlocfilehash: 48116887471709c60c9666f68c7ebdd0e6d128a1
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70247524"
---
# <a name="customizing-operations-overview"></a>操作のカスタマイズ:概要
既定では、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、対応付けに基づいて、挿入、更新、および削除の各操作のための動的な SQL を生成します。 しかし実際には、セキュリティや検証などを目的とした独自のビジネス ロジックを追加することが必要になる場合がよくあります。  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、以下の方法で、これらの操作をカスタマイズできます。  
  
## <a name="loading-options"></a>読み込みオプション  
 クエリで、データベースに接続するときに、メイン ターゲットに関係するデータをどれだけ取得するかを制御できます。 この機能は主に、<xref:System.Data.Linq.DataLoadOptions> を使用して実装します。 詳細については、「[遅延読み込みと即時読み込み](deferred-versus-immediate-loading.md)」を参照してください。  
  
## <a name="partial-methods"></a>部分メソッド  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] による既定の対応付けでは、ビジネス ロジックの実装に使用できる部分メソッドが提供されます。 詳細については、「[部分メソッドによるビジネス ロジックの追加](adding-business-logic-by-using-partial-methods.md)」を参照してください。  
  
## <a name="stored-procedures-and-user-defined-functions"></a>ストアド プロシージャおよびユーザー定義関数  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、ストアド プロシージャとユーザー定義関数の使用がサポートされています。 ストアド プロシージャは、操作のカスタマイズによく使用されます。 詳細については、「[ストアド プロシージャ](stored-procedures.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [挿入、更新、および削除の各操作のカスタマイズ](customizing-insert-update-and-delete-operations.md)
