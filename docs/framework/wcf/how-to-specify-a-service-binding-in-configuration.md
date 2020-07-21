---
title: '方法: 構成でサービス バインディングを指定する'
description: 構成ファイルで WCF サービスのエンドポイントを構成する方法について説明します。 コントラクトは、サービスに対して定義され、クラスに実装されます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 885037f7-1c2b-4d7a-90d9-06b89be172f2
ms.openlocfilehash: 3b9dd12f2a28ae2d420e82013459613cee8140f1
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051949"
---
# <a name="how-to-specify-a-service-binding-in-configuration"></a>方法: 構成でサービス バインディングを指定する
この例では、簡単な電卓サービス用に `ICalculator` コントラクトを定義し、そのサービスを `CalculatorService` クラスで実装し、そのエンドポイントを Web.config ファイルで構成します。このファイルでは、サービスが <xref:System.ServiceModel.BasicHttpBinding> を使用するように指定します。 構成ではなくコードを使用してこのサービスを構成する方法の詳細については、「[方法: コード内でサービスバインディングを指定](how-to-specify-a-service-binding-in-code.md)する」を参照してください。  
  
 通常、ベスト プラクティスは、コードで命令として記述するよりも、構成でバインディングを指定して情報を明示的にアドレス指定することです。 設置済みサービスのバインドおよびアドレスは一般的に、サービスの開発中に使用されるものとは異なるので、コード内でエンドポイントを定義することは通常、実用的ではありません。 一般的に、バインディング情報とアドレス情報をコードに含めないことで、変更時にアプリケーションの再コンパイルや再展開を行う必要がなくなります。  
  
 次のすべての構成手順は、[構成エディターツール (SvcConfigEditor.exe)](configuration-editor-tool-svcconfigeditor-exe.md)を使用して実行できます。  
  
 この例のソースコピーについては、「 [Basicbinding](./samples/basicbinding.md)」を参照してください。  
  
## <a name="to-specify-the-basichttpbinding-to-use-to-configure-the-service"></a>サービスの構成で BasicHttpBinding が使用されるように指定するには  
  
1. サービスの種類にサービス コントラクトを定義します。  
  
     [!code-csharp[C_HowTo_ConfigureServiceBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureservicebinding/cs/source.cs#1)]
     [!code-vb[C_HowTo_ConfigureServiceBinding#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_configureservicebinding/vb/source.vb#1)]  
  
2. サービス クラスにサービス コントラクトを実装します。  
  
     [!code-csharp[C_HowTo_ConfigureServiceBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureservicebinding/cs/source.cs#2)]
     [!code-vb[C_HowTo_ConfigureServiceBinding#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_configureservicebinding/vb/source.vb#2)]  
  
    > [!NOTE]
    > アドレス情報とバインディング情報は、サービスの実装内では指定されません。 また、構成ファイルからこの情報をフェッチするためのコードを記述する必要もありません。  
  
3. `CalculatorService` を使用する <xref:System.ServiceModel.WSHttpBinding> のエンドポイントを構成する Web.config ファイルを作成します。  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.serviceModel>  
        <services>  
          <service name=" CalculatorService" >  

            <!-- Leave the address blank to be populated by default -->
            <!-- from the hosting environment,in this case IIS, so -->
            <!-- the address will just be that of the IIS Virtual -->
            <!-- Directory. -->

            <!-- Specify the binding configuration name for that -->
            <!-- binding type. This is optional but useful if you -->
            <!-- want to modify the properties of the binding. -->
            <!-- The bindingConfiguration name Binding1 is defined -->
            <!-- below in the bindings element. -->
            <endpoint
                address=""
                binding="wsHttpBinding"  
                bindingConfiguration="Binding1"  
                contract="ICalculator" />  
          </service>  
        </services>  
        <bindings>  
          <wsHttpBinding>  
            <binding name="Binding1">  
              <!-- Binding property values can be modified here. -->  
              <!-- See the next procedure. -->  
            </binding>  
          </wsHttpBinding>  
       </bindings>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
4. 次の行を含む Service.svc ファイルを作成し、インターネット インフォメーション サービス (IIS: Internet Information Services) 仮想ディレクトリに配置します。  
  
    ```aspx-csharp
    <%@ServiceHost language=c# Service="CalculatorService" %>
    ```  
  
## <a name="to-modify-the-default-values-of-the-binding-properties"></a>バインディング プロパティの既定値を変更するには  
  
1. の既定のプロパティ値の1つを変更するには、 <xref:System.ServiceModel.WSHttpBinding> 要素内に新しいバインド構成名を作成 `<binding name="Binding1">` [\<wsHttpBinding>](../configure-apps/file-schema/wcf/wshttpbinding.md) し、このバインド要素でバインディングの属性の新しい値を設定します。 たとえば、開く操作と閉じる操作の既定のタイムアウト値を 1 分から 2 分に変更するには、構成ファイルに以下を追加します。  
  
    ```xml  
    <wsHttpBinding>  
      <binding name="Binding1"  
               closeTimeout="00:02:00"  
               openTimeout="00:02:00">  
      </binding>  
    </wsHttpBinding>  
    ```  
  
## <a name="see-also"></a>関連項目

- [サービスとクライアントを構成するためのバインディングの使用](using-bindings-to-configure-services-and-clients.md)
- [エンドポイント アドレスの指定](specifying-an-endpoint-address.md)
