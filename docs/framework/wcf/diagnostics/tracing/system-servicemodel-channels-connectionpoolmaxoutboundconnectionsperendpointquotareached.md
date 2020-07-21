---
title: Microsoft.Transactions.TransactionBridge.EnlistTransactionFailure
ms.date: 03/30/2017
ms.assetid: 1b9f5139-e122-4716-9ef7-2f38e1813993
ms.openlocfilehash: 742e80a3115e8f8caa728e0d8c460ee8b964ddc9
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84588718"
---
# <a name="microsofttransactionstransactionbridgeenlisttransactionfailure"></a>Microsoft.Transactions.TransactionBridge.EnlistTransactionFailure
WS-AT プロトコル サービスは、指定されたコーディネーション コンテキストを使用してトランザクションに参加することができませんでした。  
  
## <a name="description"></a>説明  
 指定された 2PC プロトコルのトランザクションに MSDTC が参加できない場合にトレースされます。  これは、トランザクションが存在しなくなった場合、参加が許可されなくなった場合、または既に参加が多すぎる場合に発生する可能性があります。  
  
## <a name="troubleshooting"></a>トラブルシューティング  
 トレース メッセージ内のステータス文字列を調べて、アクション可能な項目が存在するかどうかを確認します。  
  
## <a name="see-also"></a>関連項目

- [トレース](index.md)
- [トレースを使用したアプリケーションのトラブルシューティング](using-tracing-to-troubleshoot-your-application.md)
- [管理と診断](../index.md)
