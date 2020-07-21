---
title: COR_GC_REFERENCE 構造体
ms.date: 03/30/2017
api_name:
- COR_GC_REFERENCE
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_GC_REFERENCE
helpviewer_keywords:
- COR_GC_REFERENCE structure [.NET Framework debugging]
ms.assetid: 162e8179-0cd4-4110-8f06-5f387698bd62
topic_type:
- apiref
ms.openlocfilehash: e22269b76c230f702f4712298fddcd0df1fde50d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179327"
---
# <a name="cor_gc_reference-structure"></a>COR_GC_REFERENCE 構造体
ガベージ コレクトされるオブジェクトに関する情報が含まれます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct _COR_GC_REFERENCE {  
    ICorDebugAppDomain *domain;
    ICorDebugValue *location;  
    CorGCReferenceType type;  
    UINT64 extraData;  
} COR_GC_REFERENCE;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`domain`|ハンドルまたはオブジェクトが属するアプリケーション ドメインへのポインター。 その値は. `null`|  
|`location`|ガベージ コレクションされるオブジェクトに対応するインターフェイスまたは ICorDebugReferenceValue インターフェイス。|  
|`type`|ルートの取得元を示す[CorGCReferenceType](corgcreferencetype-enumeration.md)列挙値。 詳細については、「解説」を参照してください。|  
|`extraData`|ガベージ コレクションされるオブジェクトに関する追加データ。 この情報は、`type`フィールドで示されるオブジェクトのソースによって異なります。 詳細については、「解説」を参照してください。|  
  
## <a name="remarks"></a>解説  
 フィールド`type`は、参照の取得元を示す[CorGCReferenceType](corgcreferencetype-enumeration.md)列挙値です。 特定`COR_GC_REFERENCE`の値は、次の種類の管理オブジェクトを反映できます。  
  
- すべてのマネージ スタック (`CorGCReferenceType.CorReferenceStack`) からのオブジェクト これには、マネージ コード内のライブ参照と、共通言語ランタイムによって作成されたオブジェクトが含まれます。  
  
- ハンドル テーブル (`CorGCReferenceType.CorHandle*`) のオブジェクト これには、モジュール内の`HNDTYPE_STRONG`厳密`HNDTYPE_REFCOUNT`な参照 ( および ) と静的変数が含まれます。  
  
- ファイナライザー キュー (`CorGCReferenceType.CorReferenceFinalizer`) からのオブジェクト ファイナライザーが実行されるまで、ファイナライザー キューのルート オブジェクト。  
  
 フィールド`extraData`には、参照のソース (またはタイプ) に応じて、追加のデータが含まれます。 次のいずれかの値になります。  
  
- `DependentSource`. の`type`場合、`CorGCREferenceType.CorHandleStrongDependent`このフィールドは、生きている場合は、ガベージ コレクションされるオブジェクトをルートとするオブジェクト`COR_GC_REFERENCE.Location`です。  
  
- `RefCount`. の`type`場合、`CorGCREferenceType.CorHandleStrongRefCount`このフィールドはハンドルの参照カウントです。  
  
- `Size`. の`type`場合、`CorGCREferenceType.CorHandleStrongSizedByref`このフィールドは、ガベージ コレクターがオブジェクト ルートを計算したオブジェクト ツリーの最後のサイズです。 この計算は必ずしも最新の計算ではありません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグ構造体](debugging-structures.md)
- [デバッグ](index.md)
