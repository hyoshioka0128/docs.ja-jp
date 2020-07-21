---
title: 多重化スタブ関数を取得する (アンマネージ API リファレンス)
description: GetDemultiplexedStub関数は、クライアントが Windows 管理から非同期呼び出しを受信するのを支援するオブジェクト フォワーダ シンクを作成します。
ms.date: 11/06/2017
api_name:
- GetDemultiplexedStub
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetDemultiplexedStub
helpviewer_keywords:
- GetDemultiplexedStub function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: d15fed261db2ca2cda6dbf824dc9cb0d5c56eed3
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174967"
---
# <a name="getdemultiplexedstub-function"></a>GetDemultiplexedStub 関数
Windows 管理から非同期呼び出しを受信する際にクライアントを支援するオブジェクト転送シンクが作成されます。
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetDemultiplexedStub (
   [in] IUnknown*    pObject,
   [in] boolean      isLocal,
   [out] IUnknown**  ppObject
);
```  

## <a name="parameters"></a>パラメーター

`pObject`  
[in]クライアントのインプロセス実装の[IWbemObjectSink](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemobjectsink)へのポインター。

`isLocal`  
[in]イベントがローカルかどうかを示すフラグ (`true`;それ以外`false`の場合は、 .

`ppObject`  
[アウト]クライアントが Windows 管理から非同期呼び出しを受信するのを支援するオブジェクト フォワーダ シンク。

## <a name="return-value"></a>戻り値

関数が成功した場合、戻り値は`S_OK`(0) になります。

関数が失敗した場合、戻り値は 0 以外のエラー コードです。 拡張エラー情報を取得するには[、GetErrorInfo](geterrorinfo.md)関数を呼び出します。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
