---
title: IMetaDataTables インターフェイス
ms.date: 03/30/2017
api_name:
- IMetaDataTables
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataTables
helpviewer_keywords:
- IMetaDataTables interface [.NET Framework metadata]
ms.assetid: 31272cce-506a-4f18-bcbf-01ee45e36356
topic_type:
- apiref
ms.openlocfilehash: 2105033e684ec172e24adfb14bcab7668b388af3
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501122"
---
# <a name="imetadatatables-interface"></a>IMetaDataTables インターフェイス
テーブル内のメタデータ情報の格納と取得のためのメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetBlob メソッド](imetadatatables-getblob-method.md)|指定した列インデックスにあるバイナリラージオブジェクト (BLOB) へのポインターを取得します。|  
|[GetBlobHeapSize メソッド](imetadatatables-getblobheapsize-method.md)|BLOB ヒープのサイズ (バイト単位) を取得します。|  
|[GetCodedTokenInfo メソッド](imetadatatables-getcodedtokeninfo-method.md)|指定した行インデックスに関連付けられているトークンの配列へのポインターを取得します。|  
|[GetColumn メソッド](imetadatatables-getcolumn-method.md)|指定したテーブルインデックスにあるテーブル内の、指定した列インデックスにある列に格納されている値へのポインターを取得します。|  
|[GetColumnInfo メソッド](imetadatatables-getcolumninfo-method.md)|指定されたテーブル内の指定された列に関するデータを取得します。|  
|[GetGuid メソッド](imetadatatables-getguid-method.md)|指定したインデックス位置にある行から GUID を取得します。|  
|[GetGuidHeapSize メソッド](imetadatatables-getguidheapsize-method.md)|GUID ヒープのサイズ (バイト単位) を取得します。|  
|[GetNextBlob メソッド](imetadatatables-getnextblob-method.md)|テーブル内の次の BLOB のインデックスを取得します。|  
|[GetNextGuid メソッド](imetadatatables-getnextguid-method.md)|現在のテーブル列の次の GUID 値のインデックスを取得します。|  
|[GetNextString メソッド](imetadatatables-getnextstring-method.md)|現在のテーブル列の次の文字列のインデックスを取得します。|  
|[GetNextUserString メソッド](imetadatatables-getnextuserstring-method.md)|現在のテーブル列の次のハードコーディングされた文字列を含む行のインデックスを取得します。|  
|[GetNumTables メソッド](imetadatatables-getnumtables-method.md)|現在のインスタンスのスコープ内にあるテーブルの数を取得し `IMetaDataTables` ます。|  
|[GetRow メソッド](imetadatatables-getrow-method.md)|指定したテーブルインデックスにあるテーブル内の指定した行インデックスにある行を取得します。|  
|[GetString メソッド](imetadatatables-getstring-method.md)|現在の参照スコープのテーブル列から、指定したインデックス位置にある文字列を取得します。|  
|[GetStringHeapSize メソッド](imetadatatables-getstringheapsize-method.md)|文字列ヒープのサイズ (バイト単位) を取得します。|  
|[GetTableIndex メソッド](imetadatatables-gettableindex-method.md)|指定したトークンによって参照されるテーブルのインデックスを取得します。|  
|[GetTableInfo メソッド](imetadatatables-gettableinfo-method.md)|指定されたテーブルインデックスにあるテーブルの名前、行のサイズ、行数、列の数、およびキー列のインデックスを取得します。|  
|[GetUserString メソッド](imetadatatables-getuserstring-method.md)|現在のスコープ内の文字列列にある、指定したインデックス位置にあるハードコーディングされた文字列を取得します。|  
|[GetUserStringHeapSize メソッド](imetadatatables-getuserstringheapsize-method.md)|ユーザー文字列ヒープのサイズ (バイト単位) を取得します。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ インターフェイス](metadata-interfaces.md)
- [IMetaDataTables2 インターフェイス](imetadatatables2-interface.md)
