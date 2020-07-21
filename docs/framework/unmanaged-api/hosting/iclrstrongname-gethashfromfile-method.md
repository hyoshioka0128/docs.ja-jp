---
title: ICLRStrongName::GetHashFromFile メソッド
ms.date: 03/30/2017
api_name:
- ICLRStrongName.GetHashFromFile
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::GetHashFromFile
helpviewer_keywords:
- ICLRStrongName::GetHashFromFile method [.NET Framework hosting]
- GetHashFromFile method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: 9e50480a-8ada-4044-b2a5-97bb14ed3525
topic_type:
- apiref
ms.openlocfilehash: e4a5f6440a016176cf06704b342c173b29748e78
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762111"
---
# <a name="iclrstrongnamegethashfromfile-method"></a>ICLRStrongName::GetHashFromFile メソッド
指定したファイルの内容に対してハッシュが生成されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetHashFromFile (  
    [in]  LPCSTR   szFilePath,  
    [in, out] unsigned int   *piHashAlg,
    [out] BYTE     *pbHash,
    [in]  DWORD    cchHash,
    [out] DWORD    *pchHash  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `szFilePath`  
 からハッシュするファイルの名前。  
  
 `piHashAlg`  
 [入力、出力]ハッシュを生成するときに使用するアルゴリズム。 有効なアルゴリズムは、Win32 CryptoAPI によって定義されているものです。 が0に設定されている場合は、 `piHashAlg` 既定のアルゴリズム CALG_SHA-1 が使用されます。  
  
 `pbHash`  
 入出力生成されたハッシュを格納しているバイト配列。  
  
 `cchHash`  
 からが指すバッファーの最大サイズ `pbHash` 。  
  
 `pchHash`  
 入出力返されたのサイズ (バイト単位) `pbHash` 。  
  
## <a name="return-value"></a>戻り値  
 `S_OK`メソッドが正常に完了した場合は。それ以外の場合は、失敗を示す HRESULT 値 (「リストの[一般的な Hresult 値](/windows/win32/seccrypto/common-hresult-values)」を参照してください)。  
  
## <a name="remarks"></a>解説  
 このメソッドは[ICLRStrongName:: GetHashFromFileW](iclrstrongname-gethashfromfilew-method.md)メソッドと同じですが、ファイル名の指定は Unicode ではなく ANSI です。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [GetHashFromFileW メソッド](iclrstrongname-gethashfromfilew-method.md)
- [ICLRStrongName インターフェイス](iclrstrongname-interface.md)
