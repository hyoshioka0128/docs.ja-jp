---
title: Entity SQL の概要
ms.date: 03/30/2017
ms.assetid: f0bb8120-e709-40a3-ac1e-5520dc47477d
ms.openlocfilehash: b4fe852847d8b1b4bc0b80e3ba8e1f5b4aae9ff7
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84202246"
---
# <a name="entity-sql-overview"></a>Entity SQL の概要
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] は、Entity Framework 内の概念モデルに対するクエリの実行に使用できる SQL に似た言語です。 概念モデルでは、データがエンティティおよびリレーションシップとして表されます。[!INCLUDE[esql](../../../../../../includes/esql-md.md)] を使用すると、SQL を使用したことのあるユーザーが慣れている形式でそれらのエンティティおよびリレーションシップに対してクエリを実行できます。  

 Entity Framework では、ストレージ固有のデータ プロバイダーとの連携により、汎用的な [!INCLUDE[esql](../../../../../../includes/esql-md.md)] がストレージ固有のクエリに変換されます。 EntityClient プロバイダーには、エンティティ モデルに対して [!INCLUDE[esql](../../../../../../includes/esql-md.md)] コマンドを実行し、スカラー結果、結果セット、オブジェクト グラフなど、さまざまなデータ型を返すための手段が用意されています。 <xref:System.Data.EntityClient.EntityCommand> オブジェクトを構築する場合は、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] のクエリ文字列を <xref:System.Data.EntityClient.EntityCommand.CommandText%2A?displayProperty=nameWithType> プロパティに割り当てることで、ストアド プロシージャの名前またはクエリのテキストを指定できます。 EDM に対する <xref:System.Data.EntityClient.EntityDataReader> の実行結果は、<xref:System.Data.EntityClient.EntityCommand> によって公開されます。 <xref:System.Data.EntityClient.EntityDataReader> を返すコマンドを実行するには、<xref:System.Data.EntityClient.EntityCommand.ExecuteReader%2A> を呼び出します。  
  
 EntityClient プロバイダーだけでなく Entity Framework でも、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] を使用して概念モデルに対するクエリを実行し、エンティティ型のインスタンスである厳密に型指定された CLR オブジェクトとしてデータを返すことができます。 詳しくは、「[オブジェクトの使用](../working-with-objects.md)」をご覧ください。  
  
 ここでは、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] の概念について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [Entity SQL と Transact-SQL の相違点](how-entity-sql-differs-from-transact-sql.md)  
  
 [Entity SQL クイック リファレンス](entity-sql-quick-reference.md)  
  
 [型システム](type-system-entity-sql.md)  
  
 [型定義](type-definitions-entity-sql.md)  
  
 [コンストラクター](constructing-types-entity-sql.md)  
  
 [クエリ プランのキャッシュ](query-plan-caching-entity-sql.md)  
  
 [名前空間](namespaces-entity-sql.md)  
  
 [識別子](identifiers-entity-sql.md)  
  
 [パラメーター](parameters-entity-sql.md)  
  
 [変数](variables-entity-sql.md)  
  
 [サポートされていない式](unsupported-expressions-entity-sql.md)  
  
 [リテラル](literals-entity-sql.md)  
  
 [NULL リテラルと型推論](null-literals-and-type-inference-entity-sql.md)  
  
 [入力文字セット](input-character-set-entity-sql.md)  
  
 [クエリ式](query-expressions-entity-sql.md)  
  
 [関数](functions-entity-sql.md)  
  
 [演算子の優先順位](operator-precedence-entity-sql.md)  
  
 [ページング](paging-entity-sql.md)  
  
 [比較セマンティクス](comparison-semantics-entity-sql.md)  
  
 [入れ子になった Entity SQL クエリの作成](composing-nested-entity-sql-queries.md)  
  
 [NULL 値が許容される構造化型](nullable-structured-types-entity-sql.md)  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
- [Entity SQL 言語](entity-sql-language.md)
- [CSDL、SSDL、および MSL 仕様](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)
