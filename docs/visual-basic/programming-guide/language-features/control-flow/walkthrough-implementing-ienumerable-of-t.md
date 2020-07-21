---
title: IEnumerable の実装
ms.date: 07/31/2018
helpviewer_keywords:
- control flow [Visual Basic]
- enumerable interfaces
- loop structures [Visual Basic], optimizing performance
- control flow [Visual Basic]
ms.assetid: c60d7589-51f2-4463-a2d5-22506bbc1554
ms.openlocfilehash: 582957c91eac63cf7f72dd2f6c0cf40e627be686
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402032"
---
# <a name="walkthrough-implementing-ienumerableof-t-in-visual-basic"></a>チュートリアル: Visual Basic での IEnumerable(Of T) の実装
<xref:System.Collections.Generic.IEnumerable%601> インターフェイスは、値のシーケンスを、一度に 1 項目ずつ返すことができるクラスによって実装されます。 一度に 1 項目ずつデータを返す利点は、データ セット全体をメモリに読み込んで操作する必要がないことです。 データから 1 つの項目を読み込むのに必要なメモリを使用するだけで済みます。 `IEnumerable(T)` インターフェイスを実装するクラスを、`For Each` ループまたは LINQ クエリで使用できます。  
  
 たとえば、大きなテキスト ファイルを読み取り、そのファイルから、特定の検索条件に一致する各行を返す必要があるアプリケーションがあるとします。 アプリケーションは LINQ クエリを使用して、指定された条件に一致する行をファイルから返します。 LINQ クエリを使用してファイルのコンテンツにクエリを実行するために、アプリケーションでは、ファイルのコンテンツを配列またはコレクションに読み込むことができます。 ただし、ファイル全体を配列またはコレクションに読み込むと、必要以上にメモリが消費されます。 LINQ クエリは、列挙可能なクラスを使用してファイルのコンテンツにクエリを実行し、検索条件に一致する値のみを返すことができます。 一致する値だけをいくつか返すクエリの場合、消費メモリは格段に少なくなります。  
  
 <xref:System.Collections.Generic.IEnumerable%601> インターフェイスを実装するクラスを作成して、ソース データを、列挙可能なデータとして公開できます。 `IEnumerable(T)` インターフェイスを実装するクラスには、ソース データを反復処理するために <xref:System.Collections.Generic.IEnumerator%601> インターフェイスを実装する別のクラスが必要です。 この 2 つのクラスを使用すると、データの項目を特定の型として順番に返すことができます。  
  
 このチュートリアルでは、`IEnumerable(Of String)` インターフェイスを実装するクラスと `IEnumerator(Of String)` インターフェイスを実装するクラスを作成して、テキスト ファイルを 1 行ずつ読み取ります。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="creating-the-enumerable-class"></a>列挙可能なクラスの作成  
  
**列挙可能なクラス プロジェクトを作成する**

1. Visual Basic で、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

1. **[新しいプロジェクト]** ダイアログ ボックスの **[プロジェクトの種類]** ペインで、 **[Windows]** が選択されていることを確認します。 **[テンプレート]** ペインで **[クラス ライブラリ]** を選択します。 **[名前]** ボックスに `StreamReaderEnumerable` と入力して、 **[OK]** をクリックします。 新しいプロジェクトが表示されます。

1. **ソリューション エクスプローラー**で、Class1.vb ファイルを右クリックし、 **[名前の変更]** をクリックします。 ファイルの名前を `StreamReaderEnumerable.vb` に変更し、Enter キーを押します。 ファイルの名前を変更すると、クラスの名前も `StreamReaderEnumerable` に変更されます。 このクラスが `IEnumerable(Of String)` インターフェイスを実装します。

1. StreamReaderEnumerable プロジェクトを右クリックして **[追加]** をポイントし、 **[新しい項目]** をクリックします。 **[クラス]** テンプレートを選択します。 **[名前]** ボックスに「`StreamReaderEnumerator.vb`」と入力し、 **[OK]** をクリックします。

 このプロジェクトの最初のクラスは列挙可能なクラスであり、`IEnumerable(Of String)` インターフェイスを実装します。 このジェネリック インターフェイスは <xref:System.Collections.IEnumerable> インターフェイスを実装し、このクラスのコンシューマーが、`String` として型指定された値にアクセスできることを保証します。  
  
**IEnumerable を実装するコードを追加する**

1. StreamReaderEnumerable.vb ファイルを開きます。

2. `Public Class StreamReaderEnumerable` の後の行に以下を入力し、Enter キーを押します。

     [!code-vb[VbVbalrIteratorWalkthrough#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#1)]

   `IEnumerable(Of String)` インターフェイスに必要なメンバーが、クラスに自動入力されます。
  
3. この列挙可能なクラスは、テキスト ファイルから 1 行ずつ行を読み取ります。 次のコードをクラスに追加して、ファイル パスを入力パラメーターとして取るパブリック コンストラクターを公開します。

     [!code-vb[VbVbalrIteratorWalkthrough#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#2)]

4. `IEnumerable(Of String)` インターフェイスの <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> メソッドの実装は、`StreamReaderEnumerator` クラスの新しいインスタンスを返します。 `IEnumerable(Of String)` インターフェイスのメンバーのみを公開する必要があるため、`IEnumerable` インターフェイスの `GetEnumerator` メソッドの実装は `Private` にできます。 `GetEnumerator` メソッド用に生成されたコードを次のコードに置き換えます。

     [!code-vb[VbVbalrIteratorWalkthrough#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#3)]  
  
**IEnumerator を実装するコードを追加する**

1. StreamReaderEnumerator.vb ファイルを開きます。

2. `Public Class StreamReaderEnumerator` の後の行に以下を入力し、Enter キーを押します。

     [!code-vb[VbVbalrIteratorWalkthrough#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#4)]

   `IEnumerator(Of String)` インターフェイスに必要なメンバーが、クラスに自動入力されます。

3. 列挙子クラスはテキスト ファイルを開き、ファイルから行を読み取るためにファイル I/O を実行します。 次のコードをクラスに追加して、ファイル パスを入力パラメーターとして取るパブリック コンストラクターを公開し、読み取るテキスト ファイルを開きます。

     [!code-vb[VbVbalrIteratorWalkthrough#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#5)]

4. `IEnumerator(Of String)` インターフェイスと `IEnumerator` インターフェイスの両方の `Current` プロパティが、テキスト ファイルから現在の項目を `String` として返します。 `IEnumerator(Of String)` インターフェイスのメンバーのみを公開する必要があるため、`IEnumerator` インターフェイスの `Current` プロパティの実装は `Private` にできます。 `Current` プロパティ用に生成されたコードを次のコードに置き換えます。

     [!code-vb[VbVbalrIteratorWalkthrough#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#6)]

5. `IEnumerator` インターフェイスの `MoveNext` メソッドは、テキスト ファイル内の次の項目に移動し、`Current` プロパティによって返される値を更新します。 読み取る項目がない場合、`MoveNext` メソッドは `False` を返します。それ以外の場合、`MoveNext` メソッドは `True` を返します。 `MoveNext` メソッドに次のコードを追加します。

     [!code-vb[VbVbalrIteratorWalkthrough#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#7)]

6. `IEnumerator` インターフェイスの `Reset` メソッドは、テキスト ファイルの先頭を指すよう反復子に指示し、現在の項目の値をクリアします。 `Reset` メソッドに次のコードを追加します。

     [!code-vb[VbVbalrIteratorWalkthrough#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#8)]

7. `IEnumerator` インターフェイスの `Dispose` メソッドは、反復子が破棄される前にすべてのアンマネージ リソースが解放されることを保証します。 `StreamReader` オブジェクトによって使用されるファイル ハンドルはアンマネージ リソースです。このハンドルは、反復子インスタンスが破棄される前に閉じる必要があります。 `Dispose` メソッド用に生成されたコードを次のコードに置き換えます。

     [!code-vb[VbVbalrIteratorWalkthrough#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/StreamReaderIterator.vb#9)]
  
## <a name="using-the-sample-iterator"></a>サンプル反復子の使用

 コードでは、`For Next` ループや LINQ クエリなどの `IEnumerable` を実装するオブジェクトを必要とする制御構造と一緒に、列挙可能なクラスを使用できます。 次の例は、LINQ クエリの `StreamReaderEnumerable` を示しています。  
  
 [!code-vb[VbVbalrIteratorWalkthrough#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIteratorWalkthrough/VB/Module1.vb#10)]  
  
## <a name="see-also"></a>関連項目

- [Visual Basic における LINQ の概要](../linq/introduction-to-linq.md)
- [制御フロー](index.md)
- [ループ構造](loop-structures.md)
- [For Each...Next ステートメント](../../../language-reference/statements/for-each-next-statement.md)
