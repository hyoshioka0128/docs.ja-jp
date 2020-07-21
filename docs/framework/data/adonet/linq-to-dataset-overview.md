---
title: LINQ to DataSet の概要
ms.date: 03/30/2017
ms.assetid: dc20a8fb-03f6-4b68-9c2b-7f7299e3070b
ms.openlocfilehash: 20d9be052ba2567c16718b4b1c1019427c9b5df1
ms.sourcegitcommit: 7bc6887ab658550baa78f1520ea735838249345e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75634821"
---
# <a name="linq-to-dataset-overview"></a>LINQ to DataSet の概要
<xref:System.Data.DataSet> は、ADO.NET のコンポーネントの中でもよく使用されるものの 1 つです。 ADO.NET の基になっている非接続型プログラミング モデルの重要な要素であり、さまざまなデータ ソースからのデータを明示的にキャッシュできます。 プレゼンテーション層では、<xref:System.Data.DataSet> とデータ バインディングの GUI コントロールとが密接に連携します。 中間層では、リレーショナル形式のデータを維持するキャッシュとして機能し、単純で高速なクエリと、階層的なナビゲーション サービスを提供します。 データベースに対する要求の数を減らすためによく使用される手法は、中間層でのキャッシュに <xref:System.Data.DataSet> を使用することです。 たとえば、データ ドリブンの ASP.NET Web アプリケーションについて考えます。 ほとんど変更されないアプリケーション データがかなりの割合で存在し、しかも、複数のセッションまたは複数のユーザー間で共通して使用されているケースがよくあります。 このデータを Web サーバー上のメモリに維持しておくことで、データベースに対する要求数を減らし、高速な対話処理をユーザーに提供できます。 <xref:System.Data.DataSet> のもう 1 つの便利な特長は、アプリケーションで、1 つまたは複数のデータ ソースから取得したデータのサブセットを、アプリケーション空間に取り込むことができることです。 アプリケーションは、そのデータをリレーショナル形式を維持したままインメモリで操作できます。  
  
 こうした突出した特長がある反面、<xref:System.Data.DataSet> のクエリ機能には制限があります。 <xref:System.Data.DataTable.Select%2A> メソッドでデータのフィルター処理や並べ替えを行ったり、<xref:System.Data.DataRow.GetChildRows%2A> メソッドや <xref:System.Data.DataRow.GetParentRow%2A> メソッドを使って階層のナビゲーションを行うことはできます。 しかし、さらに複雑な処理を行うには、開発者が独自にクエリを作成する必要があります。 その結果、アプリケーションで期待したパフォーマンスが得られなかったり、メンテナンスが難しくなったりする可能性があります。  
  
 LINQ to DataSet を使うと、<xref:System.Data.DataSet> オブジェクトにキャッシュされたデータに対するクエリを、いっそう簡単かつ高速に実行できるようになります。 これらのクエリはアプリケーション コードに文字列リテラルとして記述するのではなく、プログラミング言語そのもので表現できます。 つまり、開発者はクエリ言語を個別に習得する必要はありません。 さらに、LINQ to DataSet を使用すると、Visual Studio の IDE で LINQ に対するコンパイル時の構文チェック、静的な型指定、IntelliSense などの機能を利用できるため、Visual Studio 開発者の生産性が向上します。 また、LINQ to DataSet を使用すると、1 つまたは複数のデータ ソースから取得して統合したデータを照会することもできます。 これにより、データの表現方法や扱いに柔軟性が要求されるさまざまなシナリオが実現します。 特に、汎用のレポート作成、分析、ビジネス インテリジェンスを行うアプリケーションでは、この手法を用いたデータ操作が欠かせません。  
  
## <a name="querying-datasets-using-linq-to-dataset"></a>LINQ to DataSet を使った DataSet のクエリ  
 LINQ to DataSet を使用して <xref:System.Data.DataSet> オブジェクトのクエリを行うには、あらかじめ <xref:System.Data.DataSet> を設定しておく必要があります。 <xref:System.Data.DataSet> にデータを読み込むには、<xref:System.Data.Common.DataAdapter> クラスまたは [LINQ to SQL](./sql/linq/index.md) を使用するなど、複数の方法があります。 <xref:System.Data.DataSet> オブジェクトにデータを読み込んだ後は、そのクエリを始めることができます。 LINQ to DataSet を使用したクエリの作成は、他の LINQ (統合言語クエリ) 対応データ ソースに対して LINQ を使用する場合と似ています。 LINQ のクエリは、<xref:System.Data.DataSet> の単一のテーブルに対して、または <xref:System.Linq.Enumerable.Join%2A> や <xref:System.Linq.Enumerable.GroupJoin%2A> などの標準クエリ演算子を使用して複数のテーブルに対して、実行することができます。  
  
 LINQ のクエリでは、<xref:System.Data.DataSet> の型指定されたオブジェクトと、型指定されていないオブジェクトの両方がサポートされています。 アプリケーションのデザイン時に <xref:System.Data.DataSet> のスキーマがわかっている場合は、型指定された <xref:System.Data.DataSet> を使用することをお勧めします。 型指定された <xref:System.Data.DataSet> のテーブルおよび行は、列ごとに型指定されたメンバーを持ちます。これにより、クエリが簡素化され、読みやすくなります。  
  
 System.Core.dll で実装されている標準クエリ演算子に加え、LINQ to DataSet では、一連の <xref:System.Data.DataRow> オブジェクトに対して容易にクエリを実行することのできる複数の <xref:System.Data.DataSet> 固有の拡張機能が追加されています。 これらの <xref:System.Data.DataSet> 固有の拡張機能には、<xref:System.Data.DataRow> の列値にアクセスするためのメソッドのほか、一連の行を比較するための演算子があります。  
  
## <a name="n-tier-applications-and-linq-to-dataset"></a>n 層アプリケーションと LINQ to DataSet  
 n 層データ アプリケーションは、複数の論理レイヤー (層) に分けられた、データ処理を中心とするアプリケーションです。 一般に、n 層アプリケーションには、プレゼンテーション層、中間層、およびデータ層が含まれます。 アプリケーション コンポーネントを別個の層に分離すると、アプリケーションの保守容易性とスケーラビリティが向上します。 n 層データ アプリケーションについて詳しくは、「[n 層アプリケーションでのデータセットの操作](/visualstudio/data-tools/work-with-datasets-in-n-tier-applications)」をご覧ください。  
  
 n 層アプリケーションでは、Web アプリケーションの情報をキャッシュするために <xref:System.Data.DataSet> が中間層で使用されます。 拡張メソッドによって実装される LINQ to DataSet のクエリ機能により、既存の ADO.NET 2.0 の <xref:System.Data.DataSet> が強化されています。  
  
## <a name="see-also"></a>関連項目

- [DataSet のクエリ](querying-datasets-linq-to-dataset.md)
- [統合言語クエリ (LINQ) - C#](../../../csharp/programming-guide/concepts/linq/index.md)
- [統合言語クエリ (LINQ) - Visual Basic](../../../visual-basic/programming-guide/concepts/linq/index.md)
- [LINQ to SQL](./sql/linq/index.md)
