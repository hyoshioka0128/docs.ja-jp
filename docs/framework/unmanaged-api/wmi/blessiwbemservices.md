---
title: 関数 (アンマネージ API リファレンス)
description: 関数は、ユーザー資格情報が IWbemServices クラスへのアクセスを許可するかどうかを示します。
ms.date: 11/06/2017
api_name:
- BlessIWbemServices
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BlessIWbemServices
helpviewer_keywords:
- BlessIWbemServices function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 4b15af840cc00b3ec261604db4f3625c6b975d3e
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176865"
---
# <a name="blessiwbemservices-function"></a>BlessIWbemServices 関数
ユーザー資格情報で指定された[IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices)クラスへのアクセスを許可するかどうかを示します。
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT BlessIWbemServices (
   [in] IWbemServices* pIWbemServices,
   [in] BSTR strUser,
   [in] BSTR strPassword,
   [in] BSTR strAuthority,
   [in] DWORD impLevel,
   [in] DWORD authnLevel
);
```  

## <a name="parameters"></a>パラメーター

`pIWbemServices`\
[in]アクセス許可が必要な[IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices)オブジェクトへのポインター。

`strUser`\
[in]ユーザー名。

`strPassword`\
[in]に関連付けられている`strUser`パスワード。

`strAuthority`\
[in]ユーザーのドメイン名。 詳細については、[関数](connectserverwmi.md)を参照してください。

`impLevel`\
[in]偽装レベル。

`authnLevel`\
[in]権限レベル。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WinError.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
| `E_INVALIDARG` | 0x80070057 | 1 つ以上の引数が無効です。 |
| `E_POINTER` | 0x80004003 | `pIWbemServices` は `null` です。 |
| `E_FAIL` | 0x80000008 | 特定できないエラーが発生しました。 |
| `E_OUTOFMEMORY` | 0x80000002 | メモリ不足のため、操作を実行できません。 |
| `S_OK` | 0 | 関数呼び出しが正常に行われました。 |

## <a name="requirements"></a>必要条件  

 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
