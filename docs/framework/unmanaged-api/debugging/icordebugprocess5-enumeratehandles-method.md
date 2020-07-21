---
title: ICorDebugProcess5::EnumerateHandles メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5.EnumerateHandles
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::EnumerateHandles
helpviewer_keywords:
- EnumerateHandles method, ICorDebugProcess5 interface [.NET Framework debugging]
- ICorDebugProcess5::EnumerateHandles method [.NET Framework debugging]
ms.assetid: 7d7fa796-0dc6-4ee8-9d56-40166246d91d
topic_type:
- apiref
ms.openlocfilehash: 291b384d6f0c8c1404b380c653693ec65fcfc960
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213414"
---
# <a name="icordebugprocess5enumeratehandles-method"></a>ICorDebugProcess5::EnumerateHandles メソッド
プロセス内のオブジェクトハンドルの列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumerateHandles(     [in] CorGCReferenceType types,  
    [out] ICorDebugGCReferenceEnum **ppEnum);  
```  
  
## <a name="parameters"></a>パラメーター  
 `types`  
 からコレクションに含めるハンドルの種類を指定する[Corgcreの](corgcreferencetype-enumeration.md)値のビットごとの組み合わせ。  
  
 `ppENum`  
 入出力ガベージコレクションの対象となるオブジェクトの列挙子[である、](icordebuggcreferenceenum-interface.md)ツールのアドレスへのポインターです。  
  
## <a name="remarks"></a>Remarks  
 `EnumerateHandles`は、ハンドルテーブルの検査をサポートするヘルパー関数です。 これは[ICorDebugProcess5:: EnumerateGCReferences](icordebugprocess5-enumerategcreferences-method.md)メソッドに似ていますが、すべてのオブジェクトがガベージコレクトされるよう[に、すべて](icordebuggcreferenceenum-interface.md)のオブジェクトを使用してすべてのオブジェクトを作成するのではなく、handle テーブルからハンドルを持つオブジェクトのみが含まれる点が異なります。  
  
 パラメーターは、 `types` コレクションに含めるハンドルの種類を指定します。 `types`は、 [Corgcreの型](corgcreferencetype-enumeration.md)の列挙体の次の3つのメンバーのいずれかになります。  
  
- `CorHandleStrongOnly`(厳密な参照へのハンドルのみ)。  
  
- `CorHandleWeakOnly`(弱参照のみを処理します)。  
  
- `CorHandleAll`(すべてのハンドル)。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグ構造体](debugging-structures.md)
- [デバッグ](index.md)
