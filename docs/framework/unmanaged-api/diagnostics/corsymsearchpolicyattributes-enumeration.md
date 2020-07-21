---
title: CorSymSearchPolicyAttributes 列挙体
ms.date: 03/30/2017
api_name:
- CorSymSearchPolicyAttributes
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorSymSearchPolicyAttributes
helpviewer_keywords:
- CorSymSearchPolicyAttributes enumeration [.NET Framework debugging]
ms.assetid: 03abde84-930a-49d3-bac3-23abb34a0184
topic_type:
- apiref
ms.openlocfilehash: 8af71314cf8a24c710d3b8980c082daaf9186715
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501873"
---
# <a name="corsymsearchpolicyattributes-enumeration"></a>CorSymSearchPolicyAttributes 列挙体
シンボルリーダーの検索を実行するときに使用するポリシーを指定します。 これらの定数は、 [ISymUnmanagedBinder2:: GetReaderForFile2](isymunmanagedbinder2-getreaderforfile2-method.md)メソッドと[ISymUnmanagedBinder3:: GetReaderFromCallback](isymunmanagedbinder3-getreaderfromcallback-method.md)メソッドによって使用されます。  
  
> [!IMPORTANT]
> 信頼されていないソースからプログラムデータベース (PDB) ファイルを開くと、セキュリティ上の危険があります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum CorSymSearchPolicyAttributes  
{  
    AllowRegistryAccess      = 0x1,
    AllowSymbolServerAccess  = 0x2,  
    AllowOriginalPathAccess  = 0x4,     //
    AllowReferencePathAccess = 0x8  
} CorSymSearchPolicyAttributes;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`AllowRegistryAccess`|シンボル検索パスのレジストリを照会します。|  
|`AllowSymbolServerAccess`|シンボルサーバーにアクセスします。|  
|`AllowOriginalPathAccess`|デバッグディレクトリに指定されているパスを検索します。|  
|`AllowReferencePathAccess`|.Exe ファイルがある場所で PDB を検索します。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断列挙型](diagnostics-symbol-store-enumerations.md)
