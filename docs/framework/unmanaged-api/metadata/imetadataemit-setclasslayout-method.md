---
title: IMetaDataEmit::SetClassLayout メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetClassLayout
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetClassLayout
helpviewer_keywords:
- IMetaDataEmit::SetClassLayout method [.NET Framework metadata]
- SetClassLayout method [.NET Framework metadata]
ms.assetid: 2576c449-388d-4434-a0e1-9f53991e11b6
topic_type:
- apiref
ms.openlocfilehash: a18583ce807ffa672811f3a0cd1e744233f6eb30
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008834"
---
# <a name="imetadataemitsetclasslayout-method"></a>IMetaDataEmit::SetClassLayout メソッド
以前に呼び出した[Typedef メソッド](imetadataemit-definetypedef-method.md)の呼び出しで定義されたクラスのフィールドのレイアウトを完了します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetClassLayout (  
    [in]  mdTypeDef           td,
    [in]  DWORD               dwPackSize,
    [in]  COR_FIELD_OFFSET    rFieldOffsets[],
    [in]  ULONG               ulClassSize
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `td`  
 から`mdTypeDef`レイアウトするクラスを指定するトークン。  
  
 `dwPackSize`  
 からパッキングサイズは1、2、4、8、または16バイトです。 パッキングサイズは、隣接するフィールド間のバイト数です。  
  
 `rFieldOffsets`  
 から[COR_FIELD_OFFSET](cor-field-offset-structure.md)構造体の配列。各構造体は、クラスのフィールドと、クラス内のフィールドのオフセットを指定します。 で配列を終了 `mdTokenNil` します。  
  
 `ulClassSize`  
 からクラスのサイズ (バイト単位)。  
  
## <a name="remarks"></a>コメント  
 クラスを最初に定義するには、 [IMetaDataEmit::D efineTypeDef](imetadataemit-definetypedef-method.md)メソッドを呼び出し、クラスのフィールドに対して3つのレイアウト (automatic、シーケンシャル、explicit) のいずれかを指定します。 通常は、自動レイアウトを使用し、フィールドをレイアウトする最適な方法をランタイムが選択できるようにします。  
  
 ただし、アンマネージコードが使用する配置に従って、フィールドをレイアウトすることが必要になる場合があります。 この場合は、シーケンシャルまたは明示的なレイアウトを選択し、を呼び出して、 `SetClassLayout` フィールドのレイアウトを完成させます。  
  
- シーケンシャルレイアウト: パッキングサイズを指定します。 フィールドは、自然サイズまたはパッキングサイズのいずれかに従って整列されます。どちらの場合も、フィールドのオフセットは小さくなります。 `rFieldOffsets`を `ulClassSize` 0 に設定します。  
  
- 明示的なレイアウト: 各フィールドのオフセットを指定するか、クラスのサイズとパッキングサイズを指定します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
