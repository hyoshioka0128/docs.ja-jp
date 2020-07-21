---
title: ICLRAssemblyIdentityManager::GetCLRAssemblyReferenceList メソッド
ms.date: 03/30/2017
api_name:
- ICLRAssemblyIdentityManager.GetCLRAssemblyReferenceList
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyIdentityManager::GetCLRAssemblyReferenceList
helpviewer_keywords:
- GetClrAssemblyReferenceList method [.NET Framework hosting]
- ICLRAssemblyIdentityManager::GetCLRAssemblyReferenceList method [.NET Framework hosting]
ms.assetid: cb5ffae5-287b-4a87-9ca8-7ce3ae0601b7
topic_type:
- apiref
ms.openlocfilehash: 7f09cb2264b21fdfbc892069f2c2f0a963b131f8
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615970"
---
# <a name="iclrassemblyidentitymanagergetclrassemblyreferencelist-method"></a>ICLRAssemblyIdentityManager::GetCLRAssemblyReferenceList メソッド
指定された部分アセンブリ id のリストから、 [ICLRAssemblyReferenceList](iclrassemblyreferencelist-interface.md)インスタンスへのインターフェイスポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT  GetCLRAssemblyReferenceList (  
    [in] LPCWSTR *ppwzAssemblyReferences,  
    [in] DWORD    dwNumOfReferences,  
    [out] ICLRAssemblyReferenceList **ppReferenceList  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppwzAssemblyReferences`  
 から"Name, property = value..." の形式で、null で終わる文字列の配列部分アセンブリ id の一覧を指定する。  
  
 `dwNumOfReferences`  
 から内の項目の数 `ppwzAssemblyReferences` 。  
  
 `ppReferenceList`  
 入出力`ICLRAssemblyReferenceList`で指定されたアセンブリの一覧のアセンブリ id データを格納しているオブジェクトへのインターフェイスポインター `ppwzAssemblyReferences` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドから正常に値が返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返す場合、そのプロセス内で CLR は使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRAssemblyIdentityManager インターフェイス](iclrassemblyidentitymanager-interface.md)
- [ICLRAssemblyReferenceList インターフェイス](iclrassemblyreferencelist-interface.md)
