---
title: StrongNameSignatureSize 関数
ms.date: 03/30/2017
api_name:
- StrongNameSignatureSize
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameSignatureSize
helpviewer_keywords:
- StrongNameSignatureSize function [.NET Framework strong naming]
ms.assetid: 4fde4cd0-f53e-4411-a2fe-fc5c54472f95
topic_type:
- apiref
ms.openlocfilehash: a19d875b8fb81f2af3821e69452f0f0ed591cd22
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176891"
---
# <a name="strongnamesignaturesize-function"></a>StrongNameSignatureSize 関数
厳密な名前の署名のサイズが返されます。 `StrongNameSignatureSize`通常は、遅延署名されたアセンブリを作成するときに、ファイルに確保する領域を決定するためにコンパイラによって使用されます。  
  
 この関数は廃止されました。 代わりに、メソッド[を](../hosting/iclrstrongname-strongnamesignaturesize-method.md)使用します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
BOOLEAN StrongNameSignatureSize (
    [in]  BYTE   *pbPublicKeyBlob,  
    [in]  ULONG  cbPublicKeyBlob,
    [in]  DWORD  *pcbSize  
);
```  
  
## <a name="parameters"></a>パラメーター  
 `pbPublicKeyBlob`  
 [in]厳密な名前の署名を生成するために使用されるキー ペアのパブリック部分を含む[、型の PublicKeyBlob](publickeyblob-structure.md)の構造体。  
  
 `cbPublicKeyBlob`  
 [in]のサイズ (バイト単位)`pbPublicKeyBlob`です。  
  
 `pcbSize`  
 [in]厳密な名前の署名を格納するために必要なバイト数。  
  
## <a name="return-value"></a>戻り値  
 `true`正常に完了した場合。それ以外`false`の場合は、 .  
  
## <a name="remarks"></a>解説  
 関数が`StrongNameSignatureSize`正常に完了しない場合は、[関数](strongnameerrorinfo-function.md)を呼び出して、最後に生成されたエラーを取得します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ストロングネーム.h  
  
 **ライブラリ:** MsCorEE.dll にリソースとして含まれる  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [StrongNameSignatureSize メソッド](../hosting/iclrstrongname-strongnamesignaturesize-method.md)
- [ICLRStrongName インターフェイス](../hosting/iclrstrongname-interface.md)
