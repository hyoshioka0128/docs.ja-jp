---
title: IHostAssemblyManager::GetNonHostStoreAssemblies メソッド
ms.date: 03/30/2017
api_name:
- IHostAssemblyManager.GetNonHostStoreAssemblies
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostAssemblyManager::GetNonHostStoreAssemblies
helpviewer_keywords:
- IHostAssemblyManager::GetNonHostStoreAssemblies method [.NET Framework hosting]
- GetNonHostStoreAssemblies method [.NET Framework hosting]
ms.assetid: d2250b38-c76a-40ce-80c8-ba45149886e8
topic_type:
- apiref
ms.openlocfilehash: 9a1440be7011130b16d7112ae15026eb74856190
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501595"
---
# <a name="ihostassemblymanagergetnonhoststoreassemblies-method"></a>IHostAssemblyManager::GetNonHostStoreAssemblies メソッド
ホストが読み込みのために共通言語ランタイム (CLR) を必要とするアセンブリのリストを表す[ICLRAssemblyReferenceList](iclrassemblyreferencelist-interface.md)へのインターフェイスポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetNonHostStoreAssemblies (  
    [out] ICLRAssemblyReferenceList **ppReferenceList  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppReferenceList`  
 入出力`ICLRAssemblyReferenceList`ホストが CLR を読み込むことを想定しているアセンブリへの参照の一覧を含むのアドレスへのポインター。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`GetNonHostStoreAssemblies`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_OUTOFMEMORY|要求されたの参照の一覧を作成するのに十分なメモリがありませんでした `ICLRAssemblyReferenceList` 。|  
  
## <a name="remarks"></a>解説  
 CLR は、次の一連のガイドラインを使用して参照を解決します。  
  
- まず、によって返されるアセンブリ参照の一覧を参照し `GetNonHostStoreAssemblies` ます。  
  
- アセンブリが一覧に表示されている場合、CLR は通常どおりにバインドします。  
  
- アセンブリが一覧に表示されず、ホストが[IHostAssemblyStore](ihostassemblystore-interface.md)の実装を提供した場合、CLR は[IHostAssemblyStore::P rovideassembly](ihostassemblystore-provideassembly-method.md)を呼び出して、バインド先のアセンブリをホストが指定できるようにします。  
  
- それ以外の場合、CLR はアセンブリへのバインドに失敗します。  
  
 ホストが null に設定されている場合、 `ppReferenceList` CLR はまずグローバルアセンブリキャッシュをプローブし、 `ProvideAssembly` を呼び出してから、アプリケーションベースをプローブしてアセンブリ参照を解決します。  
  
> [!NOTE]
> 初期化時に、CLR は `GetNonHostStoreAssemblies` 1 回だけを呼び出します。 メソッドが再度呼び出されていません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRAssemblyReferenceList インターフェイス](iclrassemblyreferencelist-interface.md)
- [IHostAssemblyManager インターフェイス](ihostassemblymanager-interface.md)
- [IHostAssemblyStore インターフェイス](ihostassemblystore-interface.md)
