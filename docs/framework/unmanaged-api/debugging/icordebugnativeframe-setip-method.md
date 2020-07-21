---
title: ICorDebugNativeFrame::SetIP メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.SetIP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::SetIP
helpviewer_keywords:
- ICorDebugNativeFrame::SetIP method [.NET Framework debugging]
- SetIP method, ICorDebugNativeFrame interface [.NET Framework debugging]
ms.assetid: 57784a51-c76d-48f8-9392-584d0e1946d9
topic_type:
- apiref
ms.openlocfilehash: 786c0e7b38c74fd02dd6f7536af1899f295b0305
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83206442"
---
# <a name="icordebugnativeframesetip-method"></a>ICorDebugNativeFrame::SetIP メソッド
命令ポインターをネイティブコード内の指定されたオフセット位置に設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetIP (  
    [in] ULONG32 nOffset  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `nOffset`  
 からネイティブコード内のオフセット位置。  
  
## <a name="remarks"></a>Remarks  
 を呼び出す `SetIP` と、現在のスレッドのすべてのフレームとチェーンがすぐに無効になります。 を呼び出した後にデバッガーがフレーム情報を必要とする場合は `SetIP` 、新しいスタックトレースを実行する必要があります。  
  
 [ICorDebug](icordebug-interface.md)は、スタックフレームを有効な状態のままにします。 ただし、フレームが有効な状態の場合でも、ランタイムの場合と同様に、初期化されていないローカル変数などの問題がまだ発生している可能性があります。 呼び出し元は、実行中のプログラムの一貫性を保証する役割を担います。  
  
 64ビットプラットフォームでは、命令ポインターをまたはブロックの外に移動することはできません `catch` `finally` 。 `SetIP`このような移動を64ビットプラットフォームで実行するためにを呼び出すと、エラーを示す HRESULT が返されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目
