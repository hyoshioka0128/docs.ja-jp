---
title: ICorProfilerInfo4::GetILToNativeMapping2 メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.GetILToNativeMapping2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::GetILToNativeMapping2
helpviewer_keywords:
- ICorProfilerInfo4::GetILToNativeMapping2 method [.NET Framework profiling]
- GetILToNativeMapping2 method, ICorProfilerInfo4 interface [.NET Framework profiling]
ms.assetid: 756c1c25-08a7-4060-9798-dbeaa2f3bee5
topic_type:
- apiref
ms.openlocfilehash: 9a6ee58cda5e0b673b3ff1378240f89323e30194
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496062"
---
# <a name="icorprofilerinfo4getiltonativemapping2-method"></a>ICorProfilerInfo4::GetILToNativeMapping2 メソッド
Microsoft Intermediate Language (MSIL) オフセットから、指定した関数の JIT 再コンパイル バージョンに含まれるコードのネイティブ オフセットへのマップを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetILToNativeMapping(  
    [in] FunctionID functionId,  
    [in] ReJITID reJitId,  
    [in] ULONG32 cMap,  
    [out] ULONG32 *pcMap,  
    [out, size_is(cMap), length_is(*pcMap)]  
        COR_DEBUG_IL_TO_NATIVE_MAP map[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `functionId`  
 [in] コードを含む関数の ID。  
  
 `pReJitId`  
 [in] JIT 再コンパイルされた関数のID。 .NET Framework 4.5 では、id は0である必要があります。  
  
 `cMap`  
 [in] `map` 配列の最大サイズ。  
  
 `pcMap`  
 [out]使用できる COR_DEBUG_IL_TO_NATIVE_MAP 構造体の総数。  
  
 `map`  
 [out] `COR_DEBUG_IL_TO_NATIVE_MAP` 構造体の配列。各構造体はオフセットを指定します。 `GetILToNativeMapping2` メソッドから制御が戻ると、`COR_DEBUG_IL_TO_NATIVE_MAP` 構造体の一部または全部が `map` に格納されます。  
  
## <a name="remarks"></a>解説  
 `GetILToNativeMapping2`は[ICorProfilerInfo:: GetILToNativeMapping](icorprofilerinfo-getiltonativemapping-method.md)メソッドに似ていますが、今後のリリースでプロファイラーが再コンパイルされた関数の ID を指定できる点が異なります。  
  
> [!NOTE]
> [ICorProfilerFunctionControl:: SetILInstrumentedCodeMap](icorprofilerfunctioncontrol-setilinstrumentedcodemap-method.md)メソッドは .NET Framework 4.5 で実装されていないため、JIT 再コンパイルされた関数は、最初にコンパイルされた関数とは異なる IL からネイティブへのマッピングを持つことができません。 そのため、 `GetILToNativeMapping2` .NET Framework 4.5 では、0以外の JIT 再コンパイル ID で呼び出すことはできません。  
  
 `GetILToNativeMapping2` メソッドは、`COR_DEBUG_IL_TO_NATIVE_MAP` 構造体の配列を返します。 ネイティブ命令の特定の範囲がコードの特別な領域 (プロローグなど) に対応することを伝えるために、配列内のエントリは、その `ilOffset` フィールドを[CorDebugIlToNativeMappingTypes](../debugging/cordebugiltonativemappingtypes-enumeration.md)列挙値に設定できます。  
  
 `GetILToNativeMapping2` から制御が戻ったら、`map` バッファーのサイズが十分で、すべての `COR_DEBUG_IL_TO_NATIVE_MAP` 構造体を格納できたかどうかを確認する必要があります。 これを行うには、`cMap` の値を `pcMap` パラメーターの値と比較します。 `pcMap` 値 に `COR_DEBUG_IL_TO_NATIVE_MAP` 構造体のサイズを乗算した結果が `cMap` より大きい場合は、`map` バッファーの割り当てを増やし、`cMap` を新しい大きいサイズに更新した後、`GetILToNativeMapping2` を再度呼び出します。  
  
 別の方法として、最初に `GetILToNativeMapping2` を長さゼロの `map` バッファーで呼び出して、適切なバッファーのサイズを取得します。 その後、バッファーのサイズを `pcMap` で返された値に設定し、`GetILToNativeMapping2` を再度呼び出します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [GetILToNativeMapping メソッド](icorprofilerinfo-getiltonativemapping-method.md)
- [ICorProfilerInfo4 インターフェイス](icorprofilerinfo4-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [プロファイル](index.md)
