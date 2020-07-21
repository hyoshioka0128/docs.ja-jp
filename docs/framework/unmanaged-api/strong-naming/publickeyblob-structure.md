---
title: PublicKeyBlob 構造体
ms.date: 03/30/2017
api_name:
- PublicKeyBlob
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- PublicKeyBlob
helpviewer_keywords:
- PublicKeyBlob structure [.NET Framework strong naming]
ms.assetid: b9240712-829c-4c8d-9a09-a6e7aa63f63a
topic_type:
- apiref
ms.openlocfilehash: 3b00bf8295a635871bd7263928ff21c97053cc39
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176956"
---
# <a name="publickeyblob-structure"></a>PublicKeyBlob 構造体
公開キーと秘密キーのペアの公開キーをバイナリ形式で表します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct {  
    unsigned int SigAlgId;  
    unsigned int HashAlgId;  
    ULONG cbPublicKey;  
    BYTE PublicKey[1]  
} PublicKeyBlob;
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`SigAlgId`|公開キーの署名アルゴリズム (WinCrypt.h で定義されている種類`ALG_ID`) の識別子。|  
|`HashAlgId`|公開キーのハッシュ アルゴリズム (WinCrypt.h で定義されている種類`ALG_ID`) の識別子。|  
|`cbPublicKey`|キーの長さ (バイト単位)。|  
|`PublicKey`|CryptoAPI によって返される形式のキー値を格納する可変長バイト配列。|  
  
## <a name="remarks"></a>解説  
 構造体`PublicKeyBlob`は、パブリック キーと秘密キーのペアの公開キーを表すために、厳密な名前の取得[、](strongnamegetpublickey-function.md)厳密な名前[の生成](strongnamesignaturegeneration-function.md)、およびその他の厳密な名前関数で使用されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ストロングネーム.h  
  
 **ライブラリ:** MsCorEE.dll にリソースとして含まれる  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [StrongNameGetPublicKey 関数](strongnamegetpublickey-function.md)
- [StrongNameSignatureGeneration 関数](strongnamesignaturegeneration-function.md)
