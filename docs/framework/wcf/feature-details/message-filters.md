---
title: メッセージ フィルター
ms.date: 03/30/2017
helpviewer_keywords:
- routing [WCF], message filters
ms.assetid: cb33ba49-8b1f-4099-8acb-240404a46d9a
ms.openlocfilehash: a953dea9224d75907c593d87f06a0b0888f0af2d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79184662"
---
# <a name="message-filters"></a>メッセージ フィルター
コンテンツ ベースのルーティングを実装する場合、ルーティング サービスは、アドレス、エンドポイント名、特定の XPath ステートメントなど、メッセージの特定のセクションを確認する <xref:System.ServiceModel.Dispatcher.MessageFilter> 実装を使用します。 [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] に付属のメッセージ フィルターの中にニーズを満たすものがない場合は、<xref:System.ServiceModel.Dispatcher.MessageFilter> 基本クラスの新しい実装を作成することで、カスタム フィルターを作成できます。  
  
 ルーティング サービスを構成する場合は **、MessageFilter**の<xref:System.ServiceModel.Routing.Configuration.FilterElement>種類と、メッセージ内で検索する特定の文字列値など、フィルタの作成に必要なサポート データを記述するフィルタ要素 (オブジェクト) を定義する必要があります。 フィルター要素を作成しても、個々のメッセージ フィルターが定義されるだけです。フィルターを使用してメッセージを評価およびルーティングするには、フィルター テーブル (<xref:System.ServiceModel.Routing.Configuration.FilterTableEntryCollection>) を定義する必要もあります。  
  
 フィルター テーブル内の各エントリは、特定のフィルター要素を参照し、メッセージがフィルターに一致した場合にメッセージのルーティング先となるクライアント エンドポイントを指定します。 フィルター テーブルのエントリでは、バックアップ エンドポイントのコレクション (<xref:System.ServiceModel.Routing.Configuration.BackupEndpointCollection>) を指定することもできます。このコレクションは、プライマリ エンドポイントへの送信時に転送エラーが発生した場合に、メッセージの転送先となるエンドポイントのリストを定義します。 それらのエンドポイントのいずれかで転送が成功するまで、指定された順番でバックアップ エンドポイントへの転送が試行されます。  
  
## <a name="message-filters"></a>メッセージ フィルター  
 ルーティング サービスが使用するメッセージ フィルターは、メッセージの送信先の名前、SOAP アクション、メッセージの送信先のアドレスまたはアドレス プレフィックスの評価など、一般的なメッセージ選択機能を提供します。 フィルターに `AND` 条件を付けて、メッセージが両方のフィルターに一致した場合は、特定のエンドポイントにのみルーティングされるように指定することもできます。 また、<xref:System.ServiceModel.Dispatcher.MessageFilter> の独自の実装を作成することで、カスタム フィルターを作成することもできます。  
  
 次の表に、ルーティング サービスが使用する <xref:System.ServiceModel.Routing.Configuration.FilterType>、そのメッセージ フィルターを実装するクラス、および必須の <xref:System.ServiceModel.Routing.Configuration.FilterElement.FilterData%2A> パラメーターを示します。  
  
|フィルターの型|説明|フィルター データの意味|フィルターの例|  
|------------------|-----------------|-------------------------|--------------------|  
|アクション|<xref:System.ServiceModel.Dispatcher.ActionMessageFilter> クラスを使用して、特定のアクションを含むメッセージを照合します。|フィルター処理するアクション。|\<フィルター名="アクション1" フィルタータイプ="アクション" フィルターデータhttp://namespace/contract/operation=" "/>|  
|EndpointAddress|特定の<xref:System.ServiceModel.Dispatcher.EndpointAddressMessageFilter>アドレスを含<xref:System.ServiceModel.Dispatcher.EndpointAddressMessageFilter.IncludeHostNameInComparison%2A> == `true`むメッセージを照合するために、クラスを使用します。|フィルター処理するアドレス (To ヘッダー)。|\<フィルター名="アドレス1"フィルタータイプ="エンドポイントアドレス"フィルターデータ=""/>http://host/vdir/s.svc/b|  
|EndpointAddressPrefix|特定の<xref:System.ServiceModel.Dispatcher.PrefixEndpointAddressMessageFilter>アドレス プレフィックス<xref:System.ServiceModel.Dispatcher.PrefixEndpointAddressMessageFilter.IncludeHostNameInComparison%2A> == `true`を含むメッセージを照合するために、クラスを使用します。|最長プレフィックス一致を使用してフィルター処理するアドレス。|\<フィルター名="プレフィックス1" フィルタータイプ="エンドポイントアドレスプレフィックス" フィルターデータhttp://host/=" "/>|  
|And|常に両方の条件を評価してから結果を返す <xref:System.ServiceModel.Dispatcher.StrictAndMessageFilter> クラスを使用します。|フィルターデータは使用されません。代わりに、filter1 と filter2 には対応するメッセージ フィルターの名前 (テーブル内) があり **、AND**を結合する必要があります。|\<フィルター名="と1" フィルタータイプ="と"フィルター1="アドレス1"フィルタ2="アクション1"/>|  
|Custom|<xref:System.ServiceModel.Dispatcher.MessageFilter> クラスを拡張し、文字列を受け取るコンストラクターを持つユーザー定義の型。|customType 属性は、作成するクラスの完全修飾型名で、filterData は、フィルターの作成時にコンストラクターに渡す文字列です。|\<フィルター名="カスタム1" フィルタータイプ="カスタム" カスタムタイプ="カスタムアセンブリ.カスタムMsgFilter, カスタムアセンブリ" フィルターデータ="カスタムデータ" />|  
|EndpointName|<xref:System.ServiceModel.Dispatcher.EndpointNameMessageFilter> クラスを使用して、メッセージを受信したサービス エンドポイントの名前を基にメッセージを照合します。|サービス エンドポイントの名前 ("serviceEndpoint1" など)。  このサービス エンドポイントは、ルーティング サービスで公開されるいずれかのエンドポイントでなければなりません。|\<フィルター名="stock1" フィルタータイプ="エンドポイント" フィルターデータ="Svc エンドポイント" />|  
|MatchAll|<xref:System.ServiceModel.Dispatcher.MatchAllMessageFilter> クラスを使用します。 このフィルターは、すべての着信メッセージを照合します。|filterData は使用されません。 このフィルターは、常にすべてのメッセージを照合します。|\<フィルター名="マッチAll1" フィルタータイプ="マッチオール" />|  
|XPath|<xref:System.ServiceModel.Dispatcher.XPathMessageFilter> クラスを使用して、メッセージ内の特定の XPath クエリを照合します。|メッセージの照合時に使用する XPath クエリ。|\<フィルター名="XPath1" フィルタータイプ="XPath" フィルターデータ="//ns:要素" />|  
  
 次の例では、XPath、EndpointName、および PrefixEndpointAddress メッセージ フィルターを使用するフィルター エントリを定義しています。 また、この例では、RoundRobinFilter1 エントリと RoundRobinFilter2 エントリに対するカスタム フィルターの使用方法も示しています。  
  
```xml  
<filters>  
     <filter name="XPathFilter" filterType="XPath"
             filterData="/s12:Envelope/s12:Header/custom:RoundingCalculator = 1"/>  
     <filter name="EndpointNameFilter" filterType="EndpointName"
             filterData="calculatorEndpoint"/>  
     <filter name="PrefixAddressFilter" filterType="PrefixEndpointAddress"
             filterData="http://localhost/routingservice/router/rounding/"/>  
     <filter name="RoundRobinFilter1" filterType="Custom"
             customType="RoutingServiceFilters.RoundRobinMessageFilter,
             RoutingService" filterData="group1"/>  
     <filter name="RoundRobinFilter2" filterType="Custom"
             customType="RoutingServiceFilters.RoundRobinMessageFilter,
             RoutingService" filterData="group1"/>  
</filters>  
```  
  
> [!NOTE]
> 単にフィルターを定義しただけでは、そのフィルターに対してメッセージが評価されるとは限りません。 フィルターをフィルター テーブルに追加する必要があります。テーブルに追加することで、ルーティング サービスが公開するサービス エンドポイントに関連付けられます。  
  
### <a name="namespace-table"></a>名前空間テーブル  
 XPath フィルターを使用すると、XPath クエリを含むフィルター データは、名前空間を使用するため、非常に大きくなることがあります。 この問題を軽減するために、ルーティング サービスでは、名前空間テーブルを使用して、独自の名前空間プレフィックスを定義できるようにしています。  
  
 名前空間テーブルは、XPath で使用できる一般的な名前空間の名前空間プレフィックスを定義する <xref:System.ServiceModel.Routing.Configuration.NamespaceElement> オブジェクトのコレクションです。 以下は、名前空間テーブルに格納されている既定の名前空間およびプレフィックスです。  
  
|Prefix|名前空間|  
|------------|---------------|  
|s11|`http://schemas.xmlsoap.org/soap/envelope`|  
|s12|`http://www.w3.org/2003/05/soap-envelope`|  
|wsaAugust2004|`http://schemas.xmlsoap.org/ws/2004/08/addressing`|  
|wsa10|`http://www.w3.org/2005/08/addressing`|  
|sm|`http://schemas.microsoft.com/serviceModel/2004/05/xpathfunctions`|  
|tempuri|`http://tempuri.org`|  
|ser|`http://schemas.microsoft.com/2003/10/Serialization`|  
  
 XPath クエリに特定の名前空間を使用することがわかっている場合は、その名前空間を一意の名前空間プレフィックスと併せて名前空間テーブルに追加し、完全名前空間ではなく、プレフィックスを XPath クエリで使用できます。 次の例では、名前空間`"http://my.custom.namespace"`に "custom" というプレフィックスを定義し、filterData に含まれる XPath クエリで使用します。  
  
```xml  
<namespaceTable>  
     <add prefix="custom" namespace="http://my.custom.namespace/"/>  
</namespaceTable>  
<filters>  
     <filter name="XPathFilter" filterType="XPath" filterData="/s12:Envelope/s12:Header/custom:RoundingCalculator = 1"/>  
</filters>  
```  
  
## <a name="filter-tables"></a>フィルター テーブル  
 各フィルター要素では、メッセージに適用できる論理比較が定義されますが、フィルター テーブルでは、フィルター要素と送信先クライアント エンドポイントが関連付けられます。 フィルター テーブルは、フィルター、プライマリの送信先エンドポイント、および代替のバックアップ エンドポイントのリスト間の関連付けを定義する <xref:System.ServiceModel.Routing.Configuration.FilterTableEntryElement> オブジェクトの名前付きコレクションです。 フィルター テーブル エントリでは、必要に応じて、各フィルター条件に優先度を指定することもできます。 次の例では、まず、2 つのフィルターを定義し、各フィルターを送信先エンドポイントに関連付けるフィルター テーブルを定義しています。  
  
```xml  
<routing>  
     <filters>  
       <filter name="AddAction" filterType="Action" filterData="Add" />  
       <filter name="SubtractAction" filterType="Action" filterData="Subtract" />  
     </filters>  
     <filterTables>  
       <table name="routingTable1">  
         <filters>  
           <add filterName="AddAction" endpointName="Addition" />  
           <add filterName="SubtractAction" endpointName="Subtraction" />  
         </filters>  
       </table>  
     </filterTables>
</routing>  
```  
  
### <a name="filter-evaluation-priority"></a>フィルター評価の優先度  
 既定では、フィルター テーブルのすべてのエントリが同時に評価され、評価対象のメッセージは、一致するフィルター エントリに関連付けられているエンドポイントにルーティングされます。 複数のフィルターが `true` に評価され、メッセージが一方向または双方向である場合は、メッセージが、一致するすべてのフィルターのエンドポイントにマルチキャストされます。 要求/応答メッセージは、クライアントに返すことができる応答が 1 つのみであるため、マルチキャストできません。  
  
 各フィルターに優先度レベルを指定することで、より複雑なルーティング ロジックを実装できます。ルーティング サービスは、優先度レベルが最も高いフィルターをすべて最初に評価します。 メッセージがこのレベルのフィルターに一致した場合、優先度がこれよりも低いフィルターは処理されません。 たとえば、一方向の受信メッセージは、最初に、優先度が 2 であるすべてのフィルターに対して評価されるとします。 この優先度レベルのどのフィルターにもメッセージが一致しなかった場合は、次に、優先度が 1 のフィルターと比較されます。 優先度 1 のフィルターのうち、2 つがメッセージに一致した場合、メッセージは、一方向のメッセージであるため、両方の送信先エンドポイントにルーティングされます。  優先度 1 のフィルターの中に一致するものが見つかったため、優先度が 0 のフィルターは評価されません。  
  
> [!NOTE]
> 優先度が指定されていない場合は、既定の優先度の 0 が使用されます。  
  
 次の例では、フィルター テーブルを定義しています。このテーブルでは、テーブルで参照しているフィルターに優先度 2、1、および 0 を指定しています。  
  
```xml  
<filterTables>  
     <filterTable name="filterTable1">  
          <add filterName="XPathFilter" endpointName="roundingCalcEndpoint"
               priority="2"/>  
          <add filterName="EndpointNameFilter" endpointName="regularCalcEndpoint"
               priority="1"/>  
          <add filterName="PrefixAddressFilter" endpointName="roundingCalcEndpoint"
               priority="1"/>  
          <add filterName="MatchAllMessageFilter" endpointName="defaultCalcEndpoint"
               priority="0"/>  
     </filterTable>  
</filterTables>  
```  
  
 上記の例では、メッセージが XPathFilter に一致すると、roundingCalcEndpoint にルーティングされます。また、その他のフィルターはすべて、これよりも優先度が低いため、テーブル内の他のフィルターは評価されません。 ただし、メッセージが XPathFilter に一致しなかった場合は、次に優先度が低いすべてのフィルター、つまり、EndpointNameFilter と PrefixAddressFilter に対してメッセージが評価されます。  
  
> [!NOTE]
> 可能な場合は、優先度の評価によってパフォーマンスが低下する可能性があるため、優先度を指定する代わりに、排他的なフィルターを使用してください。  
  
### <a name="backup-lists"></a>バックアップ リスト  
 フィルター テーブルの各フィルターには、必要に応じて、バックアップ リストを指定できます。バックアップ リストは、エンドポイントの名前付きコレクション (<xref:System.ServiceModel.Routing.Configuration.BackupEndpointCollection>) です。 このコレクションには、<xref:System.ServiceModel.CommunicationException> に指定されているプライマリ エンドポイントへの送信時に <xref:System.ServiceModel.Routing.Configuration.FilterTableEntryElement.EndpointName%2A> が発生した場合に、メッセージの転送先となるエンドポイントの順序指定されたリストが保持されます。 次の例では、2 つのエンドポイントを含む "backupServiceEndpoints" という名前のバックアップ リストを定義します。  
  
```xml  
<filterTables>  
     <filterTable name="filterTable1">  
          <add filterName="MatchAllFilter1" endpointName="Destination" backupList="backupEndpointList"/>  
     </filterTable>  
</filterTables>  
<backupLists>  
     <backupList name="backupEndpointList">  
          <add endpointName="backupServiceQueue" />  
          <add endpointName="alternateServiceQueue" />  
     </backupList>  
</backupLists>  
```  
  
 前の例では、プライマリ エンドポイント "宛先" への送信が失敗した場合、ルーティング サービスは、リストされている順序で各エンドポイントに送信を試み、最初に backupServiceQueue に送信し、次に代替サービス キューに送信します。バックアップに送信サービスキューが失敗します。 すべてのバックアップ エンドポイントへの送信が失敗した場合は、エラーが返されます。
