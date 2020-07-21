---
title: IMetaDataDispenserEx::GetCORSystemDirectory メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx.GetCORSystemDirectory
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx::GetCORSystemDirectory
helpviewer_keywords:
- IMetaDataDispenserEx::GetCORSystemDirectory method [.NET Framework metadata]
- GetCORSystemDirectory method [.NET Framework metadata]
ms.assetid: d9e0f3b6-e106-4820-bada-5bfba34ce360
topic_type:
- apiref
ms.openlocfilehash: a76c17e663fdf6555ed878cca1b86b6a9395730e
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008795"
---
# <a name="imetadatadispenserexgetcorsystemdirectory-method"></a>IMetaDataDispenserEx::GetCORSystemDirectory メソッド
現在の共通言語ランタイム (CLR) が格納されているディレクトリを取得します。 このメソッドは、アウトプロセスデバッガーでの使用に対してのみサポートされています。 別のコンポーネントから呼び出された場合は、E_NOTIMPL を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCORSystemDirectory (  
    [out] LPWSTR      szBuffer,
    [in]  DWORD       cchBuffer,
    [out] DWORD*      pchBuffer  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `szBuffer`  
 入出力ディレクトリ名を受け取るバッファー。  
  
 `cchBuffer`  
 からのサイズ (バイト単位) `szBuffer` 。  
  
 `pchBuffer`  
 入出力実際にで返されたバイト数 `szBuffer` 。  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataDispenserEx インターフェイス](imetadatadispenserex-interface.md)
- [IMetaDataDispenser インターフェイス](imetadatadispenser-interface.md)
