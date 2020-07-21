---
title: ValidatorFlags 列挙型
ms.date: 03/30/2017
api_name:
- ValidatorFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ValidatorFlags
helpviewer_keywords:
- ValidatorFlags enumeration [.NET Framework hosting]
ms.assetid: a3f5c266-3fcc-4ad1-aaf5-4cdbe26304ad
topic_type:
- apiref
ms.openlocfilehash: d5eb225241f597baf7a0a5584f4aaf8bf8411ea2
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84009471"
---
# <a name="validatorflags-enumeration"></a>ValidatorFlags 列挙型
[ICLRValidator:: Validate](iclrvalidator-validate-method.md)メソッドの呼び出しで実行する必要がある検証の種類を示す値を格納します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
enum ValidatorFlags {  
    VALIDATOR_EXTRA_VERBOSE =       0x00000001,  
    VALIDATOR_SHOW_SOURCE_LINES =   0x00000002,  
    VALIDATOR_CHECK_ILONLY =        0x00000004,  
    VALIDATOR_CHECK_PEFORMAT_ONLY = 0x00000008,  
    VALIDATOR_NOCHECK_PEFORMAT =    0x00000010,  
};  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`VALIDATOR_CHECK_ILONLY`|実行可能ファイル内の Microsoft 中間言語 (MSIL) のみを検証するように指定します。|  
|`VALIDATOR_CHECK_PEFORMAT_ONLY`|実行可能ファイルの形式だけを検証することを指定します。|  
|`VALIDATOR_EXTRA_VERBOSE`|すべての種類の検証を実行してレポートすることを指定します。|  
|`VALIDATOR_NOCHECK_PEFORMAT`|実行可能ファイルの形式を検証しないことを指定します。|  
|`VALIDATOR_SHOW_SOURCE_LINES`|検証エラーメッセージに検証エラーを発生させるソースコード行を含めるように指定します。 このフィールド値は .NET Framework バージョン2.0 では無効です。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** IValidator、IValidator  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRErrorReportingManager インターフェイス](iclrerrorreportingmanager-interface.md)
- [ホスティングの列挙型](hosting-enumerations.md)
