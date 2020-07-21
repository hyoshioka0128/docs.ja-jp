---
title: IMetaDataEmit::MergeEnd メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.MergeEnd
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::MergeEnd
helpviewer_keywords:
- MergeEnd method [.NET Framework metadata]
- IMetaDataEmit::MergeEnd method [.NET Framework metadata]
ms.assetid: 2d64315a-1af1-4c60-aedf-f8a781914aea
topic_type:
- apiref
ms.openlocfilehash: feb81b86190f953b50f43f244f4e58a0a482f86e
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84003920"
---
# <a name="imetadataemitmergeend-method"></a>IMetaDataEmit::MergeEnd メソッド

[IMetaDataEmit:: Merge](imetadataemit-merge-method.md)の1つ以上の前の呼び出しで指定されたすべてのメタデータスコープを現在のスコープにマージします。

## <a name="syntax"></a>構文

```cppcpp
HRESULT MergeEnd ();
```

## <a name="parameters"></a>パラメーター

このメソッドはパラメーターを受け取りません。

## <a name="remarks"></a>コメント

このルーチンは、の前の呼び出しで指定されたすべてのインポートスコープのメタデータの実際のマージを `IMetaDataEmit::Merge` 現在の出力スコープにトリガーします。

マージには、次の特殊な条件が適用されます。

- モジュールバージョン識別子 (MVID) はインポートされません。これは、インポートスコープ内のメタデータに固有であるためです。

- 既存のモジュール全体のプロパティは上書きされません。

  モジュールのプロパティが現在のスコープに対して既に設定されている場合は、モジュールのプロパティはインポートされません。 ただし、モジュールのプロパティが現在のスコープで設定されていない場合は、最初に検出されたときに1回だけインポートされます。 これらのモジュールのプロパティが再度検出された場合、それらは重複しています。 すべてのモジュールプロパティ (MVID を除く) の値が比較され、重複が見つからない場合は、エラーが発生します。

- 型定義 () の場合 `TypeDef` 、重複は現在のスコープにマージされません。 `TypeDef`オブジェクトは、完全修飾された*オブジェクト名*  +  *GUID*の  +  *バージョン番号*ごとに重複しているかどうかをチェックします。 名前または GUID に一致するものがあり、他の2つの要素のいずれかが異なる場合は、エラーが発生します。 それ以外の場合、3つのすべての項目が一致すると、は、 `MergeEnd` エントリが実際に重複していることを確認するための大まかなチェックを行います。そうでない場合は、エラーが発生します。 この大まかなチェックは次のようになります。

  - 同じ順序で発生する同じメンバー宣言。 としてフラグが設定されているメンバー `mdPrivateScope` ( [CorMethodAttr](cormethodattr-enumeration.md)列挙を参照) は、このチェックには含まれていません。これらは特別にマージされます。

  - 同じクラスレイアウト。

  これは、 `TypeDef` オブジェクトが宣言されているすべてのメタデータスコープで常に完全かつ一貫して定義されている必要があることを意味します。そのメンバー実装 (クラスの場合) が複数のコンパイル単位にわたって分散されている場合、完全定義はすべてのスコープに存在し、各スコープに増分されません。 たとえば、パラメーター名がコントラクトに関連する場合は、すべてのスコープに同じ方法で出力する必要があります。これらが関連性のない場合は、メタデータに出力されません。

  例外は、オブジェクトが `TypeDef` というフラグが付けられた増分メンバーを持つことができることです `mdPrivateScope` 。 これらが検出さ `MergeEnd` れると、重複を考慮せずに、それらを現在のスコープに増分的に追加します。 コンパイラはプライベートスコープを認識しているため、コンパイラは規則の適用を行う必要があります。

- 相対仮想アドレス (RVAs) はインポートまたはマージされません。コンパイラは、この情報を再生成する必要があります。

- カスタム属性は、関連付けられているアイテムがマージされた場合にのみマージされます。 たとえば、クラスに関連付けられているカスタム属性は、クラスが最初に検出されたときにマージされます。 カスタム属性がに関連付けられている場合、 `TypeDef` または `MemberDef` コンパイル単位 (メンバーコンパイルのタイムスタンプなど) に固有の場合は、マージされず、そのようなメタデータを削除または更新するためにコンパイラによって行われます。

## <a name="requirements"></a>必要条件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

**ヘッダー:** Cor

**ライブラリ:** Mscoree.dll のリソースとして使用されます。

**.NET Framework のバージョン:**[!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]

## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
