---
title: '方法: COM+ サービス設定を構成する'
ms.date: 03/30/2017
helpviewer_keywords:
- COM+ [WCF], configuring service settings
ms.assetid: f42a55a8-3af8-4394-9fdd-bf12a93780eb
ms.openlocfilehash: 3fb4b31038845d223248e72d32b3e7413f2aef63
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597177"
---
# <a name="how-to-configure-com-service-settings"></a>方法: COM+ サービス設定を構成する
COM+ サービス構成ツールを使用してアプリケーション インターフェイスを追加または削除すると、アプリケーション構成ファイル内の Web サービス構成が更新されます。 COM + でホストされるモードでは、アプリケーションのルートディレクトリに app.config ファイルが配置されます (%Programfiles%\complus applications\ Applications \\ {appid} が既定値です)。 いずれの Web ホスト モードでも、Web.config ファイルは指定した vroot ディレクトリに配置されます。  
  
> [!NOTE]
> クライアントとサーバー間のメッセージの改ざんを防止するには、メッセージの署名を使用する必要があります。 また、クライアントとサーバー間のメッセージから情報が漏えいするのを防止するには、メッセージまたはトランスポート層の暗号化を使用する必要があります。 Windows Communication Foundation (WCF) サービスと同様に、同時呼び出し、接続、インスタンス、および保留中の操作の数を制限するには、調整を使用する必要があります。 これによりリソースの過剰消費を防ぐことができます。 調整の動作は、サービス構成ファイルの設定で指定します。  
  
## <a name="example"></a>例  
 次のインターフェイスを実装するコンポーネントについて考えます。  
  
```csharp
[Guid("C551FBA9-E3AA-4272-8C2A-84BD8D290AC7")]  
public interface IFinances  
{  
    string Debit(string accountNo, double amount);  
    string Credit(string accountNo, double amount);  
}  
```  
  
 コンポーネントを Web サービスとして公開する場合、クライアントが準拠する必要のある対応の公開サービス コントラクトは次のとおりです。  
  
```csharp
[ServiceContract(Session = true,  
Namespace = "http://tempuri.org/C551FBA9-E3AA-4272-8C2A-84BD8D290AC7",  
Name = "IFinances")]  
public interface IFinancesContract : IDisposable  
{  
    [OperationContract]  
    string Debit(string accountNo, double amount);  
    [OperationContract]  
    string Credit(string accountNo, double amount);  
}  
```  
  
> [!NOTE]
> IID はコントラクトの初期名前空間の一部です。  
  
 このサービスを使用するクライアント アプリケーションはこのコントラクトに準拠し、さらにアプリケーションの構成に指定したバインディングと互換性のあるバインディングを使用する必要があります。  
  
 次のコード例は、既定の構成ファイルの例を示しています。 これは、Windows Communication Foundation (WCF) Web サービスであり、これは標準のサービスモデル構成スキーマに準拠しており、他の WCF サービス構成ファイルと同じ方法で編集できます。  
  
 通常、次のような変更を行います。  
  
- エンドポイント アドレスを既定の ApplicationName/ComponentName/InterfaceName という形式から、より利用しやすい形式に変更する。  
  
- サービスの名前空間を既定のフォームから `http://tempuri.org/InterfaceID` より適切な形式に変更します。  
  
- 異なるトランスポート バインディングを使用するようにエンドポイントを変更する。  
  
     COM+ ホスト モードの場合、既定では名前付きパイプ トランスポートが使用されますが、その代わりに TCP などのコンピューターに関係のないトランスポートも使用できます。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
    <system.serviceModel>  
        <bindings>  
            <netNamedPipeBinding>  
                <binding name="comNonTransactionalBinding" />  
                <binding name="comTransactionalBinding" transactionFlow="true" />  
            </netNamedPipeBinding>  
        </bindings>  
        <comContracts>  
            <comContract contract="{C551FBA9-E3AA-4272-8C2A-84BD8D290AC7}"  
                name="IFinances" namespace="http://tempuri.org/C551FBA9-E3AA-4272-8C2A-84BD8D290AC7"  
                requiresSession="true">  
                <exposedMethods>  
                    <add exposedMethod="Debit" />  
                    <add exposedMethod="Credit" />  
                </exposedMethods>  
            </comContract>  
        </comContracts>  
        <services>  
            <service name="{DCDB24CC-0B19-4534-95CD-FBBFF4D67DD9},{C942B840-AD54-4A44-B5F7-928130980AB9}">  
                <endpoint address="IFinances" binding="netNamedPipeBinding" bindingConfiguration="comNonTransactionalBinding"  
                    contract="{C551FBA9-E3AA-4272-8C2A-84BD8D290AC7}" />  
                <host>  
                    <baseAddresses>  
                        <add baseAddress="net.pipe://localhost/ServiceModelDocSampleApp/ServiceModelDocSample.esFinance" />  
                    </baseAddresses>  
                </host>  
            </service>  
        </services>  
    </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [COM + アプリケーションとの統合](integrating-with-com-plus-applications.md)
