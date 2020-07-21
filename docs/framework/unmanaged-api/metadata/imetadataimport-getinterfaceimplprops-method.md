---
title: IMetaDataImport::GetInterfaceImplProps メソッド
ms.date: 02/25/2019
api_name:
- IMetaDataImport.GetInterfaceImplProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetInterfaceImplProps
helpviewer_keywords:
- IMetaDataImport::GetInterfaceImplProps method [.NET Framework metadata]
- GetInterfaceImpProps method [.NET Framework metadata]
ms.assetid: be3f5985-b1e4-4036-8602-c16e8508d4af
topic_type:
- apiref
ms.openlocfilehash: 1c9d9647084aa729817eeeb17ee3f5cd320c0d29
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84491245"
---
# <a name="imetadataimportgetinterfaceimplprops-method"></a>IMetaDataImport::GetInterfaceImplProps メソッド
指定したメソッドを実装するのメタデータトークンへのポインター <xref:System.Type> と、そのメソッドを宣言するインターフェイスを取得します。
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetInterfaceImplProps (  
   [in]  mdInterfaceImpl        iiImpl,  
   [out] mdTypeDef              *pClass,  
   [out] mdToken                *ptkIface  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `iiImpl`  
 からクラスとインターフェイストークンを返すメソッドを表すメタデータトークン。  
  
 `pClass`  
 入出力メソッドを実装するクラスを表すメタデータトークン。  
  
 `ptkIface`  
 入出力実装されたメソッドを定義するインターフェイスを表すメタデータトークン。  

## <a name="remarks"></a>解説

 の値を取得する `iImpl` には、 [EnumInterfaceImpls](imetadataimport-enuminterfaceimpls-method.md)メソッドを呼び出します。

 たとえば、クラスの `mdTypeDef` トークン値が0x02000007 で、型がトークンを持つ3つのインターフェイスを実装しているとします。

- 0x02000003 (TypeDef)
- 0x0100000A (TypeRef)
- 0x0200001C (TypeDef)

概念的には、この情報は次のようにインターフェイス実装テーブルに格納されます。

| 行番号 | クラストークン | インターフェイストークン |
|------------|-------------|-----------------|
| 4          |             |                 |
| 5          | 02000007    | 02000003        |
| 6          | 02000007    | 0100000A        |
| 7          |             |                 |
| 8          | 02000007    | 0200001C        |

これは、トークンが4バイトの値であることを思い出してください。

- 下位3バイトは、行番号 (RID) を保持します。
- 上位バイトは、のトークンの種類 (0x09) を保持し `mdtInterfaceImpl` ます。

`GetInterfaceImplProps`引数で指定したトークンを持つ行に保持されている情報を返し `iImpl` ます。
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
