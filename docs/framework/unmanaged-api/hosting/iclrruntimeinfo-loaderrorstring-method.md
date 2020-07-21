---
title: ICLRRuntimeInfo::LoadErrorString メソッド
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.LoadErrorString
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::LoadErrorString
helpviewer_keywords:
- ICLRRuntimeInfo::LoadErrorString method [.NET Framework hosting]
- LoadErrorString method [.NET Framework hosting]
ms.assetid: 52c543ab-9ef5-4ee7-b836-c0ffc35cd45b
topic_type:
- apiref
ms.openlocfilehash: da6efae38cd70a68feea56b12e86be23fde7f0cb
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762189"
---
# <a name="iclrruntimeinfoloaderrorstring-method"></a>ICLRRuntimeInfo::LoadErrorString メソッド
HRESULT 値を、指定したカルチャの適切なエラーメッセージに変換します。  
  
 このメソッドは、次の関数を置き換えます。  
  
- [LoadStringRC](loadstringrc-function.md)  
  
- [LoadStringRCEx](loadstringrcex-function.md)  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT LoadErrorString(  
     [in] UINT iResourceID,  
     [out, size_is(*pcchBuffer)] LPWSTR pwzBuffer,  
     [in, out]  DWORD *pcchBuffer,  
     [in, lcid] LONG iLocaleID);  
```  
  
## <a name="parameters"></a>パラメーター  
 `iResourceID`  
 から変換する HRESULT。  
  
 `pwzBuffer`  
 入出力指定した HRESULT に関連付けられているメッセージ文字列。  
  
 `pcchBuffer`  
 [入力、出力]`pwzbuffer`バッファーオーバーランを回避するためののサイズ。 `pwzbuffer`が null の場合、は、 `pcchBuffer` の予期されるサイズを提供して、事前割り当て `pwzbuffer` を可能にします。  
  
 `iLocaleID`  
 からカルチャ識別子。 既定のカルチャを使用するには、-1 を指定する必要があります。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_POINTER|`pcchBuffer` が null です。|  
|E_INVALIDARG|`pwzBuffer` が null です。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRRuntimeInfo インターフェイス](iclrruntimeinfo-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
