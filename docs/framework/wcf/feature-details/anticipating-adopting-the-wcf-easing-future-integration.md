---
title: Windows Communication Foundation 導入の準備:将来的な統合の容易化
ms.date: 03/30/2017
ms.assetid: 3028bba8-6355-4ee0-9ecd-c56e614cb474
ms.openlocfilehash: 6392194b3124c999031123225dcc28c8de6171e9
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84576526"
---
# <a name="anticipating-adopting-the-windows-communication-foundation-easing-future-integration"></a>Windows Communication Foundation 導入の準備:将来的な統合の容易化
現在、ASP.NET を使用していて、今後 WCF を使用する予定がある場合、このトピックでは、新しい ASP.NET Web サービスが WCF アプリケーションと連携して機能するようにするためのガイダンスを提供します。  
  
## <a name="general-recommendations"></a>一般的な推奨事項  
 ASP.NET 2.0 を使用して、すべての新規サービスを作成します。 こうすることで、拡張および強化された新バージョンの機能にアクセスできます。 ただし、同じアプリケーションで ASP.NET 2.0 コンポーネントを WCF コンポーネントと共に使用することもできます。  
  
## <a name="protocols"></a>プロトコル  
 WS-I Basic Profile 1.1 への準拠を検証するには、次のように ASP.NET 2.0 の新機能を使用します。  
  
```csharp  
[WebService(Namespace = "http://tempuri.org/")]  
[WebServiceBinding(  
     ConformsTo = WsiProfiles.BasicProfile1_1,  
     EmitConformanceClaims=true)]  
public interface IEcho  
```  
  
 WS-I Basic Profile 1.1 に準拠している ASP.NET Web サービスは、wcf の定義済みバインディングを使用して、WCF クライアントと相互運用でき <xref:System.ServiceModel.BasicHttpBinding> ます。  
  
## <a name="service-development"></a>サービスの開発  
 SOAPAction HTTP ヘッダーではなく、SOAP メッセージの本文要素の完全修飾名に基づいてメッセージをメソッドにルーティングする場合は、<xref:System.Web.Services.Protocols.SoapDocumentServiceAttribute> 属性の使用を避けます。 WCF は、メッセージのルーティングに SOAPAction HTTP ヘッダーを使用します。  
  
## <a name="data-representation"></a>データ表現  
 <xref:System.Xml.Serialization.XmlSerializer> によって既定で型のシリアル化が行われる XML は、XML の名前空間が明示的に定義されている場合、<xref:System.Runtime.Serialization.DataContractSerializer> によって型のシリアル化が行われる XML と意味的に同一です。 将来 WCF を導入するために ASP.NET ウェブサービスで使用するデータ型を定義する場合は、次の手順を実行します。  
  
1. XML スキーマではなく、.NET Framework クラスを使用して型を定義します。  
  
2. <xref:System.SerializableAttribute> と <xref:System.Xml.Serialization.XmlRootAttribute> だけをそのクラスに追加します。後者を使用して型の名前空間を明示的に定義してください。 .NET Framework クラスを XML に変換する方法を制御する目的で、<xref:System.Xml.Serialization> 名前空間の属性を追加しないでください。  
  
 この手法を採用すると、後から <xref:System.Runtime.Serialization.DataContractAttribute> および <xref:System.Runtime.Serialization.DataMemberAttribute> を追加することで、転送のためにクラスをシリアル化する XML に大きな変更を加えることなく .NET クラスをデータ コントラクトにすることができます。 ASP.NET Web サービスによってメッセージで使用される型は、WCF アプリケーションによるデータコントラクトとして処理され、他の利点とは別に WCF アプリケーションのパフォーマンスが向上します。  
  
## <a name="security"></a>Security  
 インターネット インフォメーション サービス (IIS) に用意されている認証オプションは使用しないでください。 WCF クライアントはこれらをサポートしていません。 サービスをセキュリティで保護する必要がある場合は、WCF に用意されているオプションを使用します。これらのオプションは豊富で、標準プロトコルに基づいているためです。  
  
## <a name="see-also"></a>関連項目

- [Windows Communication Foundation 導入の準備:将来の移行の簡略化](anticipating-adopting-wcf-migration.md)
