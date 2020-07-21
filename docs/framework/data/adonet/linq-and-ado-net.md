---
title: LINQ と ADO.NET
description: ADO.NET で統合言語クエリ (LINQ) を使用することにより、別のクエリ言語を使用せずに、アプリケーション コード内でセット ベースのクエリを作成する方法について説明します。
titleSuffix: ''
ms.date: 03/30/2017
ms.assetid: bf0c8f93-3ff7-49f3-8aed-f2b7ac938dec
ms.openlocfilehash: a663d36f1e07c53d20e22d051e38123bd8873f06
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286754"
---
# <a name="linq-and-adonet"></a>LINQ と ADO.NET

今日、ビジネス アプリケーション開発者の多くは、2 つ (またはそれ以上) のプログラミング言語を使ってアプリケーションを開発しています。ビジネス ロジックやプレゼンテーション層には高級言語 (Visual C# や Visual Basic など) が、データベースとの対話にはクエリ言語 (Transact-SQL など) が使用されています。 開発者は実質的に複数の言語に精通していることが要求され、開発環境における言語の不整合が生じる原因にもなっています。 たとえば、データ アクセス API を使用してデータベースを照会するアプリケーションでは、クエリは文字列リテラルとして引用符で囲んで指定する必要があります。 コンパイラはこのクエリ文字列を認識できないため、エラー (無効な構文、参照されている列または行が実際に存在するかどうかなど) のチェック機構が働きません。 クエリ パラメーターの型チェックや `IntelliSense` のサポートもありません。  
  
 LINQ (統合言語クエリ) により、開発者はアプリケーション コード内でプログラミング言語とクエリ言語を使い分けることなく、セット ベースのクエリを作成できます。 インメモリのデータ構造、XML ドキュメント、SQL データベース、<xref:System.Data.DataSet> オブジェクトなど、列挙可能な各種データ ソース (つまり、<xref:System.Collections.IEnumerable> インターフェイスが実装されているデータ ソース) に対する LINQ クエリを作成できます。 実装方法には違いがありますが、こうした列挙可能なデータ ソースはすべて同じ構文および言語構造を公開しています。 クエリはプログラミング言語のみで作成できるため、コンパイラによる認識も検証もできない文字列リテラルとしてクエリ言語を記述する必要はありません。 クエリをプログラミング言語に統合することにより、コンパイル時の型チェックや構文チェック、`IntelliSense` の使用などが可能となるため、Visual Studio プログラマは生産性を高めることができます。 クエリのデバッグやエラーの修正に伴う手間は、これらの機能によって軽減されます。  
  
 SQL テーブルのデータをメモリ内のオブジェクトに転送することは、面倒であるだけでなく間違いの元にもなります。 LINQ to DataSet と [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] によって実装されている LINQ プロバイダーでは、ソース データが <xref:System.Collections.IEnumerable> ベースのオブジェクト コレクションに変換されます。 プログラマからは、クエリの実行時も更新時も常にデータが <xref:System.Collections.IEnumerable> コレクションとして見えます。 これらのコレクションに対するクエリを記述する際には、`IntelliSense` の機能を完全に利用できます。  
  
 ADO.NET 統合言語クエリ (LINQ) には、3 つのテクノロジがあります。LINQ to DataSet、[!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)]、LINQ to Entities です。 LINQ to DataSet により、<xref:System.Data.DataSet> に対する高度で最適化されたクエリの実行が提供され、[!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] により、SQL Server データベース スキーマに対して直接クエリを実行できます。LINQ to Entities では、Entity Data Model のクエリを実行できます。  
  
 次の図は、ADO.NET LINQ テクノロジが、高級プログラミング言語および LINQ 対応のデータ ソースとどのように関係しているかを簡単に表したものです。  
  
 ![LINQ to ADO.NET の概要](./media/dpue-linqtoadonetoverview-bpuedev11.gif "DPUE_LinqToAdoNetOverview_bpuedev11")  
  
 LINQ について詳しくは、「[統合言語クエリ (LINQ)](../../../csharp/programming-guide/concepts/linq/index.md)」をご覧ください。
  
 以降のセクションでは、LINQ to DataSet、[!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)]、LINQ to Entities について詳しく説明します。  
  
## <a name="linq-to-dataset"></a>LINQ to DataSet  
 <xref:System.Data.DataSet> は、ADO.NET の基礎である非接続型プログラミング モデルの重要な要素であり、幅広く使用されています。 LINQ to DataSet により、開発者は、他の多くのデータ ソースで利用できる共通のクエリ作成メカニズムを使用しながら、より高度なクエリ機能を <xref:System.Data.DataSet> に組み込むことができます。 詳細については、「[LINQ to DataSet](linq-to-dataset.md)」を参照してください。  
  
## <a name="linq-to-sql"></a>LINQ to SQL  
 [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] は、概念モデルへのマッピングを必要としない開発者にとって有用なツールです。 [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] を使用することにより、LINQ プログラミング モデルを既存のデータベース スキーマ上で直接利用できるようになります。 開発者は、[!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] を使用して、データを表す .NET Framework クラスを生成できます。 こうして生成されたクラスは、概念データ モデルではなく、直接データベースのテーブル、ビュー、ストアド プロシージャ、およびユーザー定義関数にマッピングされます。  
  
 [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] では、開発者が、XML などのデータ ソースに加え、インメモリ コレクションや <xref:System.Data.DataSet> と同じ LINQ プログラミング パターンを使用して、ストレージ スキーマに対して直接コードを記述できます。 詳細については、「[LINQ to SQL](./sql/linq/index.md)」を参照してください。  
  
## <a name="linq-to-entities"></a>LINQ to Entities  
 現在、多くのアプリケーションが、リレーショナル データベースを基にして作成されています。 ある時点で、これらのアプリケーションにはリレーショナル形式で表されるデータと対話する必要が生じます。 データベース スキーマはアプリケーションの構築に理想的であるとは限らず、アプリケーションの概念モデルはデータベースの論理モデルと同じではありません。 Entity Data Model は、アプリケーションがデータをオブジェクトとして操作するために特定のドメインのデータをモデル化するときに使用できる概念データ モデルです。 詳しくは、「[ADO.NET Entity Framework](./ef/index.md)」をご覧ください。  
  
 Entity Data Model では、リレーショナル データが .NET 環境にオブジェクトとして公開されます。 これにより、LINQ の利用に最適なオブジェクト レイヤーが実現されます。開発者は、ビジネス ロジックの構築に使用する言語で、データベースを照会するクエリを作成できます。 この機能は、LINQ to Entities と呼ばれます。 詳しくは、「[LINQ to Entities](./ef/language-reference/linq-to-entities.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [LINQ to DataSet](linq-to-dataset.md)
- [LINQ to SQL](./sql/linq/index.md)
- [LINQ to Entities](./ef/language-reference/linq-to-entities.md)
- [統合言語クエリ (LINQ)](../../../csharp/programming-guide/concepts/linq/index.md)
- [ADO.NET の概要](ado-net-overview.md)
