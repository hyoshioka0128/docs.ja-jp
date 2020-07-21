---
title: 関数 (アンマネージ API リファレンス)
description: 関数は列挙子の論理コピーを作成します。
ms.date: 11/06/2017
api_name:
- CloneEnumWbemClassObject
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- CloneEnumWbemClassObject
helpviewer_keywords:
- CloneEnumWbemClassObject function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: f2a3a7e848108e50c04f0ec70cf42586755a0a88
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79175019"
---
# <a name="cloneenumwbemclassobject-function"></a>CloneEnumWbemClassObject 関数
列挙型内での位置を維持して、列挙子の論理コピーが作成されます。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>構文

```cpp
HRESULT CloneEnumWbemClassObject (
   [out] IEnumWbemClassObject**  ppEnum,
   [in] DWORD                    authLevel,
   [in] DWORD                    impLevel,
   [in] IEnumWbemClassObject*    pCurrentEnumWbemClassObject,
   [in] BSTR                     strUser,
   [in] BSTR                     strPassword,
   [in BSTR]                     strAuthority
);
```

## <a name="parameters"></a>パラメーター

`ppEnum`\
[アウト]新しい[IEnumWbemClass オブジェクト](/windows/desktop/api/wbemcli/nn-wbemcli-ienumwbemclassobject)へのポインターを受け取ります。

`authLevel`\
[in]権限レベル。

`impLevel`\
[in]偽装レベル。

`pCurrentEnumWbemClassObject`\
[アウト]複製される[インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-ienumwbemclassobject)へのポインター。

`strUser`\
[in]ユーザー名。 詳細については、[関数](connectserverwmi.md)を参照してください。

`strPassword`\
[in]パスワード。 詳細については、[関数](connectserverwmi.md)を参照してください。

`strAuthority`\
[in]ユーザーのドメイン名。 詳細については、[関数](connectserverwmi.md)を参照してください。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 一般的なエラーが発生しました。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | パラメータが無効です。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | メモリ不足が発生し、操作を完了します。 |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | 現在のプロセスと WMI 間のリモート プロシージャ コール (RPC) リンクに失敗しました。 |
| `WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |

## <a name="remarks"></a>解説

この関数は、メソッドの呼び出しをラップ[します](/windows/desktop/api/wbemcli/nf-wbemcli-ienumwbemclassobject-clone)。

この方法では、"ベスト エフォート" コピーのみが作成されます。 多くの CIM オブジェクトの動的な性質により、新しい列挙子がソース列挙子と同じオブジェクトのセットを列挙しない可能性があります。

関数呼び出しが失敗した場合は[、GetErrorInfo](geterrorinfo.md)関数を呼び出すことによって、追加のエラー情報を取得できます。

## <a name="example"></a>例

例については、[メソッド](/windows/desktop/api/wbemcli/nf-wbemcli-ienumwbemclassobject-clone)を参照してください。

## <a name="requirements"></a>必要条件
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

 **ヘッダー:** WMINet_Utils.idl

 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
