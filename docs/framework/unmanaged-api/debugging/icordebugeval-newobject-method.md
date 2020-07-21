---
title: ICorDebugEval::NewObject メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugEval.NewObject
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::NewObject
helpviewer_keywords:
- NewObject method [.NET Framework debugging]
- ICorDebugEval::NewObject method [.NET Framework debugging]
ms.assetid: ce3025e8-defa-4c5e-8298-f49d71fa5736
topic_type:
- apiref
ms.openlocfilehash: e9570d3c916123093f69e7f26d3778f1c7184b1f
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976188"
---
# <a name="icordebugevalnewobject-method"></a>ICorDebugEval::NewObject メソッド
新しいオブジェクトインスタンスを割り当て、指定したコンストラクターメソッドを呼び出します。  
  
 このメソッドは .NET Framework バージョン2.0 では廃止されています。 代わりに[ICorDebugEval2:: NewParameterizedObject](icordebugeval2-newparameterizedobject-method.md)を使用してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT NewObject (  
    [in] ICorDebugFunction  *pConstructor,  
    [in] ULONG32            nArgs,  
    [in, size_is(nArgs)] ICorDebugValue *ppArgs[]  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pConstructor`  
 から呼び出されるコンストラクター。  
  
 `nArgs`  
 [in] `ppArgs` 配列のサイズ。  
  
 `ppArgs`  
 からICorDebugValue オブジェクトの配列。各オブジェクトは、コンストラクターに渡される引数を表します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** 1.1、1.0  
  
## <a name="see-also"></a>関連項目

- [NewParameterizedObject メソッド](icordebugeval2-newparameterizedobject-method.md)
