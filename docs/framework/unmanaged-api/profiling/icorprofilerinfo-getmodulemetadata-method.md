---
title: ICorProfilerInfo::GetModuleMetaData メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetModuleMetaData
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetModuleMetaData
helpviewer_keywords:
- GetModuleMetaData method [.NET Framework profiling]
- ICorProfilerInfo::GetModuleMetaData method [.NET Framework profiling]
ms.assetid: 7a439d92-348a-44dd-b60f-cad7cba56379
topic_type:
- apiref
ms.openlocfilehash: 62b34128be99ce7750d45e6c19e26bef7fcc98c5
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502952"
---
# <a name="icorprofilerinfogetmodulemetadata-method"></a>ICorProfilerInfo::GetModuleMetaData メソッド
指定したモジュールにマップされるメタデータインターフェイスインスタンスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetModuleMetaData(  
    [in]  ModuleID moduleId,  
    [in]  DWORD    dwOpenFlags,  
    [in]  REFIID   riid,  
    [out] IUnknown **ppOut);  
```  
  
## <a name="parameters"></a>パラメーター  
 `moduleId`  
 からインターフェイスインスタンスのマップ先となるモジュールの ID。  
  
 `dwOpenFlags`  
 からマニフェストファイルを開くモードを指定する[Coropenflags](../metadata/coropenflags-enumeration.md)列挙体の値。 、、 `ofRead` およびの各 `ofWrite` ビットのみ `ofNoTransform` が有効です。  
  
 `riid`  
 からインスタンスを取得するメタデータインターフェイスの参照 ID (GUID)。 インターフェイスの一覧については、「[メタデータインターフェイス](../metadata/metadata-interfaces.md)」を参照してください。  
  
 `ppOut`  
 入出力メタデータインターフェイスインスタンスのアドレスへのポインター。  
  
## <a name="remarks"></a>解説  
 メタデータを読み取り/書き込みモードで開くように要求することはできますが、メタデータに対して行われた変更はコンパイラからのものとして最適化できないため、プログラムのメタデータ実行が遅くなります。  
  
 一部のモジュール (リソースモジュールなど) にはメタデータがありません。 このような場合、 `GetModuleMetaData` は S_FALSE の HRESULT 値を返し、* では null を返し `ppOut` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
