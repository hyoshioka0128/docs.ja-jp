---
title: ICorProfilerCallback5::ConditionalWeakTableElementReferences メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback5.ConditionalWeakTableReferences
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ConditionalWeakTableElementReferences
helpviewer_keywords:
- ConditionalWeakTableElementReferences method, ICorProfilerCallback5 interface [.NET Framework profiling]
- ICorProfilerCallback5::ConditionalWeakTableElementReferences method [.NET Framework profiling]
ms.assetid: 532c7a02-a9de-4cea-bb2b-7f470da594de
topic_type:
- apiref
ms.openlocfilehash: 17fbc99b30921f795c1f7ff882ec73432aade8c6
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499247"
---
# <a name="icorprofilercallback5conditionalweaktableelementreferences-method"></a>ICorProfilerCallback5::ConditionalWeakTableElementReferences メソッド

直接のメンバー フィールド参照および `ConditionalWeakTable` 依存を介してこれらのルーツによって参照されるオブジェクトの推移的終了を識別します。

## <a name="syntax"></a>構文

```cpp
HRESULT ConditionalWeakTableElementReferences(
     [in]                     ULONG    cRootRefs,
     [in, size_is(cRootRefs)] ObjectID keyRefIds[],
     [in, size_is(cRootRefs)] ObjectID valueRefIds[],
     [in, size_is(cRootRefs)] GCHandleID rootIds[]
);
```

## <a name="parameters"></a>パラメーター

`cRootRefs`\
[入力] `keyRefIds`、`valueRefIds` および `rootIds` 配列にある要素数。

`keyRefIds`\
[入力] それぞれが依存ハンドル ペアのプライマリ要素の `ObjectID` を含む、オブジェクト ID の配列。

`valueRefIds`\
[入力] それぞれが依存ハンドル ペアのセカンダリ要素の `ObjectID` を含む、オブジェクト ID の配列。 ( `keyRefIds[i]` `valueRefIds[i]` alive を保持します)。

`rootIds`\
[入力] ガーベッジ コレクション ルートについての追加情報を含む整数を指し示す `GCHandleID` 値の配列

ガーベッジ コレクターがオブジェクトを古い場所から新しい場所へ移動中の可能性があるため、コールバックの間は `ObjectID` メソッドによって返される `ConditionalWeakTableElementReferences` 値の値は無効です。 このため、`ConditionalWeakTableElementReferences` 呼び出しの間、プロファイラーはオブジェクトを検査するべきではありません。 `GarbageCollectionFinished` では、全てのオブジェトが新しい場所へ移動しているので、検査を行うことができます。

## <a name="example"></a>例

次のコード例は、 [ICorProfilerCallback5](icorprofilercallback5-interface.md)を実装し、このメソッドを使用する方法を示しています。

```cpp
HRESULT Callback5Impl::ConditionalWeakTableElementReferences(
    ULONG      cRootRefs,
    ObjectID   keyRefIds[],
    ObjectID   valueRefIds[],
    GCHandleID rootIds[])
{
    printf("Callback5Impl::ConditionalWeakTableElementReferences called\n");
    for (unsigned int i = 0; i < cRootRefs; ++i)
    {
        // Save dependency to XML for later retrieval
        PersistDependencyToXml(rootIds[i], keyRefIds[i], valueRefIds[i]);
        // or store dependency to an internal map
        m_cwt_deps->add_dep(rootIds[i], keyRefIds[i], valueRefIds[i]);
        // or add arc to object graph
        m_obj_graph->add_arc(keyRefIds[i], valueRefIds[i], rootIds[i]);
    }
    return S_OK;
}
```

## <a name="remarks"></a>解説

.NET Framework 4.5 以降のバージョンのプロファイラーは、 [ICorProfilerCallback5](icorprofilercallback5-interface.md)インターフェイスを実装し、メソッドによって指定された依存関係を記録し `ConditionalWeakTableElementReferences` ます。 `ICorProfilerCallback5`エントリによって表されるライブオブジェクト間の依存関係の完全なセットを提供し `ConditionalWeakTable` ます。 これらの依存関係および[ICorProfilerCallback:: ObjectReferences](icorprofilercallback-objectreferences-method.md)メソッドによって指定されたメンバーフィールド参照を使用すると、マネージプロファイラーでライブオブジェクトの完全オブジェクトグラフを生成できます。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

**ヘッダー** : CorProf.idl、CorProf.h

**.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]

## <a name="see-also"></a>関連項目

- [ICorProfilerCallback5 インターフェイス](icorprofilercallback5-interface.md)
