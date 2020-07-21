---
title: <relativeBindForResources> 要素
ms.date: 03/30/2017
helpviewer_keywords:
- RelativeBindForResources element
- <relativeBindForResources> element
ms.assetid: 846ffa47-7257-4ce3-8cac-7ff627e0e34f
ms.openlocfilehash: cd49d424019a4e8422fee0ae16217d49cfc456b1
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153907"
---
# <a name="relativebindforresources-element"></a>\<relativeBindForResources> 要素
サテライト アセンブリのプローブを最適化します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<relativeBindForResources>**  
  
## <a name="syntax"></a>構文  
  
```xml
<relativeBindForResources
   enabled="true|false" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`enabled`|必須の属性です。<br /><br /> 共通言語ランタイムがサテライトアセンブリのプローブを最適化するかどうかを指定します。|  
  
## <a name="enabled-attribute"></a>enabled 属性  
  
|値|Description|  
|-----------|-----------------|  
|`false`|ランタイムは、サテライトアセンブリのプローブを最適化しません。 これが既定値です。|  
|`true`|ランタイムは、サテライトアセンブリのプローブを最適化します。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`runtime`|ランタイム初期化オプションに関する情報を含んでいます。|  
  
## <a name="remarks"></a>解説  
 一般に、リソースの[パッケージ化とデプロイ](../../../resources/packaging-and-deploying-resources-in-desktop-apps.md)に関するトピックで説明されているように、Resource Manager はリソースをプローブします。 これは、resource Manager が特定のローカライズされたバージョンのリソースをプローブするときに、グローバルアセンブリキャッシュを検索し、アプリケーションのコードベースでカルチャ固有のフォルダーを検索し、サテライトアセンブリの Windows インストーラーを照会して、イベントを発生させることができることを意味し <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> ます。 要素は、 `<relativeBindForResources>` リソースマネージャーがサテライトアセンブリをプローブする方法を最適化します。 次の条件下でリソースを調査するときにパフォーマンスを向上させることができます。  
  
- サテライトアセンブリがコードアセンブリと同じ場所に配置されている場合。 つまり、コードアセンブリがグローバルアセンブリキャッシュにインストールされている場合は、サテライトアセンブリもインストールする必要があります。 コードアセンブリがアプリケーションのコードベースにインストールされている場合は、サテライトアセンブリをコードベースのカルチャ固有のフォルダーにもインストールする必要があります。  
  
- Windows インストーラーが使用されていない場合、またはサテライトアセンブリのオンデマンドインストールではあまり使用されない場合。  
  
- アプリケーションコードがイベントを処理しない場合 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 。  
  
 `enabled`要素の属性 `<relativeBindForResources>` をに設定すると、次のように、 `true` サテライトアセンブリのリソースマネージャーのプローブが最適化されます。  
  
- 親コードアセンブリの場所を使用して、サテライトアセンブリをプローブします。  
  
- サテライトアセンブリの Windows インストーラーに対してはクエリを実行しません。  
  
- イベントは発生しません <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 。  
  
## <a name="see-also"></a>関連項目

- [リソースのパッケージ化と配置](../../../resources/packaging-and-deploying-resources-in-desktop-apps.md)
- [ランタイム設定スキーマ](index.md)
- [構成ファイル スキーマ](../index.md)
