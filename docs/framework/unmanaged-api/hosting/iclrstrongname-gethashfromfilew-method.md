---
title: ICLRStrongName::GetHashFromFileW メソッド
ms.date: 03/30/2017
api_name:
- ICLRStrongName.GetHashFromFileW
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::GetHashFromFileW
helpviewer_keywords:
- GetHashFromFileW method, ICLRStrongName interface [.NET Framework hosting]
- ICLRStrongName::GetHashFromFileW method [.NET Framework hosting]
ms.assetid: c6ff45fc-905d-4c6e-b00c-97c6c7c55d99
topic_type:
- apiref
ms.openlocfilehash: 6dbb3360132186c38c007fb5fa12a3724ca145aa
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762098"
---
# <a name="iclrstrongnamegethashfromfilew-method"></a>ICLRStrongName::GetHashFromFileW メソッド
Unicode 文字列で指定されたファイルの内容に対してハッシュが作成されます。  
  
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
 からハッシュするファイルの Unicode 名。  
  
 `piHashAlg`  
 [入力、出力]ハッシュを生成するときに使用するアルゴリズム。 有効なアルゴリズムは、Win32 CryptoAPI によって定義されているものです。 が0に設定されている場合は、 `piHashAlg` 既定のアルゴリズム CALG_SHA-1 が使用されます。  
  
 `pbHash`  
 入出力生成されたハッシュを格納しているバイト配列。  
  
 `cchHash`  
 からが指すバッファーの最大サイズ `pbHash` 。  
  
 `pchHash`  
 入出力のサイズ (バイト単位) `pbHash` 。  
  
## <a name="return-value"></a>戻り値  
 `S_OK`メソッドが正常に完了した場合は。それ以外の場合は、失敗を示す HRESULT 値 (「リストの[一般的な Hresult 値](/windows/win32/seccrypto/common-hresult-values)」を参照してください)。  
  
## <a name="remarks"></a>解説  
 このメソッドは[ICLRStrongName:: GetHashFromFile](iclrstrongname-gethashfromfile-method.md)メソッドと同じですが、ファイル名の指定は ANSI ではなく Unicode である点が異なります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [GetHashFromFile メソッド](iclrstrongname-gethashfromfile-method.md)
- [ICLRStrongName インターフェイス](iclrstrongname-interface.md)
