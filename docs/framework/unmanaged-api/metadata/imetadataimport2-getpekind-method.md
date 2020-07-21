---
title: IMetaDataImport2::GetPEKind メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport2.GetPEKind
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport2::GetPEKind
helpviewer_keywords:
- GetPEKind method [.NET Framework metadata]
- IMetaDataImport2::GetPEKind method [.NET Framework metadata]
ms.assetid: d91c3d89-8022-4a4c-a2a2-a8af2c387507
topic_type:
- apiref
ms.openlocfilehash: 3626998c456e23fb922ae45a68bedb0e45a7ccba
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84490433"
---
# <a name="imetadataimport2getpekind-method"></a>IMetaDataImport2::GetPEKind メソッド
現在のメタデータスコープで定義されている、ポータブル実行可能 (PE) ファイル (通常は DLL または EXE ファイル) 内のコードの性質を示す値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetPEKind (  
   [out] DWORD *pdwPEKind,  
   [out] DWORD *pdwMachine  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pdwPEKind`  
 入出力PE ファイルを記述する[Corpekind](corpekind-enumeration.md)列挙型の値へのポインター。  
  
 `pdwMachine`  
 入出力コンピューターのアーキテクチャを識別する値へのポインター。 使用可能な値については、次のセクションを参照してください。  
  
## <a name="remarks"></a>解説  
 パラメーターによって参照される値には、 `pdwMachine` 次のいずれかを指定できます。  
  
|値|コンピューターのアーキテクチャ|  
|-----------|--------------------------|  
|IMAGE_FILE_MACHINE_I386<br /><br /> 0x014C|x86|  
|IMAGE_FILE_MACHINE_IA64<br /><br /> 0x0200|Intel IPF|  
|IMAGE_FILE_MACHINE_AMD64<br /><br /> 0x8664|X64|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [CorPEKind 列挙型](corpekind-enumeration.md)
