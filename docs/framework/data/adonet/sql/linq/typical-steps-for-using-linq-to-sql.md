---
title: 典型的な LINQ to SQL の使用手順
ms.date: 03/30/2017
ms.assetid: 9a88bd51-bd74-48f7-a9b1-f650e8d55a3e
ms.openlocfilehash: c7964c821a838e027302cddce704d86cc6a34f66
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792347"
---
# <a name="typical-steps-for-using-linq-to-sql"></a>典型的な LINQ to SQL の使用手順
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] アプリケーションを実装するには、このトピックで説明する手順に従います。 多くの手順は省略できます。 既定の状態でオブジェクト モデルを使用することもできます。  
  
 オブジェクト リレーショナル デザイナーを使用してオブジェクト モデルを作成し、クエリのコーディングを開始すると、非常に簡単です。  
  
## <a name="creating-the-object-model"></a>オブジェクト モデルの作成  
 最初に、既存のリレーショナル データベースのメタデータからオブジェクト モデルを作成します。 オブジェクト モデルは、開発者のプログラミング言語に従ってデータベースを表します。 詳しくは、「[LINQ to SQL オブジェクト モデル](the-linq-to-sql-object-model.md)」をご覧ください。  
  
### <a name="1-select-a-tool-to-create-the-model"></a>1.モデルを作成するツールを選択します。  
 モデルを作成するツールとして、3 つのツールを使用できます。  
  
- オブジェクト リレーショナル デザイナー  
  
     このデザイナーは、既存のデータベースからモデルを作成する多機能なユーザー インターフェイスを備えています。 このツールは Visual Studio IDE の一部であり、小規模または中規模のデータベースに最適です。  
  
- SQLMetal コード生成ツール  
  
     このコマンド ライン ユーティリティは、O/R デザイナーと多少異なるオプション セットを備えています。 このツールは、大規模なデータベースのモデル化に適しています。 詳しくは、「[SqlMetal.exe (コード生成ツール)](../../../../tools/sqlmetal-exe-code-generation-tool.md)」をご覧ください。  
  
- コード エディター  
  
     Visual Studio のコード エディターまたは他のエディターを使用して、独自のコードを作成できます。 既存のデータベースがあり、O/R デザイナーまたは SQLMetal ツールを使用できる場合は、この方法はエラーを発生する可能性が高いため、その使用はお勧めできません。 ただし、コード エディターは、他のツールを使用して既に生成されたコードを調整または変更する場合に役立ちます。 詳細については、[コード エディターを使用してエンティティ クラスをカスタマイズする](how-to-customize-entity-classes-by-using-the-code-editor.md)」を参照してください。  
  
### <a name="2-select-the-kind-of-code-you-want-to-generate"></a>2.生成するコードの種類を選択します。  
  
- 属性ベースの対応付け用の C# または Visual Basic のソース コード ファイル。  
  
     このコード ファイルを、Visual Studio プロジェクトに含めます。 詳しくは、「[属性ベースの対応付け](attribute-based-mapping.md)」をご覧ください。  
  
- 外部マッピング用の XML ファイル。  
  
     この方法を使用すると、アプリケーション コードとは別にマッピング メタデータを保持できます。 詳細については、「[外部マップ](external-mapping.md)」を参照してください。  
  
    > [!NOTE]
    > O/R デザイナーでは、外部マッピング ファイルの生成はサポートされていません。 SQLMetal ツールを使用してこの機能を実装する必要があります。  
  
- 最終コード ファイルを生成する前に変更できる DBML ファイル。  
  
     これは高度な機能です。  
  
### <a name="3-refine-the-code-file-to-reflect-the-needs-of-your-application"></a>3.コード ファイルを調整して、アプリケーションのニーズを反映します。  
 この目的には、O/R デザイナーまたはコード エディターを使用できます。  
  
## <a name="using-the-object-model"></a>オブジェクト モデルの使用  
 2 層シナリオでの開発者とデータの関係を次の図に示します。 その他のシナリオについては、「[LINQ to SQL での N 層およびリモート アプリケーション](n-tier-and-remote-applications-with-linq-to-sql.md)」を参照してください。  
  
 ![Linq オブジェクト モデルを示すスクリーンショット。](./media/the-linq-to-sql-object-model/linq-object-model-two-tier.png)  
  
 オブジェクト モデルが完成したので、そのモデル内で情報要求を記述し、データを操作します。 オブジェクト モデルのオブジェクトとプロパティを使用し、データベースの行と列は使用しません。 データベースを直接操作することはありません。  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] に対して、記述したクエリの実行、または操作したデータに対する `SubmitChanges()` の呼び出しを指示すると、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、データベースの言語でデータベースとの通信が行われます。  
  
 作成したオブジェクト モデルの典型的な使用手順を次に示します。  
  
### <a name="1-create-queries-to-retrieve-information-from-the-database"></a>1.クエリを作成し、データベースから情報を取得します。  
 詳しくは、「[クエリの概念](query-concepts.md)」と「[クエリの例](query-examples.md)」をご覧ください。  
  
### <a name="2-override-default-behaviors-for-insert-update-and-delete"></a>2.挿入、更新、および削除の既定の動作をオーバーライドします。  
 この手順は省略できます。 詳細については、「[挿入、更新、および削除の各操作のカスタマイズ](customizing-insert-update-and-delete-operations.md)」を参照してください。  
  
### <a name="3-set-appropriate-options-to-detect-and-report-concurrency-conflicts"></a>3.適切なオプションを設定し、コンカレンシーの競合を検出およびレポートします。  
 コンカレンシーの競合の処理について、モデルの既定値をそのまま使用することも、目的に合わせて変更することもできます。 詳細については、[コンカレンシーの競合を検査するメンバーを指定する](how-to-specify-which-members-are-tested-for-concurrency-conflicts.md)」および「[方法: コンカレンシー例外をいつスローするかを指定する](how-to-specify-when-concurrency-exceptions-are-thrown.md)」を参照してください。  
  
### <a name="4-establish-an-inheritance-hierarchy"></a>4.継承階層を確立します。  
 この手順は省略できます。 詳細については、「[継承のサポート](inheritance-support.md)」を参照してください。  
  
### <a name="5-provide-an-appropriate-user-interface"></a>5.適切なユーザー インターフェイスを提供します。  
 この手順は省略でき、アプリケーションの使用方法によって異なります。  
  
### <a name="6-debug-and-test-your-application"></a>6.アプリケーションをデバッグおよびテストします。  
 詳しくは、「[デバッグのサポート](debugging-support.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [はじめに](getting-started.md)
- [オブジェクト モデルの作成](creating-the-object-model.md)
- [ストアド プロシージャ](stored-procedures.md)
