---
title: 型指定されたデータセット
ms.date: 03/30/2017
ms.assetid: 033d2548-cf24-4c05-8179-67d8b009c048
ms.openlocfilehash: 7c8111e0e62a57b6745a5ea0387fc65a05839df8
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785841"
---
# <a name="typed-datasets"></a>型指定されたデータセット
厳密に型指定されていない変数を使用した値への遅延バインディング アクセスに加えて、<xref:System.Data.DataSet> には、厳密に型指定された変数を使用したデータへのアクセスも用意されています。 **DataSet** の一部であるテーブルと列は、ユーザーが認識しやすい名前と厳密に型指定された変数を使用してアクセスできます。  
  
 型指定された **DataSet** とは、**DataSet** から派生するクラスのことです。 したがって、**DataSet** のすべてのメソッド、イベント、プロパティを継承します。 さらに、型指定された **DataSet** には、厳密に型指定されたメソッド、イベント、およびプロパティが用意されています。 つまり、コレクションベースのメソッドを使用せずに名前でテーブルおよび列にアクセスできます。 コードが読みやすく変更されただけでなく、型指定された **DataSet** を使用して、入力するとおりにラインを Visual Studio .NET コード エディターに自動挿入できます。  
  
 さらに、厳密に型指定された **DataSet** を使用してコンパイル時に正しい型で値にアクセスできます。 厳密に型指定された **DataSet** を使用すると、型の不一致が実行時ではなく、コードのコンパイル時にキャッチされます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [厳密に型指定された DataSet の生成](generating-strongly-typed-datasets.md)  
 厳密に型指定された **DataSet** の作成および使用方法について説明します。  
  
 [型指定された DataSet の注釈](annotating-typed-datasets.md)  
 基になるスキーマを変更せずに **DataSet** の要素にフレンドリ名を付けるために、厳密に型指定された **DataSet** の生成に使用する XML スキーマ定義言語 (XSD) スキーマに注釈を付ける方法について説明します。  
  
## <a name="see-also"></a>関連項目

- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
