---
title: ICorDebugILFrame4 インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame4
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 1e739183-3e05-49e5-846f-4075256e41de
topic_type:
- apiref
ms.openlocfilehash: d0b1c31d45efea4892182c43c801112530361994
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213703"
---
# <a name="icordebugilframe4-interface"></a>ICorDebugILFrame4 インターフェイス
[.NET Framework 4.5.2 以降のバージョンでのみでサポート]  
  
 ローカル変数にアクセスできるようにするメソッドおよび中間言語 (IL) コードのスタック フレームのコードを提供します。 パラメーターは、プロファイラーの ReJIT インストルメンテーションに追加される変数およびコードへデバッガーがアクセスできるかどうかを指定します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[EnumerateLocalVariablesEx メソッド](icordebugilframe4-enumeratelocalvariablesex-method.md)|現在のフレームで使用可能なローカル変数の一覧を返します。|  
|[GetCodeEx メソッド](icordebugilframe4-getcodeex-method.md)|このスタック フレームが実行するコードを返します。|  
|[GetLocalVariableEx メソッド](icordebugilframe4-getlocalvariableex-method.md)|IL フレーム内のローカル変数の値を返します。|  
  
## <a name="remarks"></a>Remarks  
 これらのメソッドは、 [EnumerateLocalVariables](icordebugilframe-enumeratelocalvariables-method.md)、 [GetCode](icordebugframe-getcode-method.md)、および[getlocalvariable](icordebugilframe-getlocalvariable-method.md)の各メソッドによって提供される機能に加えて機能を提供します。 各メソッドには、追加のローカル変数またはプロファイラーの ReJIT 要求によって定義されているコードが参照可能かどうかを指定する `flags` パラメーターが含まれます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
