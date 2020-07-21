---
title: ICorProfilerAssemblyReferenceProvider::AddAssemblyReference メソッド
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorProfilerAssemblyReferenceProvider.AddAssemblyReference
api_location:
- mscorwks.dll
api_type:
- COM
ms.assetid: 3d5af8e7-c337-48f4-9fa6-97c83878b9b1
topic_type:
- apiref
ms.openlocfilehash: 6d732c6c2871cc5e042b8504db26aabb19963f8c
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500508"
---
# <a name="icorprofilerassemblyreferenceprovideraddassemblyreference-method"></a>ICorProfilerAssemblyReferenceProvider::AddAssemblyReference メソッド
[.NET Framework 4.5.2 以降のバージョンでのみでサポート]  
  
 プロファイラーが[ICorProfilerCallback:: ModuleLoadFinished](icorprofilercallback-moduleloadfinished-method.md)コールバックに追加することを計画しているアセンブリ参照の共通言語ランタイム (CLR) に通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT AddAssemblyReference(  
        const COR_PRF_ASSEMBLY_REFERENCE_INFO* pAssemblyRefInfo  
);  
```  
  
## <a name="parameters"></a>パラメーター

- `pAssemblyRefInfo`

  アセンブリ参照クロージャウォークを実行するときに考慮する必要があるアセンブリ参照に関する情報を CLR に提供する、 [COR_PRF_ASSEMBLY_REFERENCE_INFO](cor-prf-assembly-reference-info-structure.md)構造体へのポインター。
  
## <a name="remarks"></a>解説  
 プロファイラーは、 `wszAssemblyPath` [ICorProfilerCallback6:: GetAssemblyReferences](icorprofilercallback6-getassemblyreferences-method.md)コールバックの引数で指定されたアセンブリから参照するターゲットアセンブリごとに、このメソッドを呼び出します。 [ICorProfilerAssemblyReferenceProvider](icorprofilerassemblyreferenceprovider-interface.md)インターフェイスオブジェクトは、引数のアセンブリパスと名前と共に、プロファイラーの[ICorProfilerCallback6:: GetAssemblyReferences](icorprofilercallback6-getassemblyreferences-method.md)コールバックに渡され `wszAssemblyPath` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerAssemblyReferenceProvider インターフェイス](icorprofilerassemblyreferenceprovider-interface.md)
- [GetAssemblyReferences メソッド](icorprofilercallback6-getassemblyreferences-method.md)
- [ModuleLoadFinished メソッド](icorprofilercallback-moduleloadfinished-method.md)
