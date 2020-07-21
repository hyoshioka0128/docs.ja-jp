---
title: ICLRDataTarget::Request メソッド
ms.date: 03/30/2017
api_name:
- ICLRDataTarget.Request
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget::Request
helpviewer_keywords:
- ICLRDataTarget::Request method [.NET Framework debugging]
- Request method [.NET Framework debugging]
ms.assetid: 4723bd1c-eddb-4ed2-897a-010024a47e01
topic_type:
- apiref
ms.openlocfilehash: b913affb4728dc80ba67438384cbeac87265f76d
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860538"
---
# <a name="iclrdatatargetrequest-method"></a>ICLRDataTarget::Request メソッド
実装で定義されているように、操作を要求するために、共通言語ランタイム (CLR) データアクセスサービスによって呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Request (  
    [in] ULONG32            reqCode,  
    [in] ULONG32            inBufferSize,  
    [in, size_is(inBufferSize)]
        BYTE                *inBuffer,  
    [in] ULONG32            outBufferSize,  
    [out, size_is(outBufferSize)]
        BYTE                *outBuffer  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `reqCode`  
 からユーザー定義。  
  
 `inBufferSize`  
 から受信要求に使用される入力バッファーのサイズ。  
  
 `inBuffer`  
 から要求を格納しているバッファー。  
  
 `outBufferSize`  
 から応答に使用される出力バッファーのサイズ。  
  
 `outBuffer`  
 入出力応答を格納しているバッファー。  
  
## <a name="remarks"></a>解説  
 メソッド`Request`は、指定されていないカスタム操作の追加を容易にします。 つまり、このメソッドは、インターフェイス定義のリビジョンを必要とせずに、拡張機能を提供します。  
  
 このメソッドは、デバッグ アプリケーションの作成者によって実装されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ClrData .idl, ClrData .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRDataTarget インターフェイス](iclrdatatarget-interface.md)
