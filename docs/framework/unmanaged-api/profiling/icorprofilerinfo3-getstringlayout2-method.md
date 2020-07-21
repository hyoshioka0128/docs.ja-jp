---
title: ICorProfilerInfo3::GetStringLayout2 メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.GetStringLayout2 Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::GetStringLayout2
helpviewer_keywords:
- ICorProfilerInfo3::GetStringLayout2 method [.NET Framework profiling]
- GetStringLayout2 method [.NET Framework profiling]
ms.assetid: 1a268496-ee51-4d84-8700-ee56fd0c499d
topic_type:
- apiref
ms.openlocfilehash: 51d5b2f2ee17cc177e3b0ddc7d2e0b82fd70063d
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496374"
---
# <a name="icorprofilerinfo3getstringlayout2-method"></a>ICorProfilerInfo3::GetStringLayout2 メソッド
文字列オブジェクトのレイアウトに関する情報を取得します。 このメソッドは、 [ICorProfilerInfo2:: GetStringLayout](icorprofilerinfo2-getstringlayout-method.md)メソッドよりも優先されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetStringLayout2(  
    [out] ULONG *pStringLengthOffset,  
    [out] ULONG *pBufferOffset);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pStringLengthOffset`  
 入出力`ObjectID`文字列自体の長さを格納する、ポインターを基準とした位置のオフセットへのポインター。 長さはとして格納され `DWORD` ます。  
  
 `pBufferOffset`  
 入出力ワイド文字の文字列を格納するポインターを基準とした、バッファーのオフセットへのポインター `ObjectID` 。  
  
## <a name="remarks"></a>解説  
 文字列は、null で終わることができます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo3 インターフェイス](icorprofilerinfo3-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
