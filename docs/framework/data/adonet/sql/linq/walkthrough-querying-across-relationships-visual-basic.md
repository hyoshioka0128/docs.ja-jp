---
title: 'チュートリアル: リレーションシップを介したクエリの実行 (Visual Basic)'
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: a7da43e3-769f-4e07-bcd6-552b8bde66f4
ms.openlocfilehash: 3164656bb183e7773b098cab79d8fe5e0dc5de34
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792147"
---
# <a name="walkthrough-querying-across-relationships-visual-basic"></a>チュートリアル: リレーションシップを介したクエリの実行 (Visual Basic)
このチュートリアルでは、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の "*関連付け*" を使用してデータベース内の外部キー リレーションシップを表現する方法について説明します。  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 このチュートリアルは、Visual Basic 開発設定を使用して記述されています。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 「[チュートリアル:簡単なオブジェクト モデルとクエリ (Visual Basic)](walkthrough-simple-object-model-and-query-visual-basic.md)」を完了している必要があります。 このチュートリアルは前のチュートリアルに基づいて作成されており、c:\linqtest に northwnd.mdf ファイルがあることが前提です。  
  
## <a name="overview"></a>概要  
 このチュートリアルは、主に次の 3 つの手順で構成されています。  
  
- エンティティ クラスを追加して、Northwind サンプル データベース内の Orders テーブルを表します。  
  
- `Customer` クラスに注釈を付けて、`Customer` クラスと `Order` クラス間のリレーションシップを強化します。  
  
- クエリを作成および実行して、`Order` クラスによる `Customer` 情報の取得のプロセスをテストします。  
  
## <a name="mapping-relationships-across-tables"></a>テーブル間のリレーションシップを指定する  
 `Customer` クラス定義の後に、次のコードから成る `Order` エンティティ クラス定義を作成します。これは、`Orders.Customer` が外部キーとして `Customers.CustomerID` に関係することを示しています。  
  
#### <a name="to-add-the-order-entity-class"></a>Order エンティティ クラスを追加するには  
  
- `Customer` クラスの後に次のコードを入力または貼り付けます。  
  
     [!code-vb[DLinqWalk2VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#1)]  
  
## <a name="annotating-the-customer-class"></a>Customer クラスに注釈を付ける  
 ここでは、`Customer` クラスに注釈を付けて、`Order` クラスとのリレーションシップを指定します。 いずれかの方向のリレーションシップが定義されていればリンクを作成できるため、この注釈の追加は必ずしも必要ではありません。 しかし、この注釈を追加することで、どちらの方向でも簡単にオブジェクトを移動できます。  
  
#### <a name="to-annotate-the-customer-class"></a>Customer クラスに注釈を付けるには  
  
- `Customer` クラスに次のコードを入力または貼り付けます。  
  
     [!code-vb[DLinqWalk2VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#2)]  
  
## <a name="creating-and-running-a-query-across-the-customer-order-relationship"></a>Customer-Order リレーションシップ間のクエリを作成および実行する  
 `Order` オブジェクトから `Customer` オブジェクトに、またはその逆の順序で、直接アクセスできます。 Customer と Order の間に、明示的な "*結合*" は必要ありません。  
  
#### <a name="to-access-order-objects-by-using-customer-objects"></a>Customer オブジェクトを使用して Order オブジェクトにアクセスするには  
  
1. `Sub Main` メソッドに次のコードを入力または貼り付けることによって、メソッドを変更します。  
  
     [!code-vb[DLinqWalk2VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#3)]  
  
2. F5 キーを押して、アプリケーションをデバッグします。  
  
     2 つの名前がメッセージ ボックスに表示され、生成された SQL コードがコンソール ウィンドウに表示されます。  
  
3. メッセージ ボックスを閉じて、デバッグを停止します。  
  
## <a name="creating-a-strongly-typed-view-of-your-database"></a>データベースの厳密に型指定されたビューを作成する  
 データベースの厳密に型指定されたビューを使用すると、操作が非常に簡単になります。 <xref:System.Data.Linq.DataContext> オブジェクトを厳密に型指定することによって、<xref:System.Data.Linq.DataContext.GetTable%2A> を呼び出す必要がありません。 厳密に型指定された <xref:System.Data.Linq.DataContext> オブジェクトを使用する場合は、すべてのクエリで、厳密に型指定されたテーブルを使用できます。  
  
 次の手順では、データベース内の Customers テーブルに対応する厳密に型指定されたテーブルとして、`Customers` を作成します。  
  
#### <a name="to-strongly-type-the-datacontext-object"></a>DataContext オブジェクトを厳密に型指定するには  
  
1. `Customer` クラス宣言の上に次のコードを追加します。  
  
     [!code-vb[DLinqWalk2VB#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#4)]  
  
2. `Sub Main` を次のように変更し、厳密に型指定された <xref:System.Data.Linq.DataContext> を使用するようにします。  
  
     [!code-vb[DLinqWalk2VB#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#5)]  
  
3. F5 キーを押して、アプリケーションをデバッグします。  
  
     コンソール ウィンドウの出力は次のとおりです。  
  
     `ID=WHITC`  
  
4. コンソール ウィンドウで Enter キーを押してアプリケーションを終了します。  
  
5. このアプリケーションを保存するには、 **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
 次のチュートリアル「[チュートリアル: データの操作 (Visual Basic)](walkthrough-manipulating-data-visual-basic.md)」では、データの操作方法について説明します。 そのチュートリアルを実行するのに、既に終了したこのシリーズの 2 つのチュートリアルを保存する必要はありません。  
  
## <a name="see-also"></a>関連項目

- [チュートリアルによる学習](learning-by-walkthroughs.md)
