---
title: ICorProfilerInfo3::GetModuleInfo2 メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.GetModuleInfo2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::GetModuleInfo2
helpviewer_keywords:
- ICorProfilerInfo3::GetModuleInfo2 method [.NET Framework profiling]
- GetModuleInfo2 method [.NET Framework profiling]
ms.assetid: f1f6b8f3-dcfc-49e8-be76-ea50ea90d5a7
topic_type:
- apiref
ms.openlocfilehash: d2b7e93866bf0aa79849925234a4d6e4cc9b5b52
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502822"
---
# <a name="icorprofilerinfo3getmoduleinfo2-method"></a>ICorProfilerInfo3::GetModuleInfo2 メソッド
モジュール ID を指定して、モジュールのファイル名、モジュールの親アセンブリの ID、およびモジュールのプロパティを示すビットマスクを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetModuleInfo2(  
    [in]  ModuleID   moduleId,  
    [out] LPCBYTE    *ppBaseLoadAddress,  
    [in]  ULONG      cchName,  
    [out] ULONG      *pcchName,  
    [out, annotation("__out_ecount_part(cchName, *pcchName)")]  
          WCHAR      szName[] ,  
    [out] AssemblyID *pAssemblyId);  
    [out] DWORD                 *pdwModuleFlags);  
```  
  
## <a name="parameters"></a>パラメーター  
 `moduleId`  
 [in] 情報が取得されるモジュールの ID。  
  
 `ppBaseLoadAddress`  
 [out] モジュールが読み込まれるベース アドレス。  
  
 `cchName`  
 [in] `szName` 戻りバッファーの長さ (文字単位)。  
  
 `pcchName`  
 [out] 返されるモジュールのファイル名の文字列長の合計へのポインター。  
  
 `szName`  
 [out] 呼び出し元が提供したワイド文字バッファー。 メソッドから制御が戻るとき、このバッファーにモジュールのファイル名が格納されます。  
  
 `pAssemblyId`  
 [out] モジュールの親アセンブリ ID へのポインター。  
  
 `pdwModuleFlags`  
 入出力モジュールのプロパティを指定する[COR_PRF_MODULE_FLAGS](cor-prf-module-flags-enumeration.md)列挙体の値のビットマスク。  
  
## <a name="remarks"></a>解説  
 動的モジュールの場合、`szName` パラメーターはモジュールのメタデータ名になり、ベース アドレスは 0 (ゼロ) になります。 メタデータ名は、メタデータ内の Module テーブルの Name 列の値です。 これは、マネージコードにプロパティとして公開され、 <xref:System.Reflection.Module.ScopeName%2A?displayProperty=nameWithType> `szName` [IMetaDataImport:: getscopeprops](../metadata/imetadataimport-getscopeprops-method.md)メソッドのパラメーターとしてアンマネージメタデータクライアントコードにも公開されます。  
  
 メソッドは、 `GetModuleInfo2` モジュールの id が存在するとすぐに呼び出される場合がありますが、プロファイラーが[ICorProfilerCallback:: ModuleAttachedToAssembly](icorprofilercallback-moduleattachedtoassembly-method.md)コールバックを受信するまで、親アセンブリの id は使用できません。  
  
 `GetModuleInfo2` から制御が戻ったら、`szName` バッファーのサイズが十分で、モジュールのファイル名全体を格納できたかどうかを確認する必要があります。 これを行うには、`pcchName` が指している値を `cchName` パラメーターの値と比較します。 `pcchName` が指している値が `cchName` の値より大きい場合は、`szName` バッファーの割り当てを増やし、`cchName` を新しい大きいサイズに更新して、`GetModuleInfo2` を再度呼び出します。  
  
 別の方法として、最初に `GetModuleInfo2` を長さゼロの `szName` バッファーで呼び出して、適切なバッファーのサイズを取得します。 その後、バッファーのサイズを `pcchName` で返された値に設定し、`GetModuleInfo2` を再度呼び出します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [プロファイル](index.md)
