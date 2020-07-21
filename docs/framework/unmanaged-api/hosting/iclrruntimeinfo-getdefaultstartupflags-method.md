---
title: ICLRRuntimeInfo::GetDefaultStartupFlags メソッド
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.GetDefaultStartupFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::GetDefaultStartupFlags
helpviewer_keywords:
- ICLRRuntimeInfo::GetDefaultStartupFlags method [.NET Framework hosting]
- GetDefaultStartupFlags method [.NET Framework hosting]
ms.assetid: 35c2173e-3b0b-4b2a-950d-e0a01c6df052
topic_type:
- apiref
ms.openlocfilehash: 8513787f48ae89632816face386bbcda20555dac
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703885"
---
# <a name="iclrruntimeinfogetdefaultstartupflags-method"></a>ICLRRuntimeInfo::GetDefaultStartupFlags メソッド
ランタイムを開始するために使用されるスタートアップフラグとホスト構成ファイルを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetDefaultStartupFlags(  
     [out]  DWORD *pdwStartupFlags,  
     [out, size_is(*pcchHostConfigFile)] LPWSTR pwzHostConfigFile,  
     [in, out]  DWORD *pcchHostConfigFile);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pdwStartupFlags`  
 入出力現在設定されているホストのスタートアップフラグへのポインター。  
  
 `pwzHostConfigFile`  
 入出力現在のホスト構成ファイルのディレクトリパスへのポインター。  
  
 `pcchHostConfigFile`  
 [入力、出力]入力時には、 `pwzHostConfigFile` バッファーオーバーランを回避するためののサイズ。 `pwzHostConfigFile`が null の場合、メソッドは、 `pwzHostConfigFile` 事前割り当てのために必要なサイズを返します。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドエラーを示す HRESULT エラーを返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
  
## <a name="remarks"></a>解説  
 このメソッドは、既定のフラグ値 ( `STARTUP_CONCURRENT_GC` および `NULL` )、または[ICLRRuntimeInfo:: SetDefaultStartupFlags メソッド](iclrruntimeinfo-setdefaultstartupflags-method.md)の以前の呼び出しによって提供された値、または `CorBind*` メソッドがこのランタイムにバインドされている場合は、いずれかのメソッドによって設定された値を返します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRRuntimeInfo インターフェイス](iclrruntimeinfo-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
