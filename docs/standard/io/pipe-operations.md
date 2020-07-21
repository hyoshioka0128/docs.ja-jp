---
title: .NET のパイプ操作
description: .NET のパイプ操作について説明します。 パイプは、プロセス間通信の手段となります。 パイプには、匿名パイプと名前付きパイプの 2 種類があります。
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- pipes [.NET Framework]
- pipe operations [.NET Framework]
- interprocess communication [.NET Framework], pipes
- I/O [.NET Framework], pipes
ms.assetid: 7b964ebd-7a4f-4d28-8194-7841f9e4c702
ms.openlocfilehash: 35a3910bbab1b34f085a55524be0b18b3fa81958
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84768886"
---
# <a name="pipe-operations-in-net"></a>.NET のパイプ操作
パイプは、プロセス間通信の手段となります。 パイプには、2 種類あります。  
  
- 匿名パイプ。  
  
     匿名パイプは、ローカル コンピューターでのプロセス間通信を実現します。 匿名パイプは、名前付きパイプより必要なオーバーヘッドは少ないですが、提供するサービスは限られています。 匿名パイプは一方向であり、ネットワーク経由で使用することはできません。 これでは、1 つのサーバー インスタンスのみをサポートしています。 匿名パイプは、スレッド間、またはパイプ ハンドルを作成時に子プロセスに簡単に渡すことができる親と子のプロセス間の通信で便利です。  
  
     .NET では、<xref:System.IO.Pipes.AnonymousPipeServerStream> クラスと <xref:System.IO.Pipes.AnonymousPipeClientStream> クラスを使用して匿名パイプを実装します。  
  
     「[方法:ローカルのプロセス間通信で匿名パイプを使用する](how-to-use-anonymous-pipes-for-local-interprocess-communication.md)」を参照してください。  
  
- 名前付きパイプ。  
  
     名前付きパイプは、パイプ サーバーと 1 つ以上のパイプ クライアントとの間でのプロセス間通信を提供します。 名前付きパイプは、一方向であることも、双方向であることも可能です。 これでは、メッセージ ベースの通信がサポートされ、同じパイプ名を使用して複数のクライアントが同時にサーバー プロセスに接続することができます。 名前付きパイプでは、プロセスを接続してリモート サーバーで独自のアクセス許可を使用する、偽装もサポートしています。  
  
     .NET では、<xref:System.IO.Pipes.NamedPipeServerStream> クラスと <xref:System.IO.Pipes.NamedPipeClientStream> クラスを使用して名前付きパイプを実装します。  
  
     「[方法:ネットワークのプロセス間通信で名前付きパイプを使用する](how-to-use-named-pipes-for-network-interprocess-communication.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [ファイルおよびストリーム入出力](index.md)
- [方法: ローカルのプロセス間通信で匿名パイプを使用する](how-to-use-anonymous-pipes-for-local-interprocess-communication.md)
- [方法: ネットワークのプロセス間通信で名前付きパイプを使用する](how-to-use-named-pipes-for-network-interprocess-communication.md)
