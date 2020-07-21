---
title: GetRealProcAddress 関数
ms.date: 03/30/2017
api_name:
- GetRealProcAddress
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- GetRealProcAddress
helpviewer_keywords:
- GetRealProcAddress function [.NET Framework hosting]
ms.assetid: f1f2fab1-400b-488f-95f2-d49c4fca3556
topic_type:
- apiref
ms.openlocfilehash: 6bbf8366054c58543444a4b710a687198f365e6e
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83617192"
---
# <a name="getrealprocaddress-function"></a>GetRealProcAddress 関数
インストールされている最新バージョンの共通言語ランタイム (CLR) からエクスポートされた、指定された関数のアドレスを取得します。  
  
 この関数は .NET Framework 4 で非推奨とされました。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetRealProcAddress (  
    [in]  LPCSTR  pwszProcName,
    [out] VOID  **ppv  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pwszProcName`  
 から関数の名前。  
  
 `ppv`  
 入出力関数のアドレスへのポインターを受け取る位置。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、Winerror.h で定義されているように、CorError. h で定義されている次の値に加えて、標準の Component Object Model (COM) エラーコードを返します。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_POINTER|`ppv` が無効です。|  
|CLR_E_SHIM_RUNTIMEEXPORT|関数はランタイムからエクスポートされません。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)
