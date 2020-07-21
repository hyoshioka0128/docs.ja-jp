---
title: ICorDebugNativeFrame::GetLocalMemoryRegisterValue メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetLocalMemoryRegisterValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetLocalMemoryRegisterValue
helpviewer_keywords:
- ICorDebugNativeFrame::GetLocalMemoryRegisterValue method [.NET Framework debugging]
- GetLocalMemoryRegisterValue method
ms.assetid: 33a19f6e-1029-4d53-af64-19591c6e58ee
topic_type:
- apiref
ms.openlocfilehash: 91f0a75f127afcff89c2b92bf3ed67466b205081
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213050"
---
# <a name="icordebugnativeframegetlocalmemoryregistervalue-method"></a>ICorDebugNativeFrame::GetLocalMemoryRegisterValue メソッド
引数またはローカル変数の値を取得します。この値は、このネイティブフレームについて、指定したレジスタとメモリ位置にそれぞれ、下位ワードと上位ワードが格納されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetLocalMemoryRegisterValue (  
    [in] CORDB_ADDRESS      highWordAddress,  
    [in] CorDebugRegister   lowWordRegister,  
    [in] ULONG              cbSigBlob,  
    [in] PCCOR_SIGNATURE    pvSigBlob,  
    [out] ICorDebugValue    **ppValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `highWordAddress`  
 から`CORDB_ADDRESS`値の上位ワードを格納しているメモリ位置を指定する値。  
  
 `lowWordRegister`  
 から値の下位ワードを含むレジスタを指定する "CorDebugRegister" 列挙体の値。  
  
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
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目
