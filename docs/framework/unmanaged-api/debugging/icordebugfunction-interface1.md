---
title: ICorDebugFunction インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugFunction
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction
helpviewer_keywords:
- ICorDebugFunction interface [.NET Framework debugging]
ms.assetid: 783faea9-8083-41c1-b04a-51a81ac4c8f3
topic_type:
- apiref
ms.openlocfilehash: 6b7b6969c1f207decbf47217e98b7fee3aa9ce54
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213243"
---
# <a name="icordebugfunction-interface"></a>ICorDebugFunction インターフェイス

マネージド関数またはマネージド メソッドを表します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[CreateBreakpoint メソッド](icordebugfunction-createbreakpoint-method.md)|この関数の先頭にブレークポイントを作成します。|  
|[GetClass メソッド](icordebugfunction-getclass-method.md)|この関数がメンバーとなっているクラスを表す、のオブジェクトを取得します。|  
|[GetCurrentVersionNumber メソッド](icordebugfunction-getcurrentversionnumber-method.md)|この関数に対して行われた最新の編集のバージョン番号を取得します。|  
|[GetILCode メソッド](icordebugfunction-getilcode-method.md)|この関数の MSIL (Microsoft 中間言語) コードを取得します。|  
|[GetLocalVarSigToken メソッド](icordebugfunction-getlocalvarsigtoken-method.md)|このインスタンスによって表される関数のローカル変数シグネチャのメタデータトークンを取得し `ICorDebugFunction` ます。|  
|[GetModule メソッド](icordebugfunction-getmodule-method.md)|この関数が定義されているモジュールを取得します。|  
|[GetNativeCode メソッド](icordebugfunction-getnativecode-method.md)|この関数のネイティブコードを取得します。|  
|[GetToken メソッド](icordebugfunction-gettoken-method.md)|この関数のメタデータトークンを取得します。|  
  
## <a name="remarks"></a>Remarks  
 インターフェイスは、 `ICorDebugFunction` ジェネリック型パラメーターを持つ関数を表していません。 たとえば、インスタンスはを `ICorDebugFunction` 表しますが、では `Func<T>` ありません `Func<string>` 。 [ICorDebugILFrame2:: EnumerateTypeParameters](icordebugilframe2-enumeratetypeparameters-method.md)を呼び出して、ジェネリック型パラメーターを取得します。  
  
 メソッドのメタデータトークン、 `mdMethodDef` 、およびメソッドのオブジェクト間のリレーションシップ `ICorDebugFunction` は、関数でエディットコンティニュが許可されているかどうかによって異なります。  
  
- 関数でエディットコンティニュを使用できない場合は、オブジェクトとトークンの間に一対一のリレーションシップが存在し `ICorDebugFunction` `mdMethodDef` ます。 つまり、関数は、1つの `ICorDebugFunction` オブジェクトと1つのトークンを持ち `mdMethodDef` ます。  
  
- 関数でエディットコンティニュが許可されている場合は、オブジェクトとトークンの間に多対一のリレーションシップが存在し `ICorDebugFunction` `mdMethodDef` ます。 つまり、関数は、 `ICorDebugFunction` 関数の各バージョンに1つずつ、1つのトークンのみを含むのインスタンスを多数持つことができ `mdMethodDef` ます。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids .lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
