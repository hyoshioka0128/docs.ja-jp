---
title: COR_PRF_EX_CLAUSE_INFO 構造体
ms.date: 03/30/2017
api_name:
- COR_PRF_EX_CLAUSE_INFO
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_EX_CLAUSE_INFO
helpviewer_keywords:
- COR_PRF_EX_CLAUSE_INFO structure [.NET Framework profiling]
ms.assetid: 7d0d6fb7-bc9d-40f0-8163-c0d162eaba7d
topic_type:
- apiref
ms.openlocfilehash: 5c764031f709eefe61022d0662f37bc5d3f3e281
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501002"
---
# <a name="cor_prf_ex_clause_info-structure"></a>COR_PRF_EX_CLAUSE_INFO 構造体
特定の例外句インスタンスおよび関連するフレームに関する情報を格納します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct COR_PRF_EX_CLAUSE_INFO {  
    COR_PRF_CLAUSE_TYPE clauseType;  
    UINT_PTR programCounter;  
    UINT_PTR framePointer;  
    UINT_PTR shadowStackPointer;  
} COR_PRF_EX_CLAUSE_INFO;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`clauseType`|入力または左にあるコードの例外句の種類を指定する[COR_PRF_CLAUSE_TYPE](cor-prf-clause-type-enumeration.md)列挙体の値。|  
|`programCounter`|句ハンドラーのネイティブエントリポイント (たとえば、X86 EIP レジスタの内容)。|  
|`framePointer`|句ハンドラーの論理フレームへのポインター。たとえば、X86 EBP レジスタの内容。|  
|`shadowStackPointer`|シャドウスタックへのポインター。 この値は、BSP レジスタの内容であり、IA64 にのみ適用されます。|  
  
## <a name="remarks"></a>解説  
 例外通知が受信されると、 [ICorProfilerInfo2:: GetNotifiedExceptionClauseInfo](icorprofilerinfo2-getnotifiedexceptionclauseinfo-method.md)を使用して、実行しようとし `catch` / `finally` ているまたは実行されたばかりの例外句 (フィルター) のネイティブアドレスとフレーム情報を取得できます。  
  
 Exception 句の実行には、共通言語ランタイム (CLR) からのこれらのコールバックが含まれます。  
  
- [ICorProfilerCallback:: ExceptionCatcherEnter](icorprofilercallback-exceptioncatcherenter-method.md)  
  
- [ICorProfilerCallback:: ExceptionUnwindFinallyEnter](icorprofilercallback-exceptionunwindfinallyenter-method.md)  
  
- [ICorProfilerCallback:: ExceptionSearchFilterEnter](icorprofilercallback-exceptionsearchfilterenter-method.md)  
  
- [ICorProfilerCallback:: ExceptionCatcherLeave](icorprofilercallback-exceptioncatcherleave-method.md)  
  
- [ICorProfilerCallback:: ExceptionUnwindFinallyLeave](icorprofilercallback-exceptionunwindfinallyleave-method.md)  
  
- [ICorProfilerCallback:: ExceptionSearchFilterLeave](icorprofilercallback-exceptionsearchfilterleave-method.md)  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Corprof.idl  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [構造体のプロファイリング](profiling-structures.md)
