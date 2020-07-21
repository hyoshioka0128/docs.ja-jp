---
title: <serviceHostingEnvironment>
ms.date: 03/30/2017
ms.assetid: 4f8a7c4f-e735-4987-979a-b74fcdae2652
ms.openlocfilehash: 165dbed1b78d00f8d4dd3e482b9fee8a23db60da
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70399611"
---
# \<serviceHostingEnvironment>
この要素は、環境をホストするサービスがインスタンス化する特定のトランスポートの型を定義します。 この要素が空の場合は、既定の型が使用されます。 この要素は、アプリケーション レベルまたはコンピューター レベルの構成ファイルでのみ使用できます。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<serviceHostingEnvironment>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<serviceHostingEnvironment aspNetCompatibilityEnabled="Boolean"
                           minFreeMemoryPercentageToActivateService="Integer"
                           multipleSiteBindingsEnabled="Boolean">
  <baseAddressPrefixFilters>
    <add prefix="string" />
  </baseAddressPrefixFilters>
  <serviceActivations>
    <add factory="String"
         service="String" />
  </serviceActivations>
  <transportConfigurationTypes>
    <add name="String"
         transportConfigurationType="String" />
  </transportConfigurationTypes>
</serviceHostingEnvironment>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|aspNetCompatibilityEnabled|ASP.NET の互換モードが現在のアプリケーションに対して有効になっているかどうかを示すブール値。 既定値は、`false` です。<br /><br /> この属性がに設定されている場合 `true` 、Windows Communication Foundation (WCF) サービスへの要求は ASP.NET http パイプラインを通過し、http 以外のプロトコルでの通信は禁止されます。 詳細については、「 [WCF Services と ASP.NET](../../../wcf/feature-details/wcf-services-and-aspnet.md)」を参照してください。|  
|minFreeMemoryPercentageToActivateService|WCF サービスをアクティブ化する前に、システムで使用可能にする必要がある最小空きメモリ容量を指定する整数です。 **注意:** この属性を、WCF サービスの web.config ファイルで部分信頼と共に指定すると、 <xref:System.Security.SecurityException> サービスが実行されたときにが発生します。|  
|multipleSiteBindingsEnabled|1 つのサイトで複数の IIS バインディングが有効になっているかどうかを指定するブール値。<br /><br /> IIS は、仮想ディレクトリを含む仮想アプリケーションのコンテナーとしての Web サイトで構成されています。 サイト内のアプリケーションに、1 つ以上の IIS バインディングからアクセスできます。 IIS バインディングは、バインディング プロトコルとバインディング情報という 2 つの情報を提供します。 バインディング プロトコルは通信を行うスキームを定義するもので、バインディング情報はサイトにアクセスするために使用する情報です。 バインディング プロトコルの例には HTTP があり、一方、バインディング情報には IP アドレス、ポート、ホスト ヘッダーなどを含めることができます。<br /><br /> IIS ではサイトごとに複数の IIS バインディングを指定でき、これによりスキームごとに複数のベース アドレスをサポートできます。 ただし、サイトでホストされている Windows Communication Foundation (WCF) サービスでは、スキームごとに1つの baseAddress にしかバインドできません。<br /><br /> Windows Communication Foundation (WCF) サービス用にサイトごとに複数の IIS バインドを有効にするには、この属性をに設定 `true` します。 複数のサイト バインディングは HTTP プロトコルに対してのみサポートされています。 構成ファイル内のエンドポイントのアドレスには完全な URI を指定する必要があります。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<baseAddressPrefixFilters>](baseaddressprefixfilters.md)|サービス ホストによって使用されるベース アドレスのプレフィックス フィルターを指定する構成要素のコレクション。|  
|[\<serviceActivations>](serviceactivations.md)|アクティベーション設定を記述する構成セクション。|  
|[\<transportConfigurationTypes>](transportconfigurationtypes.md)|特定のトランスポートの型を識別する構成要素のコレクション。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|serviceModel|すべての Windows Communication Foundation (WCF) 構成要素のルート要素です。|  
  
## <a name="remarks"></a>解説  
 既定では、WCF サービスは、ホストされるアプリケーション ドメイン (AppDomain) で ASP.NET と並行で実行します。 WCF と ASP.NET が同じ AppDomain で共存できても、既定では WCF 要求は ASP.NET HTTP パイプラインでは処理されません。 結果として、ASP.NET アプリケーション プラットフォームのいくつかの要素は、WCF サービスでは使用できません。 次のような方法があります。  
  
- ASP.NET ファイル/URL 承認  
  
- ASP.NET の偽装  
  
- クッキー ベースのセッションの状態  
  
- HttpContext.Current  
  
- カスタム HttpModule を経由するパイプライン拡張  
  
 WCF サービスが ASP.NET のコンテキストで機能し、HTTP 経由でのみ通信する必要がある場合は、WCF の ASP.NET 互換モードを使用できます。 このモードは、`aspNetCompatibilityEnabled` 属性がアプリケーション レベルで `true` に設定されている場合に有効です。 サービス実装では、<xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> クラスを使用して互換モードで実行できる機能を宣言する必要があります。 互換モードが有効な場合、  
  
- ASP.NET ファイル/URL 承認が、WCF 承認の前に強制的に実行されます。 承認決定は、要求のトランスポート レベルの ID に基づいています。 メッセージ レベルでの ID は、無視されます。  
  
- WCF サービス操作は、ASP.NET の偽装コンテキストで実行を開始します。 ASP.NET の偽装と WCF の偽装の両方が特定のサービスで有効な場合は、WCF の偽装コンテキストが適用されます。  
  
- HttpContext.Current を WCF サービス コードから使用できるため、サービスは非 HTTP エンドポイントを公開しません。  
  
- WCF 要求は、ASP.NET パイプラインによって処理されます。 受信要求を処理するように構成された HttpModules は、WCF 要求も処理できます。 これらには、ASP.NET プラットフォーム コンポーネント (<xref:System.Web.SessionState.SessionStateModule> など) とカスタム サードパーティ モジュールが含まれます。  
  
## <a name="example"></a>例  
 次のコード サンプルは、ASP 互換モードを有効にする方法を示します。  
  
## <a name="code"></a>コード  
  
```xml  
<serviceHostingEnvironment aspNetCompatibilityEnabled="true"/>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>
- <xref:System.ServiceModel.ServiceHostingEnvironment>
- [ホスティング](../../../wcf/feature-details/hosting.md)
- [WCF サービスと ASP.NET](../../../wcf/feature-details/wcf-services-and-aspnet.md)
