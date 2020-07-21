---
title: サービス トレース ビューアーを使用した相関トレースの表示とトラブルシューティング
ms.date: 03/30/2017
ms.assetid: 05d2321c-8acb-49d7-a6cd-8ef2220c6775
ms.openlocfilehash: e1cd1443e96e7195127cb95e7ef1b2c4d6d9c176
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84587756"
---
# <a name="using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting"></a>サービス トレース ビューアーを使用した相関トレースの表示とトラブルシューティング

ここでは、トレース データの形式、表示方法、およびサービス トレース ビューアーを使用したアプリケーションのトラブルシューティングの方法について説明します。

## <a name="using-the-service-trace-viewer-tool"></a>サービス トレース ビューアー ツールの使用

Windows Communication Foundation (WCF) サービストレースビューアーツールを使用すると、WCF リスナーによって生成される診断トレースを関連付けて、エラーの根本原因を特定できます。 このツールを使用すると、トレースの表示、グループ化、およびフィルター処理を簡単に行うことができるため、WCF サービスの問題を診断、修復、および検証することができます。 このツールの使用方法の詳細については、「[サービストレースビューアーツール (svctraceviewer.exe)](../../service-trace-viewer-tool-svctraceviewer-exe.md)」を参照してください。

このトピックには、[サービストレースビューアーツール (svctraceviewer.exe)](../../service-trace-viewer-tool-svctraceviewer-exe.md)を使用して表示したときに[トレースとメッセージログ](../../samples/tracing-and-message-logging.md)のサンプルを実行して生成されるトレースのスクリーンショットが含まれています。 ここでは、トレースの内容、アクティビティ、およびアクティビティの相関関係を理解する方法と、トラブルシューティングを行うときに多数のトレースを分析する方法について説明します。

## <a name="viewing-trace-content"></a>トレースの内容の表示

トレース イベントには、次のような最も重要な情報が含まれています。

- 設定時のアクティビティ名。

- 出力時間。

- トレース レベル。

- トレースのソース名です。

- プロセス名。

- スレッド ID。

- 一意のトレース識別子。トレースに関連する詳細情報を取得できる、Microsoft Docs 内の宛先を指す URL です。

 これらはすべて、サービストレースビューアーの右上のパネル、またはトレースを選択したときに、右下のパネルの [書式付き] ビューの [**基本情報**] セクションに表示されます。

> [!NOTE]
> クライアントとサービスが同じコンピューター上にある場合、両方のアプリケーションのトレースが存在します。 これらは、[**プロセス名**列を使用してフィルター処理できます。

また、[書式付き] ビューには、トレースの説明と追加詳細情報も表示されます (利用できる場合)。 追加詳細情報には、例外の種類とメッセージ、呼び出しスタック、メッセージ アクション、転送元/転送先フィールド、およびその他の例外情報が含まれる場合があります。

[XML] ビューには、以下の有用な XML タグが含まれます。

- `<SubType>`(トレースレベル)。

- `<TimeCreated>`.

- `<Source>`(トレースソース名)。

- `<Correlation>`(トレースの出力時に設定されるアクティビティ id)。

- `<Execution>`(プロセスとスレッド id)。

- `<Computer>`.

- `<ExtendedData>`(を含む)、 `<Action>` `<MessageID>` およびメッセージ `<ActivityId>` を送信するときのメッセージヘッダーのセット。

"チャネル経由でメッセージを送信しました" トレースを調べると、次のような内容を確認できます。

```xml
<E2ETraceEvent xmlns="http://schemas.microsoft.com/2004/06/E2ETraceEvent">
   <System xmlns="http://schemas.microsoft.com/2004/06/windows/eventlog/system">
      <EventID>262163</EventID>
      <Type>3</Type>
      <SubType Name="Information">0</SubType>
      <Level>8</Level>
      <TimeCreated SystemTime="2006-08-04T18:45:30.8491051Z" />
      <Source Name="System.ServiceModel" />
       <Correlation ActivityID="{27c6331d-8998-43aa-a382-03239013a6bd}"/>
       <Execution ProcessName="client" ProcessID="1808" ThreadID="1" />
       <Channel />
       <Computer>TEST1</Computer>
   </System>
   <ApplicationData>
       <TraceData>
          <DataItem>
             <TraceRecord xmlns="http://schemas.microsoft.com/2004/10/E2ETraceEvent/TraceRecord" Severity="Information">
                 <TraceIdentifier>http://msdn.microsoft.com/library/System.ServiceModel.Channels.MessageSent.aspx</TraceIdentifier>
                 <Description>Sent a message over a channel.</Description>
                 <AppDomain>client.exe</AppDomain>
                 <Source>System.ServiceModel.Channels.ClientFramingDuplexSessionChannel/35191196</Source>
                <ExtendedData xmlns="http://schemas.microsoft.com/2006/08/ServiceModel/MessageTransmitTraceRecord">

                  <MessageProperties>
                     <AllowOutputBatching>False</AllowOutputBatching>
                  </MessageProperties>
                  <MessageHeaders>
                     <Action d4p1:mustUnderstand="1" xmlns:d4p1="http://www.w3.org/2003/05/soap-envelope" xmlns="http://www.w3.org/2005/08/addressing">http://Microsoft.ServiceModel.Samples/ICalculator/Multiply</Action>
                     <MessageID xmlns="http://www.w3.org/2005/08/addressing">urn:uuid:7c6670d8-4c9c-496e-b6a0-2ceb6db35338</MessageID>
                     <ActivityId CorrelationId="b02e2189-0816-4387-980c-dd8e306440f5" xmlns="http://schemas.microsoft.com/2004/09/ServiceModel/Diagnostics">27c6331d-8998-43aa-a382-03239013a6bd</ActivityId>
                     <ReplyTo xmlns="http://www.w3.org/2005/08/addressing">
                        <Address>http://www.w3.org/2005/08/addressing/anonymous</Address>
                    </ReplyTo>
                    <To d4p1:mustUnderstand="1" xmlns:d4p1="http://www.w3.org/2003/05/soap-envelope" xmlns="http://www.w3.org/2005/08/addressing">net.tcp://localhost/servicemodelsamples/service</To>
                  </MessageHeaders>
                  <RemoteAddress>net.tcp://localhost/servicemodelsamples/service</RemoteAddress>
                </ExtendedData>
            </TraceRecord>
          </DataItem>
       </TraceData>
   </ApplicationData>
</E2ETraceEvent>
```

## <a name="servicemodel-e2e-tracing"></a>ServiceModel のエンドツーエンドのトレース

`System.ServiceModel`トレースソースが Off 以外ので設定されている場合、 `switchValue` `ActivityTracing` wcf は wcf 処理のためにアクティビティと転送を作成します。

アクティビティとは、その処理単位に関連するすべてのトレースをグループ化する処理の論理単位です。 たとえば、要求ごとに 1 つのアクティビティを定義できます。 転送により、エンドポイント内のアクティビティ間の因果関係が作成されます。 アクティビティ ID を伝達することにより、エンドポイント間でアクティビティを関連付けることができます。 これを行うには、 `propagateActivity` = `true` すべてのエンドポイントの [構成] でを設定します。 アクティビティ、転送、および伝達により、エラーの関連付けを行うことができます。 このようにして、エラーの根本原因をよりすばやく見つけることができるようになります。

クライアントでは、オブジェクトモデルの呼び出しごとに1つの WCF アクティビティが作成されます (たとえば、オープン ChannelFactory、加算、除算など)。各操作呼び出しは、"処理アクション" アクティビティで処理されます。

[トレースとメッセージログ](../../samples/tracing-and-message-logging.md)のサンプルから抽出された次のスクリーンショットでは、左側のパネルに、クライアントプロセスで作成されたアクティビティの一覧が作成時刻順に並べ替えられて表示されます。 以下に、各アクティビティを時系列で示します。

- チャネル ファクトリ (ClientBase) を作成しました。

- チャネル ファクトリを開きました。

- Add アクションを処理しました。

- セキュリティで保護されたセッションを設定し (これは最初の要求で発生します)、RST、RSTR、SCT (プロセス メッセージ 1、2、3) の 3 つのセキュリティ インフラストラクチャ応答メッセージを処理しました。

- Subtract、Multiply、および Divide の各要求を処理しました。

- チャネル ファクトリを閉じ、これにより、セキュリティで保護されたセッションを閉じました。また、セキュリティ メッセージ応答の Cancel を処理しました。

 セキュリティ インフラストラクチャ メッセージがあるのは、wsHttpBinding を使用しているためです。

> [!NOTE]
> WCF では、最初に個別のアクティビティ (プロセスメッセージ) で処理される応答メッセージを示しています。これは、転送を通じて、要求メッセージを含む対応するプロセスアクションアクティビティに関連付けられる前に行われます。 これは、インフラストラクチャ メッセージと非同期要求に対して行います。非同期要求の場合、インフラストラクチャ メッセージを調べて activityId ヘッダーを確認し、該当の ID を持つ既存の "プロセス アクション" アクティビティを特定してこれに関連付ける必要があるためです。 同期要求の場合は、応答のためにブロックするため、応答を関連付けるプロセス アクションがわかります。

次の図は、作成時刻 (左側のパネル) および入れ子になったアクティビティとトレース (右上のパネル) によって一覧表示される WCF クライアントアクティビティを示しています。

![作成時刻に一覧表示された WCF クライアントアクティビティを示すスクリーンショット。](./media/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting/wcf-client-activities-creation-time.gif)

左のパネルでアクティビティを選択すると、右上のパネルに入れ子にされたアクティビティとトレースが表示されます。 したがって、これは、選択した親アクティビティに基づいて、左側のアクティビティのリストの階層表示を減らしたものです。 選択した "プロセス アクション Add" は最初に作成された要求であるため、このアクティビティには、"セキュリティで保護されたセッションの設定" アクティビティ (転送先と返送元) と、Add アクションの実際の処理のトレースが含まれます。

左側のパネルで [プロセスの追加] アクティビティをダブルクリックすると、追加に関連するクライアント WCF アクティビティがグラフィカルに表示されます。 左の最初のアクティビティがルート アクティビティ (0000) であり、既定のアクティビティです。 WCF は、アンビエントアクティビティから転送されます。 これが定義されていない場合、WCF は0000から転送されます。 ここでは、2 番目のアクティビティである "プロセス アクション Add" が 0 から転送します。 次に、"セキュリティで保護されたセッションの設定" が示されています。

次の図は、WCF クライアントアクティビティのグラフビューを示しています。具体的には、アンビエントアクティビティ (ここでは 0)、プロセスアクション、およびセキュリティで保護されたセッションの設定です。

![アンビエントアクティビティとプロセスアクションを示すトレースビューアーのグラフ。](./media/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting/wcf-activities-graph-ambient-process.gif)

右上のパネルでは、"プロセス アクション Add" アクティビティに関連するすべてのトレースを確認できます。 具体的には、同じアクティビティで、要求メッセージ ("チャネル経由でメッセージを送信しました") を送信し、応答 ("チャネル経由でメッセージを受信しました") を受け取っています。 これを次のグラフに示します。 わかりやすくするために、このグラフでは、"セキュリティで保護されたセッションの設定" アクティビティを折りたたんでいます。

次の図は、"プロセスアクション" アクティビティのトレースの一覧を示しています。 同じアクティビティで要求を送信し、応答を受信します。

![プロセスアクションアクティビティのトレースの一覧を示すトレースビューアーのスクリーンショット](./media/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting/process-action-traces.gif)

ここでは、わかりやすくするためだけにクライアントトレースを読み込みますが、サービストレース (送信された要求メッセージと応答メッセージ) は、ツールにも読み込まれている場合は同じアクティビティに表示され、 `propagateActivity` 後の図に示すように設定されてい `true.` ます。

サービスでは、アクティビティモデルは次のように WCF の概念にマップされます。

1. ServiceHost を作成して開きます (たとえば、セキュリティの場合、複数のホスト関連アクティビティを作成できます)。

2. ServiceHost のリスナーごとに "リッスン" アクティビティを作成します (Open ServiceHost との間の転送を使用)。

3. リスナーは、クライアントによって開始された通信要求を検出すると、"受信バイト" アクティビティに転送します。このアクティビティでは、クライアントから送信されたすべてのバイトが処理されます。 このアクティビティでは、クライアントとサーバーの対話中に発生したすべての接続エラーを確認できます。

4. メッセージに対応する受信バイトセットごとに、"メッセージの処理" アクティビティでこれらのバイトを処理します。ここでは、WCF Message オブジェクトを作成します。 このアクティビティでは、不正なエンベロープや誤った形式のメッセージに関連するエラーを確認できます。

5. メッセージが作成されたら、"プロセス アクション" アクティビティに転送します。 クライアントとサービスの両方で、`propagateActivity` が `true` に設定されている場合、既に説明したように、このアクティビティはクライアントに定義されている ID と同じ ID を持ちます。 この段階から、エンドポイント間の直接の相関関係を活用できます。これは、要求に関連付けられている WCF で生成されたすべてのトレースが、応答メッセージの処理を含め、同じアクティビティ内にあるためです。

6. プロセス外のアクションでは、"ユーザーコードの実行" アクティビティを作成して、ユーザーコードで生成されたトレースを WCF で出力されたものから分離します。 前の例では、"サービスが追加の応答を送信します" というトレースは、クライアントによって伝達されたアクティビティではなく、"ユーザーコードの実行" アクティビティで出力されます (該当する場合)。

次の図では、左の最初のアクティビティがルート アクティビティ (0000) であり、既定のアクティビティです。 次の 3 つのアクティビティは、ServiceHost を開くためのアクティビティです。 5 列目のアクティビティはリスナーです。残りのアクティビティ (6 ～ 8 列目) は、バイト処理からユーザー コードのアクティブ化までの、WCF でのメッセージ処理を示しています。

次の図は、WCF サービスアクティビティのグラフビューを示しています。

![WCF サービスアクティビティの一覧を示すトレースビューアーのスクリーンショット](./media/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting/wcf-service-activities.gif)

次のスクリーンショットは、クライアントとサービスの両方のアクティビティを示しています。プロセス全体にわたり、"プロセス アクション Add" アクティビティはオレンジで強調表示されています。 矢印は、クライアントとサービスによって送受信された要求メッセージと応答メッセージを関連付けています。 このグラフでは、"プロセス アクション" のトレースはプロセス間で分かれていますが、右上のパネルには同じアクティビティの一部として示されています。 このパネルには、送信されたメッセージのクライアント トレースの後に、受信および処理されたメッセージのサービス トレースが表示されています。

次の図は、WCF クライアントとサービスの両方のアクティビティのグラフビューを示しています。

![WCF クライアントとサービスの両方のアクティビティを表示するトレースビューアーのグラフ。](./media/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting/wcf-client-service-activities.gif)

次のエラー シナリオでは、サービスとクライアントのエラー トレースおよび警告トレースが関連付けられます。 サービスのユーザー コードで最初に例外がスローされています ("サービスはユーザー コードでこの要求を処理できません" という例外の警告トレースを含む右端の緑のアクティビティ)。 クライアントに応答が送信されると、警告トレースが再度出力されて、エラー メッセージが表示されます (左のピンクのアクティビティ)。 その後、クライアントは WCF クライアントを閉じます (左下の黄色のアクティビティ)。これにより、サービスへの接続が中止されます。 サービスはエラーをスローします (右側の最も長いピンクのアクティビティ)。

![トレース ビューアーの使用](media/wcfc-e2etrace9s.gif "wcfc_e2etrace9s")

サービスとクライアント間のエラーの相関関係

これらのトレースの生成に使用したサンプルは、wsHttpBinding を使用する一連の同期要求です。 セキュリティを使用しないシナリオ、または非同期要求を使用するシナリオの場合は、このグラフとは違う部分があります。非同期要求の場合、"プロセス アクション" アクティビティは、非同期呼び出しを構成する開始操作と終了操作の間に配置され、コールバック アクティビティへの転送が示されます。 その他のシナリオの詳細については、「[エンドツーエンドのトレースのシナリオ](end-to-end-tracing-scenarios.md)」を参照してください。

## <a name="troubleshooting-using-the-service-trace-viewer"></a>サービス トレース ビューアーを使用したトラブルシューティング

サービス トレース ビューアー ツールにトレース ファイルを読み込むと、左のパネルの赤または黄色のアクティビティを選択することによって、アプリケーションの問題の原因を突き止めることができます。 通常、000 アクティビティには、ユーザーにバブリングする未処理の例外が含まれます。

次の図は、赤または黄のアクティビティを選択して問題の根本原因を特定する方法を示しています。
![問題の根本原因を特定するための赤または黄のアクティビティのスクリーンショット。](./media/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting/service-trace-viewer.gif)

右上のパネルでは、左側で選択したアクティビティのトレースを調べることができます。 このパネルで赤または黄色のトレースを調べ、それらがどのように関連しているかを確認できます。 前のグラフで、同じ "プロセス アクション" アクティビティのクライアントとサービスの警告トレースを確認します。

これらのトレースからエラーの根本原因がわからない場合は、左のパネルで選択したアクティビティ (ここでは "プロセス アクション") をダブルクリックすることでグラフを利用できます。 関連アクティビティが含まれたグラフが表示されます。 ("+" 記号をクリックして) 関連アクティビティを展開し、関連するアクティビティで最初に出力されたトレースを赤または黄で見つけることができます。 調べる対象の赤または黄色のトレースの直前に発生したアクティビティを展開し、エンドポイント間の関連アクティビティまたはメッセージ フローをたどって問題の根本原因を突き止めます。

![トレース ビューアーの使用](media/wcfc-e2etrace9s.gif "wcfc_e2etrace9s")

アクティビティを展開して問題の根本原因を追跡します。

ServiceModel の `ActivityTracing` が無効になっていても、ServiceModel トレースが有効であれば、0000 アクティビティで出力された ServiceModel のトレースを確認できます。 ただし、この場合、これらのトレースの相関関係を理解するには多くの労力を必要とします。

メッセージ ログを有効にすると、[メッセージ] タブを使用してエラーの影響を受けるメッセージを確認できます。 赤または黄色のメッセージをダブルクリックすると、関連アクティビティのグラフ ビューを表示できます。 これらのアクティビティは、エラーが発生した要求に最も密接に関連するアクティビティです。

![メッセージログが有効になっているトレースビューアーのスクリーンショット。](./media/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting/message-logging-enabled.gif)

トラブルシューティングを開始するには、赤または黄色のメッセージトレースを選択し、それをダブルクリックして根本原因を追跡することもできます。

## <a name="see-also"></a>関連項目

- [エンドツーエンドのトレースのシナリオ](end-to-end-tracing-scenarios.md)
- [サービス トレース ビューアー ツール (SvcTraceViewer.exe)](../../service-trace-viewer-tool-svctraceviewer-exe.md)
- [トレース](index.md)
