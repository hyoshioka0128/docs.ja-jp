---
title: ASP.NET Web サービスとの相互運用
ms.date: 03/30/2017
ms.assetid: 622422f8-6651-442f-b8be-e654a4aabcac
ms.openlocfilehash: f38209ffe2161e58528a108b29e730665a65da37
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598867"
---
# <a name="interoperability-with-aspnet-web-services"></a>ASP.NET Web サービスとの相互運用
ASP.NET ウェブサービスと Windows Communication Foundation (WCF) Web サービスの間の相互運用性を実現するには、両方のテクノロジを使用して実装されたサービスが WS-I Basic Profile 1.1 仕様に準拠していることを確認します。 WS-I Basic Profile 1.1 に準拠している ASP.NET Web サービスは、WCF システム指定のバインディングを使用して、WCF クライアントと相互運用 <xref:System.ServiceModel.BasicHttpBinding> できます。  
  
 <xref:System.Web.Services.WebService> <xref:System.Web.Services.WebMethodAttribute> 次のサンプルコードに示すように、属性と属性をクラスではなくインターフェイスに追加し、インターフェイスを実装するクラスを記述するには、ASP.NET 2.0 オプションを使用します。  
  
```csharp
[WebService]  
public interface IEcho  
{  
    [WebMethod]  
    string Echo(string input);  
}  
  
public class Service : IEcho  
{  
  
   public string Echo(string input)  
   {  
        return input;  
    }  
}  
```  
  
 <xref:System.Web.Services.WebService> 属性を持つインターフェイスは、同じコントラクトを異なる方法で実装する可能性のあるさまざまなクラスで再利用可能なサービスによって実行される操作のコントラクトを構成するため、このオプションを使用することをお勧めします。  
  
 <xref:System.Web.Services.Protocols.SoapDocumentServiceAttribute> 属性を使用する場合、`SOAPAction` HTTP ヘッダーではなく、SOAP メッセージの本文要素の完全修飾名に基づいてメッセージをメソッドへルーティングすることは避けます。 WCF は、 `SOAPAction` メッセージのルーティングに HTTP ヘッダーを使用します。  
  
 <xref:System.Xml.Serialization.XmlSerializer> によって既定で型のシリアル化が行われる XML は、XML の名前空間が明示的に定義されている場合、<xref:System.Runtime.Serialization.DataContractSerializer> によって型のシリアル化が行われる XML と意味的に同一です。 WCF を導入するために、ASP.NET Web サービスで使用するデータ型を定義する場合は、次の手順を実行します。  
  
- XML スキーマではなく、.NET Framework クラスを使用して型を定義します。  
  
- <xref:System.SerializableAttribute> と <xref:System.Xml.Serialization.XmlRootAttribute> だけをそのクラスに追加します。後者を使用して型の名前空間を明示的に定義してください。 .NET Framework クラスを XML に変換する方法を制御する目的で、<xref:System.Xml.Serialization> 名前空間の属性を追加しないでください。  
  
- この手法を採用すると、後から <xref:System.Runtime.Serialization.DataContractAttribute> および <xref:System.Runtime.Serialization.DataMemberAttribute> を追加することで、転送のためにクラスをシリアル化する XML に大きな変更を加えることなく .NET クラスをデータ コントラクトにすることができます。 ASP.NET Web サービスによってメッセージで使用される型は、WCF アプリケーションによるデータコントラクトとして処理することができ、その他の利点として、WCF アプリケーションでパフォーマンスを向上させることができます。  
  
 インターネット インフォメーション サービス (IIS) に用意されている認証オプションは使用しないでください。 WCF クライアントはこれらをサポートしていません。 サービスをセキュリティで保護する必要がある場合は、WCF に用意されているオプションを使用します。これらのオプションは堅牢で、標準プロトコルに基づいているためです。  
  
## <a name="performance-impact-caused-by-loading-the-servicemodel-httpmodule"></a>ServiceModel HttpModule の読み込みがパフォーマンスに及ぼす影響  
 .NET Framework Version 3.0 では、WCF `HttpModule` が、すべての ASP.NET アプリケーションが WCF 対応になるように、ルートの Web.config ファイルにインストールされます。 これによりパフォーマンスに影響が出る場合があるため、次の例に示すように、Web.config ファイルの `ServiceModel` を削除することもできます。  
  
```xml  
<httpModules>  
    <remove name="ServiceModel" />  
</httpModules>
```  
  
## <a name="see-also"></a>関連項目

- [方法: WCF サービスおよび ASP.NET Web サービス クライアントを相互運用するために構成する](config-wcf-service-with-aspnet-web-service.md)
