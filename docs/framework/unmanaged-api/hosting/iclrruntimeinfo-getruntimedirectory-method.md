---
title: ICLRRuntimeInfo::GetRuntimeDirectory メソッド
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.GetRuntimeDirectory
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::GetRuntimeDirectory
helpviewer_keywords:
- GetRuntimeDirectory method [.NET Framework hosting]
- ICLRRuntimeInfo::GetRuntimeDirectory method [.NET Framework hosting]
ms.assetid: 4401546e-4d48-453f-a1fb-b2ebda54df5c
topic_type:
- apiref
ms.openlocfilehash: d744abf5c502e9b9510cf9fd6479149b6c2177cc
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762215"
---
# <a name="iclrruntimeinfogetruntimedirectory-method"></a>ICLRRuntimeInfo::GetRuntimeDirectory メソッド
このインターフェイスに関連付けられている共通言語ランタイム (CLR) のインストールディレクトリを取得します。  
  
 このメソッドは、.NET Framework バージョン2.0、3.0、および3.5 で提供される[Getcorsystemdirectory](getcorsystemdirectory-function.md)関数よりも優先されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetRuntimeDirectory(  
[out, size_is(*pcchBuffer)] LPWSTR pwzBuffer,  
[in, out]  DWORD *pcchBuffer);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pwzBuffer`  
 入出力CLR インストールディレクトリを返します。 インストールパスは完全修飾されています。たとえば、"c:\windows\microsoft.net\framework\v1.0.3705" のように \\ なります。  
  
 `pchBuffer`  
 [入力、出力]`pwzBuffer`バッファーオーバーランを回避するためののサイズを指定します。 `pwzBuffer`が null の場合、は `pchBuffer` 必要なサイズを返し `pwzBuffer` ます。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_POINTER|`pwzBuffer` または `pchBuffer` が null です。|  
  
## <a name="remarks"></a>解説  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRRuntimeInfo インターフェイス](iclrruntimeinfo-interface.md)
- [ホスティング](index.md)
