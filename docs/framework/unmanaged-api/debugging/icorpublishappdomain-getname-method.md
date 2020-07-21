---
title: ICorPublishAppDomain::GetName メソッド
ms.date: 03/30/2017
api_name:
- ICorPublishAppDomain.GetName
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishAppDomain::GetName
helpviewer_keywords:
- GetName method, ICorPublishAppDomain interface [.NET Framework debugging]
- ICorPublishAppDomain::GetName method [.NET Framework debugging]
ms.assetid: 6ef8ac9b-9803-4b65-8b13-25f3e0b1bc6b
topic_type:
- apiref
ms.openlocfilehash: e95f96847c6e069758362fb6febc28dc31911bc9
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396297"
---
# <a name="icorpublishappdomaingetname-method"></a>ICorPublishAppDomain::GetName メソッド
この[ICorPublishAppDomain](icorpublishappdomain-interface.md)によって表されるアプリケーションドメインの名前を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetName (  
    [in]  ULONG32   cchName,
    [out] ULONG32   *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]
        WCHAR       *szName  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cchName`  
 [in] `szName` 配列のサイズ。  
  
 `pcchName`  
 入出力配列に返された、null 文字を含むワイド文字の数へのポインター `szName` 。  
  
 `szName`  
 入出力名前を格納する配列。  
  
## <a name="remarks"></a>解説  
 `szName`が null 以外の場合、 `GetName` メソッドは最大 `cchName` 文字 (null ターミネータを含む) をにコピー `szName` します。 で null 以外の値が返された場合 `pcchName` 、名前の実際の文字数 (null ターミネータを含む) が配列に格納され `szName` ます。  
  
 メソッドは、 `GetName` コピーされた文字数に関係なく、S_OK HRESULT を返します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorPub .idl、CorPub .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorPublishAppDomain インターフェイス](icorpublishappdomain-interface.md)
