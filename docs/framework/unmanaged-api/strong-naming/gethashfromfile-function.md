---
title: GetHashFromFile 関数
ms.date: 03/30/2017
api_name:
- GetHashFromFile
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- GetHashFromFile
helpviewer_keywords:
- GetHashFromFile function [.NET Framework strong naming]
ms.assetid: b3c526a4-8fb4-4ad6-b6af-42ce9c06492e
topic_type:
- apiref
ms.openlocfilehash: ea2b70f37668587fb02513ab54da6c1915e2918d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176982"
---
# <a name="gethashfromfile-function"></a>GetHashFromFile 関数
指定したファイルの内容に対してハッシュが生成されます。  
  
 この関数は廃止されました。 代わりに[、](../hosting/iclrstrongname-gethashfromfile-method.md)メソッドを使用します。  
  
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
 [in]ハッシュするファイルの名前。  
  
 `piHashAlg`  
 [イン、アウト]ハッシュを生成するときに使用するアルゴリズム。 有効なアルゴリズムは、Win32 CryptoAPI によって定義されるアルゴリズムです。 0`piHashAlg`に設定すると、デフォルトのアルゴリズム CALG_SHA-1 が使用されます。  
  
 `pbHash`  
 [アウト]生成されたハッシュを含むバイト配列。  
  
 `cchHash`  
 [in]指す`pbHash`バッファーの最大サイズ。  
  
 `pchHash`  
 [アウト]返された`pbHash`のサイズ (バイト単位)  
  
## <a name="remarks"></a>解説  
 この関数は、ファイル名の指定が Unicode ではなく ANSI であることを除けば[、GetHashFromFileW](gethashfromfilew-function.md)と同じです。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ストロングネーム.h  
  
 **ライブラリ:** MsCorEE.dll にリソースとして含まれる  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [GetHashFromFile メソッド](../hosting/iclrstrongname-gethashfromfile-method.md)
- [GetHashFromFileW メソッド](../hosting/iclrstrongname-gethashfromfilew-method.md)
- [ICLRStrongName インターフェイス](../hosting/iclrstrongname-interface.md)
