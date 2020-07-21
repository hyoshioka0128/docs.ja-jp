---
title: GetHashFromFileW 関数
ms.date: 03/30/2017
api_name:
- GetHashFromFileW
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- GetHashFromFileW
helpviewer_keywords:
- GetHashFromFileW function [.NET Framework strong naming]
ms.assetid: 97c2d7a6-5376-45a1-ba65-146a249147cc
topic_type:
- apiref
ms.openlocfilehash: 9db583c7064cb910b29e84437f31143dac0d3ec9
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79175084"
---
# <a name="gethashfromfilew-function"></a>GetHashFromFileW 関数
Unicode 文字列で指定されたファイルの内容に対してハッシュが作成されます。  
  
 この関数は廃止されました。 代わりに[、メソッド](../hosting/iclrstrongname-gethashfromfilew-method.md)を使用します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetHashFromFileW (
    [in]  LPCWSTR   wszFilePath,  
    [in, out] unsigned int   *piHashAlg,  
    [out] BYTE      *pbHash,  
    [in]  DWORD     cchHash,  
    [out] DWORD     *pchHash  
);
```  
  
## <a name="parameters"></a>パラメーター  
 `wszFilePath`  
 [in]ハッシュするファイルの Unicode 名。  
  
 `piHashAlg`  
 [イン、アウト]ハッシュを生成するときに使用するアルゴリズム。 有効なアルゴリズムは、Win32 CryptoAPI によって定義されるアルゴリズムです。 0`piHashAlg`に設定すると、デフォルトのアルゴリズム CALG_SHA-1 が使用されます。  
  
 `pbHash`  
 [アウト]生成されたハッシュを含むバイト配列。  
  
 `cchHash`  
 [in]が`pbHash`指すバッファの最大サイズ。  
  
 `pchHash`  
 [アウト]のサイズ (バイト単位)`pbHash`です。  
  
## <a name="remarks"></a>解説  
 この関数は、ファイル名指定が ANSI ではなくユニコードであることを除けば[、GetHashFromFile](gethashfromfile-function.md)と同じです。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ストロングネーム.h  
  
 **ライブラリ:** MsCorEE.dll にリソースとして含まれる  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [GetHashFromFileW メソッド](../hosting/iclrstrongname-gethashfromfilew-method.md)
- [GetHashFromFile メソッド](../hosting/iclrstrongname-gethashfromfile-method.md)
- [ICLRStrongName インターフェイス](../hosting/iclrstrongname-interface.md)
