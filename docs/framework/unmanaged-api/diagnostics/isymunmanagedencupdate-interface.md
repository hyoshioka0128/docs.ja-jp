---
title: ISymUnmanagedENCUpdate インターフェイス
ms.date: 03/30/2017
api_name:
- ISymUnmanagedENCUpdate
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedENCUpdate
helpviewer_keywords:
- ISymUnmanagedENCUpdate interface [.NET Framework debugging]
ms.assetid: 63a9ef45-01a6-46da-b958-5c6dc2dc232c
topic_type:
- apiref
ms.openlocfilehash: 1986d5f91a3dcfa31a43f729ee1f50129e083f5f
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501743"
---
# <a name="isymunmanagedencupdate-interface"></a>ISymUnmanagedENCUpdate インターフェイス
エディットコンティニュ機能の関数を提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetLocalVariableCount メソッド](isymunmanagedencupdate-getlocalvariablecount-method.md)|ローカル変数の数を取得します。|  
|[GetLocalVariables メソッド](isymunmanagedencupdate-getlocalvariables-method.md)|ローカル変数を取得します。|  
|[InitializeForEnc メソッド](isymunmanagedencupdate-initializeforenc-method.md)|[ISymUnmanagedENCUpdate:: UpdateSymbolStore2](isymunmanagedencupdate-updatesymbolstore2-method.md)メソッドの最初の呼び出しの前にメソッドの境界を計算できるようにします。|  
|[UpdateMethodLines メソッド](isymunmanagedencupdate-updatemethodlines-method.md)|再コンパイルされていないが、行が個別に移動したメソッドの行情報を更新できるようにします。 各ステートメントのデルタが許可されます。|  
|[UpdateSymbolStore2 メソッド](isymunmanagedencupdate-updatesymbolstore2-method.md)|行情報が要件を満たしている場合に、コンパイラがプログラムデータベース (PDB) ストリームから変更されていない関数を省略できるようにします。 正しい行情報は、古い PDB 行情報と、関数内のすべての行に対して1つのデルタで判別できます。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断インターフェイス](diagnostics-symbol-store-interfaces.md)
