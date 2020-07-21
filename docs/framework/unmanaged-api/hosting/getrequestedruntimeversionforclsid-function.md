---
title: GetRequestedRuntimeVersionForCLSID 関数
ms.date: 03/30/2017
api_name:
- GetRequestedRuntimeVersionForCLSID
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- GetRequestedRuntimeVersionForCLSID
helpviewer_keywords:
- GetRequestedRuntimeVersionForCLSID function [.NET Framework hosting]
ms.assetid: 5bb12f9a-0612-434b-b4ed-2db636a20bec
topic_type:
- apiref
ms.openlocfilehash: 899d6e74902e47f1f41b849bd5c25048baa175f7
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83617140"
---
# <a name="getrequestedruntimeversionforclsid-function"></a>GetRequestedRuntimeVersionForCLSID 関数
指定したを使用して、クラスの適切な共通言語ランタイム (CLR) バージョン情報を取得し `CLSID` ます。  
  
 この関数は .NET Framework 4 で非推奨とされました。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetRequestedRuntimeVersionForCLSID (  
    [in]  REFCLSID   rclsid,
    [out]  LPWSTR     pVersion,
    [in]  DWORD      cchBuffer,
    [out] DWORD*     dwLength,
    [in]  CLSID_RESOLUTION_FLAGS dwResolutionFlags  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `rclsid`  
 から `CLSID`コンポーネントの。  
  
 `pVersion`  
 入出力 正常に完了したときのバージョン番号の文字列を格納するバッファー。  
  
 `cchBuffer`  
 から バッファーのサイズ (ワイド文字単位) `pVersion` 。  
  
 `dwLength`  
 入出力返されたバッファーの長さ (バイト単位)。  
  
 `dwResolutionFlags`  
 から CLSID_RESOLUTION_FLAGS 値の1つ。 次の値がサポートされています。  
  
- CLSID_RESOLUTION_DEFAULT: (0x0) 既定の相互運用動作を使用することを指定します。  
  
- CLSID_RESOLUTION_REGISTERED: (0x1) は、レジストリを検索する必要があり、shim ポリシーを適用する必要があることを指定します。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|関数が正常に返されました。|  
|E_INVALIDARG|パラメーターの1つに無効な型または形式が指定されています。|  
|ERROR_INSUFFICIENT_BUFFER|`pVersion`バッファーのサイズが、バージョン文字列全体を保持するのに十分ではありません。|  
|REGDB_E_CLASSNOTREG|指定されたに登録されているクラスがありません `CLSID` 。|  
|E_POINTER|`dwLength`が null であるか、または `cchBuffer` バージョン文字列を保持するのに十分な大きさですが、が `pVersion` null です。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)
