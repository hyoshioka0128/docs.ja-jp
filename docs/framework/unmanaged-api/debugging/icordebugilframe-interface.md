---
title: ICorDebugILFrame インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame
helpviewer_keywords:
- ICorDebugILFrame interface [.NET Framework debugging]
ms.assetid: d5cf5056-da4d-4629-914d-afe42a5393df
topic_type:
- apiref
ms.openlocfilehash: 1f1e42cd929d2d6282d282cf62dce00104b3a925
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210242"
---
# <a name="icordebugilframe-interface"></a>ICorDebugILFrame インターフェイス

Microsoft 中間言語 (MSIL) コードのスタックフレームを表します。 このインターフェイスは、テキストボックスのインターフェイスのサブクラスです。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[CanSetIP メソッド](icordebugilframe-cansetip-method.md)|命令ポインターを指定したオフセット位置に安全に設定できるかどうかを示す値を取得します。|  
|[EnumerateArguments メソッド](icordebugilframe-enumeratearguments-method.md)|このフレーム内の引数の列挙子を取得します。|  
|[EnumerateLocalVariables メソッド](icordebugilframe-enumeratelocalvariables-method.md)|このフレーム内のローカル変数の列挙子を取得します。|  
|[GetArgument メソッド](icordebugilframe-getargument-method.md)|この MSIL スタックフレーム内の指定された引数の値を取得します。|  
|[GetIP メソッド](icordebugilframe-getip-method.md)|命令ポインターの値と、命令ポインターの値が取得された方法を示すビットごとの組み合わせ値を取得します。|  
|[GetLocalVariable メソッド](icordebugilframe-getlocalvariable-method.md)|この MSIL スタックフレーム内の指定したローカル変数の値を取得します。|  
|[GetStackDepth メソッド](icordebugilframe-getstackdepth-method.md)|実装されていません。|  
|[GetStackValue メソッド](icordebugilframe-getstackvalue-method.md)|実装されていません。|  
|[SetIP メソッド](icordebugilframe-setip-method.md)|命令ポインターを MSIL コード内の指定したオフセット位置に設定します。|  
  
## <a name="remarks"></a>Remarks  
 インターフェイスは、 `ICorDebugILFrame` 特別なテキストフレームインターフェイスです。 これは、MSIL コードフレームまたは just-in-time (JIT) コンパイルフレームに対して使用されます。 JIT でコンパイルされたフレームは、 `ICorDebugILFrame` インターフェイスとの両方のフレームインターフェイスを実装します。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
