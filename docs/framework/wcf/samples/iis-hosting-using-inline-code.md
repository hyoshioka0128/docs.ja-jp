---
title: インライン コードを使用した IIS ホスティング
ms.date: 03/30/2017
helpviewer_keywords:
- Web hosted service
- IIS Hosting Using Inline Code Sample [Windows Communication Foundation]
ms.assetid: 56fe3687-a34b-4661-8e30-b33770f413fa
ms.openlocfilehash: 47d056e35b92654c8e47647c7273c5d69b37bd97
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594648"
---
# <a name="iis-hosting-using-inline-code"></a>インライン コードを使用した IIS ホスティング

このサンプルでは、インターネット インフォメーション サービス (IIS) によってホストされるサービスを実装する方法を示します。サービス コードは .svc ファイルにインラインで含まれており、必要に応じてコンパイルされます。 サービス コードは、アプリケーションの \App_Code ディレクトリにあるソース コード ファイルに直接実装するか、または \bin に配置されるアセンブリにコンパイルすることもできます。 ただし、このサンプルではこれらの手法は示しません。

> [!NOTE]
> このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> このディレクトリが存在しない場合は、 [Windows Communication Foundation (wcf) および Windows Workflow Foundation (WF) のサンプルの .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459)にアクセスして、すべての WINDOWS COMMUNICATION FOUNDATION (wcf) とサンプルをダウンロードして [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ください。 このサンプルは、次のディレクトリに格納されます。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WebHost\InlineCode`

このサンプルでは、要求/応答通信パターンを定義するコントラクトを実装する一般的なサービスを示します。 このサービスは IIS によってホストされ、サービス コードは Service.svc ファイルに完全に含まれています。 サービスはホストによってアクティブ化され、このサービスに最初に送信されるメッセージによって必要に応じてコンパイルされます。 あらかじめコンパイルしておく必要はありません。 サービスは、次に示すコードで定義される `ICalculator` コントラクトを実装します。

```csharp
// Define a service contract.
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
    public interface ICalculator
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

このサービス実装は、計算を行い、結果を返します。

`<%@ServiceHost language=c# Debug="true" Service="Microsoft.ServiceModel.Samples.CalculatorService" %>`

```csharp
// Service class that implements the service contract.
public class CalculatorService : ICalculator
{
    public double Add(double n1, double n2)
    {
        return n1 + n2;
    }
    public double Subtract(double n1, double n2)
    {
        return n1 - n2;
    }
    public double Multiply(double n1, double n2)
    {
        return n1 * n2;
    }
    public double Divide(double n1, double n2)
    {
        return n1 / n2;
    }
}
```

このサンプルを実行すると、操作要求および応答がクライアントのコンソール ウィンドウに表示されます。 クライアントをシャットダウンするには、クライアント ウィンドウで Enter キーを押します。

```console
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714

Press <ENTER> to terminate client.
```

### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには

1. [Windows Communication Foundation サンプルの1回限りのセットアップ手順](one-time-setup-procedure-for-the-wcf-samples.md)を実行したことを確認します。

2. ソリューションの C# 版または Visual Basic .NET 版をビルドするには、「 [Building the Windows Communication Foundation Samples](building-the-samples.md)」の手順に従います。

3. ソリューションがビルドされたら、setup.exe を実行して IIS 7.0 で ServiceModelSamples アプリケーションを設定します。 これで、ServiceModelSamples ディレクトリが IIS 7.0 アプリケーションとして表示されます。

4. サンプルを単一コンピューター構成または複数コンピューター構成で実行するには、「 [Windows Communication Foundation サンプルの実行](running-the-samples.md)」の手順に従います。 このサービスを呼び出すことができるクライアントアプリケーションを作成する方法の例については、「[方法: クライアントを作成](../how-to-create-a-wcf-client.md)する」を参照してください。

## <a name="see-also"></a>関連項目

- [AppFabric のホストおよび永続化のサンプル](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))
