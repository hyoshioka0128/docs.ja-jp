---
title: ICorProfilerInfo::SetILInstrumentedCodeMap メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.SetILInstrumentedCodeMap
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::SetILInstrumentedCodeMap
helpviewer_keywords:
- ICorProfilerInfo::SetILInstrumentedCodeMap method [.NET Framework profiling]
- SetILInstrumentedCodeMap method [.NET Framework profiling]
ms.assetid: bce1dcf8-b4ec-4e73-a917-f2df1ad49c8a
topic_type:
- apiref
ms.openlocfilehash: cac8e9570dab55af6b6e1fcf6f53b6a697727972
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502913"
---
# <a name="icorprofilerinfosetilinstrumentedcodemap-method"></a>ICorProfilerInfo::SetILInstrumentedCodeMap メソッド

指定された MSIL (Microsoft 中間言語) マップエントリを使用して、指定された関数のコードマップを設定します。

> [!NOTE]
> .NET Framework バージョン2.0 では、 `SetILInstrumentedCodeMap` `FunctionID` 特定のアプリケーションドメインのジェネリック関数を表すでを呼び出すと、アプリケーションドメイン内のその関数のすべてのインスタンスに影響します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetILInstrumentedCodeMap(
    [in]  FunctionID functionId,
    [in]  BOOL       fStartJit,
    [in]  ULONG      cILMapEntries,
    [in, size_is(cILMapEntries)] COR_IL_MAP rgILMapEntries[]);
```

## <a name="parameters"></a>パラメーター

`functionId`\
からコードマップを設定する関数の ID。

`fStartJit`\
からメソッドの呼び出し `SetILInstrumentedCodeMap` が、特定のの最初のメソッドであるかどうかを示すブール値 `FunctionID` 。 `fStartJit`指定されたの最初の呼び出しでをに設定し、それ以降の場合はに設定し `true` `SetILInstrumentedCodeMap` `FunctionID` `false` ます。

`cILMapEntries`\
から配列内の要素の数 `cILMapEntries` 。

`rgILMapEntries`\
からCOR_IL_MAP 構造体の配列。それぞれが MSIL オフセットを指定します。

## <a name="remarks"></a>解説

多くの場合、プロファイラーは、メソッドのソースコード内にステートメントを挿入して、そのメソッドをインストルメント化します (たとえば、特定のソース行に到達したときに通知します)。 `SetILInstrumentedCodeMap`プロファイラーが元の MSIL 命令を新しい場所にマップできるようにします。 プロファイラーは、 [ICorProfilerInfo:: GetILToNativeMapping](icorprofilerinfo-getiltonativemapping-method.md)メソッドを使用して、指定されたネイティブオフセットの元の MSIL オフセットを取得できます。

デバッガーは、古い各オフセットが元の変更されていない MSIL コード内の MSIL オフセットを参照し、新しい各オフセットが新しいインストルメント化されたコード内の MSIL オフセットを参照することを想定します。 マップは昇順に並べ替える必要があります。 ステップ実行を正常に行うには、次のガイドラインに従ってください。

- インストルメント化された MSIL コードの順序を変更しません。

- 元の MSIL コードは削除しないでください。

- マップ内のプログラムデータベース (PDB) ファイルからのすべてのシーケンスポイントのエントリを含めます。 マップでは、不足しているエントリは補間されません。 そのため、次のマップを指定します。

  (古い0、新規 0)

  (5 歳、10新規)

  (9 歳、20新規)

  - 古いオフセット0、1、2、3、または4が新しいオフセット0にマップされます。

  - 古いオフセット5、6、7、または8は、新しいオフセット10にマップされます。

  - 9以上の古いオフセットは、新しいオフセット20にマップされます。

  - 新しいオフセット0、1、2、3、4、5、6、7、8、または9が古いオフセット0にマップされます。

  - 新しいオフセット10、11、12、13、14、15、16、17、18、19は、古いオフセット5にマップされます。

  - 20以上の新しいオフセットは、古いオフセット9にマップされます。

.NET Framework 3.5 およびそれ以前のバージョンでは、 `rgILMapEntries` [CoTaskMemAlloc](/windows/desktop/api/combaseapi/nf-combaseapi-cotaskmemalloc)メソッドを呼び出すことによって配列を割り当てます。 ランタイムはこのメモリの所有権を取得するため、プロファイラーは解放を試みることはできません。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

**ヘッダー** : CorProf.idl、CorProf.h

**ライブラリ:** CorGuids.lib

**.NET Framework のバージョン:**[!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]

## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
