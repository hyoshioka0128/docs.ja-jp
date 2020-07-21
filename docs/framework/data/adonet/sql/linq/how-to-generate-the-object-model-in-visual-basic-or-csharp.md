---
title: '方法: Visual Basic または C# でオブジェクト モデルを生成する'
ms.date: 03/30/2017
ms.assetid: a0c73b33-5650-420c-b9dc-f49310c201ee
ms.openlocfilehash: 7d2c0600534c93f5884eec48a4bdaa3ce99945e9
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002805"
---
# <a name="how-to-generate-the-object-model-in-visual-basic-or-c"></a>方法: Visual Basic または C\# でオブジェクト モデルを生成する
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、使用しているプログラミング言語のオブジェクト モデルが、リレーショナル データベースに対応付けられています。 既存のデータベースのメタデータから Visual Basic または C# のモデルを自動的に生成するには、2 つのツールを使用できます。  
  
- Visual Studio を使用している場合は、オブジェクト リレーショナル デザイナーを使用して、オブジェクト モデルを生成できます。 O/R デザイナーでは、機能が豊富なユーザー インターフェイスを使用して、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] のオブジェクト モデルを生成できます。 詳しくは、「[Visual Studio の LINQ to SQL ツール](https://docs.microsoft.com/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)」をご覧ください。
  
- SQLMetal コマンド ライン ツール。 詳しくは、「[SqlMetal.exe (コード生成ツール)](../../../../tools/sqlmetal-exe-code-generation-tool.md)」をご覧ください。  
  
    > [!NOTE]
    > 既存のデータベースがなく、オブジェクト モデルからデータベースを作成する場合は、コード エディターと <xref:System.Data.Linq.DataContext.CreateDatabase%2A> を使用してオブジェクト モデルを作成できます。 詳細については、[データベースを動的に作成する](how-to-dynamically-create-a-database.md)」を参照してください。  
  
 O/R デザイナーのドキュメントでは、O/R デザイナーを使用して Visual Basic または C# のオブジェクト モデルを生成する方法の例が提供されています。 以下の情報は、SQLMetal コマンド ライン ツールの使用方法の例です。 詳しくは、「[SqlMetal.exe (コード生成ツール)](../../../../tools/sqlmetal-exe-code-generation-tool.md)」をご覧ください。  
  
## <a name="example"></a>例  
 次の例に示す SQLMetal のコマンド ラインでは、Northwind サンプル データベースの属性ベースのオブジェクト モデルとして Visual Basic のコードが生成されます。 ストアド プロシージャと関数も含まれます。  
  
```console  
sqlmetal /code:northwind.vb /language:vb "c:\northwnd.mdf" /sprocs /functions  
```  
  
## <a name="example"></a>例  
 次の例に示す SQLMetal コマンド ラインでは、Northwind サンプル データベースの属性ベースのオブジェクト モデルとして C# コードが生成されます。 ストアド プロシージャと関数も含まれ、テーブル名は自動的に複数化されます。  
  
```console  
sqlmetal /code:northwind.cs /language:csharp "c:\northwnd.mdf" /sprocs /functions /pluralize  
```  
  
## <a name="see-also"></a>関連項目

- [プログラミング ガイド](programming-guide.md)
- [LINQ to SQL オブジェクト モデル](the-linq-to-sql-object-model.md)
- [チュートリアルによる学習](learning-by-walkthroughs.md)
- [方法: コード エディターを使用してエンティティ クラスをカスタマイズする](how-to-customize-entity-classes-by-using-the-code-editor.md)
- [属性ベースの対応付け](attribute-based-mapping.md)
- [SqlMetal.exe (コード生成ツール)](../../../../tools/sqlmetal-exe-code-generation-tool.md)
- [外部マップ](external-mapping.md)
- [サンプル データベースのダウンロード](downloading-sample-databases.md)
- [オブジェクト モデルの作成](creating-the-object-model.md)
