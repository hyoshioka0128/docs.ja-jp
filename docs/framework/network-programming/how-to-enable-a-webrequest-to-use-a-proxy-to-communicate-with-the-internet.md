---
title: '方法: WebRequest でインターネットとの通信にプロキシを使用できるようにする'
description: グローバル プロキシ インスタンスを作成し、任意の WebRequest がプロキシを使用して .NET Framework でインターネットと通信できるようにする方法について学習します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 63c0ef2c-44b5-4c54-9804-ba0b9b001ac7
ms.openlocfilehash: 0fc33cea3f5a7fe4669b110e53e71afdb9561c23
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502536"
---
# <a name="how-to-enable-a-webrequest-to-use-a-proxy-to-communicate-with-the-internet"></a>方法: WebRequest でインターネットとの通信にプロキシを使用できるようにする

この例では、<xref:System.Net.WebRequest> でインターネットとの通信にプロキシを使用できるようにするグローバル プロキシ インスタンスを作成します。 ここでは、プロキシ サーバーが `webproxy` という名前で、ポート 80 (標準 HTTP ポート) で通信を行うことを想定します。

## <a name="example"></a>例

```csharp
var proxyObject = new WebProxy("http://webproxy:80/");
GlobalProxySelection.Select = proxyObject;
```

```vb
Dim proxyObject As New WebProxy("http://webproxy:80/")
GlobalProxySelection.Select = proxyObject
```

## <a name="compiling-the-code"></a>コードのコンパイル

この例で必要な要素は次のとおりです。

- **System.Net** 名前空間の C# [`using`ディレクティブ](../../csharp/language-reference/keywords/using-directive.md)。
- **System.Net** 名前空間の Visual Basic [`Imports`ステートメント](../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)。

## <a name="see-also"></a>関連項目

- [アプリケーション プロトコルの使用](using-application-protocols.md)
- [プロキシを介したインターネットへのアクセス](accessing-the-internet-through-a-proxy.md)
