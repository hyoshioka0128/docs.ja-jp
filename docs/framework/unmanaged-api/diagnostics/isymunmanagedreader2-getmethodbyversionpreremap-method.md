---
title: ISymUnmanagedReader2::GetMethodByVersionPreRemap メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader2.GetMethodByVersionPreRemap
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader2::GetMethodByVersionPreRemap
helpviewer_keywords:
- GetMethodByVersionPreRemap method [.NET Framework debugging]
- ISymUnmanagedReader2::GetMethodByVersionPreRemap method [.NET Framework debugging]
ms.assetid: 0d144ed4-bdb0-4cac-960c-cb90f4dca173
topic_type:
- apiref
ms.openlocfilehash: b12ecfdaf7c90589ce2e96b39f7437444cb91b09
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615424"
---
# <a name="isymunmanagedreader2getmethodbyversionpreremap-method"></a>ISymUnmanagedReader2::GetMethodByVersionPreRemap メソッド
メソッドトークンとエディットコンティニュバージョン番号を指定して、シンボルリーダーメソッドを取得します。 バージョン番号は1から始まり、エディットコンティニュ操作の結果としてメソッドが変更されるたびに増分されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetMethodByVersionPreRemap(  
    [in]  mdMethodDef token,  
    [in]  int version,  
    [out, retval] ISymUnmanagedMethod** pRetVal);  
```  
  
## <a name="parameters"></a>パラメーター  
 `token`  
 からメソッドメタデータトークン。  
  
 `version`  
 からメソッドのバージョン。  
  
 `pRetVal`  
 入出力返された[ISymUnmanagedMethod](isymunmanagedmethod-interface.md)インターフェイスへのポインター。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl。 CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedReader2 インターフェイス](isymunmanagedreader2-interface.md)
