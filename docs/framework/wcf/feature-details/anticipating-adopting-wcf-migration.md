---
title: Windows Communication Foundation 導入の準備:将来の移行の簡略化
ms.date: 03/30/2017
ms.assetid: f49664d9-e9e0-425c-a259-93f0a569d01b
ms.openlocfilehash: b43f509bd49ebe89d7ed0be4c37b3ed179aaeb8c
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84576500"
---
# <a name="anticipating-adopting-the-windows-communication-foundation-easing-future-migration"></a>Windows Communication Foundation 導入の準備:将来の移行の簡略化
新しい ASP.NET アプリケーションを WCF に簡単に移行できるようにするには、前述の推奨事項に加えて、次の推奨事項に従ってください。  
  
## <a name="protocols"></a>プロトコル  
 ASP.NET 2.0 の SOAP 1.2 サポートを無効にします。  
  
```xml  
<configuration>  
     <system.web>  
      <webServices >  
          <protocols>  
           <remove name="HttpSoap12"/>  
          </protocols>
      </webServices>  
     </system.web>
</configuration>  
```  
  
 WCF では、SOAP 1.1 や SOAP 1.2 などのさまざまなプロトコルに準拠したメッセージをさまざまなエンドポイントを使用して処理する必要があるため、この方法をお勧めします。 ASP.NET 2.0 Web サービスが、既定の構成である SOAP 1.1 と SOAP 1.2 の両方をサポートするように構成されている場合は、すべての ASP.NET Web サービスの既存のクライアントと確実に互換性があるように、元のアドレスで単一の WCF エンドポイントに移行することはできません。 また、SOAP 1.1 ではなく 1.2 を選択すると、サービスの利用者がさらに厳しく制限されます。  
  
## <a name="service-development"></a>サービスの開発  
 WCF では、を <xref:System.ServiceModel.ServiceContractAttribute> インターフェイスまたはクラスのいずれかに適用することで、サービスコントラクトを定義できます。 この属性は、クラスではなくインターフェイスに適用することをお勧めします。これにより、任意の数のクラスでさまざまに実装できるコントラクト定義が作成されます。 ASP.NET 2.0 では、<xref:System.Web.Services.WebService> 属性をクラスだけでなくインターフェイスに適用することもできます。 ただし、既に説明したように ASP.NET 2.0 には不具合があり、<xref:System.Web.Services.WebService> 属性をクラスではなくインターフェイスに適用した場合、この属性の名前空間パラメーターが有効化されません。 通常は、サービスの名前空間を既定値から変更することをお勧めします。これは、 `http://tempuri.org` 属性の namespace パラメーターを使用して、 <xref:System.Web.Services.WebService> <xref:System.ServiceModel.ServiceContractAttribute> インターフェイスまたはクラスのいずれかに属性を適用することによって、ASP.NET Web サービスの定義を続ける必要があるためです。  
  
- これらのインターフェイスを定義するメソッドに含めるコードは、できるだけ少なくします。 これらのメソッドの作業を他のクラスに委任します。 新しい WCF サービスの種類では、そのようなクラスに対して、そのような作業を委任することもできます。  
  
- `MessageName` の <xref:System.Web.Services.WebMethodAttribute> パラメーターを使用して、サービスの動作の明示的な名前を指定します。  
  
    ```csharp  
    [WebMethod(MessageName="ExplicitName")]  
    string Echo(string input);  
    ```  
  
     ASP.NET での操作の既定の名前は、WCF によって提供される既定の名前とは異なるため、この操作は重要です。 明示的な名前を指定することで、既定の名前への依存を避けることができます。  
  
- ASP.NET Web サービス操作をポリモーフィックなメソッドで実装しないでください。 WCF では、ポリモーフィックなメソッドを使用した操作の実装はサポートされていません。  
  
- <xref:System.Web.Services.Protocols.SoapDocumentMethodAttribute> を使用して、HTTP 要求をメソッドにルーティングする SOAPAction HTTP ヘッダーの明示的な値を指定します。  
  
    ```csharp  
    [WebMethod]  
    [SoapDocumentMethod(RequestElementName="ExplicitAction")]  
    string Echo(string input);  
    ```  
  
     このアプローチを採用すると、ASP.NET と WCF で使用される既定の SOAPAction 値に依存しなくても済むようになります。  
  
- SOAP 拡張機能は使用しないでください。 SOAP 拡張機能が必要な場合は、その目的が WCF によって既に提供されている機能であるかどうかを判断します。 そのような場合は、WCF をすぐに導入しないことを再検討してください。  
  
## <a name="state-management"></a>状態管理  
 サービスで状態を維持する必要がないようにします。 状態を維持することは、アプリケーションのスケーラビリティを損なう傾向があるだけでなく、ASP.NET と WCF の状態管理メカニズムは大きく異なりますが、WCF では ASP.NET 互換モードの ASP.NET メカニズムがサポートされています。  
  
## <a name="exception-handling"></a>例外処理  
 サービスで送受信するデータ型の構造を設計するときは、クライアントに伝達する必要があり、サービス内で発生する可能性のあるさまざまな種類の例外を表現する構造も設計します。  
  
```csharp  
[Serializable]  
[XmlRoot(Namespace="ExplicitNamespace", IsNullable=true)]  
public partial class AnticipatedException
{
    private string anticipatedExceptionInformationField;  

    public string AnticipatedExceptionInformation
    {  
        get {
            return this.anticipatedExceptionInformationField;  
        }  
        set {  
            this.anticipatedExceptionInformationField = value;  
        }  
    }  
}  
```  
  
 これらのクラスには、自分自身を XML にシリアル化する機能を与えます。  
  
```csharp  
public XmlNode ToXML()  
{  
     XmlSerializer serializer = new XmlSerializer(  
      typeof(AnticipatedException));  
     MemoryStream memoryStream = new MemoryStream();  
     XmlTextWriter writer = new XmlTextWriter(  
     memoryStream, UnicodeEncoding.UTF8);  
     serializer.Serialize(writer, this);  
     XmlDocument document = new XmlDocument();  
     document.LoadXml(new string(  
     UnicodeEncoding.UTF8.GetChars(  
     memoryStream.GetBuffer())).Trim());  
    return document.DocumentElement;  
}  
```  
  
 これでこのクラスを使用して、明示的にスローされた <xref:System.Web.Services.Protocols.SoapException> インスタンスの詳細を指定できます。  
  
```csharp  
AnticipatedException exception = new AnticipatedException();  
exception.AnticipatedExceptionInformation = "…";  
throw new SoapException(  
     "Fault occurred",  
     SoapException.ClientFaultCode,  
     Context.Request.Url.AbsoluteUri,  
     exception.ToXML());  
```  
  
 これらの例外クラスは、WCF クラスを使用して簡単に再利用でき、 <xref:System.ServiceModel.FaultException%601> 新しいをスローします。`FaultException<AnticipatedException>(anticipatedException);`  
  
## <a name="security"></a>Security  
 セキュリティに関する推奨事項を次にいくつか示します。  
  
- ASP.NET 2.0 プロファイルは使用しないでください。これを使用すると、サービスが WCF に移行された場合に ASP.NET 統合モードの使用が制限されます。  
  
- サービスへのアクセスを制御するために Acl を使用しないでください。 ASP.NET Web サービスはインターネットインフォメーションサービス (IIS) を使用して Acl をサポートしています。 ASP.NET Web サービスはホスト用の IIS に依存しているため、WCF は必ずしも IIS でホストされている必要はありません。  
  
- サービスのリソースへのアクセスを承認するには、ASP.NET 2.0 ロール プロバイダーの使用を検討してください。  
  
## <a name="see-also"></a>関連項目

- [Windows Communication Foundation 導入の準備:将来的な統合の容易化](anticipating-adopting-the-wcf-easing-future-integration.md)
