---
title: ICLRRuntimeInfo::IsLoaded メソッド
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.IsLoaded
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::IsLoaded
helpviewer_keywords:
- IsLoaded method [.NET Framework hosting]
- ICLRRuntimeInfo::IsLoaded method [.NET Framework hosting]
ms.assetid: fdc5a3a7-71ff-4025-99a1-59e4ee0bfe1b
topic_type:
- apiref
ms.openlocfilehash: 45e27ac3c2d4912d2ed3e5d43ea3020b9db5dbdc
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504031"
---
# <a name="iclrruntimeinfoisloaded-method"></a>ICLRRuntimeInfo::IsLoaded メソッド
[ICLRRuntimeInfo](iclrruntimeinfo-interface.md)インターフェイスに関連付けられている共通言語ランタイム (CLR) をプロセスに読み込むかどうかを示します。 ランタイムは、起動しなくても読み込むことができます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT IsLoaded(  
[in]  HANDLE hndProcess,  
[out, retval] BOOL *pbLoaded);  
```  
  
## <a name="parameters"></a>パラメーター  
 `hndProcess`  
 からプロセスを処理するハンドル。  
  
 `pbLoaded`  
 [出力] `true`CLR がプロセスに読み込まれている場合は、それ以外の場合は `false` 。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_POINTER|`pbLoaded` が null です。|  
  
## <a name="remarks"></a>解説  
 このメソッドは、次の関数およびインターフェイスと下位互換性があります。  
  
- [ICorRuntimeHost](icorruntimehost-interface.md)インターフェイス (.NET Framework version 1 ホスティング API)。  
  
- [ICLRRuntimeHost](iclrruntimehost-interface.md)インターフェイス (.NET Framework 2.0 ホスティング API)。  
  
- 非推奨 `CorBindTo*` の関数 (「.NET Framework 2.0 ホスティング API での[非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)」を参照してください)。  
  
 ホストは、 `CorBindTo*` [Corbindtoruntime](corbindtoruntime-function.md)関数など、非推奨の関数の1つを呼び出して、特定のバージョンの CLR をインスタンス化することができます。 ホストは[ICLRMetaHost:: GetRuntime](iclrmetahost-getruntime-method.md)メソッドを呼び出し、同じバージョン番号を指定して[ICLRRuntimeInfo](iclrruntimeinfo-interface.md)インターフェイスを取得することができます。  
  
 その後、返された ICLRRuntimeInfo インターフェイスでホストがメソッドを呼び出すと、はを返します。 `IsLoaded` [ICLRRuntimeInfo](iclrruntimeinfo-interface.md) `pbLoaded` `true` それ以外の場合はを返し `false` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRRuntimeInfo インターフェイス](iclrruntimeinfo-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
