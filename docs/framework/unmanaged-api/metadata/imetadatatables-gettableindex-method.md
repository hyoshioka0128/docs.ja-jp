---
title: IMetaDataTables::GetTableIndex メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataTables.GetTableIndex
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataTables::GetTableIndex
helpviewer_keywords:
- GetTableIndex method [.NET Framework metadata]
- IMetaDataTables::GetTableIndex method [.NET Framework metadata]
ms.assetid: c6ec3800-e0d9-4387-afb8-ddc0b818114c
topic_type:
- apiref
ms.openlocfilehash: 3638ab12fc311ece9f24608cbb36219e10f01f2d
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501174"
---
# <a name="imetadatatablesgettableindex-method"></a>IMetaDataTables::GetTableIndex メソッド
指定したトークンによって参照されるテーブルのインデックスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetTableIndex (  
    [in]  ULONG   token,  
    [out] ULONG   *pixTbl  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `token`  
 からテーブルを参照するトークン。  
  
 `pixTbl`  
 入出力参照されるテーブルの、返されたインデックスへのポインター。  
  
## <a name="remarks"></a>解説  
 このメソッドは、一貫性のある結果を返さないため、使用しないことをお勧めします。 GUID テーブルの詳細については、共通言語基盤 (CLI) のドキュメント (特に「パーティション II: メタデータの定義とセマンティクス」) を参照してください。 ドキュメントはオンラインで入手できます。「 [Ecma C# および共通言語基盤の標準](../../../standard/components.md#applicable-standards)と[標準 ecma-335-共通言語基盤 (CLI)](http://www.ecma-international.org/publications/standards/Ecma-335.htm)」を参照してください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataTables インターフェイス](imetadatatables-interface.md)
- [IMetaDataTables2 インターフェイス](imetadatatables2-interface.md)
