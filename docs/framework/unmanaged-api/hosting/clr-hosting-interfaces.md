---
title: CLR ホスト インターフェイス
ms.date: 03/30/2017
helpviewer_keywords:
- interfaces [.NET Framework hosting], version 2.0
- hosting interfaces [.NET Framework], version 2.0
- .NET Framework 2.0, hosting interfaces
ms.assetid: 703b8381-43db-4a4d-9faa-cca39302d922
ms.openlocfilehash: e6913e18a4ff6e616f357a4ef43fb8b892264943
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616841"
---
# <a name="clr-hosting-interfaces"></a>CLR ホスト インターフェイス
ここでは、アンマネージホストが共通言語ランタイム (CLR) をアプリケーションに統合するために使用できるインターフェイスについて説明します。 この情報は .NET Framework バージョン2.0 以降のバージョンに関連します。 これらのインターフェイスを使用すると、ホストは、バージョン1.0 および1.1 で可能な限り多くのランタイムの側面を制御でき、CLR とホストの実行モデルとの間の統合が大幅に強化されます。  
  
 .NET Framework バージョン1.0 および1.1 では、ホストモデルによって、CLR をプロセスに読み込み、特定の設定を構成し、イベント通知を受信するために、管理されていないホストが有効になりました。 ただし、一般に、ホストと CLR は、そのプロセスで独立して実行されていました。 .NET Framework バージョン2.0 以降のバージョンでは、新しい階層の抽象化により、ホストは、Win32 アセンブリの型によって現在提供されている多くのリソースを提供し、ホストが構成できる一連の機能を拡張できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [IActionOnCLREvent インターフェイス](iactiononclrevent-interface.md)  
 登録されているイベントに対してコールバックを実行するメソッドを提供します。  
  
 [IApartmentCallback インターフェイス](iapartmentcallback-interface.md)  
 アパートメント内でコールバックを作成するためのメソッドを提供します。  
  
 [IAppDomainBinding インターフェイス](iappdomainbinding-interface.md)  
 実行時の構成を設定するためのメソッドを提供します。  
  
 [ICatalogServices インターフェイス](icatalogservices-interface.md)  
 サービスのカタログ化を行うためのメソッドを提供します。 (このインターフェイスは .NET Framework インフラストラクチャをサポートします。独自に作成したコードから直接使用するためのものではありません)。  
  
 [ICLRAssemblyIdentityManager インターフェイス](iclrassemblyidentitymanager-interface.md)  
 アセンブリに関するホストと CLR 間の通信をサポートするメソッドを提供します。  
  
 [ICLRAssemblyReferenceList インターフェイス](iclrassemblyreferencelist-interface.md)  
 ホストではなく、CLR によって読み込まれるアセンブリの一覧を管理します。  
  
 [ICLRControl インターフェイス](iclrcontrol-interface.md)  
 ホストが CLR に対してアクセスを取得し、さまざまな側面を構成するためのメソッドを提供します。  
  
 [ICLRDebugManager インターフェイス](iclrdebugmanager-interface.md)  
 ホストが一連のタスクを識別子とフレンドリ名に関連付けることができるようにするメソッドを提供します。  
  
 [ICLRErrorReportingManager インターフェイス](iclrerrorreportingmanager-interface.md)  
 エラー報告のためにホストがカスタムヒープダンプを構成できるようにするメソッドを提供します。  
  
 [ICLRGCManager インターフェイス](iclrgcmanager-interface.md)  
 ホストが CLR のガベージコレクションシステムと対話できるようにするメソッドを提供します。  
  
 [ICLRHostBindingPolicyManager インターフェイス](iclrhostbindingpolicymanager-interface.md)  
 ホストがアセンブリのポリシー情報の変更を評価および通知するためのメソッドを提供します。  
  
 [ICLRHostProtectionManager インターフェイス](iclrhostprotectionmanager-interface.md)  
 ホストが、部分的に信頼されたコードで実行される特定のマネージクラス、メソッド、プロパティ、およびフィールドをブロックできるようにします。  
  
 [ICLRIoCompletionManager インターフェイス](iclriocompletionmanager-interface.md)  
 ホストが、指定された i/o 要求のステータスを CLR に通知できるようにするコールバックメソッドを実装します。  
  
 [ICLRMemoryNotificationCallback インターフェイス](iclrmemorynotificationcallback-interface.md)  
 Win32 関数と同様の方法を使用して、ホストがメモリ不足状態を報告できるようにし `CreateMemoryResourceNotification` ます。  
  
 [ICLROnEventManager インターフェイス](iclroneventmanager-interface.md)  
 ホストが CLR イベントのコールバックを登録および登録解除できるようにするメソッドを提供します。  
  
 [ICLRPolicyManager インターフェイス](iclrpolicymanager-interface.md)  
 エラーとタイムアウトが発生した場合に実行されるポリシーアクションをホストが指定できるようにするメソッドを提供します。  
  
 [ICLRProbingAssemblyEnum インターフェイス](iclrprobingassemblyenum-interface.md)  
 ホストが CLR 内部のアセンブリ id 情報を使用してアセンブリのプローブ id を取得できるようにするメソッドを提供します。このメソッドは、その id を作成したり、理解したりする必要はありません。  
  
 [ICLRReferenceAssemblyEnum インターフェイス](iclrreferenceassemblyenum-interface.md)  
 CLR 内部のアセンブリ id データを使用して、ファイルまたはストリームによって参照されるアセンブリのセットをホストが操作できるようにするメソッドを提供します。これらの id を作成したり、理解したりする必要はありません。  
  
 [ICLRRuntimeHost インターフェイス](iclrruntimehost-interface.md)  
 には、 [ICorRuntimeHost](icorruntimehost-interface.md)と同様の機能が用意されており、ホストコントロールインターフェイスを設定するための追加のメソッドもあります。  
  
 [ICLRSyncManager インターフェイス](iclrsyncmanager-interface.md)  
 ホストが、要求されたタスクに関する情報を取得し、その同期実装でデッドロックを検出するためのメソッドを提供します。  
  
 [ICLRTask インターフェイス](iclrtask-interface.md)  
 ホストが CLR の要求を行うことができるようにするメソッド、または関連付けられたタスクについて CLR に通知を提供するためのメソッドを提供します。  
  
 [ICLRTaskManager インターフェイス](iclrtaskmanager-interface.md)  
 CLR が新しいタスクを作成し、現在実行中のタスクを取得し、タスクの地理的言語とカルチャを設定することをホストが明示的に要求できるようにするメソッドを提供します。  
  
 [ICLRValidator インターフェイス](iclrvalidator-interface.md)  
 ポータブル実行可能 (PE) イメージを検証し、検証エラーを報告するためのメソッドを提供します。  
  
 [ICorConfiguration インターフェイス](icorconfiguration-interface.md)  
 CLR を構成するためのメソッドを提供します。  
  
 [ICorThreadpool インターフェイス](icorthreadpool-interface.md)  
 スレッドプールにアクセスするためのメソッドを提供します。  
  
 [IDebuggerInfo Iインターフェイス](idebuggerinfo-interface.md)  
 デバッグサービスの状態に関する情報を取得するためのメソッドを提供します。  
  
 [IDebuggerThreadControl インターフェイス](idebuggerthreadcontrol-interface.md)  
 デバッグサービスによるスレッドのブロックおよびブロック解除についてホストに通知するためのメソッドを提供します。  
  
 [IGCHost インターフェイス](igchost-interface.md)  
 ガベージコレクションシステムに関する情報を取得し、ガベージコレクションのいくつかの側面を制御するためのメソッドを提供します。  
  
 [IGCHost2 インターフェイス](igchost2-interface.md)  
 ホストがガベージコレクションセグメントのサイズとガベージコレクションシステムのジェネレーション0の最大サイズをより大きい値に設定できるようにする[SetGCStartupLimitsEx](igchost2-setgcstartuplimitsex-method.md)メソッドを提供し `DWORD` ます。  
  
 [IGCHostControl インターフェイス](igchostcontrol-interface.md)  
 仮想メモリの制限を変更するように、ガベージコレクターがホストに要求できるようにするメソッドを提供します。  
  
 [IGCThreadControl インターフェイス](igcthreadcontrol-interface.md)  
 ガベージコレクションのためにブロックされるスレッドのスケジュール設定に参加するためのメソッドを提供します。  
  
 [IHostAssemblyManager インターフェイス](ihostassemblymanager-interface.md)  
 CLR またはホストによって読み込まれる必要があるアセンブリのセットをホストが指定できるようにするメソッドを提供します。  
  
 [IHostAssemblyStore インターフェイス](ihostassemblystore-interface.md)  
 ホストが CLR とは無関係にアセンブリおよびモジュールを読み込むことができるようにするメソッドを提供します。  
  
 [IHostAutoEvent インターフェイス](ihostautoevent-interface.md)  
 ホストによって実装される自動リセットイベントの表現を提供します。  
  
 [IHostControl インターフェイス](ihostcontrol-interface.md)  
 アセンブリの読み込みを構成し、ホストがサポートするホストインターフェイスを決定するためのメソッドを提供します。  
  
 [IHostCrst インターフェイス](ihostcrst-interface.md)  
 スレッド処理のためのクリティカルセクションのホストの表現として機能します。  
  
 [IHostGCManager インターフェイス](ihostgcmanager-interface.md)  
 CLR によって実装されるガベージコレクション機構でイベントのホストに通知するメソッドを提供します。  
  
 [IHostIoCompletionManager インターフェイス](ihostiocompletionmanager-interface.md)  
 ホストによって提供される i/o 完了ポートと CLR が対話できるようにするメソッドを提供します。  
  
 [IHostMalloc インターフェイス](ihostmalloc-interface.md)  
 CLR がホストを介してヒープから細かい割り当てを要求するためのメソッドを提供します。  
  
 [IHostManualEvent インターフェイス](ihostmanualevent-interface.md)  
 手動リセットイベントの表現のホストの実装を提供します。  
  
 [IHostMemoryManager インターフェイス](ihostmemorymanager-interface.md)  
 標準の Win32 仮想メモリ関数を使用する代わりに、CLR がホストを介して仮想メモリ要求を行うためのメソッドを提供します。  
  
 [IHostPolicyManager インターフェイス](ihostpolicymanager-interface.md)  
 中止、タイムアウト、またはエラーが発生した場合に CLR が実行するアクションをホストに通知するメソッドを提供します。  
  
 [IHostSecurityContext インターフェイス](ihostsecuritycontext-interface.md)  
 CLR がホストによって実装されたセキュリティコンテキスト情報を維持できるようにします。  
  
 [IHostSecurityManager インターフェイス](ihostsecuritymanager-interface.md)  
 現在実行中のスレッドのセキュリティコンテキストに対するアクセスと制御を可能にするメソッドを提供します。  
  
 [IHostSemaphore インターフェイス](ihostsemaphore-interface.md)  
 ホストによって実装されるセマフォの表現を提供します。  
  
 [IHostSyncManager インターフェイス](ihostsyncmanager-interface.md)  
 Win32 同期関数を使用する代わりに、ホストを呼び出すことによって、CLR が同期プリミティブを作成するためのメソッドを提供します。  
  
 [IHostTask インターフェイス](ihosttask-interface.md)  
 CLR がホストと通信してタスクを管理できるようにするメソッドを提供します。  
  
 [IHostTaskManager インターフェイス](ihosttaskmanager-interface.md)  
 標準のオペレーティングシステムのスレッド処理やファイバー関数を使用する代わりに、CLR がホストを通じてタスクを操作できるようにするメソッドを提供します。  
  
 [IHostThreadPoolManager インターフェイス](ihostthreadpoolmanager-interface.md)  
 CLR がスレッドプールを構成し、作業項目をスレッドプールにキューするためのメソッドを提供します。  
  
 [IManagedObject インターフェイス](imanagedobject-interface.md)  
 マネージオブジェクトを制御するためのメソッドを提供します。  
  
 IObjectHandle  
 値渡しのマーシャリングオブジェクトを間接参照からラップ解除するためのメソッドを提供します。  
  
 [ITypeName インターフェイス](itypename-interface.md)  
 型名の情報を取得するためのメソッドを提供します。 (このインターフェイスは .NET Framework インフラストラクチャをサポートします。独自に作成したコードから直接使用するためのものではありません)。  
  
 [ITypeNameBuilder インターフェイス](itypenamebuilder-interface.md)  
 型名を構築するためのメソッドを提供します。 (このインターフェイスは .NET Framework インフラストラクチャをサポートします。独自に作成したコードから直接使用するためのものではありません)。  
  
 [ITypeNameFactory インターフェイス](itypenamefactory-interface.md)  
 型名を分解するためのメソッドを提供します。 (このインターフェイスは .NET Framework インフラストラクチャをサポートします。独自に作成したコードから直接使用するためのものではありません)。  
  
 IValidator  
 ポータブル実行可能 (PE) イメージを検証し、検証エラーを報告するためのメソッドを提供します。  
  
## <a name="related-sections"></a>関連項目  
 [非推奨の CLR のホスト インターフェイスおよびコクラス](deprecated-clr-hosting-interfaces-and-coclasses.md)  
 .NET Framework バージョン1.0 および1.1 で提供されるホストインターフェイスについて説明するトピックが含まれています。  
  
 [.NET Framework 4 および 4.5 で追加された CLR ホスト インターフェイス](clr-hosting-interfaces-added-in-the-net-framework-4-and-4-5.md)  
 .NET Framework 4 で提供されるホスティングインターフェイスについて説明するトピックが含まれています。
