---
title: ICLRAssemblyIdentityManager::GetProbingAssembliesFromReference メソッド
ms.date: 03/30/2017
api_name:
- ICLRAssemblyIdentityManager.GetProbingAssembliesFromReference
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyIdentityManager::GetProbingAssembliesFromReference
helpviewer_keywords:
- ICLRAssemblyIdentityManager::GetProbingAssembliesFromReference method [.NET Framework hosting]
- GetProbingAssembliesFromReference method [.NET Framework hosting]
ms.assetid: aec05744-e8d4-44c6-b4a8-e583229ac34e
topic_type:
- apiref
ms.openlocfilehash: 21ebd0c64d6c8bbdac327258ad4c7ffec83a1ce9
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504317"
---
# <a name="iclrassemblyidentitymanagergetprobingassembliesfromreference-method"></a>ICLRAssemblyIdentityManager::GetProbingAssembliesFromReference メソッド
指定した id 型のアセンブリによって参照されるアセンブリ id の[ICLRProbingAssemblyEnum](iclrprobingassemblyenum-interface.md)列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetProbingAssembliesFromReference (  
    [in] DWORD   dwMachineType,  
    [in] DWORD   dwFlags,  
    [in] LPCWSTR pwzReferenceIdentity,  
    [out] ICLRProbingAssemblyEnum **ppProbingAssemblyEnum  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwMachineType`  
 からWinnt.h で定義されているプロセッサアーキテクチャを指定する有効な値。  
  
 `dwFlags`  
 から将来の拡張のために提供されます。 CLR_ASSEMBLY_IDENTITY_FLAGS_DEFAULT は、共通言語ランタイム (CLR) の現在のバージョンでサポートされている唯一の値です。  
  
 `pwzReferenceIdentity`  
 から通常、 [ICLRAssemblyIdentityManager:: GetBindingIdentityFromFile](iclrassemblyidentitymanager-getbindingidentityfromfile-method.md)または[ICLRAssemblyIdentityManager:: Getbinding fromstream](iclrassemblyidentitymanager-getbindingidentityfromstream-method.md)メソッドの呼び出しから返される、不透明なアセンブリバインド id。  
  
 `ppProbingAssemblyEnum`  
 入出力`ICLRProbingAssemblyEnum`によって識別されるアセンブリによって参照されるアセンブリへの参照を格納する列挙子へのインターフェイスポインター `pwzReferenceIdentity` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドから正常に値が返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
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
- [ICLRProbingAssemblyEnum インターフェイス](iclrprobingassemblyenum-interface.md)
