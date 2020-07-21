---
title: ISymUnmanagedAsyncMethod インターフェイス
ms.date: 03/30/2017
ms.assetid: f2de5224-fd91-45de-9e58-bc600c6d22f1
ms.openlocfilehash: 448ed719331469dce8f15500f14d5c1b0707ecf7
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504453"
---
# <a name="isymunmanagedasyncmethod-interface"></a>ISymUnmanagedAsyncMethod インターフェイス
このインターフェイスは、 [ISymUnmanagedAsyncMethodPropertiesWriter インターフェイス](isymunmanagedasyncmethodpropertieswriter-interface.md)への読み取り補数です。  
  
## <a name="syntax"></a>構文  
  
```idl  
[object,uuid(B20D55B3-532E-4906-87E7-25BD5734ABD2),pointer_default(unique)]interface ISymUnmanagedAsyncMethod : IUnknown  
```  
  
## <a name="methods"></a>メソッド  
 このインターフェイスには、次のメソッドが含まれています。  
  
|Method|説明|  
|------------|-----------------|  
|[GetAsyncStepInfo メソッド](isymunmanagedasyncmethod-getasyncstepinfo-method.md)|「 [DefineAsyncStepInfo メソッド](isymunmanagedasyncmethodpropertieswriter-defineasyncstepinfo-method.md)」を参照してください。|  
|[GetAsyncStepInfoCount メソッド](isymunmanagedasyncmethod-getasyncstepinfocount-method.md)|「 [DefineAsyncStepInfo メソッド](isymunmanagedasyncmethodpropertieswriter-defineasyncstepinfo-method.md)」を参照してください。|  
|[GetCatchHandlerILOffSet メソッド](isymunmanagedasyncmethod-getcatchhandleriloffset-method.md)|「 [DefineCatchHandlerILOffset メソッド](isymunmanagedasyncmethodpropertieswriter-definecatchhandleriloffset-method.md)」を参照してください。|  
|[GetKickoffMethod メソッド](isymunmanagedasyncmethod-getkickoffmethod-method.md)|「 [DefineKickoffMethod メソッド](isymunmanagedasyncmethodpropertieswriter-definekickoffmethod-method.md)」を参照してください。|  
|[HasCatchHandlerILOffSet メソッド](isymunmanagedasyncmethod-hascatchhandleriloffset-method.md)|「 [DefineCatchHandlerILOffset メソッド](isymunmanagedasyncmethodpropertieswriter-definecatchhandleriloffset-method.md)」を参照してください。|  
|[IsAsyncMethod メソッド](isymunmanagedasyncmethod-isasyncmethod-method.md)|メソッドに非同期情報があるかどうかを確認します。<br /><br /> このメソッドがを返す場合 `FALSE` 、このインターフェイス内の他のメソッドを呼び出すことはできません。 これらはすべて、 `E_UNEXPECTED` この場合はを返します。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断インターフェイス](diagnostics-symbol-store-interfaces.md)
