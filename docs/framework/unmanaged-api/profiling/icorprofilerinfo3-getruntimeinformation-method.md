---
title: ICorProfilerInfo3::GetRuntimeInformation メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.GetRuntimeInformation Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::GetRuntimeInformation
helpviewer_keywords:
- GetRuntimeInformation method [.NET Framework profiling]
- ICorProfilerInfo3::GetRuntimeInformation method [.NET Framework profiling]
ms.assetid: 4400fb8c-0407-4791-8557-f011fd2aee51
topic_type:
- apiref
ms.openlocfilehash: b8e503af11fa1d02aac2ec83edde0ffbd562d8e5
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496400"
---
# <a name="icorprofilerinfo3getruntimeinformation-method"></a>ICorProfilerInfo3::GetRuntimeInformation メソッド
プロファイリングされている共通言語ランタイム (CLR) に関するバージョン情報を提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetRuntimeInformation(  
       [out] USHORT *pClrInstanceId,  
       [out] COR_PRF_RUNTIME_TYPE *pRuntimeType,  
       [out] USHORT *pMajorVersion,  
       [out] USHORT *pMinorVersion,  
       [out] USHORT *pBuildNumber,  
       [out] USHORT *pQFEVersion,  
       [in]  ULONG  cchVersionString,  
       [out] ULONG  *pcchVersionString,  
       [out, size_is(cchVersionString), length_is(*pcchVersionString)]  
                   WCHAR  szVersionString[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pClrInstanceId`  
 入出力プロセス内で実行されている CLR インスタンスの代表 ID。 これは、 `ClrInstanceID` event tracing For Windows (ETW) のスタートアップイベントによって報告されると同じです。  
  
 `pRuntimeType`  
 入出力ランタイム型。 このパラメーター `COR_PRF_DESKTOP_CLR` は、clr のデスクトップバージョンに対して、または `COR_PRF_CORE_CLR` Silverlight で使用される clr のコアバージョンに対してを返します。  
  
 `pMajorVersion`  
 入出力CLR のメジャーバージョン番号。  
  
 `pMinorVersion`  
 入出力CLR のマイナーバージョン番号。  
  
 `pBuildVersion`  
 入出力CLR のビルドバージョン番号。  
  
 `pQFEVersion`  
 入出力ソフトウェア更新プログラムに関連付けられている CLR のバージョン番号。  
  
 `cchVersionString`  
 からが指すバッファーの長さ (文字数) `szVersionString` 。  
  
 `pcchVersionString`  
 入出力の長さ (文字数) `szVersionString` 。  
  
 `szVersionString`  
 入出力CLR のバージョン文字列。  
  
## <a name="remarks"></a>解説  
 任意のパラメーターに null を渡すことができます。 ただし、が null の場合を除き、を `pcchVersionString` null にすることはできません `szVersionString` 。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo3 インターフェイス](icorprofilerinfo3-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [プロファイル](index.md)
