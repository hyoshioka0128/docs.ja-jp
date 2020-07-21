---
title: ICLRAssemblyIdentityManager::GetBindingIdentityFromFile メソッド
ms.date: 03/30/2017
api_name:
- ICLRAssemblyIdentityManager.GetBindingIdentityFromFile
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyIdentityManager::GetBindingIdentityFromFile
helpviewer_keywords:
- GetBindingIdentityFromFile method [.NET Framework hosting]
- ICLRAssemblyIdentityManager::GetBindingIdentifyFromFile method [.NET Framework hosting]
ms.assetid: 7797562d-7b4c-4bd9-8b93-f35e0e2869e4
topic_type:
- apiref
ms.openlocfilehash: 5b537d59014afa783d3f8c5046cc02dad7ea7740
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615996"
---
# <a name="iclrassemblyidentitymanagergetbindingidentityfromfile-method"></a>ICLRAssemblyIdentityManager::GetBindingIdentityFromFile メソッド
指定したファイルパスにあるアセンブリのアセンブリ id バインドデータを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetBindingIdentityFromFile(  
    [in] LPCWSTR     pwzFilePath,  
    [in] DWORD       dwFlags,  
    [out, size_is(*pcchBufferSize)] LPWSTR pwzBuffer,  
    [in, out] DWORD *pcchBufferSize  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pwzFilePath`  
 から評価されるファイルへのパス。  
  
 `dwFlags`  
 からアセンブリの id 型を示す[Eclrassemblyidentity flags](eclrassemblyidentityflags-enumeration.md)列挙体の値。 将来の拡張のために提供されます。 CLR_ASSEMBLY_IDENTITY_FLAGS_DEFAULT は、共通言語ランタイム (CLR) バージョン2.0 でサポートされている唯一の値です。  
  
 `pwzBuffer`  
 入出力非透過アセンブリ id データを格納しているバッファー。  
  
 `pcchBufferSize`  
 [入力、出力]のサイズへのポインター `pwzBuffer` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドから正常に値が返されました。|  
|E_INVALIDARG|指定された `pwzFilePath` が null です。|  
|ERROR_INSUFFICIENT_BUFFER|のサイズ `pwzBuffer` が小さすぎます。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返す場合、そのプロセス内で CLR は使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 `GetBindingIdentityFromFile`は通常、2回呼び出されます。 最初の呼び出しでは、に null 値が指定され、 `pwzBuffer` メソッドはの適切なサイズを返し `pcchBufferSize` ます。 2番目の呼び出しでは、適切に割り当てられたバッファーが提供され、メソッドは完了時に実際のバッファーデータと共にを返します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRAssemblyIdentityManager インターフェイス](iclrassemblyidentitymanager-interface.md)
- [ICLRAssemblyReferenceList インターフェイス](iclrassemblyreferencelist-interface.md)
- [ICLRHostBindingPolicyManager インターフェイス](iclrhostbindingpolicymanager-interface.md)
