---
title: ICLRAssemblyIdentityManager::GetReferencedAssembliesFromFile メソッド
ms.date: 03/30/2017
api_name:
- ICLRAssemblyIdentityManager.GetReferencedAssembliesFromFile
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyIdentityManager::GetReferencedAssembliesFromFile
helpviewer_keywords:
- ICLRAssemblyIdentityManager::GetReferenceAssembliesFromFile method [.NET Framework hosting]
- GetReferenceAssembliesFromFile method [.NET Framework hosting]
ms.assetid: eed63d31-d977-4c7d-9443-f9d37a2a7d81
topic_type:
- apiref
ms.openlocfilehash: 3c4f673d88594e86004c6d51a4d58a0ac4642875
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615944"
---
# <a name="iclrassemblyidentitymanagergetreferencedassembliesfromfile-method"></a>ICLRAssemblyIdentityManager::GetReferencedAssembliesFromFile メソッド
指定したファイルパスにあるアセンブリによって参照されるアセンブリのリストを含む[ICLRReferenceAssemblyEnum](iclrreferenceassemblyenum-interface.md)インスタンスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetReferencedAssembliesFromFile (  
    [in]  LPCWSTR pwzFilePath,  
    [in]  DWORD   dwFlags,  
    [in]  ICLRAssemblyReferenceList   *pExcludeAssembliesList,  
    [out] ICLRReferenceAssemblyEnum  **ppReferenceEnum  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pwzFilePath`  
 から評価されるアセンブリへのパス。  
  
 `dwFlags`  
 から将来の拡張のために提供されます。 CLR_ASSEMBLY_IDENTITY_FLAGS_DEFAULT は、共通言語ランタイム (CLR) の現在のバージョンでサポートされている唯一の値です。  
  
 `pExcludeAssembliesList`  
 からから除外するアセンブリを表す[ICLRAssemblyReferenceList](iclrassemblyreferencelist-interface.md)オブジェクトへのポインター `ppReferenceEnum` 。  
  
 `ppReferenceEnum`  
 入出力によって表されるアセンブリを `ICLRReferenceAssemblyEnum` 除く、アセンブリによって参照されるアセンブリのアセンブリ id データを格納するオブジェクトのアドレスへのポインター `pwzFilePath` `pExcludeAssembliesList` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドから正常に値が返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返す場合、そのプロセス内で CLR は使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 呼び出し元は、返された一覧から一連の既知のアセンブリ参照を除外することを選択できます。 このセットは、パラメーターによって定義され `pExcludeAssembliesList` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRAssemblyIdentityManager インターフェイス](iclrassemblyidentitymanager-interface.md)
- [ICLRAssemblyReferenceList インターフェイス](iclrassemblyreferencelist-interface.md)
- [ICLRReferenceAssemblyEnum インターフェイス](iclrreferenceassemblyenum-interface.md)
