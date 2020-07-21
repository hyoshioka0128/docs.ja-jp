---
title: カスタム フィルター
ms.date: 03/30/2017
ms.assetid: 97cf247d-be0a-4057-bba9-3be5c45029d5
ms.openlocfilehash: ae020173544372c3ce097c8ac57e53f3fde37514
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79185211"
---
# <a name="custom-filters"></a>カスタム フィルター
カスタム フィルターを使用すると、システムが提供するメッセージ フィルターを使用して実現できない一致ロジックを定義できます。 たとえば、特定のメッセージ要素をハッシュし、その値を検証してフィルターが true または false のどちらを返すかを決定するカスタム フィルターを作成できます。  
  
## <a name="implementation"></a>実装  
 カスタム フィルターは、<xref:System.ServiceModel.Dispatcher.MessageFilter> 抽象基本クラスの実装です。 カスタム フィルターを実装する場合は、コンストラクターが必要に応じて、文字列パラメーターを 1 つだけ受け取ることができます。 このパラメーターには、MessageFilter コンストラクターに渡される構成情報が含まれ、フィルターが照合を実行するために実行時に必要とする値や構成を指示します。 これは、評価対象のメッセージ内でフィルターが検索する必要がある値を提供する場合などに使用できます。 文字列パラメーターを受け取るカスタムのメッセージ フィルターの基本の実装例を次に示します。  
  
```csharp  
public class MyMessageFilter: MessageFilter  
{  
    string filterData;  
    public MyMessageFilter(string filterData)  
    {  
        if(string.IsNullOrEmpty(filterData)  
            throw new ArgumentNullException("filterData");  
        this.filterData=filterData;  
    }  
    public override bool Match(System.ServiceModel.Channels.Message message)  
    {  
        ...  
        return retValue;  
    }  
    public override bool Match(System.ServiceModel.Channels.MessageBuffer buffer)  
    {  
        ...  
        return retValue;  
    }  
}  
```  
  
> [!NOTE]
> 実際の実装では、Match メソッドには、メッセージを調べて、このメッセージ フィルタが**true**または**false**を返す必要があるかどうかを判断するロジックが含まれています。  
  
### <a name="performance"></a>パフォーマンス  
 カスタム フィルターを実装する場合は、フィルターがメッセージの評価を完了するのに要する最大時間を考慮する必要があります。 メッセージは、一致が見つかるまでに複数のフィルターに対して評価される場合があるので、すべてのフィルターを評価する前にクライアント要求がタイムアウトしないようにすることが重要です。 したがって、カスタム フィルターのコードは、メッセージがフィルター条件に一致するかどうかを調べるために、メッセージのコンテンツまたは属性を評価するのに必要なコードだけにする必要があります。  
  
 一般に、カスタム フィルターを実装する場合は、次のことを避ける必要があります。  
  
- IO。たとえば、ディスクやデータベースへのデータの保存です。  
  
- 不要な処理。たとえば、ドキュメントの複数のレコードのループ処理です。  
  
- ブロック操作。たとえば、共有リソースに対するロックの取得を必要とする呼び出しや、データベースに対する検索の実行です。  
  
 実稼働環境でカスタム フィルターを使用する前に、パフォーマンス テストを実行して、フィルターがメッセージを評価するのに要する平均時間を調べる必要があります。 フィルター テーブルで使用される他のフィルターの平均処理時間と合わせることで、クライアント アプリケーションで指定する必要がある最大タイムアウト値を正確に計算できます。  
  
## <a name="usage"></a>使用法  
 ルーティング サービスでカスタム フィルタを使用するには、タイプが "Custom" の新しいフィルタ エントリ、メッセージ フィルタの完全修飾型名、およびアセンブリの名前を指定して、フィルタ テーブルに追加する必要があります。  その他の MessageFilter と同様に、カスタム フィルターのコンストラクターに渡される文字列 filterData を指定できます。  
  
 カスタム フィルターをルーティング サービスと使用する例を次に示します。  
  
```xml  
<!--ROUTING SECTION -->  
<routing>  
  <filters>  
    <filter name="CustomFilter1" filterType="Custom"
            customType="CustomAssembly.MyMessageFilter,
            CustomAssembly" filterData="custom data" />  
  </filters>  
  <filterTables>  
    <table name="routingTable1">  
      <filters>  
        <add filterName="CustomFilter1" endpointName="CalculatorService" />  
      </filters>  
    </table>  
  </filterTables>  
</routing>  
```  
  
```csharp  
RoutingConfiguration rc = new RoutingConfiguration();  
List<ServiceEndpoint> endpointList = new List<ServiceEndpoint>();  
endpointList.Add(client);  
rc.FilterTable.Add(new MyMessageFilter("CustomData"), endpointList);  
```
