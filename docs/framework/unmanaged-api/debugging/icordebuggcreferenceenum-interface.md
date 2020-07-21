---
title: ICorDebugGCReferenceEnum インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugGCReferenceEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugGCReferenceEnum
helpviewer_keywords:
- ICorDebugGCReferenceEnum interface [.NET Framework debugging]
ms.assetid: 5f3c91c9-c035-454f-96cc-011cab1ea06b
topic_type:
- apiref
ms.openlocfilehash: 5650a7e6e6cb0108f0d043914ea94debe2b703bf
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213102"
---
# <a name="icordebuggcreferenceenum-interface"></a>ICorDebugGCReferenceEnum インターフェイス
ガベージ コレクトされるオブジェクトの列挙子を提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Next メソッド](icordebuggcreferenceenum-next-method.md)|ガベージコレクトされるオブジェクトに関する情報を格納している、指定した数の[COR_GC_REFERENCE](cor-gc-reference-structure.md)インスタンスを取得します。|  
  
## <a name="remarks"></a>Remarks  
 `ICorDebugGCReferenceEnum`インターフェイスは、"ICorDebugEnum" インターフェイスを実装します。  
  
 `ICorDebugGCReferenceEnum`インスタンスには、 [ICorDebugProcess5:: EnumerateGCReferences](icordebugprocess5-enumerategcreferences-method.md)メソッドを呼び出すことによって[COR_GC_REFERENCE](cor-gc-reference-structure.md)インスタンスが設定されます。 [COR_GC_REFERENCE](cor-gc-reference-structure.md)オブジェクトは、 [ICorDebugGCReference:: Next](icordebuggcreferenceenum-next-method.md)メソッドを呼び出すことによって列挙できます。  
  
 このメソッドによって設定されるコレクション内の[COR_GC_REFERENCE](cor-gc-reference-structure.md)オブジェクトは、次の3種類のオブジェクトを表します。  
  
- すべてのマネージスタックからのオブジェクト。 これには、マネージコードのライブ参照や、共通言語ランタイムによって作成されたオブジェクトが含まれます。  
  
- ハンドルテーブルのオブジェクト。 これには、モジュール内の厳密な参照 ( `HNDTYPE_STRONG` および `HNDTYPE_REFCOUNT` ) と静的変数が含まれます。  
  
- ファイナライザーキューからのオブジェクト。 ファイナライザーが実行されるまで、ファイナライザーはオブジェクトをキューに置いています。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
