---
title: '方法: サービスに関する情報のログを記録する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- AutoLog property
- services, logging information
- Windows Service applications, logging information about
- event logs, service applications
- application event logs, service applications
- logs, service applications
ms.assetid: c0d8140f-c055-4d8e-a2e0-37358a550116
author: ghogen
ms.openlocfilehash: 3c974d5a98f8056e45899b109878e5a28ab2938e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053608"
---
# <a name="how-to-log-information-about-services"></a>方法: サービスに関する情報のログを記録する
既定では、すべての Windows サービス プロジェクトはアプリケーション イベント ログとやり取りして、そこに情報および例外を書き込むことができます。 アプリケーションにこの機能が必要かどうかを指定するには、 <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> プロパティを使用します。 既定では、Windows サービス プロジェクト テンプレートで作成したサービスには、ログが有効にされます。 <xref:System.Diagnostics.EventLog> クラスの静的フォームを使用すると、 <xref:System.Diagnostics.EventLog> コンポーネントのインスタンスを作成したり、手動でソースを登録したりすることなく、ログにサービス情報を書き込むことができます。  
  
 ログが有効にされていると、サービスのインストーラーは自動的に、プロジェクトの各サービスを有効なイベント ソースとして、サービスのインストール先コンピューター上のアプリケーション ログに登録します。 サービスの起動時、停止時、一時停止時、再開時、インストール時、アンインストール時には常に、サービスが情報をログに記録します。 また、発生したすべてのエラーもログに記録します。 既定の動作を使用している場合、ログにエントリを書き込むためのコードを作成する必要はありません。これは、サービスが自動的に処理します。  
  
 アプリケーション ログ以外のイベント ログに書き込む必要がある場合は、 <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> プロパティを `false`に設定し、サービス コード内に独自のカスタム イベント ログを作成して、そのログに有効なエントリのソースとしてサービスを登録します。 その後、対象の操作が行われるたびにログにエントリを記録するコードを作成する必要があります。  
  
> [!NOTE]
> カスタム イベント ログを使用して、そのログに書き込むようにサービス アプリケーションを構成する場合、コードでサービスの <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> プロパティを設定する前に、そのイベント ログにアクセスしようとしないでください。 サービスを有効なイベントのソースとして登録するには、イベント ログにこのプロパティの値が必要です。  
  
### <a name="to-enable-default-event-logging-for-your-service"></a>サービスの既定のイベント ログを有効にするには  
  
- コンポーネントの <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> プロパティを `true`に設定します。  
  
    > [!NOTE]
    > 既定では、このプロパティは `true`に設定されています。 条件を評価してから、その条件の結果に基づいて <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> プロパティを設定するなどの複雑な処理を作成するのでない限り、このプロパティを明示的に設定する必要はありません。  
  
### <a name="to-disable-event-logging-for-your-service"></a>サービスの既定のイベント ログを無効にするには  
  
- コンポーネントの <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> プロパティを `false`に設定します。  
  
     [!code-csharp[VbRadconService#17](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#17)]
     [!code-vb[VbRadconService#17](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#17)]  
  
### <a name="to-set-up-logging-to-a-custom-log"></a>カスタム ログへのログ記録を設定するには  
  
1. <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> プロパティを `false`に設定します。  
  
    > [!NOTE]
    > カスタム ログを使用するには、 <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> を false に設定する必要があります。  
  
2. Windows サービス アプリケーションに <xref:System.Diagnostics.EventLog> コンポーネントのインスタンスを設定します。  
  
3. <xref:System.Diagnostics.EventLog.CreateEventSource%2A> メソッドを呼び出し、作成するログ ファイルのソース文字列と名前を指定して、カスタム ログを作成します。  
  
4. <xref:System.Diagnostics.EventLog.Source%2A> コンポーネント インスタンスの <xref:System.Diagnostics.EventLog> プロパティを、手順 3 で作成したソース文字列に設定します。  
  
5. <xref:System.Diagnostics.EventLog.WriteEntry%2A> コンポーネント インスタンスで <xref:System.Diagnostics.EventLog> メソッドにアクセスして、エントリを作成します。  
  
     次のコードに、カスタム ログへのログ記録を設定する方法を示します。  
  
    > [!NOTE]
    > このコード例では、 <xref:System.Diagnostics.EventLog> コンポーネントのインスタンスに `eventLog1` という名前を付けています (Visual Basic では`EventLog1` )。 手順 2 で別の名前を持つインスタンスを作成した場合は、それに応じてコードを変更してください。  
  
     [!code-csharp[VbRadconService#14](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#14)]
     [!code-vb[VbRadconService#14](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#14)]  
    [!code-csharp[VbRadconService#15](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#15)]
    [!code-vb[VbRadconService#15](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#15)]  
  
## <a name="see-also"></a>関連項目

- [Windows サービス アプリケーションの概要](introduction-to-windows-service-applications.md)
