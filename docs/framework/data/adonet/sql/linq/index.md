---
title: LINQ to SQL
description: LINQ to SQL は .NET Framework のコンポーネントであり、リレーショナル データをオブジェクトとして管理するためのランタイム インフラストラクチャを提供します。
ms.date: 03/30/2017
ms.assetid: 73d13345-eece-471a-af40-4cc7a2f11655
ms.openlocfilehash: 13502bfee3ee24764d190dace1512bc958343973
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "85503757"
---
# <a name="linq-to-sql"></a>LINQ to SQL
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は .NET Framework バージョン 3.5 のコンポーネントであり、リレーショナル データをオブジェクトとして管理するためのランタイム インフラストラクチャを提供します。  
  
> [!NOTE]
> リレーショナル データは 2 次元テーブル (*リレーション*または*フラット ファイル*) のコレクションで表され、共通の列がテーブルを相互に関連付けます。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] を効果的に使用するには、リレーショナル データベースの基本原則を理解している必要があります。  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、リレーショナル データベースのデータ モデルが、開発者のプログラミング言語で表されるオブジェクト モデルに対応付けられています。 アプリケーションが実行されると、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、オブジェクト モデルの統合言語クエリを SQL に変換し、それをデータベースに送信して実行します。 データベースから結果が返されると、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] はそれをプログラミング言語で操作できるオブジェクトに変換し直します。  
  
 Visual Studio を使用する開発者は、通常、オブジェクト リレーショナル デザイナーを使用します。これには、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の機能の多くを実装するためのユーザー インターフェイスが用意されています。  
  
 このリリースの [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] に含まれているドキュメントでは、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] アプリケーションを構築するのに必要な基本的なビルド ブロック、プロセス、および手法について説明します。 特定の問題について Microsoft Docs を検索したり、[LINQ フォーラム](https://social.msdn.microsoft.com/forums/home?forum=linqtosql)に参加して、複雑なトピックについて専門家と検討したりすることもできます。 最後に、「[LINQ to SQL: リレーショナル データ用 .NET 統合言語クエリ](https://docs.microsoft.com/previous-versions/dotnet/articles/bb425822(v=msdn.10))」ホワイト ペーパーには、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] テクノロジの詳細と、Visual Basic および C# のコード例が記載されています。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [はじめに](getting-started.md)  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の簡単な概要と、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] を使用して作業を始める方法を示します。  
  
 [プログラミング ガイド](programming-guide.md)  
 マップ、クエリ、更新、デバッグ、および同様のタスクを行う手順を示します。  
  
 [参照](reference.md)  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] のさまざまな側面に関するリファレンス情報を示します。 SQL-CLR 型マッピング、標準クエリ演算子変換などのトピックが含まれます。  
  
 [サンプル](samples.md)  
 Visual Basic および C# のサンプルへのリンクを示します。  
  
## <a name="related-sections"></a>関連項目  
 [統合言語クエリ (LINQ) - C#](../../../../../csharp/programming-guide/concepts/linq/index.md)\
 C# での LINQ テクノロジの概要を提供します。

 [統合言語クエリ (LINQ) - Visual Basic](../../../../../visual-basic/programming-guide/concepts/linq/index.md)  
 Visual Basic での LINQ テクノロジの概要を提供します。
  
 [LINQ](../../../../../visual-basic/programming-guide/language-features/linq/index.md)  
 Visual Basic ユーザー向けの LINQ テクノロジを提供します。  
  
 [LINQ と ADO.NET](../../linq-and-ado-net.md)  
 ADO.NET ポータルへのリンク。  
  
 [LINQ to SQL チュートリアル](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/bb386295(v=vs.90))  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] のチュートリアルを一覧します。  
  
 [サンプル データベースのダウンロード](downloading-sample-databases.md)  
 ドキュメントで使用されるサンプル データベースをダウンロードする方法について説明します。  
  
 [LinqDataSource Web サーバー コントロールの概要](https://docs.microsoft.com/previous-versions/aspnet/bb547113(v=vs.100))  
 <xref:System.Web.UI.WebControls.LinqDataSource> コントロールにより ASP.NET データ ソース コントロールのアーキテクチャを通じて統合言語クエリ (LINQ) が Web 開発者に公開される方法について説明します。
