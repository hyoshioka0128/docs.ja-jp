---
title: IMetaDataDispenser::OpenScopeOnMemory メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataDispenser.OpenScopeOnMemory
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenser::OpenScopeOnMemory
helpviewer_keywords:
- OpenScopeOnMemory method [.NET Framework metadata]
- IMetaDataDispenser::OpenScopeOnMemory method [.NET Framework metadata]
ms.assetid: 14218249-bdec-48ae-b5fc-9f57f7ca8501
topic_type:
- apiref
ms.openlocfilehash: 69e5e05012d2b44a76a986591ec990f66bf8ae20
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007326"
---
# <a name="imetadatadispenseropenscopeonmemory-method"></a>IMetaDataDispenser::OpenScopeOnMemory メソッド
既存のメタデータを含むメモリ領域を開きます。 つまり、このメソッドは、既存のデータがメタデータとして扱われる、指定されたメモリ領域を開きます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT OpenScopeOnMemory (  
    [in]  LPCVOID     pData,
    [in]  ULONG       cbData,
    [in]  DWORD       dwOpenFlags,
    [in]  REFIID      riid,
    [out] IUnknown    **ppIUnk  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pData`  
 からメモリ領域の開始アドレスを指定するポインター。  
  
 `cbData`  
 からメモリ領域のサイズ (バイト単位)。  
  
 `dwOpenFlags`  
 から開くためのモード (読み取り、書き込みなど) を指定する[Coropenflags](coropenflags-enumeration.md)列挙体の値。  
  
 `riid`  
 から返される、必要なメタデータインターフェイスの IID。呼び出し元は、インターフェイスを使用して、メタデータのインポート (読み取り) または出力 (書き込み) を行います。  
  
 の値には `riid` 、"import" インターフェイスまたは "emit" インターフェイスのいずれかを指定する必要があります。 有効な値は、IID_IMetaDataEmit、IID_IMetaDataImport、IID_IMetaDataAssemblyEmit、IID_IMetaDataAssemblyImport、IID_IMetaDataEmit2、または IID_IMetaDataImport2 です。  
  
 `ppIUnk`  
 入出力返されたインターフェイスへのポインター。  
  
## <a name="remarks"></a>コメント  
 メタデータのメモリ内コピーは、"import" インターフェイスのいずれかのメソッドを使用してクエリを実行するか、"emit" インターフェイスのいずれかのメソッドを使用してに追加できます。  
  
 `OpenScopeOnMemory`メソッドは[IMetaDataDispenser:: openscope](imetadatadispenser-openscope-method.md)メソッドに似ていますが、対象のメタデータがディスク上のファイルではなくメモリに既に存在している点が異なります。  
  
 メモリのターゲット領域に共通言語ランタイム (CLR) メタデータが含まれていない場合、 `OpenScopeOnMemory` メソッドは失敗します。  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataDispenser インターフェイス](imetadatadispenser-interface.md)
- [IMetaDataDispenserEx インターフェイス](imetadatadispenserex-interface.md)
- [IMetaDataAssemblyEmit インターフェイス](imetadataassemblyemit-interface.md)
- [IMetaDataAssemblyImport インターフェイス](imetadataassemblyimport-interface.md)
- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
