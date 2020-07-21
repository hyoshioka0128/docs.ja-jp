---
title: ICLRAppDomainResourceMonitor インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRAppDomainResourceMonitor
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAppDomainResourceMonitor
helpviewer_keywords:
- ICLRAppDomainResourceMonitor interface [.NET Framework hosting]
ms.assetid: 72fa83a1-8997-41d7-b355-ab177a24a303
topic_type:
- apiref
ms.openlocfilehash: 08dc0f0891d960cb7b402b30455e606aaff7bcea
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616009"
---
# <a name="iclrappdomainresourcemonitor-interface"></a>ICLRAppDomainResourceMonitor インターフェイス
アプリケーションドメインのメモリおよび CPU 使用率を検査するメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetCurrentAllocated メソッド](iclrappdomainresourcemonitor-getcurrentallocated-method.md)|アプリケーションドメインが作成されてからアプリケーションドメインによって行われたすべてのメモリ割り当ての合計サイズ (バイト単位) を取得します。ガベージコレクトされたメモリは減算されません。|  
|[GetCurrentSurvived メソッド](iclrappdomainresourcemonitor-getcurrentsurvived-method.md)|最後の完全なブロッキングガベージコレクションの後に残った、現在のアプリケーションドメインによって参照されているバイト数を取得します。|  
|[GetCurrentCpuTime メソッド](iclrappdomainresourcemonitor-getcurrentcputime-method.md)|アプリケーションドメインが作成されてから、現在のアプリケーションドメインでの実行中にすべてのスレッドによって使用された合計プロセッサ時間を取得します。|  
  
## <a name="remarks"></a>解説  
 インターフェイスには、 `ICLRAppDomainResourceMonitor` 次のマネージプロパティと同様の機能が用意されています。  
  
- <xref:System.AppDomain.MonitoringIsEnabled%2A?displayProperty=nameWithType>  
  
- <xref:System.AppDomain.MonitoringTotalProcessorTime%2A?displayProperty=nameWithType>  
  
- <xref:System.AppDomain.MonitoringTotalAllocatedMemorySize%2A?displayProperty=nameWithType>  
  
- <xref:System.AppDomain.MonitoringSurvivedProcessMemorySize%2A?displayProperty=nameWithType>  
  
- <xref:System.AppDomain.MonitoringSurvivedMemorySize%2A?displayProperty=nameWithType>  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [\<appDomainResourceMonitoring> 要素](../../configure-apps/file-schema/runtime/appdomainresourcemonitoring-element.md)
- [アプリケーションドメインのリソース監視](../../../standard/garbage-collection/app-domain-resource-monitoring.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
