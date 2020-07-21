---
title: ICorDebugNativeFrame::GetIP メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetIP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetIP
helpviewer_keywords:
- GetIP method, ICorDebugNativeFrame interface [.NET Framework debugging]
- ICorDebugNativeFrame::GetIP method [.NET Framework debugging]
ms.assetid: 99f693f3-d3b9-4fd8-9d09-b8efd03f7b67
topic_type:
- apiref
ms.openlocfilehash: 53576ca938074fb7e5974a96bb53a84cb6ed67ab
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213596"
---
# <a name="icordebugnativeframegetip-method"></a>ICorDebugNativeFrame::GetIP メソッド
命令ポインターが現在設定されているネイティブコードのオフセット位置を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetIP (  
    [out] ULONG32           *pnOffset  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pnOffset`  
 入出力ネイティブコード内のオフセット位置を指すポインター。  
  
## <a name="remarks"></a>Remarks  
 この "テキストフレーム" によって表されるスタックフレームがアクティブな場合、オフセットは次に実行される命令のアドレスになります。 このスタックフレームがアクティブでない場合、オフセットは、スタックフレームが再アクティブ化されたときに実行される次の命令のアドレスになります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目
