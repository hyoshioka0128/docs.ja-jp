---
title: IAsyncResult を使用した非同期メソッドの呼び出し
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- ending asynchronous operations
- waiting for asynchronous operations
- asynchronous method calling
- calling asynchronous methods
- asynchronous programming, calling asynchronous methods
- IAsyncResult interface, calling asynchronous methods
- stopping asynchronous operations
ms.assetid: 07fba116-045b-473c-a0b7-acdbeb49861f
ms.openlocfilehash: 88ca1b5bfbb8bfbdfef01dea8af07c5d56784c5c
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289916"
---
# <a name="calling-asynchronous-methods-using-iasyncresult"></a>IAsyncResult を使用した非同期メソッドの呼び出し
.NET Framework とサードパーティのさまざま種類のクラス ライブラリが提供するメソッドを利用することで、アプリケーションはメインのアプリケーション スレッド以外のスレッドで非同期操作を実行しながら実行を継続できます。 次のセクションでは、コード例を取り上げ、<xref:System.IAsyncResult> 設計パターンを使用する非同期メソッドをさまざまな方法で呼び出します。  
  
- [非同期操作の終了によるアプリケーション実行のブロック](blocking-application-execution-by-ending-an-async-operation.md)。  
  
- [AsyncWaitHandle の使用によるアプリケーション実行のブロック](blocking-application-execution-using-an-asyncwaithandle.md)。  
  
- [非同期操作のステータスのポーリング](polling-for-the-status-of-an-asynchronous-operation.md)。  
  
- [AsyncCallback デリゲートの使用による非同期操作の終了](using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md)。  
  
## <a name="see-also"></a>参照

- [イベント ベースの非同期パターン (EAP)](event-based-asynchronous-pattern-eap.md)
- [イベントベースの非同期パターンの概要](event-based-asynchronous-pattern-overview.md)
