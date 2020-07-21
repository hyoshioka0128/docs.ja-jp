---
title: ICorProfilerCallback6::GetAssemblyReferences メソッド
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorProfilerCallback6.GetAssemblyReferences
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
ms.assetid: 8b391afb-d79f-41bd-94ce-43ce62c6b5fc
topic_type:
- apiref
ms.openlocfilehash: 5deacbff740ebb1dcc8cb8d1fb7e4eb0d4bdcc30
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499221"
---
# <a name="icorprofilercallback6getassemblyreferences-method"></a>ICorProfilerCallback6::GetAssemblyReferences メソッド
[.NET Framework 4.5.2 以降のバージョンでのみでサポート]  
  
 共通言語ランタイムがアセンブリ参照クロージャのウォークを実行するときに、アセンブリがごく初期のローディング状態であることをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetAssemblyReferences(        [in, string] const WCHAR* wszAssemblyPath,  
        [in] ICorProfilerAssemblyReferenceProvider* pAsmRefProvider  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `wszAssemblyPath`  
 [in] メタデータが変更されるアセンブリのパスおよび名前。  
  
 `pAsmRefProvider`  
 から追加するアセンブリ参照を指定する[ICorProfilerAssemblyReferenceProvider](icorprofilerassemblyreferenceprovider-interface.md)インターフェイスのアドレスへのポインター。  
  
## <a name="return-value"></a>戻り値  
 このコールバックからの戻り値は無視されます。  
  
## <a name="remarks"></a>解説  
 このコールバックは、 [ICorProfilerCallback5:: SetEventMask2](icorprofilerinfo5-seteventmask2-method.md)メソッドを呼び出すときに、 [COR_PRF_HIGH_ADD_ASSEMBLY_REFERENCES](cor-prf-high-monitor-enumeration.md)イベントマスクフラグを設定することによって制御されます。 プロファイラーが[ICorProfilerCallback6:: GetAssemblyReferences](icorprofilercallback6-getassemblyreferences-method.md) callback メソッドを登録すると、ランタイムは、読み込まれるアセンブリのパスと名前、およびそのメソッドへの[ICorProfilerAssemblyReferenceProvider](icorprofilerassemblyreferenceprovider-interface.md)インターフェイスオブジェクトへのポインターを渡します。 その後、プロファイラーは、 [ICorProfilerAssemblyReferenceProvider::AddAssemblyReference](icorprofilerassemblyreferenceprovider-addassemblyreference-method.md) `COR_PRF_ASSEMBLY_REFERENCE_INFO` コールバックで指定されたアセンブリから参照するターゲットアセンブリごとに、オブジェクトを使用して ICorProfilerAssemblyReferenceProvider:: addassemblyreference メソッドを呼び出すことができます `GetAssemblyReferences` 。  
  
 `GetAssemblyReferences` コールバックを使用するのは、プロファイラーがアセンブリのメタデータを変更してアセンブリ参照を追加する必要がある場合のみです (ただし、アセンブリのメタデータの実際の変更は、 [ICorProfilerCallback:: ModuleLoadFinished](icorprofilercallback-moduleloadfinished-method.md)コールバックメソッドで行われることに注意してください)。プロファイラーは、 `GetAssemblyReferences` モジュールが読み込まれたときにアセンブリ参照が追加されることを共通言語ランタイム (CLR) に通知するために、コールバックメソッドを実装する必要があります。  これにより、プロファイラーが後でメタデータのアセンブリ参照を変更するつもりでも、アセンブリが共有している "初期の段階で CLR によって行われた決定" は有効なままになります。  このため一部のインスタンスでの、プロファイラーのメタデータ変更による `SECURITY_E_INCOMPATIBLE_SHARE` エラーの発生を回避できる場合があります。  
  
 プロファイラーは、このメソッドによって提供される[ICorProfilerAssemblyReferenceProvider](icorprofilerassemblyreferenceprovider-interface.md)オブジェクトを使用して、CLR アセンブリ参照クロージャのウォーカーにアセンブリ参照を追加します。  [ICorProfilerAssemblyReferenceProvider](icorprofilerassemblyreferenceprovider-interface.md)オブジェクトは、このコールバック内からのみ使用する必要があります。 このコールバックから[ICorProfilerAssemblyReferenceProvider:: AddAssemblyReference](icorprofilerassemblyreferenceprovider-addassemblyreference-method.md)メソッドを呼び出すと、変更されたメタデータは生成されませんが、変更されたアセンブリ参照クロージャウォークでのみ発生します。 また、コールバックが実装され[IMetaDataAssemblyEmit](../metadata/imetadataassemblyemit-interface.md)ている場合でも、参照元のアセンブリの[ICorProfilerCallback:: moduleloadfinished](icorprofilercallback-moduleloadfinished-method.md)コールバック内からアセンブリ参照を明示的に追加するには、プロファイラーでは、そのオブジェクトを使用する必要があり `GetAssemblyReferences` ます。  
  
 プロファイラーは、同じアセンブリに対してこのコールバックへの重複する呼び出しを受け取るように準備する必要があります。また、同じ[ICorProfilerAssemblyReferenceProvider:: AddAssemblyReference](icorprofilerassemblyreferenceprovider-addassemblyreference-method.md)呼び出しのセットを作成することによって、重複する各呼び出しに対して同じように応答する必要があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback6 インターフェイス](icorprofilercallback6-interface.md)
- [ModuleLoadFinished メソッド](icorprofilercallback-moduleloadfinished-method.md)
- [COR_PRF_ASSEMBLY_REFERENCE_INFO 構造体](cor-prf-assembly-reference-info-structure.md)
- [ICorProfilerAssemblyReferenceProvider インターフェイス](icorprofilerassemblyreferenceprovider-interface.md)
