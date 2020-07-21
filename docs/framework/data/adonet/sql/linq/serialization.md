---
title: Serialization2
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a15ae411-8dc2-4ca3-84d2-01c9d5f1972a
ms.openlocfilehash: bf303f9a79fbcab85d33fcb3ebb132d1d3e2041d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781110"
---
# <a name="serialization"></a>シリアル化
このトピックでは、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] のシリアル化機能について説明します。 デザイン時のコード生成でシリアル化を追加する方法と、実行時の [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] のクラスのシリアル化の動作について説明します。  
  
 デザイン時には、次のいずれかの方法でシリアル化のコードを追加できます。  
  
- オブジェクト リレーショナル デザイナーで、**Serialization Mode** プロパティを **Unidirectional** に変更します。  
  
- SQLMetal コマンド ラインに **/serialization** オプションを追加します。 詳しくは、「[SqlMetal.exe (コード生成ツール)](../../../../tools/sqlmetal-exe-code-generation-tool.md)」をご覧ください。  
  
## <a name="overview"></a>概要  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] が生成するコードには、遅延読み込み機能が既定で備わっています。 遅延読み込みは、中間層でデータを必要に応じて透過的に読み込むうえでは非常に便利です。 しかし、シリアル化のときには問題です。遅延読み込みが意図されているかどうかに関係なく、シリアライザーによって遅延読み込みが発生するためです。 具体的には、オブジェクトがシリアル化されるときには、遅延読み込みされるすべての外部参照の推移的閉包がシリアル化されます。  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] のシリアル化機能では、この問題に対処しています。これには主に、次の 2 つの方法が使用されます。  
  
- <xref:System.Data.Linq.DataContext> のモードにより、遅延読み込みをオフにします (<xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A>)。 詳細については、「<xref:System.Data.Linq.DataContext>」を参照してください。  
  
- コード生成のスイッチにより、生成するエンティティに <xref:System.Runtime.Serialization.DataContractAttribute?displayProperty=nameWithType> 属性および <xref:System.Runtime.Serialization.DataMemberAttribute?displayProperty=nameWithType> 属性を生成します。 この方法と、シリアル化での遅延読み込みクラスの動作が、このトピックの主な話題です。  
  
### <a name="definitions"></a>定義  
  
- *DataContract シリアライザー*:.NET Framework 3.0 以降のバージョンの WCF (Windows Communication Framework) コンポーネントによって使用される既定のシリアライザーです。  
  
- *単方向シリアル化*:循環参照を防ぐために、一方向の関連付けプロパティのみを含む、シリアル化されたバージョンのクラスです。 慣例として、主キー/外部キーのリレーションシップの親側のプロパティをシリアル化の対象としてマークします。 双方向の関連付けの反対側はシリアル化しません。  
  
     [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、シリアル化の種類として、単方向シリアル化のみがサポートされています。  
  
## <a name="code-example"></a>コード例  
 次のコードは、Northwind サンプル データベースの典型的な `Customer` クラスおよび `Order` クラスを使用して、これらのクラスをシリアル化の属性で装飾するようすを示します。  
  
 [!code-csharp[DLinqSerialization#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#1)]
 [!code-vb[DLinqSerialization#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#1)]  
  
 [!code-csharp[DLinqSerialization#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#2)]
 [!code-vb[DLinqSerialization#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#2)]  
  
 [!code-csharp[DLinqSerialization#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#3)]
 [!code-vb[DLinqSerialization#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#3)]  
  
 次の例の `Order` クラスでは、簡略化のために、`Customer` クラスに関する逆関連付けのプロパティのみを示します。 循環参照を防ぐために、<xref:System.Runtime.Serialization.DataMemberAttribute> 属性はありません。  
  
 [!code-csharp[DLinqSerialization#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#4)]
 [!code-vb[DLinqSerialization#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#4)]  
  
 [!code-csharp[DLinqSerialization#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#5)]
 [!code-vb[DLinqSerialization#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#5)]  
  
### <a name="how-to-serialize-the-entities"></a>エンティティをシリアル化する方法  
 前のセクションで示したコードのエンティティは次のようにシリアル化できます。  
  
 [!code-csharp[DLinqSerialization#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/Program.cs#6)]
 [!code-vb[DLinqSerialization#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/Module1.vb#6)]  
  
### <a name="self-recursive-relationships"></a>自己再帰的リレーションシップ  
 自己再帰的リレーションシップも同じパターンに従います。 外部キーに関する関連付けのプロパティには <xref:System.Runtime.Serialization.DataMemberAttribute> 属性がなく、親プロパティにはあります。  
  
 次のクラスには、自己再帰的リレーションシップが 2 つあります:Employee.Manager/Reports と Employee.Mentor/Mentees。  
  
 [!code-csharp[DLinqSerialization#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#7)]
 [!code-vb[DLinqSerialization#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#7)]  
  
## <a name="see-also"></a>関連項目

- [背景情報](background-information.md)
- [SqlMetal.exe (コード生成ツール)](../../../../tools/sqlmetal-exe-code-generation-tool.md)
- [方法: エンティティをシリアル化可能にする](how-to-make-entities-serializable.md)
