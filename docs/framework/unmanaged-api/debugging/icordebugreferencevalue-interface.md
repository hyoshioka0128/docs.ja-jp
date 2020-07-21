---
title: ICorDebugReferenceValue インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugReferenceValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugReferenceValue
helpviewer_keywords:
- ICorDebugReferenceValue interface [.NET Framework debugging]
ms.assetid: 2040e2be-119a-4cfb-ae52-b0b6f052665c
topic_type:
- apiref
ms.openlocfilehash: 6c6ff428e378e973d8846674ffacdcd04b2dbdbc
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378343"
---
# <a name="icordebugreferencevalue-interface"></a>ICorDebugReferenceValue インターフェイス
オブジェクトへの参照である値を管理するメソッドを提供します。 (つまり、このインターフェイスには、ポインターを管理するメソッドが用意されています)。このインターフェイスは、"ICorDebugValue" を実装します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Dereference メソッド](icordebugreferencevalue-dereference-method.md)|参照されているオブジェクトを取得します。|  
|[DereferenceStrong メソッド](icordebugreferencevalue-dereferencestrong-method.md)|実装されていません。 このメソッドは呼び出さないでください。|  
|[GetValue メソッド](icordebugreferencevalue-getvalue-method.md)|参照先のオブジェクトの現在のメモリアドレスを取得します。|  
|[IsNull メソッド](icordebugreferencevalue-isnull-method.md)|このが null 値であるかどうかを示す値を取得します。この値を指定した `ICorDebugReferenceValue` 場合、は `ICorDebugReferenceValue` オブジェクトをポイントしません。|  
|[SetValue メソッド](icordebugreferencevalue-setvalue-method.md)|現在のメモリアドレスを設定します。 つまり、このメソッドは、 `ICorDebugReferenceValue` オブジェクトを指すようにこれを設定します。|  
  
## <a name="remarks"></a>Remarks  
 共通言語ランタイム (CLR) は、デバッグされたプロセスが続行されると、オブジェクトのガベージコレクションを実行する場合があります。 ガベージコレクションでは、メモリ内でオブジェクトを移動できます。 はガベージコレクションと連携して、ガベージコレクション `ICorDebugReferenceValue` の後に情報が更新されるか、ガベージコレクションの前に暗黙的に無効にされます。  
  
 `ICorDebugReferenceValue`デバッグされたプロセスが続行されると、オブジェクトは暗黙的に無効になる可能性があります。 派生された "の値" は、明示的に解放または公開されるまで無効になりません。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
