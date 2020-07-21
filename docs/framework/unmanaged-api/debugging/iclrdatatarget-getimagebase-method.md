---
title: ICLRDataTarget::GetImageBase メソッド
ms.date: 03/30/2017
api_name:
- ICLRDataTarget.GetImageBase
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget::GetImageBase
helpviewer_keywords:
- ICLRDataTarget::GetImageBase method [.NET Framework debugging]
- GetImageBase method [.NET Framework debugging]
ms.assetid: 091c5f32-c160-49e3-a75f-4692e084c8e4
topic_type:
- apiref
ms.openlocfilehash: 71b07e11cd3fec1a0dbebe986d98067c2e6f18e1
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860631"
---
# <a name="iclrdatatargetgetimagebase-method"></a>ICLRDataTarget::GetImageBase メソッド
指定したイメージのベースメモリアドレスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetImageBase (  
    [in, string] LPCWSTR    imagePath,  
    [out] CLRDATA_ADDRESS   *baseAddress  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `imagePath`  
 からパスを含む、イメージのファイル名。  
  
 `baseAddress`  
 入出力イメージのベースアドレスを格納する CLRDATA_ADDRESS へのポインター。  
  
## <a name="remarks"></a>解説  
 イメージファイル名には、パスを指定することも、パスを指定することもできません。 パスが指定されている場合、パス全体で一致が行われます。それ以外の場合、一致はファイル名でのみ実行されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ClrData .idl, ClrData .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRDataTarget インターフェイス](iclrdatatarget-interface.md)
