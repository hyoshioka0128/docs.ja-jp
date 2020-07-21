---
title: POCO サポート
ms.date: 03/30/2017
ms.assetid: 3846ca73-2819-4ca2-8367-dc739dde5a5b
ms.openlocfilehash: a9f8d185c58b22e68f7a8c11954e0e534c4bd48f
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600465"
---
# <a name="poco-support"></a>POCO サポート
このサンプルでは、マークされていない型 (シリアル化属性が適用されていない型で、POCO (Plain Old CLR Object) 型と呼ばれる場合もあります) のシリアル化のサポートについて説明します。 は、 <xref:System.Runtime.Serialization.DataContractSerializer> パラメーターなしのコンストラクターを持つ、すべてのパブリックのマークされていない型のデータコントラクトを推論します。 データ コントラクトを使用すると、サービスと構造化データをやり取りできます。 マークが付いていない型の詳細については、「 [Serializable 型](../feature-details/serializable-types.md)」を参照してください。  
  
 このサンプルは[はじめに](getting-started-sample.md)に基づいていますが、プリミティブな数値型ではなく複素数を使用します。 また、属性と属性が使用されない点を除いて、[基本的なデータコントラクト](basic-data-contract.md)サンプルに似てい <xref:System.Runtime.Serialization.DataContractAttribute> <xref:System.Runtime.Serialization.DataMemberAttribute> ます。  
  
 サービスはインターネット インフォメーション サービス (IIS) によってホストされています。クライアントはコンソール アプリケーション (.exe) です。  
  
> [!NOTE]
> このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。  
  
 `ComplexNumber` クラスは、`ServiceContract` で使用されます。 次のサンプル コードに示すように、`ComplexNumber` 型には、<xref:System.Runtime.Serialization.DataContractAttribute> 属性と <xref:System.Runtime.Serialization.DataMemberAttribute> 属性がありません。 既定では、パブリック プロパティとパブリック フィールドはすべてシリアル化されます。  
  
```csharp
public class ComplexNumber  
{  
    public double Real;  
    public double Imaginary;  
    public ComplexNumber()  
    {  
        Real = double.MinValue;  
        Imaginary = double.MinValue;  
    }  
    public ComplexNumber(double real, double imaginary)  
    {  
        this.Real = real;  
        this.Imaginary = imaginary;  
    }  
}  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには  
  
1. [Windows Communication Foundation サンプルの1回限りのセットアップ手順](one-time-setup-procedure-for-the-wcf-samples.md)を実行したことを確認します。  
  
2. ソリューションの C# 版または Visual Basic .NET 版をビルドするには、「 [Building the Windows Communication Foundation Samples](building-the-samples.md)」の手順に従います。  
  
3. サンプルを単一コンピューター構成または複数コンピューター構成で実行するには、「 [Windows Communication Foundation サンプルの実行](running-the-samples.md)」の手順に従います。  
  
> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は、 [Windows Communication Foundation (wcf) および Windows Workflow Foundation (WF) のサンプルの .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459)にアクセスして、すべての WINDOWS COMMUNICATION FOUNDATION (wcf) とサンプルをダウンロードして [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ください。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Data\POCO`  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute>
- [シリアル化可能な型](../feature-details/serializable-types.md)
