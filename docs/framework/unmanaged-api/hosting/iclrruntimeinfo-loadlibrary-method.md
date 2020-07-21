---
title: ICLRRuntimeInfo::LoadLibrary メソッド
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.LoadLibrary
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::LoadLibrary
helpviewer_keywords:
- ICLRRuntimeInfo::LoadLibrary method [.NET Framework hosting]
- LoadLibrary method [.NET Framework hosting]
ms.assetid: 4517ada3-4417-4ac5-a150-73da7a87c686
topic_type:
- apiref
ms.openlocfilehash: 09c80c3a56d86943ebe00e5222bb5452ab44e150
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762176"
---
# <a name="iclrruntimeinfoloadlibrary-method"></a>ICLRRuntimeInfo::LoadLibrary メソッド
[ICLRRuntimeInfo](iclrruntimeinfo-interface.md)インターフェイスによって表される共通言語ランタイム (CLR) から .NET Framework ライブラリを読み込みます。  
  
 このメソッドは、 [LoadLibraryShim](loadlibraryshim-function.md)関数よりも優先されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT LoadLibrary(  
     [in]  LPCWSTR pwzDllName,  
     [out, retval] HMODULE *phndModule);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pwzDllName`  
 から読み込むアセンブリの名前。  
  
 `phndModule`  
 入出力読み込まれたアセンブリへのハンドル。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_POINTER|`pwzDllName` または `phndModule` が null です。|  
|E_OUTOFMEMORY|要求を処理するのに十分なメモリがありません。|  
  
## <a name="remarks"></a>解説  
 このメソッドは、.NET Framework 再頒布可能パッケージに含まれている Dll のみを読み込みます。 ユーザーが生成したアセンブリを読み込むことはできません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRRuntimeInfo インターフェイス](iclrruntimeinfo-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
