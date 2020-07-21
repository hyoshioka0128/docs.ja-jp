---
title: ICorDebugType::GetBase メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugType.GetBase
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::GetBase
helpviewer_keywords:
- ICorDebugType::GetBase method [.NET Framework debugging]
- GetBase method [.NET Framework debugging]
ms.assetid: f24e1af9-c220-4f79-ae62-4153ec17ea81
topic_type:
- apiref
ms.openlocfilehash: fc406f6e87e5b2be48c6fe7d5fc988774ac5cd11
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379982"
---
# <a name="icordebugtypegetbase-method"></a>ICorDebugType::GetBase メソッド
このによって表される型の基本型 (存在する場合) を表す、の型へのインターフェイスポインターを取得し `ICorDebugType` ます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetBase (  
    [out] ICorDebugType   **pBase  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pBase`  
 入出力基本型を表すオブジェクトのアドレスへのポインター `ICorDebugType` 。  
  
## <a name="remarks"></a>Remarks  
 型の基本型を検索すると、オブジェクトまたはその親クラスのすべてのフィールドを出力するなど、一般的なデバッガー機能を実装するのに便利です。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
