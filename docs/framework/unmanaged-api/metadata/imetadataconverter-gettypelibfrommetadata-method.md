---
title: IMetaDataConverter::GetTypeLibFromMetaData メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataConverter.GetTypeLibFromMetaData
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataConverter::GetTypeLibFromMetaData
helpviewer_keywords:
- GetTypeLibFromMetaData method [.NET Framework metadata]
- IMetaDataConverter::GetTypeLibFromMetaData method [.NET Framework metadata]
ms.assetid: 90eab7b3-1fae-4af4-8bce-f7bc0e188a99
topic_type:
- apiref
ms.openlocfilehash: 79bd8901641ee587e94861c0aec85b812591ea48
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008418"
---
# <a name="imetadataconvertergettypelibfrommetadata-method"></a>IMetaDataConverter::GetTypeLibFromMetaData メソッド
指定した `ITypeLib` ライブラリ名とモジュール名を持つタイプライブラリを表すインスタンスへのポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetTypeLibFromMetaData (  
    [in]  BSTR     strModule,
    [in]  BSTR     strTlbName,
    [out] ITypeLib **ppITL  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `strModule`  
 からタイプライブラリのモジュールの名前。  
  
 `strTlbName`  
 からタイプライブラリの名前。  
  
 `ppITL`  
 入出力タイプライブラリを表すインスタンスのアドレスを受け取る場所へのポインター `ITypeLib` 。  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataConverter インターフェイス](imetadataconverter-interface.md)
