---
title: サービス コントラクトの実装
ms.date: 03/30/2017
helpviewer_keywords:
- implementing service contracts [WCF]
ms.assetid: aefb6f56-47e3-4f24-ab0a-9bc07bf9885f
ms.openlocfilehash: aefe146a8941d98d7d9138e4ece83c330c967034
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79184000"
---
# <a name="implementing-service-contracts"></a>サービス コントラクトの実装
サービスは、1 つ以上のエンドポイントでクライアントが使用できる機能を公開するクラスです。 サービスを作成するには、WCF (WCF) コントラクトを実装するクラスを記述します。 2 つの方法のいずれかでこれを行うことができます。 コントラクトを個別にインターフェイスとして定義し、そのインターフェイスを実装するクラスを作成できます。 または、クラスに <xref:System.ServiceModel.ServiceContractAttribute> 属性を配置し、サービスのクライアントが使用できるメソッドに <xref:System.ServiceModel.OperationContractAttribute> 属性を配置することによって、クラスとコントラクトを直接作成することもできます。  
  
## <a name="creating-a-service-class"></a>サービス クラスの作成  
 個別に定義された `IMath` コントラクトを実装するサービスの例を次に示します。  
  
```csharp  
// Define the IMath contract.  
[ServiceContract]  
public interface IMath  
{  
    [OperationContract]
    double Add(double A, double B);  
  
    [OperationContract]  
    double Multiply (double A, double B);  
}  
  
// Implement the IMath contract in the MathService class.  
public class MathService : IMath  
{  
    public double Add (double A, double B) { return A + B; }  
    public double Multiply (double A, double B) { return A * B; }  
}  
```  
  
 また、サービスは直接コントラクトを公開できます。 `MathService` コントラクトを定義し、実装するサービス クラスの例を次に示します。  
  
```csharp  
// Define the MathService contract directly on the service class.  
[ServiceContract]  
class MathService  
{  
    [OperationContract]  
    public double Add(double A, double B) { return A + B; }  
    [OperationContract]  
    private double Multiply (double A, double B) { return A * B; }  
}  
```  
  
 コントラクト名が異なるので、上記の 2 つのサービスが公開するコントラクトはそれぞれ異なります。 最初の例では、公開されるコントラクトの名前が "`IMath`" であるのに対し、2 番目の例では、コントラクトの名前は "`MathService`" です。  
  
 コンカレンシーやインスタンス化など、いくつかの項目は、サービス実装レベルと操作実装レベルで設定できます。 詳細については、「[サービスの設計と実装](designing-and-implementing-services.md)」を参照してください。  
  
 サービス コントラクトを実装したら、そのサービスに 1 つ以上のエンドポイントを作成する必要があります。 詳細については、「[エンドポイントの作成の概要](endpoint-creation-overview.md)」を参照してください。 サービスの実行方法の詳細については、「 サービスの[ホスティング](hosting-services.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [サービスの設計と実装](designing-and-implementing-services.md)
- [方法 : コントラクト クラスを使用してサービスを作成する](./feature-details/how-to-create-a-wcf-contract-with-a-class.md)
- [方法 : コントラクト インターフェイスを使用してサービスを作成する](./feature-details/how-to-create-a-service-with-a-contract-interface.md)
- [サービスのランタイム動作の指定](specifying-service-run-time-behavior.md)
