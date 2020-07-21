---
title: StrongNameFreeBuffer 関数
ms.date: 03/30/2017
api_name:
- StrongNameFreeBuffer
api_location:
- mscoree.dll
- mscorsn.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameFreeBuffer
helpviewer_keywords:
- StrongNameFreeBuffer function [.NET Framework strong naming]
ms.assetid: eda21ecf-4734-4f92-aaba-9f34884385db
topic_type:
- apiref
ms.openlocfilehash: 50e3cc6e677de45be9256a2a818ebd6ed7d8b843
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176917"
---
# <a name="strongnamefreebuffer-function"></a>StrongNameFreeBuffer 関数
[StrongNameGetPublicKey](strongnamegetpublickey-function.md)、[StrongNameTokenFromPublicKey](strongnametokenfrompublickey-function.md)、または[StrongNameSignatureGeneration](strongnamesignaturegeneration-function.md) などの厳密な名前の関数に対する前の呼び出しで割り当てられたメモリが解放されます。  
  
 この関数は廃止されました。 代わりに[、メソッドを](../hosting/iclrstrongname-strongnamefreebuffer-method.md)使用します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
VOID StrongNameFreeBuffer (
   [in] BYTE   *pbMemory  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pbMemory`  
 [in]解放するメモリへのポインター。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ストロングネーム.h  
  
 **ライブラリ:** MsCorEE.dll にリソースとして含まれる  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [StrongNameFreeBuffer メソッド](../hosting/iclrstrongname-strongnamefreebuffer-method.md)
- [ICLRStrongName インターフェイス](../hosting/iclrstrongname-interface.md)
