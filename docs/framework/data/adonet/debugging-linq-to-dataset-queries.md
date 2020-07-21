---
title: LINQ to DataSet クエリのデバッグ
ms.date: 03/30/2017
ms.assetid: f4c54015-8ce2-4c5c-8d18-7038144cc66d
ms.openlocfilehash: a82fd3e99a556daf40e5c65a16cf20278f38ea26
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785214"
---
# <a name="debugging-linq-to-dataset-queries"></a>LINQ to DataSet クエリのデバッグ

Visual Studio では、LINQ to DataSet のコードのデバッグがサポートされています。 ただし、LINQ to DataSet のコードのデバッグと LINQ to DataSet 以外のマネージド コードのデバッグとでは若干違いがあります。 ステップ実行、ブレークポイントの設定、デバッガー ウィンドウでの結果の確認など、ほとんどのデバッグ機能は、LINQ to DataSet のステートメントでも使用できます。 ただし、LINQ to DataSet のコードをデバッグするときは、クエリの遅延実行による副作用を考慮する必要があり、エディット コンティニュの使用についてもいくつかの制限があります。 このトピックでは、LINQ to DataSet 以外のマネージド コードと比較して LINQ to DataSet に固有のデバッグの側面について説明します。  
  
## <a name="viewing-results"></a>結果の表示  
 LINQ to DataSet のステートメントの結果を表示するには、DataTip、ウォッチ ウィンドウ、および [クイック ウォッチ] ダイアログ ボックスを使用します。 ソース ウィンドウで特定のクエリにポインターを置くと、データヒントが表示されます。 LINQ to DataSet の変数をコピーし、それをウォッチ ウィンドウまたは [クイック ウォッチ] ダイアログ ボックスに貼り付けることができます。 LINQ to DataSet のクエリは、作成または宣言された時点では評価されず、実行されるときにだけ評価されます。 これを "*遅延実行*" といいます。 したがって、それが評価されるまでは、クエリ変数に値は割り当てられません。 詳しくは、「[LINQ to DataSet でのクエリ](queries-in-linq-to-dataset.md)」をご覧ください。  
  
 デバッガーは、クエリの結果を表示するために、そのクエリを評価する必要があります。 この暗黙的な評価は、LINQ to DataSet のクエリ結果をデバッガーで表示したときに実行され、考慮する必要のある影響がいくつかあります。 クエリの評価には時間がかかります。 結果ノードを展開するときにも時間を要します。 クエリによっては繰り返し評価が実行され、パフォーマンスが著しく低下する場合があります。 さらに、データの値またはプログラムの状態が変わるという副作用が伴う場合もあります。 すべてのクエリに副作用があるわけではありません。 副作用を伴うことなく安全にクエリを評価できるかどうかを判断するには、クエリが実装されているコードを十分に理解する必要があります。 詳しくは、「[副作用と式](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/a7a250bs(v=vs.120))」をご覧ください。  
  
## <a name="edit-and-continue"></a>エディット コンティニュ  
 エディット コンティニュでは、LINQ to DataSet のクエリの変更はサポートされていません。 デバッグ セッション中に LINQ to DataSet のステートメントを追加、削除、または変更すると、そのような変更がエディット コンティニュでサポートされていないことを示すダイアログ ボックスが表示されます。 このとき、変更を元に戻すか、デバッグ セッションを中止して編集済みのコードで新たなセッションを開始するかを選択できます。  
  
 また、エディット コンティニュでは、LINQ to DataSet のステートメントで使用されている変数の型や値の変更もサポートされていません。 この場合も、変更を元に戻すか、デバッグ セッションを中止して新たなセッションを開始するかを選択できます。  
  
 Visual Studio の Visual C# では、LINQ to DataSet のクエリが含まれるメソッドのコードに対して、エディット コンティニュを使用することはできません。  
  
 Visual Studio の Visual Basic では、LINQ to DataSet のクエリが含まれるメソッドであっても、LINQ to DataSet 以外のコードであればエディット コンティニュを使用できます。 LINQ to DataSet のステートメントの前であれば、LINQ to DataSet のクエリの行番号が変わる場合でも、コードの追加や削除を行うことができます。 LINQ to DataSet 以外のコードに対する Visual Basic のデバッグ エクスペリエンスは、LINQ to DataSet が導入される前と同じです。 ただし、デバッグを中止して変更を適用しない限り、LINQ to DataSet のクエリを変更、追加、または削除することはできません。  
  
## <a name="see-also"></a>関連項目

- [マネージド コードをデバッグする](/visualstudio/debugger/debugging-managed-code)
- [プログラミング ガイド](programming-guide-linq-to-dataset.md)
