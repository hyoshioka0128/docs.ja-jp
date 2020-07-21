---
title: <backupList>
ms.date: 03/30/2017
ms.assetid: a3d9d1f9-4a53-45e9-a880-86c8bee0b833
ms.openlocfilehash: 478211755b9131c03b72777ee95ff7223b9092c9
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70850276"
---
# \<backupList>
プライマリ エンドポイントに接続できないときにルーティング サービスで使用するエンドポイント セットを列挙したバックアップ リストを定義するための構成セクションを表します。 リストの最初のエンドポイントがダウンしていると、ルーティング サービスは自動的にリスト内で次にあるエンドポイントにフェールオーバーします。  これにより、クライアント アプリケーションに複雑なパターンの処理方法やサービスの配置場所を示すことなく、アプリケーションの信頼性を高めることができます。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<routing>**](routing.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<backupLists>**](backuplists.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<backupList>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<routing>
  <backupLists>
    <backupList name="String">
      <add endpointName="String" />
    </backupList>
  </backupLists>
</routing>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|name|このエンドポイント リストを指定するために使用される名前を指定する文字列。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<filter>](filter.md)||  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<routing>](routing.md)|バックアップ エンドポイントの一覧。|  
  
## <a name="remarks"></a>解説  
 このセクションには、プライマリ エンドポイントへの送信時に通信例外が発生した場合にメッセージが送信されるエンドポイントの、順序付けられたコレクションが含まれます。  
  
 の属性に示されているプライマリエンドポイントへの送信が `endpointName` [\<add>](add-of-entries.md) 通信例外で失敗した場合、ルーティングサービスは、この構成セクションの最初のエンドポイントにメッセージを送信しようとします。 これも通信例外によって失敗した場合、ルーティング サービスは、送信に成功するか、通信例外以外のエラーを返すか、コレクション内のすべてのエンドポイントがエラーを返すまで、このセクションに格納された次のエンドポイントにメッセージを送信しようとします。  
  
 次の例では、"Destination" という名前のプライマリエンドポイントへの送信で通信例外が返された場合、サービスは "alternateServiceQueue" にメッセージを送信しようとします。 この試行でも通信例外が返された場合、ルーティング サービスはコレクション内の次のエンドポイントにメッセージを送信しようとします。  
  
```xml  
<filterTables>
  <filterTable name="filterTable1">
    <add filterName="MatchAllFilter1"
         endpointName="Destination"
         backupList="backupEndpointList" />
  </filterTable>
</filterTables>
<backupLists>
  <backupList name="backupEndpointList">
    <add endpointName="backupServiceQueue" />
    <add endpointName="alternateServiceQueue" />
  </backupList>
</backupLists>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Routing.Configuration.BackupEndpointCollection?displayProperty=nameWithType>
