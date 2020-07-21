---
title: My.WebServices オブジェクト
ms.date: 07/20/2015
f1_keywords:
- My.WebServices
- My.MyProject.WebServices
helpviewer_keywords:
- My.WebServices object
ms.assetid: f188dc05-2c75-41b6-bb68-122d1c3110a2
ms.openlocfilehash: a52f9f5f5b044273a45da5ef9478e2212def57a5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84372363"
---
# <a name="mywebservices-object"></a>My.WebServices オブジェクト
現在のプロジェクトによって参照される各 XML Web サービスの単一のインスタンスを作成してアクセスするためのプロパティを提供します。  
  
## <a name="remarks"></a>Remarks  
 `My.WebServices` オブジェクトは、現在のプロジェクトにより参照されている各 Web サービスのインスタンスを提供します。 各インスタンスは要求に応じてインスタンス化されます。 これらの Web サービスには `My.WebServices` オブジェクトのプロパティを介してアクセスできます。 プロパティの名前は、プロパティがアクセスする Web サービスの名前と同じになります。 <xref:System.Web.Services.Protocols.SoapHttpClientProtocol> から継承されたクラスはすべて Web サービスです。 プロジェクトへの Web サービスの追加の詳細については、「[アプリケーションの Web サービスへのアクセス](../../developing-apps/programming/accessing-application-web-services.md)」を参照してください。  
  
 `My.WebServices` オブジェクトでは、現在のプロジェクトに関連付けられている Web サービスのみが公開されます。 参照されている DLL で宣言されている Web サービスへのアクセスは提供されません。 DLL で提供されている Web サービスにアクセスするには、Web サービスの修飾名を *DllName*.*WebServiceName* の形式で使用する必要があります。 詳細については、「[アプリケーションの Web サービスへのアクセス](../../developing-apps/programming/accessing-application-web-services.md)」を参照してください。  
  
 オブジェクトとそのプロパティは、Web アプリケーションで使用できません。  
  
## <a name="properties"></a>プロパティ  
 `My.WebServices` オブジェクトの各プロパティにより、現在のプロジェクトで参照されている Web サービスのインスタンスにアクセスできます。 プロパティの名前は、プロパティがアクセスする Web サービスの名前と同じになり、プロパティの型は Web サービスの型と同じになります。  
  
> [!NOTE]
> 名前の競合がある場合、Web サービスにアクセスするためのプロパティ名は、*RootNamespace*_*Namespace*\_*ServiceName* になります。 たとえば、`Service1` という名前の 2 つの Web サービスがあるとします。 これらのサービスのいずれかがルート名前空間 `WindowsApplication1` および名前空間 `Namespace1` にある場合は、`My.WebServices.WindowsApplication1_Namespace1_Service1` を使用してそのサービスにアクセスします。  
  
 `My.WebServices` オブジェクトのいずれかのプロパティに初めてアクセスすると、Web サービスの新しいインスタンスが作成され、保存されます。 そのプロパティのその後のアクセスでは、Web サービスのインスタンスが返されます。  
  
 Web サービスを破棄するには、Web サービスのプロパティに `Nothing` を割り当てます。 プロパティ セッターによって、格納されている値に `Nothing` が割り当てられます。 プロパティに `Nothing` 以外の値を割り当てた場合、セッターが <xref:System.ArgumentException> 例外をスローします。  
  
 `My.WebServices` オブジェクトのプロパティに Web サービスのインスタンスが格納されているかどうかをテストするには、`Is` または `IsNot` 演算子を使用します。 これらの演算子を使用すると、プロパティの値が `Nothing` かどうかをチェックできます。  
  
> [!NOTE]
> 通常、`Is` または `IsNot` 演算子では、比較を実行するためにプロパティの値を読み取る必要があります。 ただし、プロパティに現在 `Nothing` が格納されている場合は、プロパティによって Web サービスの新しいインスタンスが作成され、そのインスタンスが返されます。 ただし、Visual Basic コンパイラでは、`My.WebServices` オブジェクトのプロパティが特別に処理されるため、`Is` または `IsNot` 演算子によって、値を変更せずにプロパティの状態をチェックできます。  
  
## <a name="example"></a>例  
 この例では、`TemperatureConverter` XML Web サービスの `FahrenheitToCelsius` メソッドを呼び出して、その結果を返しています。  
  
 [!code-vb[VbVbalrMyWebService#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyWebService/VB/Form1.vb#1)]  
  
 この例を機能させるには、プロジェクトで `Converter` という名前の Web サービスを参照し、その Web サービスで `ConvertTemperature` メソッドを公開している必要があります。 詳細については、「[アプリケーションの Web サービスへのアクセス](../../developing-apps/programming/accessing-application-web-services.md)」を参照してください。  
  
 このコードは、Web アプリケーション プロジェクトでは機能しません。  
  
## <a name="requirements"></a>必要条件  
  
### <a name="availability-by-project-type"></a>プロジェクトの種類別の可用性  
  
|プロジェクトの種類|使用可能|  
|---|---|  
|Windows アプリケーション|**はい**|  
|クラス ライブラリ|**はい**|  
|コンソール アプリケーション|**はい**|  
|Windows コントロール ライブラリ|**はい**|  
|Web コントロール ライブラリ|**はい**|  
|Windows サービス|**はい**|  
|Web サイト|いいえ|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Web.Services.Protocols.SoapHttpClientProtocol>
- <xref:System.ArgumentException>
- [アプリケーションの Web サービスへのアクセス](../../developing-apps/programming/accessing-application-web-services.md)
