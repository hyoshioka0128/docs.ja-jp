---
title: IHostAssemblyManager::GetAssemblyStore メソッド
ms.date: 03/30/2017
api_name:
- IHostAssemblyManager.GetAssemblyStore
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostAssemblyManager::GetAssemblyStore
helpviewer_keywords:
- IHostAssemblyManager::GetAssemblyStore method [.NET Framework hosting]
- GetAssemblyStore method [.NET Framework hosting]
ms.assetid: d0f74593-9bb1-4a11-8096-e29734b20698
topic_type:
- apiref
ms.openlocfilehash: 587861529c340fad9fd817b904e4d3651b236e8d
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83805068"
---
# <a name="ihostassemblymanagergetassemblystore-method"></a>IHostAssemblyManager::GetAssemblyStore メソッド
ホストによって読み込まれたアセンブリの一覧を表す[IHostAssemblyStore](ihostassemblystore-interface.md)へのインターフェイスポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetAssemblyStore (  
    [out] IHostAssemblyStore **ppAssemblyStore  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppAssemblyStore`  
 入出力インスタンスへの関数ポインター `IHostAssemblyStore` 。ホストがを実装していない場合は null `IHostAssemblyStore` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`GetAssemblyStore`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_NOINTERFACE|ホストはの実装を提供していません `IHostAssemblyStore` 。|  
  
## <a name="remarks"></a>解説  
 `IHostAssemblyStore`ホストが CLR とは無関係にアセンブリおよびモジュールにバインドできるようにするメソッドを提供します。 通常、ホストはアセンブリストアを提供して、アセンブリをファイルシステム以外の形式から読み込むことができるようにします。  
  
> [!NOTE]
> ホストがを実装していない場合 `IHostAssemblyStore` 、は `GetAssemblyStore` E_NOINTERFACE の HRESULT 値を返し、を null に設定する必要があり `ppAssemblyStore` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IHostAssemblyManager インターフェイス](ihostassemblymanager-interface.md)
- [IHostAssemblyStore インターフェイス](ihostassemblystore-interface.md)
