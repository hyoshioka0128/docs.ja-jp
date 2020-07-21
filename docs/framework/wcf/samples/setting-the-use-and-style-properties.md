---
title: 使用プロパティとスタイル プロパティのサンプルの設定
ms.date: 03/30/2017
ms.assetid: c09a0600-116f-41cf-900a-1b7e4ea4e300
ms.openlocfilehash: f400c0bc08588afa951ae33f221663b47b37602c
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79144033"
---
# <a name="setting-the-use-and-style-properties"></a>Use および Style プロパティの設定

このサンプルでは、<xref:System.ServiceModel.XmlSerializerFormatAttribute> と <xref:System.ServiceModel.DataContractFormatAttribute> で Use および Style プロパティを使用する方法を示します。 これらのプロパティは、メッセージの書式設定の方法を制御します。 既定では、メッセージの本文は、<xref:System.ServiceModel.OperationFormatStyle.Document> に設定されたスタイルを使用して書式設定されます。 こうした設定は、サービス コントラクト レベルと操作コントラクト レベルのどちらのレベルでも指定できます。

> [!NOTE]
> このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。

<xref:System.ServiceModel.DataContractFormatAttribute.Style%2A> スタイル プロパティは、サービスの WSDL メタデータの書式設定を決定します。 使用可能な値は <xref:System.ServiceModel.OperationFormatStyle.Document> と <xref:System.ServiceModel.OperationFormatStyle.Rpc> です。 RPC は、操作で交換されるメッセージの WSDL 表現がリモート プロシージャ コールである場合と同様のパラメータを含むことを意味します。 以下に例を示します。

```xml
<wsdl:message name="IUseAndStyleCalculator_Add_InputMessage">
  <wsdl:part name="n1" type="xsd:double"/>
  <wsdl:part name="n2" type="xsd:double"/>
</wsdl:message>
```

スタイルに対する <xref:System.ServiceModel.OperationFormatStyle.Document> への設定は、WSDL 表現には操作で交換されるドキュメントを表す単一の要素が含まれることを意味します。この例を次に示します。

```xml
<wsdl:message name="IUseAndStyleCalculator_Add_InputMessage">
  <wsdl:part name="parameters" element="tns:Add"/>
</wsdl:message>
```

<xref:System.ServiceModel.XmlSerializerFormatAttribute.Use%2A> プロパティは、メッセージの書式を決定します。 使用可能な値は <xref:System.ServiceModel.OperationFormatUse.Literal> と <xref:System.ServiceModel.OperationFormatUse.Encoded> で、既定値は <xref:System.ServiceModel.OperationFormatUse.Literal> です。 Literal は、メッセージが WSDL 内のスキーマのリテラル インスタンスであることを意味します。Document/Literal の例を次に示します。

```xml
<Add xmlns="http://Microsoft.ServiceModel.Samples">
  <n1>100</n1>
  <n2>15.99</n2>
</Add>
```

Encoded は、WSDL 内のスキーマが、SOAP 1.1 のセクション 5 に規定されているルールに従ってエンコードされる抽象仕様であることを意味します。 RPC/Encoded の例を次に示します。

```xml
<q1:Add xmlns:q1="http://Microsoft.ServiceModel.Samples">
  <n1 xsi:type="xsd:double" xmlns="">100</n1>
  <n2 xsi:type="xsd:double" xmlns="">15.99</n2>
</q1:Add>
```

WS-I Basic Profile 1.0 では <xref:System.ServiceModel.OperationFormatUse.Encoded> の使用が禁止されています。したがって、これを使用するのは従来のサービスで必要な場合に限ります。 `Encoded` メッセージ形式は、XmlSerializer を使用する場合にのみ利用可能です。

送受信されるメッセージを確認できるようにするため、このサンプルは[トレースとメッセージ ログ](tracing-and-message-logging.md)に基づいています。 サービス構成とソース コードは、トレースとメッセージ ログを有効化して利用できるように変更されています。 さらに、<xref:System.ServiceModel.WSHttpBinding> はセキュリティを無効にして構成されているので、ログに記録されたメッセージは暗号化されていない状態で表示できます。 結果として生成されるトレース ログ (System.ServiceModel.e2e および Message.log) は、[サービス トレース ビューアー ツール (SvcTraceViewer.exe) を](../service-trace-viewer-tool-svctraceviewer-exe.md)使用して表示する必要があります。 トレースは、C:\LOGS フォルダーに作成されるように構成されています。 サンプルを実行する前に、このフォルダーを作成します。 トレース ビューアー ツールでメッセージの内容を表示するには、ツールの左側と右側のペインで **[メッセージ**] を選択します。

次のコードでは、サービス コントラクトの <xref:System.ServiceModel.XmlSerializerFormatAttribute.Use%2A> プロパティが <xref:System.ServiceModel.OperationFormatUse> に設定され、メッセージ本文の形式が既定の <xref:System.ServiceModel.OperationFormatStyle> から <xref:System.ServiceModel.OperationFormatStyle.Document> に変更されています。

```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples"),
XmlSerializerFormat(Style = OperationFormatStyle.Rpc,
                                 Use = OperationFormatUse.Encoded)]
public interface IUseAndStyleCalculator
{
    [OperationContract]
    double Add(double n1, double n2);
    [OperationContract]
    double Subtract(double n1, double n2);
    [OperationContract]
    double Multiply(double n1, double n2);
    [OperationContract]
    double Divide(double n1, double n2);
}
```

それぞれの <xref:System.ServiceModel.XmlSerializerFormatAttribute.Use%2A> 設定と <xref:System.ServiceModel.XmlSerializerFormatAttribute.Style%2A> 設定との違いを示すには、これらの設定をサービス内で変更してクライアントを再生成し、サンプルを実行します。その後、サービス ビューア ツールを使用して c:\logs\message.logs ファイルを調べます。 また、 を表示`http://localhost/ServiceModelSamples/service.svc?wsdl`して、メタデータへの影響を観察します。 通常、サービスのメタデータは複数のページに分割されます。 メインの WSDL ページには WSDL バインディングが`http://localhost/ServiceModelSamples/service.svc?wsdl=wsdl0`含まれていますが、メッセージ定義を確認するためのビューが含まれています。

## <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには

1. [Windows コミュニケーションファウンデーション サンプルのワンタイム セットアップ手順を](one-time-setup-procedure-for-the-wcf-samples.md)実行したことを確認します。

2. メッセージのログ記録用に C:\LOGS ディレクトリを作成します。 ユーザー Network Service にそのディレクトリの書き込み権限を与えます。

3. ソリューションの C# 版または Visual Basic .NET 版をビルドするには、「 [Building the Windows Communication Foundation Samples](building-the-samples.md)」の手順に従います。

4. 単一または複数のコンピューターにまたがる構成でサンプルを実行するには[、「Windows コミュニケーション ファウンデーション サンプルの実行」の手順に](running-the-samples.md)従います。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Message\UseAndStyle`
