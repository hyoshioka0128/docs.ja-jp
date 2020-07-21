---
title: ICorDebugModule::EnableJITDebugging メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugModule.EnableJITDebugging
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule::EnableJITDebugging
helpviewer_keywords:
- ICorDebugModule::EnableJITDebugging method [.NET Framework debugging]
- EnableJITDebugging method [.NET Framework debugging]
ms.assetid: 0a65e2a4-5bb6-496c-ae6f-40474426b5a6
topic_type:
- apiref
ms.openlocfilehash: bdf027f94c8416d052cb807d04be76a39868ccf7
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212933"
---
# <a name="icordebugmoduleenablejitdebugging-method"></a>ICorDebugModule::EnableJITDebugging メソッド
Just-in-time (JIT) コンパイラが、このモジュール内のメソッドのデバッグ情報を保持するかどうかを制御します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnableJITDebugging(  
    [in] BOOL bTrackJITInfo,  
    [in] BOOL bAllowJitOpts  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `bTrackJITInfo`  
 からこの値をに設定 `true` すると、このモジュールの各メソッドの MSIL (Microsoft 中間言語) バージョンと jit コンパイルバージョンとの間のマッピング情報を jit コンパイラで保持できるようになります。  
  
 `bAllowJitOpts`  
 からこの値をに設定すると `true` 、jit コンパイラはデバッグのために特定の jit 固有の最適化を使用してコードを生成できます。  
  
## <a name="remarks"></a>Remarks  
 JIT デバッグは、デバッガーがアクティブなときに読み込まれるすべてのモジュールに対して、既定で有効になっています。 プログラムを使用して設定を有効または無効にすると、グローバル設定が上書きされます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
