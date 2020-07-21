---
title: DataView
ms.date: 03/30/2017
ms.assetid: 0fe5dfa2-c1cd-435f-90b6-b4dd2e3ef34b
ms.openlocfilehash: 1b202af052c05ed9dc671fa20c9c366f280ec5c7
ms.sourcegitcommit: 559259da2738a7b33a46c0130e51d336091c2097
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72774166"
---
# <a name="dataviews"></a>DataView
<xref:System.Data.DataView> では、<xref:System.Data.DataTable> に格納されているデータのさまざまなビューを作成できます。この機能は、データ連結アプリケーションで頻繁に使用されます。 **DataView** を使用すると、さまざまな並べ替え順序を使用してテーブルのデータを公開したり、行の状態やフィルター式に基づいてデータをフィルター処理したりできます。

 **DataView** では、基になる **DataTable** のデータの動的ビューが作成されます。ビューの内容、順序、メンバーシップには、変更が反映されます。 これは、**DataTable** の **Select** メソッドとは異なります。このメソッドでは、特定のフィルターまたは並べ替え順序ごとにテーブルから <xref:System.Data.DataRow> の配列が戻されます。戻される配列の内容には、基になるテーブルの変更内容が反映されていますが、メンバーシップと順序は静的です。 **DataView** は動的機能を備えているため、データ連結アプリケーションにとって理想的なオブジェクトです。

 **DataView** は、1 つのデータ セットの動的ビューです。データベースのビューと同様に、この動的ビューには、さまざまな並べ替え順序やフィルター処理条件を適用できます。 ただし、データベース ビューとは異なり、**DataView** は、テーブルとしては処理できず、結合テーブルのビューも作成できません。 また、ソース テーブルに存在する列を除外したり、ソース テーブルに存在しない列 (計算列など) を追加したりすることもできません。

 **DataSet** のすべてのテーブルのビュー設定を管理するには、<xref:System.Data.DataView.DataViewManager%2A> を使用します。 **DataViewManager** を使用すると、各テーブルの既定のビュー設定を簡単に管理できます。 **DataSet** の複数のテーブルにコントロールをバインドするときは、**DataViewManager** にバインドするのが最善の方法です。

## <a name="in-this-section"></a>このセクションの内容
 「[DataView の作成](creating-a-dataview.md)」では、**DataTable** の **DataView** の作成方法について説明します。

 「[データの並べ替えとフィルター処理](sorting-and-filtering-data.md)」では、特定のフィルター条件を満たすデータ行のサブセットを返すか、または特定の並べ替え順序でデータを返すように、**DataView** のプロパティを設定する方法について説明します。

 「[DataRow および DataRowView](datarows-and-datarowviews.md)」では、**DataView** によって公開されるデータへのアクセス方法について説明します。

 「[行の検索](finding-rows.md)」では、**DataView** での特定の行の検索方法について説明します。

 「[ChildView とリレーション](childviews-and-relations.md)」では、**DataView** を使用して親子のリレーションシップからデータ ビューを作成する方法について説明します。

 「[DataView の変更](modifying-dataviews.md)」では、**DataView** を使用して、基になる **DataTable** のデータを変更する方法について説明します。また、更新の有効化と無効化についても説明します。

 「[DataView イベントの処理](handling-dataview-events.md)」では、**DataView** の内容または順序が更新されるときに、**ListChanged** イベントを使用して通知を受信する方法について説明します。

 「[DataViews の管理](managing-dataviews.md)」では、**DataViewManager** を使用して **DataSet** の各テーブルの **DataView** 設定を管理する方法について説明します。

## <a name="related-sections"></a>関連項目
 [ASP.NET Web アプリケーション](https://docs.microsoft.com/previous-versions/655cec97(v=vs.100))に関する記事では、ASP.NET アプリケーション、Web Forms、および Web サービスを作成する場合の概要と詳細なステップごとの手順を示します。

 [Windows アプリケーション](https://docs.microsoft.com/previous-versions/ms184421(v=vs.100))に関する記事では、Windows フォームおよびコンソール アプリケーションの操作に関する詳細情報を提供します。

 「[DataSet、DataTable、および DataView](index.md)」では、**DataSet** オブジェクトと、それを使用してアプリケーション データを管理する方法について説明します。

 「[DataTable](datatables.md)」では、**DataTable** オブジェクトについて説明し、アプリケーション データを単独でまたは **DataSet** の一部として管理するために DataTable オブジェクトを使用する方法も示します。

 「[ADO.NET](../index.md)」では、ADO.NET のアーキテクチャとコンポーネントについて説明し、ADO.NET を使用して既存のデータ ソースにアクセスしたり、アプリケーション データを管理する方法について説明します。

## <a name="see-also"></a>関連項目

- [ADO.NET の概要](../ado-net-overview.md)
