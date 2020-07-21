---
title: サービス アプリケーションのプログラミング アーキテクチャ
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ServiceController components, programming architecture
- ServiceBase class, service states
- Windows Service applications, code model
- services, programming architecture
- ServiceController class
- services, states
- ServiceProcessInstaller class, service application code model
- Windows Service applications, states
ms.assetid: 83230026-d068-4174-97ff-e264c896eb2f
author: ghogen
ms.openlocfilehash: 1c197b487f1cb7596f507f663fe3f1fb83857cbd
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053498"
---
# <a name="service-application-programming-architecture"></a>サービス アプリケーションのプログラミング アーキテクチャ
Windows サービス アプリケーションは、<xref:System.ServiceProcess.ServiceBase?displayProperty=nameWithType> クラスから継承するクラスが基になっています。 このクラスのメソッドをオーバーライドして機能を定義し、サービスの動作を決定します。  
  
 サービスの作成に関連する主要なクラスは次のとおりです。  
  
- <xref:System.ServiceProcess.ServiceBase?displayProperty=nameWithType> — サービスを作成するときに <xref:System.ServiceProcess.ServiceBase> クラスのメソッドをオーバーライドし、この継承したクラスでサービスがどのように機能するかを決定するコードを定義します。  
  
- <xref:System.ServiceProcess.ServiceProcessInstaller?displayProperty=nameWithType>、<xref:System.ServiceProcess.ServiceInstaller?displayProperty=nameWithType> — これらのクラスは、サービスのインストールとアンインストールに使います。  
  
 さらに、<xref:System.ServiceProcess.ServiceController> という名前のクラスを使って、サービス自体を操作できます。 このクラスは、サービスの作成には含まれませんが、サービスを開始および停止し、サービスにコマンドを渡し、サービスから一連の列挙値を戻すために使用できます。  
  
## <a name="defining-your-services-behavior"></a>サービスの動作の定義  
 サービス クラスにおいて、サービス コントロール マネージャー内でサービスの状態が変更されたときの動作を決定する基底クラスの関数をオーバーライドします。 <xref:System.ServiceProcess.ServiceBase> クラスで公開されている以下のメソッドをオーバーライドして、カスタム動作を追加できます。  
  
|メソッド|オーバーライドの目的|  
|------------|-----------------|  
|<xref:System.ServiceProcess.ServiceBase.OnStart%2A>|サービスが実行を開始するときに行う必要のあるアクションを示します。 サービスが意味のある処理を実行するには、このプロシージャにコードを記述する必要があります。|  
|<xref:System.ServiceProcess.ServiceBase.OnPause%2A>|サービスが一時停止されるときに行う必要があることを示します。|  
|<xref:System.ServiceProcess.ServiceBase.OnStop%2A>|サービスが実行を停止するときに行う必要があることを示します。|  
|<xref:System.ServiceProcess.ServiceBase.OnContinue%2A>|サービスが一時停止後に正常な機能を再開するときに行う必要があることを示します。|  
|<xref:System.ServiceProcess.ServiceBase.OnShutdown%2A>|システムがシャットダウンする時点でサービスが実行している場合に、シャットダウンの直前に行う必要があることを示します。|  
|<xref:System.ServiceProcess.ServiceBase.OnCustomCommand%2A>|サービスがカスタム コマンドを受け取ったときに行う必要があることを示します。 カスタム コマンドについて詳しくは、MSDN オンラインをご覧ください。|  
|<xref:System.ServiceProcess.ServiceBase.OnPowerEvent%2A>|バッテリ低下や中断操作など、電源管理イベントを受信したときのサービスの応答方法を示します。|  
  
> [!NOTE]
> これらのメソッドは、サービスがその有効期間内に通過する状態を表しています。サービスは、ある状態から次の状態に遷移します。 たとえば、<xref:System.ServiceProcess.ServiceBase.OnStart%2A> が呼び出される前の <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> コマンドにサービスが応答することはありません。  
  
 他にも、注目する必要のあるプロパティとメソッドがいくつかあります。 次の設定があります。  
  
- <xref:System.ServiceProcess.ServiceBase> クラスの <xref:System.ServiceProcess.ServiceBase.Run%2A> メソッド。 このメソッドは、サービスのメイン エントリ ポイントです。 Windows サービス テンプレートを使ってサービスを作成するときは、アプリケーションの `Main` メソッドに、サービスを実行するコードを挿入します。 このコードは次のようになります。  
  
     [!code-csharp[VbRadconService#6](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#6)]
     [!code-vb[VbRadconService#6](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#6)]  
  
    > [!NOTE]
    > これらの例では、アプリケーションに含まれる各サービスを追加できる <xref:System.ServiceProcess.ServiceBase> 型の配列を使用しており、すべてのサービスを一緒に実行できます。 一方、作成するサービスが 1 つのみの場合は、配列は使わず、<xref:System.ServiceProcess.ServiceBase> から継承する新しいオブジェクトを単純に宣言して、それを実行します。 例については、「[方法: プログラムでサービスを作成する](how-to-write-services-programmatically.md)」を参照してください。  
  
- <xref:System.ServiceProcess.ServiceBase> クラスの一連のプロパティ。 これらは、サービスで呼び出すことができるメソッドを決定します。 たとえば、<xref:System.ServiceProcess.ServiceBase.CanStop%2A> プロパティを `true` に設定すると、サービスで <xref:System.ServiceProcess.ServiceBase.OnStop%2A> メソッドを呼び出すことができます。 <xref:System.ServiceProcess.ServiceBase.CanPauseAndContinue%2A> プロパティが `true` に設定されていると、<xref:System.ServiceProcess.ServiceBase.OnPause%2A> および <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> メソッドを呼び出すことができます。 これらのプロパティのいずれかを `true` に設定するときは、関連するメソッドをオーバーライドして処理を定義する必要があります。  
  
    > [!NOTE]
    > サービスが役に立つためには、少なくとも <xref:System.ServiceProcess.ServiceBase.OnStart%2A> と <xref:System.ServiceProcess.ServiceBase.OnStop%2A> をオーバーライドする必要があります。  
  
 また、<xref:System.ServiceProcess.ServiceController> コンポーネントを使うと、既存のサービスと通信して、その動作を制御できます。  
  
## <a name="see-also"></a>関連項目

- [Windows サービス アプリケーションの概要](introduction-to-windows-service-applications.md)
- [方法: Windows サービスを作成する](how-to-create-windows-services.md)
