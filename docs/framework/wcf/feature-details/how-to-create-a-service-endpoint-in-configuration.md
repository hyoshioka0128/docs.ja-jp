---
title: '方法: 構成にサービス エンドポイントを作成する'
description: 相対アドレスと絶対アドレスの両方を含む構成ファイルを使用して、WCF サービスのエンドポイントを追加する方法について説明します。
ms.date: 06/16/2016
ms.assetid: f474e25d-2a27-4f31-84c5-395c442b8e70
ms.openlocfilehash: 184bcb5f7f3e83f12608757b55bbb4d57be58f7d
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247066"
---
# <a name="how-to-create-a-service-endpoint-in-configuration"></a>方法: 構成にサービス エンドポイントを作成する
エンドポイントは、Windows Communication Foundation (WCF) サービスが提供する機能へのアクセスをクライアントに提供します。 エンドポイントの相対アドレスと絶対アドレスを組み合わせてサービスのエンドポイントを 1 つ以上定義できます。または、サービス エンドポイントを定義しない場合、ランタイムは既定で一部を提供します。 このトピックでは、相対アドレスと絶対アドレスの両方を含んでいる構成ファイルを使用したエンドポイントの使用方法について説明します。  
  
## <a name="example"></a>例  
 次のサービス構成では、1 つのベース アドレスと 5 つのエンドポイントを指定します。  
  
```xml  
<configuration>  
  
  <appSettings>  
    <!-- use appSetting to configure base address provided by host -->  
    <add key="baseAddress" value="http://localhost:8000/servicemodelsamples/service" />  
  </appSettings>  
  
  <system.serviceModel>  
    <services>  
    <!-- This section is optional with the default configuration introduced in .NET Framework 4. -->  
      <service name="Microsoft.ServiceModel.Samples.CalculatorService">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
          </baseAddresses>  
        </host>  
        <endpoint address=""  
                  binding="wsHttpBinding"  
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <endpoint address="/test"  
                  binding="wsHttpBinding"  
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <endpoint address="http://localhost:8001/hello/servicemodelsamples"  
                  binding="wsHttpBinding"  
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <endpoint address="net.tcp://localhost:9000/servicemodelsamples/service"  
                  binding="netTcpBinding"  
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <!-- the mex endpoint is another relative address exposed at   
             http://localhost:8000/ServiceModelSamples/service/mex -->  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange" />  
      </service>  
    </services>  
  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
  </system.serviceModel>  
  
</configuration>  
```  
  
## <a name="example"></a>例  
 ベース アドレスは、次のサンプルのように `add` 要素を使用して service/host/baseAddresses の下に指定します。  
  
```xml  
<service
    name="Microsoft.ServiceModel.Samples.CalculatorService">  
  <host>  
    <baseAddresses>  
      <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
    </baseAddresses>  
  </host>  
```  
  
## <a name="example"></a>例  
 次のサンプルの最初のエンドポイント定義では、相対アドレスを指定します。つまり、エンドポイント アドレスは、ベース アドレスと URI (Uniform Resource Identifier) 構造の規則に従った相対アドレスの組み合わせということを意味します。 相対アドレスが空 ("") のため、エンドポイント アドレスはベース アドレスと同じになります。 実際のエンドポイントアドレスは `http://localhost:8000/servicemodelsamples/service` です。  
  
```xml  
<endpoint address=""
    binding="wsHttpBinding"  
    contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
## <a name="example"></a>例  
 2 番目のエンドポイント定義でも、相対アドレスを指定します。次のサンプル構成を参照してください。 相対アドレス "test" がベース アドレスの末尾に追加されています。 実際のエンドポイントアドレスは `http://localhost:8000/servicemodelsamples/service/test` です。  
  
```xml  
<endpoint address="/test"  
    binding="wsHttpBinding"  
    contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
## <a name="example"></a>例  
 3 番目のエンドポイント定義では、絶対アドレスを指定します。次のサンプル構成を参照してください。 このアドレスでは、ベース アドレスは使用されていません。 実際のエンドポイントアドレスは `http://localhost:8001/hello/servicemodelsamples` です。  
  
```xml  
<endpoint address="http://localhost:8001/hello/servicemodelsamples"  
    binding="wsHttpBinding"  
    contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
## <a name="example"></a>例  
 4 番目のエンドポイント アドレスは、絶対アドレスと別のトランスポート (ここでは TCP) を指定しています。 このアドレスでは、ベース アドレスは使用されていません。 具体的には net.tcp://localhost:9000/servicemodelsamples/service です。  
  
```xml  
<endpoint address="net.tcp://localhost:9000/servicemodelsamples/service"  
    binding="netTcpBinding"  
    contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
## <a name="example"></a>例  
 ランタイムによって提供された既定のエンドポイントを使用するには、コードまたは構成ファイルでサービス エンドポイントを指定しないでください。 次の例では、サービスを開くときに、ランタイムは既定のエンドポイントを作成します。 既定のエンドポイントについては、「[Simplified Configuration](../simplified-configuration.md)」 (簡易構成) と「[Simplified Configuration for WCF Services](../samples/simplified-configuration-for-wcf-services.md)」 (WCF サービスの簡易構成) を参照してください。  
  
```xml  
<configuration>  
  
  <appSettings>  
    <!-- use appSetting to configure base address provided by host -->  
    <add key="baseAddress" value="http://localhost:8000/servicemodelsamples/service" />  
  </appSettings>  
  
  <system.serviceModel>  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
  </system.serviceModel>  
  
</configuration>  
```
