---
title: LINQ to SQL のソース コードの分析
ms.date: 03/30/2017
ms.assetid: cba3eef8-e108-4478-b588-ad59580e133e
ms.openlocfilehash: dda19800a9aea0d644740c5378f6d5065181993e
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70248077"
---
# <a name="analyzing-linq-to-sql-source-code"></a>LINQ to SQL のソース コードの分析
以下の手順を実行すると、Northwind サンプル データベースから [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] のソース コードを作成できます。 オブジェクト モデルの要素とデータベースの要素を比較対照することで、個別の項目がどのように対応付けられているかがわかります。  
  
> [!NOTE]
> Visual Studio を使用している開発者は、O/R デザイナーを使用してこのコードを生成できます。  
  
1. 開発用コンピューターに Northwind サンプル データベースがない場合は、無料でダウンロードできます。 詳細については、「[サンプル データベースのダウンロード](downloading-sample-databases.md)」を参照してください。  
  
2. SqlMetal コマンド ライン ツールを使用して、Visual Basic または C# のソース ファイルを生成します。 詳しくは、「[SqlMetal.exe (コード生成ツール)](../../../../tools/sqlmetal-exe-code-generation-tool.md)」をご覧ください。 コマンド プロンプトで次のコマンドを入力すると、ストアド プロシージャおよび関数を含めて Visual Basic または C# のソース ファイルを生成できます。  
  
    - `sqlmetal /code:northwind.vb /language:vb "c:\northwnd.mdf" /sprocs /functions /pluralize`  
  
    - `sqlmetal /code:northwind.cs /language:csharp "c:\northwnd.mdf" /sprocs /functions /pluralize`  
  
## <a name="see-also"></a>関連項目

- [参照](reference.md)
- [背景情報](background-information.md)
