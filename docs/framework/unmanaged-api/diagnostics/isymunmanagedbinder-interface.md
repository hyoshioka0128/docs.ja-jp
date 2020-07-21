---
title: ISymUnmanagedBinder インターフェイス
ms.date: 03/30/2017
api_name:
- ISymUnmanagedBinder
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedBinder
helpviewer_keywords:
- ISymUnmanagedBinder interface [.NET Framework debugging]
ms.assetid: b22fbe19-b30f-4696-8175-e6b91da9edab
topic_type:
- apiref
ms.openlocfilehash: f4f925282d65cd9cbc8eb1c8825f358602de68ed
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83441696"
---
# <a name="isymunmanagedbinder-interface"></a>ISymUnmanagedBinder インターフェイス
アンマネージコードのシンボルバインダーを表します。  
  
> [!IMPORTANT]
> 信頼されていないソースからプログラムデータベース (PDB) ファイルを開くと、セキュリティ上の危険があります。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetReaderForFile メソッド](isymunmanagedbinder-getreaderforfile-method.md)|メタデータインターフェイスとファイル名を指定すると、モジュールに関連付けられているデバッグシンボルを読み取る正しい[ISymUnmanagedReader](isymunmanagedreader-interface.md)構造体が返されます。|  
|[GetReaderFromStream メソッド](isymunmanagedbinder-getreaderfromstream-method.md)|メタデータインターフェイスと、シンボルストアを含むストリームが指定された場合、は、指定されたシンボルストアからデバッグシンボルを読み取る正しい[ISymUnmanagedReader](isymunmanagedreader-interface.md)構造体を返します。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断インターフェイス](diagnostics-symbol-store-interfaces.md)
- [ISymUnmanagedBinder2 インターフェイス](isymunmanagedbinder2-interface.md)
- [ISymUnmanagedBinder3 インターフェイス](isymunmanagedbinder3-interface.md)
