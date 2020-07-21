---
title: ICorDebugRuntimeUnwindableFrame インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugUnwindableFrame
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugUnwindableFrame
helpviewer_keywords:
- ICorDebugUnwindableFrame interface [.NET Framework debugging]
ms.assetid: cd6a3982-6ed3-4909-808d-a66055e813e0
topic_type:
- apiref
ms.openlocfilehash: a7b0608e85411844828cebea34c0ce5ef5b1bd11
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379383"
---
# <a name="icordebugruntimeunwindableframe-interface"></a>ICorDebugRuntimeUnwindableFrame インターフェイス
共通言語ランタイム (CLR: Common Language Runtime) でフレームをアンワインドする必要のあるアンマネージ メソッドに対してサポートを提供します。  
  
## <a name="remarks"></a>Remarks  
 `ICorDebugRuntimeUnwindableFrame`は、テキストフレームインターフェイスの特殊なバージョンです。 これは、ランタイムが現在のスタック上のフレームをアンワインドする必要があるアンマネージメソッドによって使用されます。 既存のアンワインド規則は、JIT コンパイルコードを使用しないため、機能しません。 デバッガーに unwindable フレームが表示された場合、そのフレームをアンワインドするには、[次](icordebugstackwalk-next-method.md)のメソッドを使用する必要がありますが、検査自体を実行する必要があります。 デバッガーは、を受け取ると `ICorDebugRuntimeUnwindableFrame` 、テキストフレームのコンテキストを取得するために[、を](icordebugstackwalk-getcontext-method.md)呼び出すことができます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
