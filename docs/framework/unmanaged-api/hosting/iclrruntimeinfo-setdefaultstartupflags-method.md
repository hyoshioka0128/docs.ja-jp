---
title: ICLRRuntimeInfo::SetDefaultStartupFlags メソッド
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.SetDefaultStartupFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::SetDefaultStartupFlags
helpviewer_keywords:
- ICLRRuntimeInfo::SetDefaultStartupFlags method [.NET Framework hosting]
- SetDefaultStartupFlags method [.NET Framework hosting]
ms.assetid: 98ae174f-bff0-48f1-9e05-6cb63b451824
topic_type:
- apiref
ms.openlocfilehash: aa02d42511a863434fef236f90afae2c5417a78d
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504018"
---
# <a name="iclrruntimeinfosetdefaultstartupflags-method"></a>ICLRRuntimeInfo::SetDefaultStartupFlags メソッド
ランタイムを開始するために使用されるスタートアップフラグとホスト構成ファイルを設定します。 このメソッドは、 `startupFlags` [Corbindtoruntimeex](corbindtoruntimeex-function.md)および[Corbindtoruntimeex](corbindtoruntimehost-function.md)関数でのパラメーターの使用よりも優先されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetDefaultStartupFlags(  
           [in]  DWORD dwStartupFlags,  
           [in]  LPCWSTR pwzHostConfigFile);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwStartupFlags`  
 から設定するホストスタートアップフラグ。 [Corbindtoruntimeex](corbindtoruntimeex-function.md)および[Corbindtoruntimeex](corbindtoruntimehost-function.md)関数と同じフラグを使用します。  
  
 `pwzHostConfigFile`  
 から設定するホスト構成ファイルのディレクトリパス。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドエラーを示す HRESULT エラーを返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
  
## <a name="remarks"></a>解説  
 マルチスレッドホストは、このメソッドの呼び出しを同期する必要があります。 それ以外の場合、スレッド B は、の `SetStartupFlags` 呼び出しを完了し `SetStartupFlags` てからランタイムを開始する前に、メソッドを呼び出すことがあります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRRuntimeInfo インターフェイス](iclrruntimeinfo-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
