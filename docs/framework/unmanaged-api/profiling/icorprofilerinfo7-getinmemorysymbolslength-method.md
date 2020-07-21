---
title: 'ICorProfilerInfo7:: Getinmemoryシンボルの長さメソッド'
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo7.GetInMemorySymbolsLength
api_location:
- mscorwks.dll
- icorprof.idl
api_type:
- COM
ms.assetid: d62c4a4c-8a62-45aa-8f01-a8387cf36159
ms.openlocfilehash: 43d6bdeae5f522bd73b0bdf3a5c403ec69ee384c
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84495439"
---
# <a name="icorprofilerinfo7getinmemorysymbolslength-method"></a>ICorProfilerInfo7:: Getinmemoryシンボルの長さメソッド
[.NET Framework 4.6.1 以降のバージョンでのみでサポート]  
  
 メモリ内シンボルストリームの長さを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetInMemorySymbolsLength(  
        [in] ModuleID moduleId,  
        [out] DWORD* pCountSymbolBytes  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `moduleId`  
 からメモリ内ストリームを格納しているモジュールの識別子。  
  
 Pcountシンボルバイト数  
 入出力`DWORD`メソッドから制御が戻るときに、ストリーム長がバイト単位で格納されている値へのポインター。  
  
## <a name="return-value"></a>戻り値  
 `S_OK`メモリストリームの長さがゼロ (0) であっても、このメソッドはを返します。  
  
 メソッドが `CORPROF_E_MODULE_IS_DYNAMIC` を使用して作成された場合、メソッドはを返し <xref:System.Reflection.Emit?displayProperty=nameWithType> ます。  
  
## <a name="remarks"></a>解説  
 モジュールにメモリ内シンボルがある場合は、ストリームの長さがに配置され `pCountSymbolBytes` ます。 モジュールにメモリ内シンボルがない場合は `*pCountSymbolBytes = 0` 。  
  
> [!NOTE]
> 現在の実装では、リフレクションはサポートされていません。 モジュールがリフレクションを使用して作成された場合、メソッドは `CORPROF_E_MODULE_IS_DYNAMIC` を返します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo7 インターフェイス](icorprofilerinfo7-interface.md)
