---
title: WCF 分析トレース
ms.date: 03/30/2017
ms.assetid: 6029c7c7-3515-4d36-9d43-13e8f4971790
ms.openlocfilehash: ef636a672d9384e8e3d658f0488cfaadb8d293e4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79183217"
---
# <a name="wcf-analytic-tracing"></a>WCF 分析トレース
このサンプルでは、Windows 通信財団 (WCF) が ETW に書き込む分析トレースのストリームに独自の[!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]トレース イベントを追加する方法を示します。 分析トレースは、パフォーマンスを低下させずに簡単にサービスを確認できるようにするためのものです。 このサンプルでは<xref:System.Diagnostics.Eventing?displayProperty=nameWithType>、API を使用して、WCF サービスと統合するイベントを記述する方法を示します。  
  
 API の<xref:System.Diagnostics.Eventing?displayProperty=nameWithType>詳細については、を参照してください<xref:System.Diagnostics.Eventing?displayProperty=nameWithType>。  
  
 Windows でのイベント トレースの詳細については[、「ETW を使用したデバッグとパフォーマンスのチューニングの向上](https://docs.microsoft.com/archive/msdn-magazine/2007/april/event-tracing-improve-debugging-and-performance-tuning-with-etw)」を参照してください。  
  
## <a name="disposing-eventprovider"></a>EventProvider の破棄  
 このサンプルでは、<xref:System.Diagnostics.Eventing.EventProvider?displayProperty=nameWithType> を実装した <xref:System.IDisposable?displayProperty=nameWithType> クラスを使用します。 WCF サービスのトレースを実装する場合、サービスの有効期間に対して<xref:System.Diagnostics.Eventing.EventProvider>リソースを使用する可能性があります。 そのため、読みやすくするためにも、このサンプルでは、ラップされた <xref:System.Diagnostics.Eventing.EventProvider> を破棄しません。 何かの理由で、サービスに対して別のトレースの要件を設定し、このリソースを破棄しなければならない場合は、アンマネージ リソースの破棄に関するベスト プラクティスに従ってこのサンプルを変更してください。 アンマネージ リソースの破棄の詳細については、「 [Dispose メソッドの実装](https://docs.microsoft.com/dotnet/standard/garbage-collection/implementing-dispose)」を参照してください。  
  
## <a name="self-hosting-vs-web-hosting"></a>自己ホスト型と Web ホスト型  
 Web ホスト サービスの場合、WCF の分析トレースは、トレースを生成するサービスを識別するために使用される "HostReference" と呼ばれるフィールドを提供します。 拡張可能なユーザー トレースをこのモデルに加えることができます。このサンプルで、そのためのベスト プラクティスを示します。 パイプの 「&#124;' 文字が実際に結果の文字列に現れる場合の Web ホスト参照の形式は、次のいずれかになります。  
  
- アプリケーションがルート以外にある場合  
  
     \<サービス名> \<>>&#124;アプリケーション\<仮想パス>&#124;\<サイト名  
  
- アプリケーションがルートにある場合  
  
     \<サービス名>&#124;\<サービス名パス>&#124;\<サービス名>  
  
 自己ホスト型サービスの場合、WCF の分析トレースは"HostReference" フィールドに値を設定しません。 このサンプルの `WCFUserEventProvider` クラスは、自己ホスト型サービスで使用した場合も同じように動作します。  
  
## <a name="custom-event-details"></a>カスタム イベントの詳細  
 WCF の ETW イベント プロバイダー マニフェストは、サービス コード内から WCF サービスの作成者によって生成されるように設計されている 3 つのイベントを定義します。 次の表に、その 3 つのイベントの概要を示します。  
  
|Event|説明|イベント ID|  
|-----------|-----------------|--------------|  
|UserDefinedInformationEventOccurred|このイベントは、問題以外の通知すべき処理がサービスで発生した場合に生成します。 たとえば、データベースの呼び出しに成功した後にイベントを生成します。|301|  
|UserDefinedWarningOccurred|このイベントは、後続の処理でエラーになる可能性がある問題が発生した場合に生成します。 たとえば、データベースの呼び出しが失敗したものの、冗長なデータ ストアを使用して回復できた場合に警告イベントを生成します。|302|  
|UserDefinedErrorOccurred|このイベントは、サービスが想定どおりに動作しなかった場合に生成します。 たとえば、データベースの呼び出しが失敗し、別の場所からもデータを取得できなかった場合にイベントを生成します。|303|  
  
#### <a name="to-use-this-sample"></a>このサンプルを使用するには  
  
1. Visual Studio 2012 を使用して、WCFAnalyticTracingEx 拡張性.sln ソリューション ファイルを開きます。  
  
2. ソリューションをビルドするには、Ctrl キーと Shift キーを押しながら B キーを押します。  
  
3. ソリューションを実行するには、Ctrl キーを押しながら F5 キーを押します。  
  
     Web ブラウザで、[**電卓.svc]** をクリックします。 サービスの WSDL ドキュメントの URI がブラウザーに表示されます。 その URI をコピーします。  
  
4. WCF テスト クライアントを実行します。  
  
     WCF テスト クライアント (WcfTestClient.exe)`\<Visual Studio 2012 Install Dir>\Common7\IDE\WcfTestClient.exe`は に配置されています。 既定の Visual Studio 2012`C:\Program Files\Microsoft Visual Studio 10.0`インストール ディレクトリは です。  
  
5. WCF テスト クライアント内で、[**ファイル**] を選択し、[**サービスの追加]** を選択してサービスを追加します。  
  
     入力ボックスにエンドポイントのアドレスを追加します。  
  
6. [**OK**] をクリックしてダイアログ ボックスを閉じます。  
  
     ICalculator サービスは、左側のペインの **[マイ サービス プロジェクト**] の下に追加されます。  
  
7. イベント ビューアー アプリケーションを開きます。  
  
     サービスを呼び出す前に、イベント ビューアーを起動し、イベント ログが WCF サービスから生成された追跡イベントをリッスンしていることを確認します。  
  
8. [**スタート**] メニューの [**管理ツール**] をクリックし、[**イベント ビューア**] をクリックします。 **分析**ログと**デバッグ**ログを有効にします。  
  
9. イベント ビューアのツリー ビューで、**イベント ビューア**、**アプリケーションとサービス ログ** **、Microsoft** **、Windows、** および**アプリケーション サーバー アプリケーション**に移動します。 [アプリケーション**サーバー アプリケーション**] を右クリックし、[**表示**] をクリックして、[**分析ログとデバッグ ログの表示**] を選択します。  
  
     [**分析ログとデバッグ ログの表示]** オプションがオンになっていることを確認します。 分析ログを有効**に**します。  
  
     イベント ビューアのツリー ビューで、**イベント ビューア**、**アプリケーションとサービス ログ** **、Microsoft** **、Windows**、**アプリケーション サーバー アプリケーション**、および**分析**に移動します。 **[分析**] を右クリックし、[**ログの有効化**] を選択します。  
  
10. WCF テスト クライアントを使用してサービスをテストします。  
  
    1. WCF テスト クライアントで、ICalculator サービス ノードの下で**Add()** をダブルクリックします。  
  
         **Add()** メソッドは、2 つのパラメータを持つ右側のペインに表示されます。  
  
    2. 最初のパラメーターに「2」と入力し、2 番目のパラメーターに「3」と入力します。  
  
    3. [**呼び出し**] をクリックしてメソッドを呼び出します。  
  
11. 既に開いている**イベント ビューア**ウィンドウに移動します。 イベント**ビューア**、**アプリケーションとサービス ログ**、 **Microsoft**、 **Windows**、 アプリケーション サーバー**アプリケーション に**移動します。  
  
12. **[分析**] ノードを右クリックし、[**最新の情報に更新**] を選択します。  
  
     右ペインにイベントが表示されます。  
  
13. ID が 303 のイベントを探してダブルクリックして開き、内容を確認します。  
  
     このイベントは、ICalculator`Add()`サービスのメソッドによって生成され、ペイロードが "2+3=5" に等しい。  
  
#### <a name="to-clean-up-optional"></a>クリーンアップするには (省略可能)  
  
1. **イベント ビューアー**を開きます。  
  
2. イベント**ビューア**、**アプリケーションとサービス ログ** **、Microsoft** **、Windows**、および**アプリケーション サーバー アプリケーション**に移動します。 **[分析**] を右クリックし、[**ログの無効化**] を選択します。  
  
3. イベント**ビューア**、**アプリケーションとサービス ログ**、 **Microsoft**、 **Windows**、 アプリケーション**サーバー アプリケーション**、および**分析**に移動します。 **[分析**] を右クリックし、[**ログのクリア**] を選択します。  
  
4. イベントを**クリアするには、[クリア**] をクリックします。  
  
## <a name="known-issue"></a>既知の問題  
 **イベント ビューア**に既知の問題があり、ETW イベントのデコードに失敗する可能性があります。 "ソースの Microsoft-Windows アプリケーション サーバー アプリケーションから>\<イベント ID の説明が見つかりません。 このイベントを発生させるコンポーネントがローカル コンピューターにインストールされていないか、インストールが壊れています。 コンポーネントは、ローカル コンピュータにインストールまたは修復できます。 このエラーが発生した場合は、[**アクション]** メニューの **[最新の情報に更新**] を選択します。 これにより、イベントが正常にデコードされます。  
  
> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\ETWTrace`  
  
## <a name="see-also"></a>関連項目

- [AppFabric の監視のサンプル](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))
