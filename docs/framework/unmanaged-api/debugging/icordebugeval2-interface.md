---
title: ICorDebugEval2 インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugEval2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval2
helpviewer_keywords:
- ICorDebugEval2 interface [.NET Framework debugging]
ms.assetid: fce34531-2687-406d-9131-d6ad94f2ce0e
topic_type:
- apiref
ms.openlocfilehash: b597d95b5b25e5ebf04fac48e4f3fda312a9594c
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976123"
---
# <a name="icordebugeval2-interface"></a>ICorDebugEval2 インターフェイス

"" は、"" "のように拡張して、ジェネリック型のサポートを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[CallParameterizedFunction メソッド](icordebugeval2-callparameterizedfunction-method.md)|指定された "" の呼び出しを設定します。この関数は、コンストラクターが型パラメーターを受け取る型の内部に入れ子にすることも、型パラメーターを受け取ることもできます。|  
|[CreateValueForType メソッド](icordebugeval2-createvaluefortype-method.md)|初期値が null または0の、指定した型の新しい "ICorDebugValue" へのポインターを取得します。|  
|[NewParameterizedArray メソッド](icordebugeval2-newparameterizedarray-method.md)|指定した要素の型と次元の新しい配列を割り当てます。|  
|[NewParameterizedObject メソッド](icordebugeval2-newparameterizedobject-method.md)|新しいパラメーター化された型オブジェクトをインスタンス化し、オブジェクトのコンストラクターメソッドを呼び出します。|  
|[NewParameterizedObjectNoConstructor メソッド](icordebugeval2-newparameterizedobjectnoconstructor-method.md)|コンストラクターメソッドを呼び出さずに、指定したクラスの新しいパラメーター化された型オブジェクトをインスタンス化します。|  
|[NewStringWithLength メソッド](icordebugeval2-newstringwithlength-method.md)|指定したコンテンツを使用して、指定した長さの新しい文字列を作成します。|  
|[RudeAbort メソッド](icordebugeval2-rudeabort-method.md)|この`ICorDebugEval2`が現在実行している計算を中止します。|  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
