---
title: '方法: グローバル プロキシの選択をオーバーライドする'
description: 次の例に従って、WebRequest を URL に送信することで、グローバル プロキシの選択をオーバーライドします。これにより、この選択がプロキシ サーバーでオーバーライドされます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0da481a9-b414-4230-beb0-e3ceba882fe5
ms.openlocfilehash: 91f64775e2f401be9b740fe9e4c41e1087eb9617
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502510"
---
# <a name="how-to-override-a-global-proxy-selection"></a>方法: グローバル プロキシの選択をオーバーライドする
この例では、`www.contoso.com` に **WebRequest** を送信し、ポート 80 の `alternateproxy` という名前のプロキシ サーバーでグローバル プロキシの選択をオーバーライドします。  
  
## <a name="example"></a>例  
  
```csharp  
WebRequest req = WebRequest.Create("http://www.contoso.com/");  
req.Proxy = new WebProxy("http://alternateproxy:80/");  
```  
  
```vb  
Dim req As WebRequest = WebRequest.Create("http://www.contoso.com/")  
req.Proxy = New WebProxy("http://alternateproxy:80/")  
```  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
- **System.Net** 名前空間の [`using` ディレクティブ](../../csharp/language-reference/keywords/using-directive.md)。  
  
## <a name="see-also"></a>関連項目

- [アプリケーション プロトコルの使用](using-application-protocols.md)
- [プロキシを介したインターネットへのアクセス](accessing-the-internet-through-a-proxy.md)
