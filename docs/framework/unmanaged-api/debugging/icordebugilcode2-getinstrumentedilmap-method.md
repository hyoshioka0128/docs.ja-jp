---
title: ICorDebugILCode2::GetInstrumentedILMap メソッド
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugILCode2.GetInstrumentedILMap
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 7a4e3085-8f95-40ef-a4be-7d6146f47ce2
topic_type:
- apiref
ms.openlocfilehash: c6fdb7040620bb7a5b6aea6e0dc41e08d6f346d0
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210359"
---
# <a name="icordebugilcode2getinstrumentedilmap-method"></a>ICorDebugILCode2::GetInstrumentedILMap メソッド
[.NET Framework 4.5.2 以降のバージョンでのみでサポート]  
  
 このインスタンスについて、プロファイラー インストルメント中間言語 (IL: intermediate language) オフセットから、元のメソッドの IL オフセットまでのマップを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetInstrumentedILMap(  
   [in] ULONG32 cMap,  
   [out] ULONG32 *pcMap,  
   [out, size_is(cMap), length_is(*pcMap)] COR_IL_MAP map[]  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 cMap  
 [入力] `map` 配列の記憶容量。 詳細については、「解説」を参照してください。  
  
 pcMap  
 [出力] マップ配列へ書き込まれる COR_IL_MAP 値の数。  
  
 map  
 [出力] プロファイラー インストルメント IL から元のメソッドである IL へのマッピングについて情報を提供する COR_IL_MAP 値の配列。  
  
## <a name="remarks"></a>Remarks  
 プロファイラーが[ICorProfilerInfo:: SetILInstrumentedCodeMap](../profiling/icorprofilerinfo-setilinstrumentedcodemap-method.md)メソッドを呼び出すことによってマッピングを設定した場合、デバッガーはこのメソッドを呼び出してマッピングを取得し、スタックトレースと変数の有効期間の IL オフセットを計算するときに、内部的なマッピングを使用できます。  
  
 `cMap`が0で、 `pcMap` が**null**以外の場合、 `pcMap` は使用可能な COR_IL_MAP 値の数に設定されます。 `cMap` が 0 以外の場合は、`map` アレイの記憶容量を表します。 メソッドから制御が戻るとき、に `map` は最大項目が含まれて `cMap` おり、 `pcMap` は配列に実際に書き込まれた COR_IL_MAP 値の数に設定され `map` ます。  
  
 IL がインストルメント化されていない、またはプロファイラーによってマッピングが指定されなかった場合、このメソッドは `S_OK` を返し、`pcMap` を 0 に設定します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo::SetILInstrumentedCodeMap](../profiling/icorprofilerinfo-setilinstrumentedcodemap-method.md)
- [ICorDebugILCode2 インターフェイス](icordebugilcode2-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
