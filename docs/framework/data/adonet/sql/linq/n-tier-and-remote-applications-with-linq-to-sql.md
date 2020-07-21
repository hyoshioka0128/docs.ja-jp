---
title: LINQ to SQL を使用する n 層アプリケーションとリモート アプリケーション
ms.date: 03/30/2017
ms.assetid: 854a1cdd-53cb-45f5-83ca-63962a9b3598
ms.openlocfilehash: 6758ae23c25d8e7a4255d0a784cccd1eb404bfe7
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174304"
---
# <a name="n-tier-and-remote-applications-with-linq-to-sql"></a>LINQ to SQL を使用する n 層アプリケーションとリモート アプリケーション
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] を使用する n 層つまり多層アプリケーションを作成することができます。 通常、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] のデータ コンテキスト、エンティティ クラス、およびクエリ構築ロジックは、中間層にデータ アクセス層 (DAL) として置かれます。 ビジネス ロジックと非永続的データは、エンティティとデータ コンテキストの部分クラスと部分メソッドの中に完全に実装できます。または、別個のクラスに実装することもできます。

 クライアントまたはプレゼンテーション層は、中間層のリモート インターフェイス上のメソッドを呼び出し、その層の DAL は、<xref:System.Data.Linq.DataContext> メソッドにマップされるクエリまたはストアド プロシージャを実行します。 中間層は、通常、エンティティまたはプロキシ オブジェクトの XML 表現としてデータをクライアントに返します。

 中間層では、データ コンテキストによってエンティティが作成され、データ コンテキストはエンティティの状態を追跡し、データベースからの遅延読み込み、および変更内容のデータベースへの送信を管理します。 これらのエンティティは、`DataContext` にいわばアタッチされます。 ただし、シリアル化によってエンティティが別の層に送られた後は、エンティティがデタッチされます。つまり、その状態が `DataContext` によって追跡されなくなります。 更新のためにクライアントによって戻されるエンティティは、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] が変更内容をデータベースに送信する前に、データ コンテキストに再びアタッチされる必要があります。 オプティミスティック コンカレンシー チェックのために元の値またはタイムスタンプが必要とされる場合、クライアントはこれらを中間層に戻す必要があります。

 ASP.NET アプリケーションでは、このような複雑な操作の大部分が <xref:System.Web.UI.WebControls.LinqDataSource> によって管理されます。 詳細については、「[LinqDataSource Web サーバー コントロールの概要](https://docs.microsoft.com/previous-versions/aspnet/bb547113(v=vs.100))」を参照してください。

## <a name="additional-resources"></a>その他のリソース
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] を使用する n 層アプリケーションの実装方法について、詳しくは以下のトピックを参照してください。

- [ASP.NET での LINQ to SQL N 層](linq-to-sql-n-tier-with-aspnet.md)

- [Web サービスを使用した LINQ to SQL N 層](linq-to-sql-n-tier-with-web-services.md)

- [N 層ビジネス ロジックの実装](implementing-business-logic-linq-to-sql.md)

- [N 層アプリケーションでのデータ取得および CUD 操作 (LINQ to SQL)](data-retrieval-and-cud-operations-in-n-tier-applications.md)

 ADO.NET DataSet を使用する n 層アプリケーションについて詳しくは、「[n 層アプリケーションでのデータセットの操作](/visualstudio/data-tools/work-with-datasets-in-n-tier-applications)」をご覧ください。

## <a name="see-also"></a>関連項目

- [背景情報](background-information.md)
