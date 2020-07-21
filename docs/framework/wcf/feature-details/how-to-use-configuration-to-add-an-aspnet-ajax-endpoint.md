---
title: '方法: 構成を使用して ASP.NET AJAX エンドポイントを追加する'
ms.date: 03/30/2017
ms.assetid: 7cd0099e-dc3a-47e4-a38c-6e10f997f6ea
ms.openlocfilehash: 97f8174161068f2c72b6bd2bc4e8a3044f5bccdd
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051663"
---
# <a name="how-to-use-configuration-to-add-an-aspnet-ajax-endpoint"></a>方法: 構成を使用して ASP.NET AJAX エンドポイントを追加する
Windows Communication Foundation (WCF) を使用すると、クライアント Web サイトの JavaScript から呼び出すことができる ASP.NET AJAX 対応エンドポイントを使用できるようにするサービスを作成できます。 このようなエンドポイントを作成するには、他のすべての Windows Communication Foundation (WCF) エンドポイントと同様に構成ファイルを使用するか、構成要素を必要としないメソッドを使用します。 ここでは、構成を使用する方法について説明します。  
  
 サービスエンドポイントが ASP.NET になるようにするための手順の一部は、を使用してエンドポイントの動作を追加するようにエンドポイントを構成することによって構成され <xref:System.ServiceModel.WebHttpBinding> [\<enableWebScript>](../../configure-apps/file-schema/wcf/enablewebscript.md) ます。 エンドポイントを構成した後、サービスを実装およびホストする手順は、WCF サービスで使用されているものと似ています。 実際の例については、「 [HTTP POST を使用した AJAX サービス](../samples/ajax-service-using-http-post.md)」を参照してください。  
  
 構成を使用せずに ASP.NET AJAX エンドポイントを構成する方法の詳細については、「[方法: 構成を使用せずに ASP.NET Ajax エンドポイントを追加](how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md)する」を参照してください。  
  
## <a name="to-create-a-basic-wcf-service"></a>基本的な WCF サービスを作成するには  
  
1. 属性でマークされたインターフェイスを使用して、基本的な WCF サービスコントラクトを定義 <xref:System.ServiceModel.ServiceContractAttribute> します。 各操作を <xref:System.ServiceModel.OperationContractAttribute> でマークします。 <xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A> プロパティが設定されていることを確認します。  
  
    ```csharp
    [ServiceContract(Namespace = "MyService")]  
    public interface ICalculator  
    {  
        [OperationContract]  
         // This operation returns the sum of d1 and d2.  
        double Add(double n1, double n2);  
  
        //Other operations omitted…  
  
    }  
    ```  
  
2. `ICalculator` を使用して、`CalculatorService` サービス コントラクトを実装します。  
  
    ```csharp
    public class CalculatorService : ICalculator  
    {  
        public double Add(double n1, double n2)  
        {  
            return n1 + n2;  
        }
        // Other operations omitted…
    }
    ```  
  
3. 名前空間ブロック内にラップすることにより、`ICalculator` と `CalculatorService` の実装の名前空間を定義します。  
  
    ```csharp
    namespace Microsoft.Ajax.Samples
    {  
        //Include the code for ICalculator and Caculator here.  
    }  
    ```  
  
## <a name="to-create-an-aspnet-ajax-endpoint-for-the-service"></a>サービスに ASP.NET AJAX エンドポイントを作成するには  
  
1. 動作の構成を作成し、 [\<enableWebScript>](../../configure-apps/file-schema/wcf/enablewebscript.md) サービスの ASP.NET AJAX 対応エンドポイントの動作を指定します。  
  
    ```xml  
    <system.serviceModel>  
        <behaviors>  
            <endpointBehaviors>  
                <behavior name="AspNetAjaxBehavior">  
                    <enableWebScript />  
                </behavior>  
            </endpointBehaviors>  
        </behaviors>  
    </system.serviceModel>  
    ```  
  
2. <xref:System.ServiceModel.WebHttpBinding> と、前の手順で定義した ASP.NET AJAX 動作を使用するサービスのエンドポイントを作成します。  
  
    ```xml  
    <system.serviceModel>  
        <services>  
            <service name="Microsoft.Ajax.Samples.CalculatorService">  
                <endpoint address=""  
                    behaviorConfiguration="AspNetAjaxBehavior"
                    binding="webHttpBinding"  
                    contract="Microsoft.Ajax.Samples.ICalculator" />  
            </service>  
        </services>  
    </system.serviceModel>
    ```  
  
## <a name="to-host-the-service-in-iis"></a>IIS でサービスをホストするには  
  
1. IIS でサービスをホストするには、アプリケーションで .svc 拡張子の新しいサービス ファイルを作成します。 このファイルを編集するには、サービスに適切な[ \@ ServiceHost](../../configure-apps/file-schema/wcf-directive/servicehost.md)ディレクティブ情報を追加します。 たとえば、`CalculatorService` サンプルに対応するサービス ファイルのコンテンツには、次の情報が記述されています。  
  
    ```aspx-csharp
    <%@ServiceHost
    language=c#
    Debug="true"
    Service="Microsoft.Ajax.Samples.CalculatorService"  
    %>  
    ```  
  
2. IIS でのホストの詳細については、「 [How to: Host a WCF Service IN iis](how-to-host-a-wcf-service-in-iis.md)」を参照してください。  
  
## <a name="to-call-the-service"></a>サービスを呼び出すには  
  
1. エンドポイントは、.svc ファイルを基準とした空のアドレスで構成されます。これにより、サービスが使用できるようになり、サービスに要求を送信することによって呼び出すことができます。 \<operation> たとえば、service .svc/Add を操作に送信します。 `Add` これは、ASP.NET AJAX Script Manager コントロールのスクリプト コレクションにエンドポイント URL を入力することで使用できます。 例については、「 [HTTP POST を使用した AJAX サービス](../samples/ajax-service-using-http-post.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [ASP.NET AJAX 用の WCF サービスの作成](creating-wcf-services-for-aspnet-ajax.md)
- [方法: AJAX 対応 ASP.NET Web サービスを WCF に移行する](how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf.md)
