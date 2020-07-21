---
title: ICLRAppDomainResourceMonitor::GetCurrentSurvived メソッド
ms.date: 03/30/2017
api_name:
- ICLRAppDomainResourceMonitor.GetCurrentSurvived
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAppDomainResourceMonitor::GetCurrentSurvived
helpviewer_keywords:
- ICLRAppDomainResourceMonitor::GetCurrentSurvived method [.NET Framework hosting]
- GetCurrentSurvived method [.NET Framework hosting]
ms.assetid: 392e9009-40ef-40e3-ad4d-7ce93a989e78
topic_type:
- apiref
ms.openlocfilehash: a73c0731c79dea3a0c411fe27a864ec9ac4e20b2
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616022"
---
# <a name="iclrappdomainresourcemonitorgetcurrentsurvived-method"></a>ICLRAppDomainResourceMonitor::GetCurrentSurvived メソッド
最後の完全なブロッキングガベージコレクションの後に残った、現在のアプリケーションドメインによって参照されているバイト数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT STDMETHODCALLTYPE GetCurrentSurvived(  
             [in]  DWORD dwAppDomainId,  
             [out] ULONGLONG *pAppDomainBytesSurvived,  
             [out] ULONGLONG *pTotalBytesSurvived);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwAppDomainId`  
 から要求されたアプリケーションドメインの ID。  
  
 `pAppDomainBytesSurvived`  
 入出力このアプリケーションドメインによって保持されている最後のガベージコレクションの後に残ったバイト数へのポインター。 完全なコレクションの後、この数値は正確で完全になります。 短期コレクションの後、この数値は不完全になる可能性があります。 このパラメーターは、`null` に設定できます。  
  
 `pRuntimeBytesSurvived`  
 入出力最後のガベージコレクションから残された合計バイト数へのポインター。 完全なコレクションの後、この数値はマネージヒープに保持されているバイト数を表します。 短期コレクションの後、この数は短期のジェネレーションでライブに保持されているバイト数を表します。 このパラメーターは、`null` に設定できます。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|COR_E_APPDOMAINUNLOADED|アプリケーションドメインがアンロードされているか、または存在しません。|  
  
## <a name="remarks"></a>解説  
 統計は、完全なブロッキングガベージコレクションの後にのみ更新されます。つまり、コレクションの実行中にアプリケーションを停止する、すべてのジェネレーションを含むコレクションです。 たとえば、 <xref:System.GC.Collect?displayProperty=nameWithType> メソッドオーバーロードは、完全なブロッキングコレクションを実行します。 同時実行ガベージコレクションはバックグラウンドで発生し、アプリケーションをブロックしません。  
  
 `GetCurrentSurvived`メソッドは、マネージプロパティに対応するアンマネージド <xref:System.AppDomain.MonitoringSurvivedMemorySize%2A?displayProperty=nameWithType> プロパティです。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRAppDomainResourceMonitor インターフェイス](iclrappdomainresourcemonitor-interface.md)
- [アプリケーションドメインのリソース監視](../../../standard/garbage-collection/app-domain-resource-monitoring.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
