---
title: ISymUnmanagedAsyncMethodPropertiesWriter インターフェイス
ms.date: 03/30/2017
ms.assetid: caa71820-8058-4b6a-93a2-25ee757d92d3
ms.openlocfilehash: 04876483fd42e3f6e55222416fd0747891734a52
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501860"
---
# <a name="isymunmanagedasyncmethodpropertieswriter-interface"></a>ISymUnmanagedAsyncMethodPropertiesWriter インターフェイス
各メソッドシンボルに対してオプションの非同期メソッド情報を定義できます。 開いているメソッドでは常にを使用します。つまり、 [Openmethod メソッド](isymunmanagedwriter-openmethod-method.md)と[closemethod メソッド](isymunmanagedwriter-closemethod-method.md)の呼び出しの間です。  
  
## <a name="syntax"></a>構文  
  
```idl  
[object,uuid(FC073774-1739-4232-BD56-A027294BEC15),pointer_default(unique)]interface ISymUnmanagedAsyncMethodPropertiesWriter : IUnknown  
```  
  
## <a name="methods"></a>メソッド  
 このインターフェイスには、次のメソッドが含まれています。  
  
|Method|説明|  
|------------|-----------------|  
|[DefineAsyncStepInfo メソッド](isymunmanagedasyncmethodpropertieswriter-defineasyncstepinfo-method.md)|現在のメソッドで非同期 await 操作のグループを定義します。<br /><br /> 各 yield オフセットは await の戻り命令に一致し、潜在的な yield を識別します。 各 `breakpointMethod` / `breakpointOffset` ペアは、非同期操作が再開される場所を識別します。これは、別のメソッドに存在する可能性があります。|  
|[DefineCatchHandlerILOffSet メソッド](isymunmanagedasyncmethodpropertieswriter-definecatchhandleriloffset-method.md)|非同期メソッドをラップする、コンパイラによって生成される catch ハンドラーの IL オフセットを設定します。<br /><br /> 生成された catch の IL オフセットは、ユーザーコードメソッドで発生する可能性があっても、catch を非ユーザーコードとして処理するためにデバッガーによって使用されます。 特に、 **CatchHandlerFound** exception イベントに応答して使用されます。|  
|[DefineKickoffMethod メソッド](isymunmanagedasyncmethodpropertieswriter-definekickoffmethod-method.md)|非同期操作を開始する開始メソッドを設定します。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断インターフェイス](diagnostics-symbol-store-interfaces.md)
