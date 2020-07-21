---
title: ISymUnmanagedReader::GetMethodVersion メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader.GetMethodVersion
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::GetMethodVersion
helpviewer_keywords:
- GetMethodVersion method [.NET Framework debugging]
- ISymUnmanagedReader::GetMethodVersion method [.NET Framework debugging]
ms.assetid: d6f9ac84-302a-4f5e-b990-e76f4269fceb
topic_type:
- apiref
ms.openlocfilehash: 8ee4c1bffccb44d15fa53eb3d4d6c0fcdc3e7697
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614969"
---
# <a name="isymunmanagedreadergetmethodversion-method"></a>ISymUnmanagedReader::GetMethodVersion メソッド
メソッドのバージョンを取得します。 メソッドのバージョンは1から始まり、メソッドが再コンパイルされるたびにインクリメントされます。 再コンパイルは、メソッドを変更せずに発生する可能性があります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetMethodVersion (  
    [in]  ISymUnmanagedMethod* pMethod,  
    [out] int* version);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pMethod`  
 からバージョンを取得するメソッド。  
  
 `version`  
 入出力メソッドのバージョンを受け取る変数へのポインター。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedReader インターフェイス](isymunmanagedreader-interface.md)
