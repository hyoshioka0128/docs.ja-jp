---
title: '方法: WebRequest に一致するプロトコル固有の WebResponse を取得する'
description: .NET Framework で WebRequest に一致するプロトコル固有の WebResponse を取得する方法について学習します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d8c90785-f16b-42a5-8439-ed2f731b2ba8
ms.openlocfilehash: 15b1912a7bd951df7f3c14eb96251c2bdf237b4f
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502458"
---
# <a name="how-to-retrieve-a-protocol-specific-webresponse-that-matches-a-webrequest"></a>方法: WebRequest に一致するプロトコル固有の WebResponse を取得する
この例では、WebRequest に一致するプロトコル固有の WebResponse を取得する方法を説明します。  
  
## <a name="example"></a>例  
  
```csharp  
WebRequest req = WebRequest.Create("http://www.contoso.com/");  
WebResponse resp = req.GetResponse();  
```  
  
```vb  
Dim req As WebRequest = WebRequest.Create("http://www.contoso.com")  
Dim resp As WebResponse = req.GetResponse()  
```  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
- **System.Net** 名前空間への参照。  
  
## <a name="see-also"></a>関連項目

- [データの要求](requesting-data.md)
