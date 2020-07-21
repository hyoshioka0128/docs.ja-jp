---
title: ICoreClrDebugTarget::EnumRuntimes メソッド
ms.date: 03/30/2017
api_name:
- ICoreClrDebugTarget.EnumRuntimes
api_location:
- mscordbi_macx86.dll
api_type:
- COM
f1_keywords:
- ICoreClrDebugTarget::EnumRuntimes
helpviewer_keywords:
- remote debugging API [Silverlight]
- ICorClrDebugTarget::EnumRuntimes method [Silverlight debugging]
- EnumRuntimes method, ICoreClrDebugTarget interface [Silverlight debugging]
- Silverlight, remote debugging
ms.assetid: 316df866-442d-40cc-b049-45e8adcb65d1
topic_type:
- apiref
ms.openlocfilehash: fc8269d4cc22ab53569edaa48c27b4a01970dcc7
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83397184"
---
# <a name="icoreclrdebugtargetenumruntimes-method"></a>ICoreClrDebugTarget::EnumRuntimes メソッド
リモート コンピューターで実行されている指定のプロセスの共通言語ランタイム (CLR: Common Language Runtime) を列挙します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumRuntimes (  
      [in] DWORD       dwInternalProcessID,  
      [out] DWORD*     pcRuntimes,  
      [out] CoreClrDebugRuntimeInfo**    ppRuntimes  
    );  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwInternalProcessID`  
 [in] ランタイムを列挙するプロセスの内部プロセス ID。 これは `m_dwInternalID` 、対応する[CoreClrDebugProcInfo](coreclrdebugprocinfo-structure.md)からのものになります。  
  
 `pcRuntimes`  
 [out] `ppRuntimes` に返されるランタイム数。 この値は 0 (ゼロ) になる可能性もあります。  
  
 `ppRuntimes`  
 入出力リモートターゲットプロセスに読み込まれたランタイムを表す[CoreClrDebugRuntimeInfo](coreclrdebugruntimeinfo-structure.md)構造体の配列。  
  
## <a name="return-value"></a>戻り値  
 S_OK  
 成功しました。  
  
 S_FALSE  
 `dwInternalProcessID` が、コンピューターで実行されているどのプロセスにも一致しません。多くの場合、プロセスが既に終了していることが原因です。 `pcRuntimes` と `ppRuntimes` は null になります。  
  
 E_OUTOFMEMORY  
 `ppRuntimes`  用に十分なメモリを割り当てることができません。  
  
 E_FAIL (またはその他の E_ リターン コード)  
 その他のエラーが発生しました。  
  
## <a name="remarks"></a>解説  
 このメソッドによって割り当てられたメモリを解放するには、 [ICoreClrDebugTarget:: FreeMemory](icoreclrdebugtarget-freememory-method.md)メソッドを呼び出します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Coreclrremoteデバッグインターフェイス .h  
  
 **Library:** mscordbi_macx86 .dll  
  
 **.NET Framework のバージョン:** 3.5 SP1  
  
## <a name="see-also"></a>関連項目

- [ICoreClrDebugTarget インターフェイス](icoreclrdebugtarget-interface.md)
