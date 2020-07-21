---
title: インターネット要求の作成
description: 渡された URI スキームに基づいて派生クラスを作成する WebRequest.Create メソッドを利用することでアプリケーションで WebRequest インスタンスが作成されるしくみについて説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- WebRequest class, sending and receiving data
- Networking
- HttpWebResponse class, sending and receiving data
- requesting data from Internet, creating requests
- Network Resources
- Internet, requesting data
- data requests, creating requests
ms.assetid: faab683e-3f1e-4eee-b5e9-59f7245033d5
ms.openlocfilehash: 389c7bf5969eca4322aa680a6f28dec0b899709a
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325630"
---
# <a name="create-internet-requests"></a>インターネット要求の作成

アプリケーションは、<xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType> メソッドを使用して <xref:System.Net.WebRequest> のインスタンスを作成します。 <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType> は、渡された URI スキームに基づいて <xref:System.Net.WebRequest> から派生するクラスを作成する静的メソッドです。  
  
## <a name="web-file-and-ftp-requests"></a>Web、ファイル、FTP 要求

.NET Framework は、`WebRequest` から派生する <xref:System.Net.HttpWebRequest> クラスを提供することにより、HTTP および HTTPS 要求を処理します。 ほとんどの場合、`WebRequest` クラスは要求を行うのに必要なすべてのプロパティを提供しますが、必要に応じて、`WebRequest.Create` メソッドで作成した `WebRequest` オブジェクトを `HttpWebRequest` 型にキャストすることにより、その要求の HTTP 固有のプロパティにアクセスできます。 同様に、`HttpWebResponse` オブジェクトは、HTTP および HTTPS 要求からの応答を処理します。 `HttpWebResponse` オブジェクトの HTTP 固有プロパティにアクセスするには、`WebResponse` オブジェクトを `HttpWebResponse` 型にキャストする必要があります。  
  
.NET Framework では、URI スキームの "file:" を使用するリソースの要求を処理するために、<xref:System.Net.FileWebRequest> および <xref:System.Net.FileWebResponse> クラスも提供します。 同様に、"ftp:" スキームを使用するリソースの要求を処理するために、<xref:System.Net.FtpWebRequest> および <xref:System.Net.FtpWebResponse> クラスが提供されます。 要求が、これらのスキームのいずれかを使用するリソースに対するものである場合、`WebRequest.Create` メソッドを使用して、要求を行うために使用するオブジェクトを取得できます。  
  
アプリケーション レベルの他のプロトコルを使用する要求を処理するには、`WebRequest` および `WebResponse` から派生するプロトコル固有のクラスを実装します。 詳細については、「[プラグ可能なプロトコルのプログラミング](programming-pluggable-protocols.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [方法: WebRequest クラスを使用してデータを要求する](how-to-request-data-using-the-webrequest-class.md)
- [データの要求](requesting-data.md)
