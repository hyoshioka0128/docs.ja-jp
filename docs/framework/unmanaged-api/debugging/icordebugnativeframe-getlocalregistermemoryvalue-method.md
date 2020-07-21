---
title: ICorDebugNativeFrame::GetLocalRegisterMemoryValue メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetLocalRegisterMemoryValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetLocalRegisterMemoryValue
helpviewer_keywords:
- ICorDebugNativeFrame::GetLocalRegisterMemoryValue method [.NET Framework debugging]
- GetLocalRegisterMemoryValue method [.NET Framework debugging]
ms.assetid: d350f69d-9aff-4f5a-8301-daea22dee2da
topic_type:
- apiref
ms.openlocfilehash: f16150ad7d9ecec4b4aceee5c9266e9a7859f1cb
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213297"
---
# <a name="icordebugnativeframegetlocalregistermemoryvalue-method"></a>ICorDebugNativeFrame::GetLocalRegisterMemoryValue メソッド
このネイティブフレームのメモリ位置と指定したレジスタに、下位ワードと上位ワードが格納される引数またはローカル変数の値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetLocalRegisterMemoryValue (  
    [in] CorDebugRegister   highWordReg,  
    [in] CORDB_ADDRESS      lowWordAddress,  
    [in] ULONG              cbSigBlob,  
    [in] PCCOR_SIGNATURE    pvSigBlob,  
    [out] ICorDebugValue    **ppValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `highWordReg`  
 から値の上位ワードを含むレジスタを指定する "CorDebugRegister" 列挙体の値。  
  
 `lowWordAddress`  
 から`CORDB_ADDRESS`値の下位ワードを格納しているメモリ位置を指定する値。  
  
 `cbSigBlob`  
 からパラメーターによって参照されるバイナリメタデータシグネチャのサイズを指定する整数 `pvSigBlob` 。  
  
 `pvSigBlob`  
 から`PCCOR_SIGNATURE`値の型のバイナリメタデータシグネチャを指す値。  
  
 `ppValue`  
 入出力指定されたレジスタおよびメモリ位置に格納されている取得値を表す "ICorDebugValue" オブジェクトのアドレスへのポインター。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目
