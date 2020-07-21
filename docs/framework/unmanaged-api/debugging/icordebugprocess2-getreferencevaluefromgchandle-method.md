---
title: ICorDebugProcess2::GetReferenceValueFromGCHandle メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2.GetReferenceValueFromGCHandle
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::GetReferenceValueFromGCHandle
helpviewer_keywords:
- GetReferenceValueFromGCHandle method [.NET Framework debugging]
- ICorDebugProcess2::GetReferenceValueFromGCHandle method [.NET Framework debugging]
ms.assetid: 8bdd7f4c-19f2-4ede-875e-603773e8c128
topic_type:
- apiref
ms.openlocfilehash: 143eefd557511f80007c88c1678143a885377467
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212985"
---
# <a name="icordebugprocess2getreferencevaluefromgchandle-method"></a>ICorDebugProcess2::GetReferenceValueFromGCHandle メソッド
ガベージコレクションハンドルを持つ指定したマネージオブジェクトへの参照ポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetReferenceValueFromGCHandle (  
    [in]  UINT_PTR                 handle,  
    [out] ICorDebugReferenceValue  **pOutValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `handle`  
 からガベージコレクションハンドルを持つマネージオブジェクトへのポインター。 この値はオブジェクトであり、 <xref:System.IntPtr> <xref:System.Runtime.InteropServices.GCHandle> マネージオブジェクトのから取得できます。  
  
 `pOutValue`  
 入出力指定したマネージオブジェクトへの参照を表す、値オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 返された参照値とガベージコレクション参照値を混同しないようにしてください。  
  
 返される参照は、通常の参照のように動作します。 ブレークポイント後にコードの実行が続行される場合は無効になります。 ターゲットオブジェクトの有効期間は、参照値の有効期間の影響を受けません。  
  
> [!NOTE]
> メソッドでは `GetReferenceValueFromGCHandle` 、ハンドルは検証されません。 したがって、 `GetReferenceValueFromGCHandle` メソッドは、無効なハンドルが渡された場合に、デバッガーとデバッグされているコードの両方を破損する可能性があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
