---
title: ISymENCUnmanagedMethod インターフェイス
ms.date: 03/30/2017
api_name:
- ISymENCUnmanagedMethod
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymENCUnmanagedMethod
helpviewer_keywords:
- ISymENCUnmanagedMethod interface [.NET Framework debugging]
ms.assetid: faebf594-67d5-4abf-b9c1-547fd3a1ff87
topic_type:
- apiref
ms.openlocfilehash: 54c8c7f5c3ba6b4afd4ff352a8afb947a92e2d61
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83441878"
---
# <a name="isymencunmanagedmethod-interface"></a>ISymENCUnmanagedMethod インターフェイス
エディットコンティニュ機能に関する情報を提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetDocumentsForMethod メソッド](isymencunmanagedmethod-getdocumentsformethod-method.md)|このメソッドに行が含まれているドキュメントを取得します。|  
|[GetDocumentsForMethodCount メソッド](isymencunmanagedmethod-getdocumentsformethodcount-method.md)|このメソッドに行があるドキュメントの数を取得します。|  
|[GetFileNameFromOffset メソッド](isymencunmanagedmethod-getfilenamefromoffset-method.md)|オフセットに関連付けられた行のファイル名を取得します。|  
|[GetLineFromOffset メソッド](isymencunmanagedmethod-getlinefromoffset-method.md)|オフセットに関連付けられている行情報を取得します。|  
|[GetSourceExtentInDocument メソッド](isymencunmanagedmethod-getsourceextentindocument-method.md)|特定のドキュメント内のメソッドの最小の開始行と最大の終了行を取得します。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断インターフェイス](diagnostics-symbol-store-interfaces.md)
