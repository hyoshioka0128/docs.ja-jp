---
title: ICorDebugEval::NewObjectNoConstructor メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugEval.NewObjectNoConstructor
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::NewObjectNoConstructor
helpviewer_keywords:
- NewObjectNoConstructor method [.NET Framework debugging]
- ICorDebugEval::NewObjectNoConstructor method [.NET Framework debugging]
ms.assetid: 80d509ca-b5e3-4c46-9c14-800db73d9bf7
topic_type:
- apiref
ms.openlocfilehash: d41216eb7da57d29d67ce17372f746328204649e
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976175"
---
# <a name="icordebugevalnewobjectnoconstructor-method"></a>ICorDebugEval::NewObjectNoConstructor メソッド
コンストラクターメソッドを呼び出さずに、指定した型の新しいオブジェクトインスタンスを割り当てます。  
  
 このメソッドは .NET Framework バージョン2.0 では廃止されています。 代わりに[ICorDebugEval2:: NewParameterizedObjectNoConstructor](icordebugeval2-newparameterizedobjectnoconstructor-method.md)を使用してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT NewObjectNoConstructor (  
    [in] ICorDebugClass     *pClass  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pClass`  
 からインスタンス化するオブジェクトの型を表す、のオブジェクトへのポインター。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** 1.1、1.0  
  
## <a name="see-also"></a>関連項目

- [NewParameterizedObjectNoConstructor メソッド](icordebugeval2-newparameterizedobjectnoconstructor-method.md)
