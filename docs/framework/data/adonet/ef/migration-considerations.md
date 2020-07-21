---
title: 移行に関する注意事項 (Entity Framework)
ms.date: 03/30/2017
ms.assetid: c85b6fe8-cc32-4642-8f0a-dc0e5a695936
ms.openlocfilehash: 168aec6ef369f446cfac22ee5c4361fa06aaf16d
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74569439"
---
# <a name="migration-considerations-entity-framework"></a>移行に関する注意事項 (Entity Framework)
ADO.NET の Entity Framework には、既存のアプリケーションにとっていくつかの利点があります。 特に重要な利点の 1 つが、概念モデルを使用して、アプリケーションで使用するデータ構造をデータ ソースのスキーマから分離できることです。 これにより、ストレージ モデルやデータ ソース自体の将来の変更が容易になり、その変更を補うための変更をアプリケーションに加える必要がなくなります。 Entity Framework を使用するメリットについて詳しくは、「[Entity Framework の概要](overview.md)」および「[Entity Data Model](../entity-data-model.md)」をご覧ください。  
  
 Entity Framework の利点を活用するには、既存のアプリケーションを Entity Framework に移行することができます。 移行作業の一部はすべてのアプリケーションに共通です。 こうした共通のタスクには、.NET Framework Version 3.5 Service Pack 1 (SP1) 以降を使用するようにアプリケーションをアップグレードするタスクのほか、モデルおよびマッピングの定義や Entity Framework の構成などが含まれます。 アプリケーションを Entity Framework に移行するときに適用される追加の考慮事項があります。 移行するアプリケーションの種類やアプリケーションの特定の機能に依存する注意点もあります。 このトピックでは、既存のアプリケーションをアップグレードする際に最適な方法を選択するために役立つ情報を紹介します。  
  
## <a name="general-migration-considerations"></a>全般的な移行の注意点  
 アプリケーションを Entity Framework に移行するときは、次の点に注意してください。  
  
- .NET Framework バージョン 3.5 SP1 以降を使用しているアプリケーションはどれでも Entity Framework に移行できますが、アプリケーションが使用するデータ ソースのデータ プロバイダーで Entity Framework がサポートされている必要があります。  
  
- データ ソース プロバイダーが Entity Framework をサポートしていても、そのプロバイダーのすべての機能が Entity Framework でサポートされるとは限りません。  
  
- 大規模なアプリケーションや複雑なアプリケーションの場合、アプリケーション全体を一度に Entity Framework に移行する必要はありません。 ただし、Entity Framework を使用しない部分がアプリケーションにある場合、それらの部分については、データ ソースが変更された場合に変更が必要になります。  
  
- Entity Framework では ADO.NET のデータ プロバイダーを使用してデータ ソースにアクセスするため、Entity Framework が使用するデータ プロバイダー接続をアプリケーションの他の部分と共有できます。 (たとえば、Entity Framework は SqlClient プロバイダーを使用して SQL Server データベースにアクセスします)。 詳細については、「 [Entity Framework 用の EntityClient プロバイダー](entityclient-provider-for-the-entity-framework.md)」を参照してください。  
  
## <a name="common-migration-tasks"></a>共通の移行タスク  
 既存アプリケーションの Entity Framework への移行パスは、アプリケーションの種類と既存のデータ アクセス計画の両方に依存します。 ただし、既存のアプリケーションを Entity Framework に移行するときは、以下の作業を常に実行する必要があります。  
  
> [!NOTE]
> Visual Studio 2008 以降で Entity Data Model ツールを使用すると、これらの作業はすべて自動的に実行されます。 詳細については、[Entity Data Model ウィザードを使用する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))」を参照してください。  
  
1. アプリケーションをアップグレードします。  
  
     以前のバージョンの Visual Studio と .NET Framework を使用して作成されたプロジェクトは、Visual Studio 2008 SP1 およびバージョン 3.5 SP1 以降の .NET Framework を使用するように、アップグレードする必要があります。  
  
2. モデルおよびマッピングを定義します。  
  
     モデル ファイルとマッピング ファイルでは、概念モデルのエンティティ、データ ソースの構造 (テーブル、ストアド プロシージャ、ビューなど)、およびエンティティとデータ ソース構造との間のマッピングを定義します。 詳細については、[モデル ファイルとマッピング ファイルを手動で定義する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399785(v=vs.100))」を参照してください。  
  
     ストレージ モデルに定義されている型は、データ ソースのオブジェクトと名前が一致している必要があります。 また、既存のアプリケーションでデータがオブジェクトとして公開されている場合は、概念モデルに定義するエンティティおよびプロパティの名前を既存のデータ クラスおよびプロパティの名前に一致させる必要があります。 詳細については、[カスタム オブジェクトを操作できるようにモデリング ファイルとマッピング ファイルをカスタマイズする](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738625(v=vs.100))」を参照してください。  
  
    > [!NOTE]
    > Entity Data Model デザイナーを使用すると、概念モデルのエンティティの名前を既存のオブジェクトに合わせて変更できます。 詳しくは、「[Entity Data Model デザイナー](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716685(v=vs.100))」をご覧ください。  
  
3. 接続文字列を定義します。  
  
     Entity Framework で概念モデルに対するクエリを実行するときは、特殊な形式の接続文字列を使用します。 この接続文字列は、モデル ファイルとマッピング ファイルに関する情報とデータ ソースへの接続に関する情報をカプセル化したものです。 詳細については、[接続文字列を定義する](how-to-define-the-connection-string.md)」を参照してください。  
  
4. Visual Studio プロジェクトを構成します。  
  
     Entity Framework アセンブリへの参照およびモデル ファイルとマッピング ファイルを、Visual Studio プロジェクトに追加する必要があります。 これらのマッピング ファイルをプロジェクトに追加することで、接続文字列で指定された場所にアプリケーションと共に配置されるようにすることができます。 詳細については、[Entity Framework プロジェクトを手動で構成する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738546(v=vs.100))」を参照してください。  
  
## <a name="considerations-for-applications-with-existing-objects"></a>既存のオブジェクトを含むアプリケーションの注意点  
 .NET Framework 4 以降の Entity Framework では、POCO ("plain old" CLR object、永続化非依存オブジェクトとも呼ばれます) がサポートされています。 ほとんどの場合、既存のオブジェクトを少し変更すれば Entity Framework で使用できます。 詳しくは、「[POCO エンティティの使用](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456853(v=vs.100))」をご覧ください。 アプリケーションを Entity Framework に移行し、Entity Framework ツールによって生成されたデータ クラスを使用することもできます。 詳細については、[Entity Data Model ウィザードを使用する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))」を参照してください。  
  
## <a name="considerations-for-applications-that-use-adonet-providers"></a>ADO.NET プロバイダーを使用するアプリケーションの注意点  
 SqlClient などの ADO.NET プロバイダーを使用すると、データ ソースに対するクエリを実行して表形式のデータを取得できます。 データを ADO.NET の DataSet に読み込むこともできます。 以下は、既存の ADO.NET プロバイダーを使用するアプリケーションをアップグレードする場合の注意点です。  
  
- データ リーダーを使用して表形式のデータを表示している場合  

  EntityClient プロバイダーを使用して [!INCLUDE[esql](../../../../../includes/esql-md.md)] クエリを実行し、返された <xref:System.Data.EntityClient.EntityDataReader> オブジェクトを列挙処理することも考えられます。 この方法を使用するのは、データ リーダーを使用して表形式のデータを表示するアプリケーションで、データをオブジェクトに具体化したり、変更を追跡したり、更新を行ったりするための Entity Framework の機能が不要である場合だけにしてください。 データ ソースを更新する既存のデータ アクセス コードも引き続き使用できますが、<xref:System.Data.EntityClient.EntityConnection.StoreConnection%2A> の <xref:System.Data.EntityClient.EntityConnection> プロパティから既存の接続にアクセスできます。 詳細については、「 [Entity Framework 用の EntityClient プロバイダー](entityclient-provider-for-the-entity-framework.md)」を参照してください。  
  
- DataSet を使用している場合  

  Entity Framework では、メモリへの保持、変更の追跡、データ バインディング、オブジェクトの XML データとしてのシリアル化など、DataSet によって提供される機能の多くが提供されます。 詳しくは、「[オブジェクトの使用](working-with-objects.md)」をご覧ください。  
  
  アプリケーションで必要な DataSet の機能が Entity Framework によって提供されない場合も、LINQ to DataSet を使用して LINQ クエリを活用することができます。 詳細については、「[LINQ to DataSet](../linq-to-dataset.md)」を参照してください。  
  
## <a name="considerations-for-applications-that-bind-data-to-controls"></a>データをコントロールにバインドするアプリケーションの注意点  
 .NET Framework では、データをデータ ソース (DataSet や ASP.NET データ ソース コントロールなど) にカプセル化して、それらのデータ コントロールにユーザー インターフェイス要素をバインドすることができます。 以下は、コントロールを Entity Framework データにバインドする場合の注意点です。  
  
- コントロールへのデータ バインディング  

  概念モデルに対してクエリを実行すると、Entity Framework によって、エンティティ型のインスタンスであるオブジェクトとしてデータが返されます。 それらのオブジェクトは直接コントロールにバインドでき、そのバインドで更新がサポートされます。 したがって、<xref:System.Data.Objects.ObjectContext.SaveChanges%2A> メソッドが呼び出されると、コントロールのデータ (<xref:System.Windows.Forms.DataGridView> の行など) に対する変更が自動的にデータベースに保存されます。  
  
  クエリの結果を列挙して、データ バインドをサポートする <xref:System.Windows.Forms.DataGridView> などのコントロールにデータを表示するアプリケーションは、そのコントロールを <xref:System.Data.Objects.ObjectQuery%601> の結果にバインドするように変更できます。  
  
  詳しくは、「[コントロールへのオブジェクトのバインド](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738469(v=vs.100))」をご覧ください。  
  
- ASP.NET のデータ ソース コントロール。  

  Entity Framework には、ASP.NET Web アプリケーションのデータ バインディングを単純化するために作られたデータ ソース コントロールが含まれています。 詳しくは、「[EntityDataSource Web サーバー コントロールの概要](https://docs.microsoft.com/previous-versions/aspnet/cc488502(v=vs.100))」をご覧ください。  
  
## <a name="other-considerations"></a>その他の注意事項  
 以下は、特定の種類のアプリケーションを Entity Framework に移行する場合の注意点です。  
  
- データ サービスを公開するアプリケーション  

  Windows Communication Foundation (WCF) をベースとする Web サービスやアプリケーションは、XML 要求/応答メッセージ形式を使用して基になるデータ ソースのデータを公開します。 Entity Framework では、バイナリ、XML、または WCF データ コントラクトのシリアル化を使用してエンティティ オブジェクトをシリアル化できます。 バイナリ シリアル化と WCF シリアル化ではオブジェクト グラフの完全なシリアル化がサポートされています。 詳しくは、「[N 層アプリケーションのビルド](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896304(v=vs.100))」をご覧ください。  
  
- XML データを使用するアプリケーション  

  オブジェクトのシリアル化を使用すると、Entity Framework のデータ サービスを作成できます。 XML データを使用するアプリケーション (AJAX ベースのインターネット アプリケーションなど) にデータを提供する  データ サービスを作成できます。 このようなケースでは、WCF Data Services の使用を検討してください。 これらのデータ サービスは Entity Data Model に基づいており、GET、PUT、POST などの標準の Representational State Transfer (REST) HTTP アクションを使用したエンティティ データへの動的アクセスが提供されます。 詳細については、「[WCF Data Services 4.5](../../wcf/index.md)」を参照してください。  
  
  Entity Framework では、ネイティブ XML データ型はサポートされていません。 そのため、XML 列を持つテーブルにエンティティをマップすると、その XML 列に対応するエンティティ プロパティは文字列になります。 このような場合は、オブジェクトを切断して XML としてシリアル化することができます。 詳しくは、「[オブジェクトのシリアル化](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738446(v=vs.100))」をご覧ください。  
  
  アプリケーションで XML データのクエリ機能が必要な場合も、LINQ to XML を使用して LINQ クエリを活用することができます。 詳しくは、「[LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-overview.md)」または「[LINQ to XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md)」をご覧ください。  
  
- 状態を保持するアプリケーション  

  ASP.NET Web アプリケーションでは、Web ページやユーザー セッションの状態を保持しなければならないことがよくあります。 <xref:System.Data.Objects.ObjectContext> インスタンス内のオブジェクトは、クライアントのビュー ステートやサーバーのセッション状態に格納できます。格納したオブジェクトを取得して新しいオブジェクト コンテキストに再アタッチすることもできます。 詳しくは、「[オブジェクトのアタッチとデタッチ](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896271(v=vs.100))」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [配置に関する注意事項](deployment-considerations.md)
- [Entity Framework の用語](terminology.md)
