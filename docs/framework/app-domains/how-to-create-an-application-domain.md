---
title: '方法: アプリケーション ドメインを作成する'
description: .NET のアプリケーション ドメインを作成する方法について確認します。 アプリケーション ドメインを作成して、個人的に管理するアセンブリを読み込んだり、コードを実行したりすることができます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- application domains, creating
ms.assetid: ba1fa43e-49f5-47d9-bd7f-3024af16f4ba
ms.openlocfilehash: 8e44e682f64854dbc0181b26f6ed3fa2905b7814
ms.sourcegitcommit: 1c37a894c923bea021a3cc38ce7cba946357bbe1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85104806"
---
# <a name="how-to-create-an-application-domain"></a>方法: アプリケーション ドメインを作成する
共通言語ランタイム ホストにより、必要なときに、アプリケーション ドメインが自動的に作成されます。 ただし、独自のアプリケーション ドメインを作成し、個人的に管理するアセンブリにそれを読み込むことができます。 アプリケーション ドメインを作成し、そこからコードを実行することもできます。  
  
 <xref:System.AppDomain?displayProperty=nameWithType> クラスのオーバーロードされた **CreateDomain** メソッドの 1 つを利用し、新しいアプリケーション ドメインを作成します。 アプリケーション ドメインに名前を付け、その名前で参照できます。  
  
 次の例では、新しいアプリケーション ドメインを作成し、それに `MyDomain` という名前を割り当て、ホスト ドメインの名前と新しく作成された子アプリケーション ドメインがコンソールに出力されます。  
  
## <a name="example"></a>例  
 [!code-cpp[ADCreateDomain#2](../../../samples/snippets/cpp/VS_Snippets_CLR/ADCreateDomain/CPP/source2.cpp#2)]
 [!code-csharp[ADCreateDomain#2](../../../samples/snippets/csharp/VS_Snippets_CLR/ADCreateDomain/CS/source2.cs#2)]
 [!code-vb[ADCreateDomain#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/ADCreateDomain/VB/source2.vb#2)]  
  
## <a name="see-also"></a>関連項目

- [アプリケーション ドメインを使用したプログラミング](application-domains.md#programming-with-application-domains)
- [アプリケーション ドメインの使用](use.md)
