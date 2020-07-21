---
title: '方法: Web ページを要求し、ストリームとして結果を取得する'
description: この例では、.NET Framework で Web ページを要求し、ストリームで結果を取得する方法を示します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d32b7f35-29d8-4fb7-ad71-d219edc5e359
ms.openlocfilehash: bd57f9af6be29c783d044e785ebb36aaa8592df2
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502484"
---
# <a name="how-to-request-a-web-page-and-retrieve-the-results-as-a-stream"></a>方法: Web ページを要求し、ストリームとして結果を取得する

この例では、Web ページを要求し、ストリームとして結果を取得する方法を示します。
  
## <a name="example"></a>例

```csharp
var myClient = new WebClient();
Stream response = myClient.OpenRead("https://docs.microsoft.com/dotnet/");
// The stream data is used here.
response.Close();
```

```vb
Dim myClient As New WebClient()
Dim response As Stream = myClient.OpenRead("https://docs.microsoft.com/dotnet/")
' The stream data is used here.
response.Close()
```

## <a name="compiling-the-code"></a>コードのコンパイル

 この例で必要な要素は次のとおりです。

- <xref:System.IO> 名前空間と <xref:System.Net> 名前空間への参照。

## <a name="see-also"></a>関連項目

- [データの要求](requesting-data.md)
