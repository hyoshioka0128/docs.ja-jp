---
title: エラーの定義と指定
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- handling faults [WCF], specifying
- handling faults [WCF], defining
ms.assetid: c00c84f1-962d-46a7-b07f-ebc4f80fbfc1
ms.openlocfilehash: 10fc045cab995cca8d78e470d74ec9341e167308
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176696"
---
# <a name="defining-and-specifying-faults"></a>エラーの定義と指定
SOAP エラーを使用する目的は、エラー状態情報をサービスからクライアントに伝達し、双方向のシナリオでは、相互利用が可能な手段でクライアントからサービスにも伝達することです。 ここでは、カスタムのエラー コンテンツをいつどのように定義し、そのエラーを返す操作をどのように指定するかについて説明します。 サービスまたは双方向クライアントがそれらの障害を送信する方法、およびクライアントまたはサービス アプリケーションがこれらの障害を処理する方法の詳細については、「エラーの[送受信](sending-and-receiving-faults.md)」を参照してください。 Wcf (Windows 通信基盤) アプリケーションでのエラー処理の概要については、「[コントラクトとサービスでのエラーの指定と処理](specifying-and-handling-faults-in-contracts-and-services.md)」を参照してください。  
  
## <a name="overview"></a>概要  
 宣言された SOAP エラーは、カスタム SOAP エラーの種類を指定する <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType> を含む操作で発生します。 宣言されていない SOAP エラーとは、操作のコントラクトに指定されていないエラーです。 ここでは、各種のエラー状態を特定したうえで、サービスに関するエラー コントラクトを作成する方法について説明します。クライアントは、カスタムの SOAP エラーから通知を受けたときに、これらを使用することでエラーを適切に処理できます。 基本的なタスクは、次の順序で行います。  
  
1. サービスのクライアントに通知する必要があるエラー状態を定義します。  
  
2. そのエラー状態に対して SOAP エラーのカスタム コンテンツを定義します。  
  
3. 操作でスローされた特定の SOAP エラーがクライアントに公開されるように、WSDL でその操作にマークします。  
  
### <a name="defining-error-conditions-that-clients-should-know-about"></a>クライアントに通知する必要があるエラー状態の定義  
 SOAP エラーは、特定の操作に関するフォールト情報を伝達するためにパブリックに記述されたメッセージです。 これらのメッセージは、WSDL で他の操作メッセージと共に記述されているので、クライアントは、操作を呼び出した時点でこのようなエラー処理を予測できます。 しかし、WCF サービスはマネージ コードで記述されているため、マネージ コードのどのエラー条件をエラーに変換してクライアントに返すかを決定すると、サービスのエラー条件とバグを正式なエラーから分離する機会が得られます。クライアントとの会話。  
  
 たとえば、次のコード例には、2 つの整数を受け取り、別の整数を返す操作があります。 ここではいくつかの例外がスローされる可能性があります。そのため、エラー コントラクトを設計するときに、クライアントにとって重要なエラー状態を判別する必要があります。 この場合、サービスでは <xref:System.DivideByZeroException?displayProperty=nameWithType> 例外を検出する必要があります。  
  
```csharp  
[ServiceContract]  
public class CalculatorService  
{  
    [OperationContract]
    int Divide(int a, int b)  
    {  
      if (b==0) throw new Exception("Division by zero!");  
      return a/b;  
    }  
}  
```  
  
```vb
<ServiceContract> _
Public Class CalculatorService
    <OperationContract> _
    Public Function Divide(a As Integer, b As Integer) As Integer
        If b = 0 Then Throw New DivideByZeroException("Division by zero!")
        Return a / b
    End Function
End Class
```
  
 この例で操作から返せるエラーには、ゼロによる除算に特化したカスタム SOAP エラー、ゼロ除算に特化した情報が算術演算に特化したエラーに含まれているもの、複数の異なるエラー状態に対する複数のエラーなどがあります。SOAP エラーを返さないことも選択できます。  
  
### <a name="define-the-content-of-error-conditions"></a>エラー状態のコンテンツの定義  
 意義のあるカスタム SOAP エラーを返すエラー状態を特定したら、次の手順では、そのエラーのコンテンツを定義し、コンテンツ構造をシリアル化できるようにします。 前のセクションのコード例では、`Divide` 演算に特化したエラーを示していました。しかし、`Calculator` サービスに他の演算がある場合、1 つのカスタム SOAP エラーで、`Divide` を含むすべての電卓エラー状態をクライアントに通知することも可能です。 次のコード例では、`MathFault` を含むすべての算術演算で生成されたエラーを報告するためのカスタム SOAP エラー `Divide` を作成しています。 このクラスでは、操作 (`Operation` プロパティ) と問題を説明する値 (`ProblemType` プロパティ) を指定できますが、カスタム SOAP エラーでクライアントに転送するには、クラスとこれらのプロパティがシリアル化可能である必要があります。 このため、<xref:System.Runtime.Serialization.DataContractAttribute?displayProperty=nameWithType> 属性と <xref:System.Runtime.Serialization.DataMemberAttribute?displayProperty=nameWithType> 属性を使用して、型とそのプロパティをシリアル化可能にし、できる限り相互運用可能にします。  
  
 [!code-csharp[Faults#2](../../../samples/snippets/csharp/VS_Snippets_CFX/faults/cs/service.cs#2)]
 [!code-vb[Faults#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faults/vb/service.vb#2)]  
  
 データをシリアル化可能にする方法の詳細については、「サービス[コントラクトでのデータ転送の指定](./feature-details/specifying-data-transfer-in-service-contracts.md)」を参照してください。 提供するシリアル化サポートの一覧については、「[データ コントラクト シリアライザーでサポートされる型](./feature-details/types-supported-by-the-data-contract-serializer.md)」を参照してください。 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>  
  
### <a name="mark-operations-to-establish-the-fault-contract"></a>エラー コントラクトを確立するための操作のマーク  
 カスタム SOAP エラーの一部として返されるシリアル化可能なデータ構造を定義したら、最後に、その型の SOAP エラーをスローできることを操作コントラクトにマークします。 これには、<xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType> 属性を使用して、作成したカスタム データ型の型を渡します。 <xref:System.ServiceModel.FaultContractAttribute> 属性を使用して、`Divide` 操作で `MathFault` 型の SOAP エラーを返すように指定する方法を次のコード例に示します。 他の算術に関する操作でも、`MathFault` を返せるように指定できます。  
  
 [!code-csharp[Faults#1](../../../samples/snippets/csharp/VS_Snippets_CFX/faults/cs/service.cs#1)]
 [!code-vb[Faults#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faults/vb/service.vb#1)]  
  
 操作に複数の <xref:System.ServiceModel.FaultContractAttribute> 属性をマークすることによって、その操作で複数のカスタム エラーを返すことを指定できます。  
  
 次の手順では、操作の実装で障害コントラクトを実装する方法について、トピック「[送信および受信障害](sending-and-receiving-faults.md)」で説明します。  
  
#### <a name="soap-wsdl-and-interoperability-considerations"></a>SOAP、WSDL、相互運用性に関する考慮事項  
 特に他のプラットフォームと相互運用するときなど、状況によっては、SOAP メッセージでエラーを表す方法または WSDL メタデータでエラーを記述する方法を制御することが重要な場合があります。  
  
 <xref:System.ServiceModel.FaultContractAttribute> 属性の <xref:System.ServiceModel.FaultContractAttribute.Name%2A> プロパティを使用すると、エラーに対してメタデータで生成される WSDL エラー要素名を制御できます。  
  
 SOAP 標準に従って、エラーには、`Action`、`Code`、および `Reason` を指定することができます。 `Action` は、<xref:System.ServiceModel.FaultContractAttribute.Action%2A> プロパティによって制御されます。 <xref:System.ServiceModel.FaultException.Code%2A> プロパティと <xref:System.ServiceModel.FaultException.Reason%2A> プロパティは、ジェネリック <xref:System.ServiceModel.FaultException?displayProperty=nameWithType> の親クラスである <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType> クラスのプロパティです。 `Code` プロパティには、<xref:System.ServiceModel.FaultCode.SubCode%2A> メンバーが含まれています。  
  
 エラーを生成する非サービスを利用する場合には、特定の制限事項があります。 WCF は、スキーマが記述し、データ コントラクトと互換性がある詳細な型のエラーのみをサポートします。 たとえば、前述のように、WCF は詳細の種類で XML 属性を使用するエラー、または詳細セクションで複数の最上位要素を持つフォールトをサポートしていません。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.FaultContractAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- [コントラクトおよびサービスのエラーの指定と処理](specifying-and-handling-faults-in-contracts-and-services.md)
- [エラーの送受信](sending-and-receiving-faults.md)
- [方法: サービス コントラクトでのエラーを宣言する](how-to-declare-faults-in-service-contracts.md)
- [保護レベルの理解](understanding-protection-level.md)
- [方法: ProtectionLevel プロパティを設定する](how-to-set-the-protectionlevel-property.md)
- [Specifying Data Transfer in Service Contracts](./feature-details/specifying-data-transfer-in-service-contracts.md)
