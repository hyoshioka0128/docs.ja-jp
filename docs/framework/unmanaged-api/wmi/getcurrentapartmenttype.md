---
title: 関数 (アンマネージ API リファレンス)
description: 関数は、呼び出し元が実行されているアパートメントの型を取得します。
ms.date: 11/06/2017
api_name:
- GetCurrentApartmentType
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetCurrentApartmentType
helpviewer_keywords:
- GetCurrentApartmentType function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 3fc88f7997ee5a6c25359243e1ee97a041050eb7
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176826"
---
# <a name="getcurrentapartmenttype-function"></a>GetCurrentApartmentType 関数
呼び出し元が実行されているアパートメントの種類が取得されます。
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCurrentApartmentType (
   [in] int                   vFunc,
   [in] IComThreadingInfo*    ptr,
   [out] APTTYPE*             aptType
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`  
[in][インスタンスへの](/windows/desktop/api/objidlbase/nn-objidlbase-icomthreadinginfo)ポインター。

`aptType`  
[アウト]呼び出し元のアパートメントを示す[APTTYPE](/windows/win32/api/objidlbase/ne-objidlbase-apttype)列挙値へのポインター。

## <a name="return-value"></a>戻り値

|常時  |Value  |説明  |
|---------|---------|---------|
| `S_OK` | 0 | 関数は正常に完了しました。 |
| `E_FAIL` | 0x80000008 | 呼び出し元がアパートメントで実行されていません。 |
  
## <a name="remarks"></a>解説

この関数は、メソッドの呼び出し[をラップします](/windows/desktop/api/objidlbase/nf-objidlbase-icomthreadinginfo-getcurrentapartmenttype)。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
