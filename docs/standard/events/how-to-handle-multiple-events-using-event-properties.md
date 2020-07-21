---
title: '方法: イベント プロパティを使用して複数のイベントを処理する'
description: イベント プロパティを使用して多数のイベントを処理する方法について説明します。 デリゲート コレクション、イベント キー、イベント プロパティを定義します。 アクセス機構の追加と削除を実装します。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- event properties [.NET Framework]
- multiple events [.NET Framework]
- event handling [.NET Framework], with multiple events
- events [.NET Framework], multiple
ms.assetid: 30047cba-e2fd-41c6-b9ca-2ad7a49003db
ms.openlocfilehash: 5b528aa2145ba703ce605ce22ae7d643f1e5b8d0
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84769016"
---
# <a name="how-to-handle-multiple-events-using-event-properties"></a>方法: イベント プロパティを使用して複数のイベントを処理する
イベント プロパティを使用するには、イベントを発生させるクラスにイベント プロパティを定義し、そのイベントを処理するクラスにイベント プロパティのデリゲートを設定します。 1 つのクラスにイベント プロパティを複数実装するには、そのクラス内部に、各イベント用に定義されたデリゲートを格納および保持する必要があります。 通常は、イベント キーをインデックスとするデリゲート コレクションを実装することによってこれを実現します。  
  
 イベントのデリゲートを格納するには、<xref:System.ComponentModel.EventHandlerList> クラスを使用するか、独自のコレクションを実装します。 コレクション クラスには、イベント キーに基づいてイベント ハンドラー デリゲートに対する設定、アクセス、および取得を行うメソッドを用意する必要があります。 たとえば、<xref:System.Collections.Hashtable> クラスを使用したり、<xref:System.Collections.DictionaryBase> クラスからカスタム クラスを派生させたりできます。 デリゲート コレクションの実装の詳細をクラスの外部に公開する必要はありません。  
  
 クラス内の各イベント プロパティには、add アクセサー メソッドおよび remove アクセサー メソッドを定義します。 イベント プロパティの add アクセサーは、入力デリゲート インスタンスをデリゲート コレクションに追加します。 イベント プロパティの remove アクセサーは、デリゲート コレクションから入力デリゲート インスタンスを削除します。 これらのイベント プロパティ アクセサーでは、イベント プロパティに定義済みのキーを使用して、デリゲート コレクションに対するインスタンスの追加や削除を行います。  
  
### <a name="to-handle-multiple-events-using-event-properties"></a>イベント プロパティを使用して複数のイベントを処理するには  
  
1. イベントを発生させるクラスにデリゲート コレクションを定義します。  
  
2. 各イベントについて、キーを定義します。  
  
3. イベントを発生させるクラスにイベント プロパティを定義します。  
  
4. デリゲート コレクションを使用して、各イベント プロパティに対する add アクセサーおよび remove アクセサーを実装します。  
  
5. パブリック イベント プロパティを使用して、イベントを処理するクラスのイベント ハンドラー デリゲートの追加と削除を行います。  
  
## <a name="example"></a>例  
 各イベントのデリゲートを格納するために `MouseDown` を使用して、`MouseUp` イベント プロパティおよび <xref:System.ComponentModel.EventHandlerList> イベント プロパティを実装する C# コードの例を次に示します。 イベント プロパティ コンストラクトのキーワードは、太字で示されています。  
  
 [!code-cpp[Conceptual.Events.Other#31](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.events.other/cpp/example3.cpp#31)]
 [!code-csharp[Conceptual.Events.Other#31](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.events.other/cs/example3.cs#31)]
 [!code-vb[Conceptual.Events.Other#31](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.events.other/vb/example3.vb#31)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.ComponentModel.EventHandlerList?displayProperty=nameWithType>
- [イベント](index.md)
- <xref:System.Web.UI.Control.Events%2A?displayProperty=nameWithType>
- [方法: カスタム イベントを宣言してメモリを節約する](../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md)
