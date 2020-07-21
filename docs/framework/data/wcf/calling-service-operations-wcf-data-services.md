---
title: サービス操作の呼び出し (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1767f3a7-29d2-4834-a763-7d169693fa8b
ms.openlocfilehash: f1ff707c90e884dc66ab10563dc41ea7789f5cda
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84202002"
---
# <a name="calling-service-operations-wcf-data-services"></a>サービス操作の呼び出し (WCF Data Services)
Open Data Protocol (OData) では、データ サービスのサービス操作が定義されています。 WCF Data Services では、データ サービスのメソッドとしてこのような操作を定義できます。 他のデータ サービス リソースと同様に、これらのサービス操作は URI によってアドレス指定できます。 サービス操作では、エンティティ型のコレクション、1 つのエンティティ型のインスタンス、およびプリミティブ型 (整数、文字列など) を返すことができます。 さらに、サービス操作では、`null` (Visual Basic の場合は `Nothing`) を返すこともできます。 WCF Data Services クライアント ライブラリを使用して、HTTP GET 要求をサポートするサービス操作にアクセスすることができます。 この種のサービス操作は、<xref:System.ServiceModel.Web.WebGetAttribute> が適用されたメソッドとして定義されます。 詳細については、「[サービス操作](service-operations-wcf-data-services.md)」を参照してください。  
  
 サービス操作は、OData を実装するデータ サービスによって返されるメタデータで公開されます。 メタデータ内で、サービス操作は、`FunctionImport` 要素として表されます。 厳密に型指定された <xref:System.Data.Services.Client.DataServiceContext> を生成するとき、この要素は "サービス参照の追加" と DataSvcUtil.exe ツールで無視されます。 このため、サービス操作を直接呼び出すために使用できるコンテキストにはメソッドはありません。 ただし、次のいずれかの方法を使用して、WCF Data Services クライアントでサービス操作を呼び出すことができます。  
  
- <xref:System.Data.Services.Client.DataServiceContext.Execute%2A> で <xref:System.Data.Services.Client.DataServiceContext> メソッドを呼び出し、サービス操作の URI をその他のパラメーターと共に指定します。 このメソッドは、GET サービス操作の呼び出しに使用されます。  
  
- <xref:System.Data.Services.Client.DataServiceContext.CreateQuery%2A> の <xref:System.Data.Services.Client.DataServiceContext> メソッドを使用して、<xref:System.Data.Services.Client.DataServiceQuery%601> オブジェクトを作成します。 <xref:System.Data.Services.Client.DataServiceContext.CreateQuery%2A> を呼び出すとき、サービス操作の名前が `entitySetName` パラメーターに渡されます。 このメソッドは、列挙されたときまたは <xref:System.Data.Services.Client.DataServiceQuery%601> メソッドが呼び出されたときにサービス操作を呼び出す <xref:System.Data.Services.Client.DataServiceQuery%601.Execute%2A> オブジェクトを返します。 このメソッドは、コレクションを返す GET サービス操作の呼び出しに使用されます。 1 つのパラメーターは、<xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> メソッドを使用して指定することができます。 このメソッドによって返される <xref:System.Data.Services.Client.DataServiceQuery%601> オブジェクトは、クエリ オブジェクトのようにさらに構成できます。 詳細については、「[データ サービスに対するクエリ](querying-the-data-service-wcf-data-services.md)」を参照してください。  
  
## <a name="considerations-for-calling-service-operations"></a>サービス操作の呼び出しに関する考慮事項  
 WCF Data Services クライアントを使用してサービス操作を呼び出すときは、次の点に注意してください。  
  
- データ サービスに非同期にアクセスするときは、<xref:System.Data.Services.Client.DataServiceContext> の同等の非同期 <xref:System.Data.Services.Client.DataServiceContext.BeginExecute%2A>/<xref:System.Data.Services.Client.DataServiceContext.EndExecute%2A> メソッドまたは <xref:System.Data.Services.Client.DataServiceQuery%601> の <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A>/<xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A> メソッドを使用する必要があります。  
  
- WCF Data Services クライアント ライブラリは、プリミティブ型のコレクションを返すサービス操作からの結果を具体化できません。  
  
- WCF Data Services クライアント ライブラリでは、POST サービス操作の呼び出しはサポートされていません。 HTTP POST によって呼び出されるサービス操作は、<xref:System.ServiceModel.Web.WebInvokeAttribute> に `Method="POST"` パラメーターを使用して定義します。 HTTP POST 要求を使用してサービス操作を呼び出すには、代わりに <xref:System.Net.HttpWebRequest> を使用する必要があります。  
  
- <xref:System.Data.Services.Client.DataServiceContext.CreateQuery%2A> を使用して、エンティティまたはプリミティブ型の単一の結果を返す GET サービス操作または 1 つ以上の入力パラメーターを必要とする GET サービス操作を呼び出すことはできません。 代わりに <xref:System.Data.Services.Client.DataServiceContext.Execute%2A> メソッドを呼び出す必要があります。  
  
- ツールによって生成される厳密に型指定された <xref:System.Data.Services.Client.DataServiceContext> 部分クラスで <xref:System.Data.Services.Client.DataServiceContext.CreateQuery%2A> メソッドまたは <xref:System.Data.Services.Client.DataServiceContext.Execute%2A> メソッドを使用してサービス操作を呼び出す拡張メソッドを作成することを検討してください。 これにより、コンテキストから直接サービス操作を呼び出すことができます。 詳細については、ブログの投稿「[サービス操作および WCF Data Services クライアント](https://docs.microsoft.com/archive/blogs/astoriateam/service-operations-and-the-wcf-data-services-client)」を参照してください。  
  
- <xref:System.Data.Services.Client.DataServiceContext.CreateQuery%2A> を使用してサービス操作を呼び出す場合、クライアント ライブラリは、アンパサンド (&) などの予約文字のパーセント エンコードを実行し、文字列内の単一引用符をエスケープして、<xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> に入力された文字を自動的にエスケープします。 ただし、いずれかの *Execute* メソッドを呼び出してサービス操作を呼び出す場合は、このユーザーが指定した任意の文字列値のエスケープを実行する必要があります。 URI 内の単一引用符は、単一引用符のペアとしてエスケープされます。  
  
## <a name="examples-of-calling-service-operations"></a>サービス操作の呼び出しの例  
 このセクションには、WCF Data Services クライアント ライブラリを使用してサービス操作を呼び出す方法を示す次の例が含まれています。  
  
- [Execute&lt;T&gt; を呼び出してエンティティのコレクションを返す](calling-service-operations-wcf-data-services.md#ExecuteIQueryable)  
  
- [CreateQuery&lt;T&gt; を使用してエンティティのコレクションを返す](calling-service-operations-wcf-data-services.md#CreateQueryIQueryable)  
  
- [Execute&lt;T&gt; を呼び出して 1 つのエンティティを返す](calling-service-operations-wcf-data-services.md#ExecuteSingleEntity)  
  
- [Execute&lt;T&gt; を呼び出してプリミティブ値のコレクションを返す](calling-service-operations-wcf-data-services.md#ExecutePrimitiveCollection)  
  
- [Execute&lt;T&gt; を呼び出して 1 つのプリミティブ値を返す](calling-service-operations-wcf-data-services.md#ExecutePrimitiveValue)  
  
- [データを返さないサービス操作を呼び出す](calling-service-operations-wcf-data-services.md#ExecuteVoid)  
  
- [サービス操作を非同期に呼び出す](calling-service-operations-wcf-data-services.md#ExecuteAsync)  
  
<a name="ExecuteIQueryable"></a>
### <a name="calling-executet-to-return-a-collection-of-entities"></a>Execute\<T> を呼び出してエンティティのコレクションを返す  
 次の例では、文字列パラメーター `city` を受け取り、<xref:System.Linq.IQueryable%601> を返す、GetOrdersByCity という名前のサービス操作を呼び出します。  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationIQueryable](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationiqueryable)]
 [!code-vb[Astoria Northwind Client#CallServiceOperationIQueryable](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#callserviceoperationiqueryable)]  
  
 この例では、サービス操作は、`Order` オブジェクトのコレクションを関連する `Order_Detail` オブジェクトと共に返します。  
  
<a name="CreateQueryIQueryable"></a>
### <a name="using-createqueryt-to-return-a-collection-of-entities"></a>CreateQuery\<T> を使用してエンティティのコレクションを返す  
 次の例では、<xref:System.Data.Services.Client.DataServiceContext.CreateQuery%2A> を使用して、同じ GetOrdersByCity サービス操作を呼び出すために使用される <xref:System.Data.Services.Client.DataServiceQuery%601> を返します。  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationCreateQuery](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationcreatequery)]
 [!code-vb[Astoria Northwind Client#CallServiceOperationCreateQuery](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#callserviceoperationcreatequery)]  
  
 この例では、<xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> メソッドを使用してクエリにパラメーターを追加し、<xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> メソッドを使用して関連する Order_Details オブジェクトを結果に含めています。  
  
<a name="ExecuteSingleEntity"></a>
### <a name="calling-executet-to-return-a-single-entity"></a>Execute\<T> を呼び出して 1 つのエンティティを返す  
 次の例では、単一の Order エンティティのみを返す、GetNewestOrder という名前のサービス操作を呼び出します。  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationSingleEntity](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationsingleentity)]
 [!code-vb[Astoria Northwind Client#CallServiceOperationSingleEntity](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#callserviceoperationsingleentity)]  
  
 この例では、<xref:System.Linq.Enumerable.FirstOrDefault%2A> メソッドを使用して、実行時に単一の Order エンティティのみを要求します。  
  
<a name="ExecutePrimitiveCollection"></a>
### <a name="calling-executet-to-return-a-collection-of-primitive-values"></a>Execute\<T> を呼び出してプリミティブ値のコレクションを返す  
 次の例では、文字列値のコレクションを返すサービス操作を呼び出します。  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationEnumString](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationenumstring)]  
  
<a name="ExecutePrimitiveValue"></a>
### <a name="calling-executet-to-return-a-single-primitive-value"></a>Execute\<T> を呼び出して 1 つのプリミティブ値を返す  
 次の例では、単一の文字列値を返すサービス操作を呼び出します。  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationSingleInt](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationsingleint)]
 [!code-vb[Astoria Northwind Client#CallServiceOperationSingleInt](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#callserviceoperationsingleint)]  
  
 この例において、<xref:System.Linq.Enumerable.FirstOrDefault%2A> メソッドを使用して、実行時に単一の整数値のみを要求しています。  
  
<a name="ExecuteVoid"></a>
### <a name="calling-a-service-operation-that-returns-no-data"></a>データを返さないサービス操作を呼び出す  
 次の例では、データを返さないサービス操作を呼び出します。  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationVoid](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationvoid)]
 [!code-vb[Astoria Northwind Client#CallServiceOperationVoid](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#callserviceoperationvoid)]  
  
 データが返されないため、実行の値は割り当てられません。 要求が成功したことを示す唯一の印は、<xref:System.Data.Services.Client.DataServiceQueryException> が発生しないことです。  
  
<a name="ExecuteAsync"></a>
### <a name="calling-a-service-operation-asynchronously"></a>サービス操作を非同期に呼び出す  
 次の例では、<xref:System.Data.Services.Client.DataServiceContext.BeginExecute%2A> と <xref:System.Data.Services.Client.DataServiceContext.EndExecute%2A> を呼び出してサービス操作を非同期に呼び出しています。  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationAsync](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationasync)]
 [!code-vb[Astoria Northwind Client#CallServiceOperationAsync](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#callserviceoperationasync)]  
  
 [!code-csharp[Astoria Northwind Client#OnAsyncExecutionComplete](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#onasyncexecutioncomplete)]
 [!code-vb[Astoria Northwind Client#OnAsyncExecutionComplete](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#onasyncexecutioncomplete)]  
  
 データが返されないため、実行によって返される値は割り当てられません。 要求が成功したことを示す唯一の印は、<xref:System.Data.Services.Client.DataServiceQueryException> が発生しないことです。  
  
 次の例では、<xref:System.Data.Services.Client.DataServiceContext.CreateQuery%2A> を使用して同じサービス操作を非同期に呼び出しています。  
  
 [!code-csharp[Astoria Northwind Client#CallServiceOperationQueryAsync](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#callserviceoperationqueryasync)]
 [!code-vb[Astoria Northwind Client#CallServiceOperationQueryAsync](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#callserviceoperationqueryasync)]  
  
 [!code-csharp[Astoria Northwind Client#OnAsyncQueryExecutionComplete](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#onasyncqueryexecutioncomplete)]
 [!code-vb[Astoria Northwind Client#OnAsyncQueryExecutionComplete](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#onasyncqueryexecutioncomplete)]  
  
## <a name="see-also"></a>関連項目

- [WCF Data Services クライアント ライブラリ](wcf-data-services-client-library.md)
