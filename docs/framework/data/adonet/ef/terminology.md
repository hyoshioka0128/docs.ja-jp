---
title: Entity Framework の用語
ms.date: 03/30/2017
ms.assetid: fa2a1bd1-6118-487b-8673-eebc66b92945
ms.openlocfilehash: 83420660b22c5c23256351f5828d49ecafe5e79f
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81646001"
---
# <a name="entity-framework-terminology"></a>Entity Framework の用語
このトピックでは、Entity Framework のドキュメントでよく使用される用語の定義について説明します。 追加情報を確認できる関連トピックへのリンクも示しています。  
  
|用語|定義|  
|----------|----------------|  
|関連付け|エンティティ型間のリレーションシップの定義。<br /><br /> 詳しくは、「[Association 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#association-element-csdl)」および「[アソシエーション型](../association-type.md)」をご覧ください。|  
|関連付けセット|同じ型のアソシエーションのインスタンスの論理コンテナー。<br /><br /> 詳しくは、「[AssociationSet 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#associationset-element-csdl)」および「[アソシエーション セット](../association-set.md)」をご覧ください。|  
|Code First|Entity Framework 4.1 以降では、Code First の開発を使用してモデルをプログラムで作成することもできます。 Code First の開発に対しては、2 つの異なるシナリオがあります。 どちらの場合でも、開発者は .NET Framework のクラス定義をコーディングしてモデルを定義し、データ注釈または Fluent API を使用してオプションで追加のマッピングまたは構成を指定します。<br /><br /> Code First の開発は Entity Framework 5.0 の一部です。 Entity Framework 5.0 は .NET Framework の一部ではありませんが、.NET Framework 4.5 が基になっています。 Entity Framework 5.0 は、[Entity Framework](https://www.nuget.org/packages/EntityFramework) NuGet パッケージとして使用できます。 詳しくは、「[Entity Framework の過去のリリース](/ef/ef6/what-is-new/past-releases)」をご覧ください。|  
|コマンド ツリー|1 つ以上の式で構成されるすべての Entity Framework クエリの共通プログラム表現。<br /><br /> 詳しくは、「[Entity Framework の概要](overview.md)」をご覧ください。|  
|複合型|概念モデルに定義されている複合プロパティを表す .NET Framework クラス。 複合型により、スカラー プロパティをエンティティ内で整理することができます。 複合オブジェクトは、複合型のインスタンスです。 詳しくは、「[ComplexType 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#complextype-element-csdl)」および「[複合型](../complex-type.md)」をご覧ください。|  
|ComplexType|キー プロパティを持たないエンティティ型の非スカラー プロパティを表すデータ型の仕様。<br /><br /> 詳しくは、「[ComplexType 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#complextype-element-csdl)」および「[複合型](../complex-type.md)」をご覧ください。|  
|概念モデル|Entity Framework のアプリケーションのドメインにおけるエンティティ型、複合型、アソシエーション、エンティティ コンテナー、エンティティ セット、およびアソシエーション セットの抽象的な仕様。 概念モデルは、CSDL で .csdl ファイルに定義されます。<br /><br /> 詳しくは、「[モデリングとマッピング](modeling-and-mapping.md)」をご覧ください。|  
|.csdl ファイル|CSDL で表現された概念モデルを含む XML ファイル。|  
|概念スキーマ定義言語 (CSDL)|概念モデルのエンティティ型、関連付け、エンティティ コンテナー、エンティティ セット、および関連付けセットを定義するための XML ベースの言語。<br /><br /> 詳細については、「 [CSDL Specification](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)」を参照してください。|  
|コンテナー|エンティティ セットとアソシエーション セットの論理的なグループ。<br /><br /> 詳しくは、「[EntityContainer 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#entitycontainer-element-csdl)」および「[エンティティ コンテナー](../entity-container.md)」をご覧ください。|  
|コンカレンシー|複数のユーザーが共有データに同時にアクセスや変更を行うことができるようにする処理。 既定では、Entity Framework にはオプティミスティック コンカレンシー モデルが実装されています。|  
|方向|一部のアソシエーションの非対称の性質を表します。 方向は、スキーマの `FromRole` 要素または `ToRole` 要素の `NavigationProperty` 属性と `ReferentialConstraint` 属性で指定されます。<br /><br /> 詳しくは、「[NavigationProperty 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#navigationproperty-element-csdl)」および「[ナビゲーション プロパティ](../navigation-property.md)」をご覧ください。|  
|一括読み込み|関連オブジェクトの特定のセットを、クエリで明示的に要求されたオブジェクトと共に読み込むプロセス。|  
|.edmx ファイル|概念モデル (CSDL)、ストレージ モデル (SSDL)、および概念モデルとストレージ モデルの間のマッピング (MSL) を含む XML ファイル。 .edmx ファイルは、Entity Data Model ツールによって作成されます。 詳しくは、「[.edmx ファイルの概要](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))」をご覧ください。|  
|end|アソシエーションに参加しているエンティティ。<br /><br /> 詳しくは、「[End 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#end-element-csdl)」および「[アソシエーション End](../association-end.md)」をご覧ください。|  
|entity|データ型を定義する際に基づくアプリケーションのドメインにおける概念。<br /><br /> 詳しくは、「[EntityType 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#entitytype-element-csdl)」および「[エンティティ型](../entity-type.md)」をご覧ください。|  
|EntityClient|`EntityConnection`、`EntityCommand`、`EntityDataReader` などのクラスを含む、ストレージの影響を受けない ADO.NET データ プロバイダー。 [!INCLUDE[esql](../../../../../includes/esql-md.md)] で動作し、`SqlClient` などのストレージ固有の ADO.NET データ プロバイダーに接続します。<br /><br /> 詳細については、「 [Entity Framework 用の EntityClient プロバイダー](entityclient-provider-for-the-entity-framework.md)」を参照してください。|  
|エンティティ コンテナー|指定された名前空間に実装されるエンティティ セットとアソシエーション セットを指定します。<br /><br /> 詳しくは、「[EntityContainer 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#entitycontainer-element-csdl)」および「[エンティティ コンテナー](../entity-container.md)」をご覧ください。|  
|Entity Data Model (EDM)|格納される形式に関係なく、エンティティおよびリレーションシップとしてデータ構造を記述する一連の概念。<br /><br /> 詳細については、「[Entity Data Model](../entity-data-model.md)」を参照してください。|  
|Entity Framework|開発者がデータ ソースの論理スキーマにマップされた概念モデルを使用できるようにすることで、データ指向のソフトウェア アプリケーションの開発をサポートするテクノロジ セット。<br /><br /> 詳しくは、「[Entity Framework の概要](overview.md)」をご覧ください。|  
|エンティティ セット|指定された型とそのサブタイプのエンティティの論理コンテナー。 エンティティ セットは、データベース内のテーブルにマップされます。<br /><br /> 詳しくは、「[EntitySet 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#entityset-element-csdl)」および「[エンティティ セット](../entity-set.md)」をご覧ください。|  
|Entity SQL|エンティティの概念スキーマを直接操作し、継承やリレーションシップなどの概念モデルの概念をサポートする、ストレージの影響を受けない SQL の言語。<br /><br /> 詳しくは、「[Entity SQL 言語](./language-reference/entity-sql-language.md)」をご覧ください。|  
|エンティティ型|概念モデルで定義されているエンティティを表す .NET Framework クラス。 エンティティ型には、スカラー プロパティ、複合プロパティ、およびナビゲーション プロパティが含まれる場合があります。 オブジェクトは、エンティティ型のインスタンスです。 詳しくは、「[オブジェクトの使用](working-with-objects.md)」をご覧ください。|  
|EntityType|キーやプロパティの名前付きセットを含み、概念モデルまたはストレージ モデルの最上位項目を表すデータ型の仕様。<br /><br /> 詳しくは、「[EntityType 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#entitytype-element-csdl)」および「[エンティティ型](../entity-type.md)」をご覧ください。|  
|明示的な読み込み|クエリがオブジェクトを返す場合、関連オブジェクトは同時に読み込まれません。 既定では、関連オブジェクトは、ナビゲーション プロパティの `Load` メソッドを使用して明示的に要求されるまで読み込まれません。|  
|外部キーの関連付け (アソシエーション)|外部キー プロパティで管理されるエンティティ間のアソシエーション。|  
|依存リレーションシップ|プリンシパル エンティティの主キーが依存エンティティの主キーの一部であるリレーションシップ。 このようなリレーションシップでは、プリンシパル エンティティが存在しないと、依存エンティティは存在できません。|  
|独立した関連付け (アソシエーション)|独立オブジェクトによって表され、追跡されるエンティティ間のアソシエーション。|  
|key|エンティティ型の一意のインスタンスを識別するために使用されるプロパティまたはプロパティ セットを指定するエンティティ型の属性。 オブジェクト レイヤーでは、<xref:System.Data.EntityKey> クラスで表現されます。<br /><br /> 詳しくは、「[Key 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#key-element-csdl)」および「[エンティティ キー](../entity-key.md)」をご覧ください。|  
|遅延読み込み|クエリがオブジェクトを返す場合、関連オブジェクトは同時に読み込まれません。 代わりに、ナビゲーション プロパティへのアクセス時に自動的に読み込まれます。|  
|LINQ to Entities|走査、フィルター、および射影操作を Visual C# と Visual Basic で直接的な宣言型の方法で表現できるようにする一連のクエリ演算子を定義するクエリ構文。<br /><br /> 詳しくは、「[LINQ to Entities](./language-reference/linq-to-entities.md)」をご覧ください。|  
|マップ|概念モデルの項目とストレージ モデルの項目の対応付けの指定。<br /><br /> 詳しくは、「[MSL 仕様](/ef/ef6/modeling/designer/advanced/edmx/msl-spec)」をご覧ください。|  
|.msl ファイル|MSL で表現された概念モデルとストレージ モデルの間のマッピングを含む XML ファイル。|  
|マッピング仕様言語 (MSL)|概念モデルで定義された項目をストレージ モデルの項目に対応付ける XML ベースの言語。<br /><br /> 詳しくは、「[MSL 仕様](/ef/ef6/modeling/designer/advanced/edmx/msl-spec)」をご覧ください。|  
|変更関数|データ ソースでデータを挿入、更新、および削除するために使用されるストアド プロシージャ。 この関数は、Entity Framework で生成されるコマンドの代わりに使用されます。 変更関数は、ストレージ モデルの `Function` 要素で定義されます。 [ModificationFunctionMapping](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716778(v=vs.100)) 要素によって、概念モデルで定義されているエンティティに対する挿入、更新、削除などの操作にこの変更関数がマップされます。|  
|多重度|アソシエーションによって定義されているリレーションシップの両側に存在できるエンティティの数。 カーディナリティとも呼ばれます。<br /><br /> 詳しくは、「[End 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#end-element-csdl)」および「[アソシエーション End](../association-end.md)」をご覧ください。|  
|Multiple-Entity-Sets-per-Type|1 つのエンティティ型を複数のエンティティ セットで定義できる機能。<br /><br /> 詳しくは、「[EntitySet 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#entityset-element-csdl)」および「[方法: Multiple-Entity-Sets-per-Type でモデルを定義する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738537(v=vs.100))」をご覧ください。|  
|ナビゲーション プロパティ|アソシエーションによって定義されている別のエンティティ型とのリレーションシップを表すエンティティ型のプロパティ。 ナビゲーション プロパティは、アソシエーションのもう一方の End での複数要素の接続性に応じて、関連オブジェクトを <xref:System.Data.Objects.DataClasses.EntityCollection%601> または <xref:System.Data.Objects.DataClasses.EntityReference%601> として返すために使用されます。<br /><br /> 詳しくは、「[NavigationProperty 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#navigationproperty-element-csdl)」および「[ナビゲーション プロパティ](../navigation-property.md)」をご覧ください。|  
|クエリ パス|オブジェクト クエリの実行時に返す関連オブジェクトを指定するパスの文字列表記。 クエリ パスは、<xref:System.Data.Objects.ObjectQuery%601.Include%2A> に対して <xref:System.Data.Objects.ObjectQuery%601> メソッドを呼び出すことによって定義されます。<br /><br /> 詳しくは、「[関連オブジェクトの読み込み](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896272(v=vs.100))」をご覧ください。|  
|オブジェクト コンテキスト|概念モデルで定義したエンティティ コンテナーを表します。 基になるデータ ソースへの接続を含み、変更の追跡や ID 解決などのサービスを提供します。 オブジェクト コンテキストは、<xref:System.Data.Objects.ObjectContext> クラスまたは `DbContext` クラスのインスタンスで表されます。<br /><br /> `DbContext` は Entity Framework 5.0 の一部です。 Entity Framework 5.0 は .NET Framework の一部ではありませんが、.NET Framework 4.5 が基になっています。 Entity Framework 5.0 は、[Entity Framework](https://www.nuget.org/packages/EntityFramework) NuGet パッケージとして使用できます。 詳しくは、「[Entity Framework の過去のリリース](/ef/ef6/what-is-new/past-releases)」をご覧ください。|  
|オブジェクト レイヤー|Entity Framework によって使用されるエンティティ型およびオブジェクト コンテキストの定義。|  
|オブジェクト クエリ|データをオブジェクトとして返す概念モデルに対してオブジェクト コンテキスト内で実行されるクエリ。<br /><br /> 詳しくは、「[オブジェクト クエリ](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896241(v=vs.100))」をご覧ください。|  
|オブジェクト リレーショナル マッピング|リレーショナル データベースのデータをオブジェクト指向のソフトウェア アプリケーションで使用できるデータ型に変換する手法。<br /><br /> Entity Framework では、ストレージ モデルで定義されたリレーショナル データを概念モデルで定義されたデータ型にマップすることにより、オブジェクト リレーショナル マッピング サービスが提供されます。<br /><br /> 詳しくは、「[モデリングとマッピング](modeling-and-mapping.md)」をご覧ください。|  
|オブジェクト サービス|アプリケーション コードから .NET Framework オブジェクトのようなエンティティを操作できるようにする、Entity Framework によって提供されるサービス。|  
|永続化非依存オブジェクト|データ ストレージに関連するロジックが含まれていないオブジェクト。 POCO エンティティとも呼ばれます。|  
|POCO|Plain Old CLR Object の略。 別のクラスから継承しないオブジェクト、またはインターフェイスを実装しないオブジェクト。|  
|POCO エンティティ|Entity Framework の、<xref:System.Data.Objects.DataClasses.EntityObject> または <xref:System.Data.Objects.DataClasses.ComplexObject> を継承せず、Entity Framework インターフェイスを実装していないエンティティ。 多くの場合、POCO エンティティは、Entity Framework アプリケーションで使用される既存のドメイン オブジェクトです。 このようなエンティティは、永続化非依存性をサポートしています。 詳しくは、「[POCO エンティティの使用](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456853(v=vs.100))」をご覧ください。|  
|プロキシ オブジェクト|POCO クラスから派生し、Entity Framework によって生成されたオブジェクト。変更追跡と遅延読み込みをサポートするために使用されます。 詳しくは、「[POCO プロキシの作成要件](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd468057(v=vs.100))」をご覧ください。|  
|参照制約|エンティティが他のエンティティと依存関係にあることを示す、概念モデルで定義された制約。 この制約は、依存エンティティのインスタンスが対応する主要エンティティのインスタンスなしでは存在できないことを意味します。<br /><br /> 詳しくは、「[ReferentialConstraint 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#referentialconstraint-element-csdl)」および「[参照整合性制約](../referential-integrity-constraint.md)」をご覧ください。|  
|リレーションシップ|エンティティ間の論理的な関係。|  
|ロール|リレーションシップのセマンティクスを明確にするためにアソシエーションの両方の `End` に付けられた名前。<br /><br /> 詳しくは、「[End 要素 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#end-element-csdl)」および「[アソシエーション End](../association-end.md)」をご覧ください。|  
|スカラー プロパティ|ストレージ モデルの単一のフィールドにマップされるエンティティのプロパティ。|  
|自己追跡エンティティ|スカラー プロパティ、複合プロパティ、およびナビゲーション プロパティの変更を報告できる、テキスト テンプレート変換ツールキット (T4) から構築されるエンティティ。|  
|単純型|概念モデルでプロパティを定義するために使用されるプリミティブ型。<br /><br /> 詳しくは、「[概念モデルの型 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#conceptual-model-types-csdl)」および「[Entity Data Model: プリミティブ データ型](../entity-data-model-primitive-data-types.md)」をご覧ください。|  
|分割されたエンティティ|ストレージ モデルの 2 つの別個の型にマップされる 1 つのエンティティ型。<br /><br /> 詳細については、[単一のエンティティが 2 つのテーブルにマップされたモデルを定義する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896233(v=vs.100))」をご覧ください。|  
|ストレージ モデル|リレーショナル データベースなど、サポートされているデータ ソースのデータの論理モデルの定義。 ストレージ モデルは、SSDL で .ssdl ファイルに定義されます。<br /><br /> 詳しくは、「[モデリングとマッピング](modeling-and-mapping.md)」および「[SSDL 仕様](/ef/ef6/modeling/designer/advanced/edmx/ssdl-spec)」をご覧ください。|  
|.ssdl ファイル|SSDL で表現されたストレージ モデルを含む XML ファイル。|  
|ストア スキーマ定義言語 (SSDL)|一般的にデータベース スキーマに対応するストレージ モデルのエンティティ型、アソシエーション、エンティティ コンテナー、エンティティ セット、およびアソシエーション セットの定義に使用される XML ベースの言語。<br /><br /> 詳しくは、「[SSDL 仕様](/ef/ef6/modeling/designer/advanced/edmx/ssdl-spec)」をご覧ください。|  
|table-per-hierarchy|あらゆる型の属性を 1 つのテーブル内の階層構造に含める、データベースにおける型階層のモデリング手法。|  
|table-per-type|一対一リレーションシップを持った複数のテーブルを使用して各種の型をモデリングする、データベースにおける型階層のモデリング手法。|  
  
## <a name="see-also"></a>関連項目

- [ADO.NET Entity Framework](index.md)
- [Entity Framework の概要](overview.md)
- [はじめに](getting-started.md)
- [Entity Framework のリソース](resources.md)
