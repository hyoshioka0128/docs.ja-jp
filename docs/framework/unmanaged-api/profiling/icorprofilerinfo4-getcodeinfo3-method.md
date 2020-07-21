---
title: ICorProfilerInfo4::GetCodeInfo3 メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.GetCodeInfo3
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::GetCodeInfo3
helpviewer_keywords:
- GetCodeInfo3 method, ICorProfilerInfo4 interface [.NET Framework profiling]
- ICorProfilerInfo4::GetCodeInfo3 method [.NET Framework profiling]
ms.assetid: bb8c105e-4d9a-4684-8c05-ed6909cc1b8c
topic_type:
- apiref
ms.openlocfilehash: 54e522aaaf23ae81b96b6be7168a9a13f28a16d2
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496140"
---
# <a name="icorprofilerinfo4getcodeinfo3-method"></a>ICorProfilerInfo4::GetCodeInfo3 メソッド
指定した関数の JIT 再コンパイル バージョンに関連付けられているネイティブ コードの範囲を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCodeInfo3(  
    [in]  FunctionID functionID,  
    [in]  ReJITID reJitId,  
    [in]  ULONG32 cCodeInfos,  
    [out] ULONG32 *pcCodeInfos,  
    [out, size_is(cCodeInfos), length_is(*pcCodeInfos)]  
    COR_PRF_CODE_INFO codeInfos[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `functionID`  
 [in] ネイティブ コードが関連付けられている関数の ID。  
  
 `reJitId`  
 [in] JIT 再コンパイルされた関数のID。  
  
 `cCodeInfos`  
 [in] `codeInfos` 配列のサイズ。  
  
 `pcCodeInfos`  
 入出力使用可能な[COR_PRF_CODE_INFO](cor-prf-code-info-structure.md)構造体の合計数へのポインター。  
  
 `codeInfos`  
 [out] 呼び出し元が提供したバッファー。 メソッドから制御が戻った後で、それぞれがネイティブ コードのブロックを記述する `COR_PRF_CODE_INFO` の構造体の配列が含まれます。  
  
## <a name="remarks"></a>解説  
 `GetCodeInfo3`メソッドは、指定された IP アドレスを含む関数の JIT 再コンパイルされた ID を取得する点を除いて、 [GetCodeInfo2](icorprofilerinfo2-getcodeinfo2-method.md)に似ています。  
  
> [!NOTE]
> `GetCodeInfo3`はガベージコレクションをトリガーできますが、 [GetCodeInfo2](icorprofilerinfo2-getcodeinfo2-method.md)はトリガーしません。 詳細については、 [CORPROF_E_UNSUPPORTED_CALL_SEQUENCE](corprof-e-unsupported-call-sequence-hresult.md) HRESULT を参照してください。  
  
 エクステントは共通中間言語 (CIL) オフセットの昇順に並べ替えられます。  
  
 が返された後 `GetCodeInfo3` 、バッファーが `codeInfos` すべての[COR_PRF_CODE_INFO](cor-prf-code-info-structure.md)構造を格納するのに十分な大きさであったことを確認する必要があります。 これを行うには、`cCodeInfos` の値を `cchName` パラメーターの値と比較します。 `cCodeInfos` [COR_PRF_CODE_INFO](cor-prf-code-info-structure.md)構造体のサイズで除算されたがより小さい場合は `pcCodeInfos` 、大きいバッファーを割り当て、を `codeInfos` `cCodeInfos` 新しい大きいサイズに更新して、を `GetCodeInfo3` 再度呼び出します。  
  
 別の方法として、最初に `GetCodeInfo3` を長さゼロの `codeInfos` バッファーで呼び出して、適切なバッファーのサイズを取得します。 次に、 `codeInfos` バッファーサイズをで返された値に設定し、 `pcCodeInfos` [COR_PRF_CODE_INFO](cor-prf-code-info-structure.md)構造体のサイズを乗算して、を `GetCodeInfo3` 再度呼び出します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [GetCodeInfo2 メソッド](icorprofilerinfo2-getcodeinfo2-method.md)
- [ICorProfilerInfo4 インターフェイス](icorprofilerinfo4-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [プロファイル](index.md)
