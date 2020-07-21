---
title: ICoreClrDebugTarget::FreeMemory メソッド
ms.date: 03/30/2017
api_name:
- ICoreDebugTarget.FreeMemory
api_location:
- mscordbi_macx86.dll
api_type:
- COM
f1_keywords:
- ICoreClrDebugTarget::FreeMemory
helpviewer_keywords:
- remote debugging API [Silverlight]
- FreeMemory method, ICoreClrDebugTarget interface [Silverlight debugging]
- ICorClrDebugTarget::FreeMemory method [Silverlight debugging]
- Silverlight, remote debugging
ms.assetid: 98f2a0db-a6ec-4f9b-861d-f82485237d08
topic_type:
- apiref
ms.openlocfilehash: 061a2b9990d4b4d6398d0a31b97bc403a5f10de4
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83397167"
---
# <a name="icoreclrdebugtargetfreememory-method"></a>ICoreClrDebugTarget::FreeMemory メソッド
[ICoreClrDebugTarget:: EnumProcesses](icoreclrdebugtarget-enumprocesses-method.md)メソッドおよび[ICoreClrDebugTarget:: enumruntimes](icoreclrdebugtarget-enumruntimes-method.md)メソッドによって割り当てられたメモリを解放します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
void FreeMemory (  
     [in] void*pMemory);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pMemory`  
 から[ICoreClrDebugTarget:: EnumProcesses](icoreclrdebugtarget-enumprocesses-method.md)または[ICoreClrDebugTarget:: enumruntimes](icoreclrdebugtarget-enumruntimes-method.md)メソッドによって返される配列へのポインター。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Coreclrremoteデバッグインターフェイス .h  
  
 **Library:** mscordbi_macx86 .dll  
  
 **.NET Framework のバージョン:** 3.5 SP1  
  
## <a name="see-also"></a>関連項目

- [ICoreClrDebugTarget インターフェイス](icoreclrdebugtarget-interface.md)
