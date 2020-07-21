---
title: LPOVERLAPPED_COMPLETION_ROUTINE 関数ポインター
ms.date: 03/30/2017
api_name:
- LPOVERLAPPED_COMPLETION_ROUTINE
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- LPOVERLAPPED_COMPLETION_ROUTINE
helpviewer_keywords:
- LPOVERLAPPED_COMPLETION_ROUTINE function pointer [.NET Framework hosting]
ms.assetid: 5fb645d9-b818-401c-8c2c-c30d86de58ba
topic_type:
- apiref
ms.openlocfilehash: c0bdd9e59f5794dbb0d447dc2cc6cb682bfdf09f
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008483"
---
# <a name="lpoverlapped_completion_routine-function-pointer"></a>LPOVERLAPPED_COMPLETION_ROUTINE 関数ポインター
デバイスに対する重複 I/O (非同期 I/O) が完了したときに、ホストに通知する関数を指します。  
  
 この関数ポインターは .NET Framework 4 で非推奨とされました。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef VOID (*LPOVERLAPPED_COMPLETION_ROUTINE) (  
    [in] DWORD  dwErrorCode,  
    [in] DWORD  dwNumberOfBytesTransfered,  
    [in] LPVOID lpOverlapped  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwErrorCode`  
 からデバイスが閉じられている場合は、エラーコードである値。それ以外の場合、この値は0です。  
  
 デバイスを閉じると、デバイスに対するすべての保留中の i/o が直ちに完了します。  
  
 `dwNumberOfBytesTransfered`  
 からI/o 操作によって転送されたバイト数。  
  
 `lpOverlapped`  
 からI/o 要求を完了するために使用される情報を格納する構造体へのポインター。  
  
## <a name="remarks"></a>コメント  
 `LPOVERLAPPED_COMPLETION_ROUTINE`ポイントがコールバック関数であり、ホストアプリケーションのライターによって実装されている必要がある関数。 コールバック関数を使用すると、ホストは、完了した i/o 要求を処理できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscorwks.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)
