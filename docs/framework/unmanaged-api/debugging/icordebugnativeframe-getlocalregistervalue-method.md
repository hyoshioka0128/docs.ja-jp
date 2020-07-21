---
title: ICorDebugNativeFrame::GetLocalRegisterValue メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetLocalRegisterValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetLocalRegisterValue
helpviewer_keywords:
- GetLocalRegisterValue method [.NET Framework debugging]
- ICorDebugNativeFrame::GetLocalRegisterValue method [.NET Framework debugging]
ms.assetid: 5ccb74f3-f891-430c-b70a-e370624edde2
topic_type:
- apiref
ms.openlocfilehash: 97d79f70097bef7768316907887cea2c38dd81e1
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212829"
---
# <a name="icordebugnativeframegetlocalregistervalue-method"></a>ICorDebugNativeFrame::GetLocalRegisterValue メソッド
このネイティブフレームの指定したレジスタに格納されている引数またはローカル変数の値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetLocalRegisterValue (  
    [in]  CorDebugRegister   reg,  
    [in]  ULONG              cbSigBlob,  
    [in]  PCCOR_SIGNATURE    pvSigBlob,  
    [out] ICorDebugValue     **ppValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `reg`  
 から値を含むレジスタを指定する "CorDebugRegister" 列挙の値。  
  
 `cbSigBlob`  
 からパラメーターによって参照されるバイナリメタデータシグネチャのサイズを指定する整数 `pvSigBlob` 。  
  
 `pvSigBlob`  
 から`PCCOR_SIGNATURE`値の型のバイナリメタデータシグネチャを指す値。  
  
 `ppValue`  
 入出力指定したレジスタに格納されている取得した値を表す "ICorDebugValue" オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 メソッドは、 `GetLocalRegisterValue` ネイティブフレームまたは just-in-time (JIT) でコンパイルされたフレームのどちらでも使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目
