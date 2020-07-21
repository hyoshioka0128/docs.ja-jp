---
title: SetPEKind メソッド
ms.date: 03/30/2017
api_name:
- IALink2.SetPEKind
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- SetPEKind
helpviewer_keywords:
- SetPEKind method
ms.assetid: 050e77ee-3014-45c0-9e29-2ebe29347b0d
topic_type:
- apiref
ms.openlocfilehash: 5a8442b1f0869e1592a05dfeeb0f5e6d583f3ea8
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179382"
---
# <a name="setpekind-method"></a>SetPEKind メソッド
ポータブル実行可能ファイルの種類を、コンピューター固有またはマシンに依存しない型を決定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetPEKind(  
    mdAssembly AssemblyID,  
    mdToken FileToken,  
    DWORD dwPEKind,  
    DWORD dwMachine  
) PURE;
```  
  
## <a name="parameters"></a>パラメーター  
 `AssemblyID`  
 アセンブリの ID。  
  
 `FileToken`  
 PE タイプが設定されるファイルのトークン。 非バインドネットモジュール`AssemblyID`を示さない場合は NULL にできます。  
  
 `dwPEKind`  
 [CorPEKind 列挙](../metadata/corpekind-enumeration.md)で示されている PE の型。  
  
 `dwMachine`  
 NT ヘッダーに示されている、ターゲット コンピュータのアーキテクチャ。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は、S_OKを返します。  
  
## <a name="requirements"></a>必要条件  
 alink.h が必要です。  
  
## <a name="see-also"></a>関連項目

- [GetPEKind メソッド](../metadata/imetadataimport2-getpekind-method.md)
- [IALink2 インターフェイス](ialink2-interface.md)
- [IALink インターフェイス](ialink-interface.md)
- [ALink API](index.md)
