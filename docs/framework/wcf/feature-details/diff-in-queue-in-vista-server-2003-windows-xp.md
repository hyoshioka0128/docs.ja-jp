---
title: Windows Vista、Windows Server 2003、および Windows XP におけるキュー機能の相違点
ms.date: 03/30/2017
helpviewer_keywords:
- queues [WCF], differences in operating systems
ms.assetid: aa809d93-d0a3-4ae6-a726-d015cca37c04
ms.openlocfilehash: 77491981bdef7d02da6894cbbee93c779972d803
ms.sourcegitcommit: a4f9b754059f0210e29ae0578363a27b9ba84b64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74837429"
---
# <a name="differences-in-queuing-features-in-windows-vista-windows-server-2003-and-windows-xp"></a>Windows Vista、Windows Server 2003、および Windows XP におけるキュー機能の相違点
このトピックでは、Windows Vista、[!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]、および [!INCLUDE[wxp](../../../../includes/wxp-md.md)]間の Windows Communication Foundation (WCF) キュー機能の違いについて説明します。  
  
## <a name="application-specific-dead-letter-queue"></a>アプリケーションごとの配信不能キュー  
 キューに置かれたメッセージは、受信側のアプリケーションでタイムリーに読み取らなれないと、無期限にキューに残ることがあります。 時間依存のメッセージでは、このような動作は適切ではありません。 時間依存のメッセージとは、キューに置かれたバインディングで `TimeToLive` プロパティが設定されているメッセージです。 このプロパティでは、メッセージの期限が切れるまでのキュー内での保持期間を指定します。 期限切れのメッセージは、配信不能キューと呼ばれる特別なキューに送信されます。 また、キューのクォータの超過、認証エラーの発生など、その他の理由でメッセージが配信不能キューに送信される場合もあります。  
  
 通常は、同じキュー マネージャーを共有する、キューに置かれたすべてのアプリケーションに対して、システム全体の配信不能キューが 1 つ存在します。 アプリケーションごとの配信不能キューを使用した場合は、個々のアプリケーションがそのアプリケーションごとの配信不能キューを指定できます。このため、キューに置かれた、同じキュー マネージャーを共有しているアプリケーション間の分離を改善できます。 配信不能キューを他のアプリケーションと共有しているアプリケーションは、キューをブラウズしてそのアプリケーション用のメッセージを見つける必要があります。 アプリケーションごとの配信不能キューが使用されている場合、アプリケーション専用の配信不能キューにあるメッセージはすべて、そのアプリケーション用ということになります。  
  
 Windows Vista には、アプリケーション固有の配信不能キューが用意されています。 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] と [!INCLUDE[wxp](../../../../includes/wxp-md.md)] では、アプリケーションごとの配信不能キューを使用できないので、アプリケーションは、システム全体の配信不能キューを使用する必要があります。  
  
## <a name="poison-message-handling"></a>有害メッセージの処理  
 有害メッセージとは、受信側アプリケーションへの配信試行の回数が最大値を超えたメッセージのことです。 この状況が生じるのは、トランザクション キューからメッセージを読み取るアプリケーションが、エラーなどの原因でメッセージをすぐに処理できないような場合です。 アプリケーションは、キューに置かれたメッセージを受信したトランザクションを中止した場合、メッセージをキューに戻します。 その後、アプリケーションは、新しいトランザクションで再度メッセージを取得しようとします。 エラーを引き起こす問題が解決しないと、受信側のアプリケーションは、同じメッセージの受信と中止を繰り返すループから出られなくなる可能性があります。その結果、配信試行回数が最大値を超過し、有害メッセージの状況が生じます。  
  
 Windows Vista、[!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]、および有害扱いに関連する [!INCLUDE[wxp](../../../../includes/wxp-md.md)] のメッセージキュー (MSMQ) の主な相違点を次に示します。  
  
- Windows Vista の MSMQ はサブキューをサポートしていますが、[!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] と [!INCLUDE[wxp](../../../../includes/wxp-md.md)] はサブキューをサポートしていません。 サブキューは、有害メッセージ処理で使用されます。 再試行キューと有害キューは、有害メッセージ処理の設定に基づいて作成されるアプリケーション キューのサブキューです。 作成する再試行サブキューの数は、`MaxRetryCycles` で指定します。 したがって、[!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] または [!INCLUDE[wxp](../../../../includes/wxp-md.md)] で実行している場合、`MaxRetryCycles` は無視されるため、`ReceiveErrorHandling.Move` は使用できません。  
  
- Windows Vista の MSMQ は否定受信確認をサポートしていますが、[!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] と [!INCLUDE[wxp](../../../../includes/wxp-md.md)] ではサポートされていません。 受信側キュー マネージャーから否定受信確認を受け取ると、送信側キュー マネージャーは拒否されたメッセージを配信不能キューに入れます。 そのため、`ReceiveErrorHandling.Reject` は、[!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] と [!INCLUDE[wxp](../../../../includes/wxp-md.md)] では使用できません。  
  
- Windows Vista の MSMQ では、メッセージの配信が試行された回数を保持するメッセージプロパティをサポートしています。 この中止回数のプロパティは、[!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] と [!INCLUDE[wxp](../../../../includes/wxp-md.md)] では使用できません。 WCF では、abort count がメモリ内に保持されるため、同じメッセージが Web ファーム内の複数の WCF サービスによって読み取られる場合、このプロパティに正確な値が含まれていない可能性があります。  
  
## <a name="remote-transactional-read"></a>リモート トランザクション読み取り  
 Windows Vista の MSMQ は、リモートトランザクション読み取りをサポートしています。 これによって、キューから読み取りを行うアプリケーションを、そのキューをホストしているコンピューターとは別のコンピューター上でホストすることが可能になります。 これにより、サービスのファーム全体で中央のキューから読み取りを行うことができるようになり、システムの全体のスループットが向上します。 また、メッセージの読み取り中および処理中にエラーが発生した場合、トランザクションはロールバックし、メッセージは後で処理できるようにキューに残るようにもなります。  
  
## <a name="see-also"></a>参照

- [配信不能キューを使用したメッセージ転送エラー処理](../../../../docs/framework/wcf/feature-details/using-dead-letter-queues-to-handle-message-transfer-failures.md)
- [有害メッセージ処理](../../../../docs/framework/wcf/feature-details/poison-message-handling.md)
