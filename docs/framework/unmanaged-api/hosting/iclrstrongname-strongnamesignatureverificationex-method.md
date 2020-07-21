---
title: ICLRStrongName::StrongNameSignatureVerificationEx メソッド
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameSignatureVerificationEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameSignatureVerificationEx
helpviewer_keywords:
- StrongNameSignatureVerificationEx method, ICLRStrongName interface [.NET Framework hosting]
- ICLRStrongName::StrongNameSignatureVerificationEx method [.NET Framework hosting]
ms.assetid: dbd2f662-208b-4174-b301-5c99af91040f
topic_type:
- apiref
ms.openlocfilehash: 5bd985a6870ae6f4cc2302b6a11e8e139180d839
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503992"
---
# <a name="iclrstrongnamestrongnamesignatureverificationex-method"></a>ICLRStrongName::StrongNameSignatureVerificationEx メソッド
指定したパスにあるアセンブリマニフェストに厳密な名前の署名が含まれているかどうかを示す値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT StrongNameSignatureVerificationEx (  
    [in]  LPCWSTR   wszFilePath,  
    [in]  BOOLEAN   fForceVerification,  
    [out] BOOLEAN   *pfWasVerified  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `wszFilePath`  
 から検証するアセンブリの移植可能な実行可能ファイル (.exe または .dll) のパス。  
  
 `fForceVerification`  
 [入力] `true`レジストリ設定を上書きする必要がある場合でも、検証を実行するにはそれ以外の場合は `false` 。  
  
 `pfWasVerified`  
 [出力] `true`厳密な名前の署名が検証された場合は。それ以外の場合は `false` 。 `pfWasVerified``false`レジストリ設定によって検証が成功した場合は、もに設定されます。  
  
## <a name="return-value"></a>戻り値  
 `S_OK`検証が成功した場合は、それ以外の場合は、失敗を示す HRESULT 値 (「リストの[一般的な Hresult 値](/windows/win32/seccrypto/common-hresult-values)」を参照してください)。  
  
## <a name="remarks"></a>解説  
 [ICLRStrongName:: StrongNameSignatureVerificationEx](iclrstrongname-strongnamesignatureverificationex-method.md)メソッドには、 [ICLRStrongName:: StrongNameSignatureVerification](iclrstrongname-strongnamesignatureverification-method.md)メソッドと同様の機能が用意されています。 ただし、 [ICLRStrongName:: StrongNameSignatureVerificationEx](iclrstrongname-strongnamesignatureverificationex-method.md)の2番目の入力パラメーターと出力パラメーターは、 `BOOLEAN` の代わりに型に `DWORD` なります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [StrongNameSignatureVerification メソッド](iclrstrongname-strongnamesignatureverification-method.md)
- [ICLRStrongName インターフェイス](iclrstrongname-interface.md)
