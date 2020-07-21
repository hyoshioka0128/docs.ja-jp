---
title: ICorProfilerInfo::GetILFunctionBody メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetILFunctionBody
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetILFunctionBody
helpviewer_keywords:
- GetILFunctionBody method [.NET Framework profiling]
- ICorProfilerInfo::GetILFunctionBody method [.NET Framework profiling]
ms.assetid: e29b46bc-5fdc-4894-b0c2-619df4b65ded
topic_type:
- apiref
ms.openlocfilehash: 5984c63f0e1a1859dd5cc2550d6dc37c963affb3
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503004"
---
# <a name="icorprofilerinfogetilfunctionbody-method"></a>ICorProfilerInfo::GetILFunctionBody メソッド
Microsoft 中間言語 (MSIL) コード内のメソッドの本文へのポインターを、ヘッダーを開始位置として取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetILFunctionBody(  
    [in]  ModuleID    moduleId,  
    [in]  mdMethodDef methodId,  
    [out] LPCBYTE     *ppMethodHeader,  
    [out] ULONG       *pcbMethodSize);  
```  
  
## <a name="parameters"></a>パラメーター  
 `moduleId`  
 から関数が存在するモジュールの ID。  
  
 `methodId`  
 からメソッドのメタデータトークン。  
  
 `ppMethodHeader`  
 入出力メソッドのヘッダーへのポインター。  
  
 `pcbMethodSize`  
 入出力メソッドのサイズを指定する整数。  
  
## <a name="remarks"></a>解説  
 メソッドは、それが存在するモジュールによってスコープが設定されます。 メソッドは、 `GetILFunctionBody` MSIL コードが共通言語ランタイム (CLR) によって読み込まれる前に、ツールにアクセスできるように設計されているため、メソッドのメタデータトークンを使用して目的のインスタンスを検索します。  
  
 `GetILFunctionBody`は、が `methodId` MSIL コード (抽象メソッドやプラットフォーム呼び出し (PInvoke) メソッドなど) を持たないメソッドを指している場合、CORPROF_E_FUNCTION_NOT_IL HRESULT を返すことができます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
