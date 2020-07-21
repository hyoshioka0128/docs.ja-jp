---
title: ICorProfilerInfo6::EnumNgenModuleMethodsInliningThisMethod メソッド
ms.date: 03/30/2017
ms.assetid: b933dfe6-7833-40cb-aad8-40842dc3034f
ms.openlocfilehash: 8ed3f305deceacb976aeff994db1588f9e1ce1fb
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84495529"
---
# <a name="icorprofilerinfo6enumngenmodulemethodsinliningthismethod-method"></a>ICorProfilerInfo6::EnumNgenModuleMethodsInliningThisMethod メソッド

特定の NGen モジュールで定義され、指定されたメソッドにインライン化されているすべてのメソッドに対する列挙子を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumNgenModuleMethodsInliningThisMethod(
        [in] ModuleID inlinersModuleId,
        [in] ModuleID inlineeModuleId,
        [in] mdMethodDef inlineeMethodId,
        [out] BOOL *incompleteData,
        [out] ICorProfilerMethodEnum** ppEnum
);
```

## <a name="parameters"></a>パラメーター

`inlinersModuleId`\
からNGen モジュールの識別子。

`inlineeModuleId`\
からを定義するモジュールの識別子 `inlineeMethodId` 。 詳細については、「解説」を参照してください。

`inlineeMethodId`\
からインラインメソッドの識別子。 詳細については、「解説」を参照してください。

`incompleteData`\
入出力`ppEnum`に、指定したメソッドをインライン展開するメソッドがすべて含まれているかどうかを示すフラグ。  詳細については、「解説」を参照してください。

`ppEnum`\
入出力列挙子のアドレスへのポインター

## <a name="remarks"></a>解説

`inlineeModuleId`と `inlineeMethodId` は、インライン化される可能性のあるメソッドの完全な識別子を形成します。 たとえば、module `A` がメソッドを定義するとし `Simple.Add` ます。

```csharp
Simple.Add(int a, int b)
{ return a + b; }
```

モジュール B は次を定義し `Fancy.AddTwice` ます。

```csharp
Fancy.AddTwice(int a, int b)
{ return Simple.Add(a,b) + Simple.Add(a,b); }
```

は、への呼び出しをインラインで使用することも想定 `Fancy.AddTwice` `SimpleAdd` しています。 プロファイラーは、この列挙子を使用して、モジュール B でインラインで定義されているすべてのメソッドを検索し、結果を列挙することができ `Simple.Add` `AddTwice` ます。  `inlineeModuleId`はモジュールの識別子で、 `A` `inlineeMethodId` はの識別子です `Simple.Add(int a, int b)` 。

`incompleteData`関数からが返された後にが true の場合、列挙子には、特定のメソッドをインライン展開するメソッドがすべて含まれているわけではありません。 これは、inliners モジュールの1つ以上の直接または間接的な依存関係がまだ読み込まれていない場合に発生する可能性があります。 プロファイラーが正確なデータを必要とする場合、より多くのモジュールが読み込まれると、後でモジュールの負荷に応じて、後で再試行する必要があります。

`EnumNgenModuleMethodsInliningThisMethod`メソッドを使用すると、ReJIT のインライン展開に関する制限を回避できます。 ReJIT を使用すると、プロファイラーはメソッドの実装を変更し、その場で新しいコードを作成できます。 たとえば、次のように変更でき `Simple.Add` ます。

```csharp
Simple.Add(int a, int b)
{ return 42; }
```

ただし、は既にインライン化されているため `Fancy.AddTwice` `Simple.Add` 、以前と同じ動作を続けます。 この制限を回避するために、呼び出し元は、 `Simple.Add` `ICorProfilerInfo5::RequestRejit` これらの各メソッドでインラインで使用されるすべてのモジュール内のすべてのメソッドを検索する必要があります。 メソッドを再コンパイルすると、以前の動作ではなく、の新しい動作が行われ `Simple.Add` ます。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

**ヘッダー** : CorProf.idl、CorProf.h

**ライブラリ:** CorGuids.lib

**.NET Framework のバージョン:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]

## <a name="see-also"></a>関連項目

- [ICorProfilerInfo6 インターフェイス](icorprofilerinfo6-interface.md)
