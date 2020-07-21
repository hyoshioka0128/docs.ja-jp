---
title: データ コントラクトの列挙型
description: データコントラクトモデルが、WFC プログラミングモデルの一部として列挙を表現する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data contracts [WCF], enumeration types
ms.assetid: b5d694da-68cb-4b74-a5fb-75108a68ec3b
ms.openlocfilehash: ff3184a285e88d47d4545a38a6c74b2f209827fb
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247300"
---
# <a name="enumeration-types-in-data-contracts"></a>データ コントラクトの列挙型
列挙はデータ コントラクト モデルで表現できます。 このトピックでは、いくつかの例を通してプログラミング モデルを説明します。  
  
## <a name="enumeration-basics"></a>列挙の基本  
 データ コントラクト モデルで列挙型を使用する 1 つの方法として、<xref:System.Runtime.Serialization.DataContractAttribute> 属性を型に割り当てる方法があります。 この場合、データ コントラクトに含める必要のある各メンバーに <xref:System.Runtime.Serialization.EnumMemberAttribute> 属性を適用する必要があります。  
  
 2 つのクラスを次の例に示します。 1 つ目は列挙を使用し、2 つ目は列挙を定義します。  
  
 [!code-csharp[c_DataContractEnumerations#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#1)]
 [!code-vb[c_DataContractEnumerations#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#1)]  
  
 `Car` クラスのインスタンスは、`condition` フィールドの値が `New`、`Used`、`Rental` のいずれかに設定されている場合にのみ送受信できます。 `condition` が、`Broken` または `Stolen` の場合、<xref:System.Runtime.Serialization.SerializationException> がスローされます。  
  
 <xref:System.Runtime.Serialization.DataContractAttribute> プロパティ (<xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> と <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>) を、列挙データ コントラクトとして通常通り使用できます。  
  
### <a name="enumeration-member-values"></a>列挙メンバー値  
 通常、データ コントラクトには、数値ではなく列挙メンバー名が含まれます。 ただし、データコントラクトモデルを使用する場合、受信側が WCF クライアントの場合、エクスポートされたスキーマは数値を保持します。 [XmlSerializer クラスを使用](using-the-xmlserializer-class.md)してを使用する場合は、この方法ではないことに注意してください。  
  
 前の例では、`condition` が `Used` に設定され、データが XML にシリアル化されると、結果の XML は `<condition>Used</condition>` になりますが `<condition>1</condition>` にはなりません。 したがって、次のデータ コントラクトは、`CarConditionEnum` のデータ コントラクトと同じです。  
  
 [!code-csharp[c_DataContractEnumerations#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#2)]
 [!code-vb[c_DataContractEnumerations#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#2)]  
  
 たとえば、`CarConditionEnum` を送信側で使用し、`CarConditionWithNumbers` を受信側で使用できます。 送信側で `Used` に値 "1" を使用し、受信側で値 "20" を使用しても、XML 表現は送信側と受信側共に `<condition>Used</condition>` です。  
  
 データ コントラクトに含めるには、<xref:System.Runtime.Serialization.EnumMemberAttribute> 属性を適用する必要があります。 .NET Framework では、常に特別な値 0 (ゼロ) を列挙型に適用できます。これは、列挙体の既定値でもあります。 ただし、この特殊値ゼロも <xref:System.Runtime.Serialization.EnumMemberAttribute> 属性を使用してマークされない限りシリアル化できません。  
  
 これには、次のような 2 つの例外があります。  
  
- フラグ列挙体 (このトピックの後で説明)  
  
- <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> プロパティが `false` に設定された列挙データ メンバー (この場合、値がゼロの列挙はシリアル化されたデータから除外される)  
  
### <a name="customizing-enumeration-member-values"></a>列挙メンバー値のカスタマイズ  
 データ コントラクトの一部を形成する列挙メンバー値は、<xref:System.Runtime.Serialization.EnumMemberAttribute.Value%2A> 属性の <xref:System.Runtime.Serialization.EnumMemberAttribute> プロパティを使ってカスタマイズできます。  
  
 たとえば、次のデータ コントラクトは `CarConditionEnum` のデータ コントラクトとも等価です。  
  
 [!code-csharp[c_DataContractEnumerations#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#3)]
 [!code-vb[c_DataContractEnumerations#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#3)]  
  
 シリアル化されると、`PreviouslyOwned` の値には XML 表現 `<condition>Used</condition>` が含まれます。  
  
## <a name="simple-enumerations"></a>単純な列挙  
 <xref:System.Runtime.Serialization.DataContractAttribute> 属性が割り当てられていない列挙型をシリアル化することもできます。 このような列挙型は、前の説明とまったく同じように扱われます。ただし、すべてのメンバー (<xref:System.NonSerializedAttribute> 属性は適用されていない) に <xref:System.Runtime.Serialization.EnumMemberAttribute> 属性が適用されているかのように扱われる点が異なります。 たとえば、次の列挙は、前の `CarConditionEnum` の例と同じデータ コントラクトが暗黙的に含まれます。  
  
 [!code-csharp[c_DataContractEnumerations#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#6)]
 [!code-vb[c_DataContractEnumerations#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#6)]  
  
 列挙のデータ コントラクト名と名前空間、および列挙メンバー値をカスタマイズする必要がない場合に、単純な列挙を使用できます。  
  
#### <a name="notes-on-simple-enumerations"></a>単純な列挙に関するメモ  
 <xref:System.Runtime.Serialization.EnumMemberAttribute> 属性を単純な列挙に適用しても効力はありません。  
  
 <xref:System.SerializableAttribute> 属性を列挙に適用してもしなくても変わりはありません。  
  
 <xref:System.Runtime.Serialization.DataContractSerializer> クラスが、列挙メンバーに適用された <xref:System.NonSerializedAttribute> 属性を受け入れるという事実は、<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> と <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> の動作とは異なります。 この 2 つのシリアライザーは <xref:System.NonSerializedAttribute> 属性を無視します。  
  
## <a name="flag-enumerations"></a>フラグ列挙体  
 列挙体に <xref:System.FlagsAttribute> 属性を適用できます。 この場合、ゼロ個以上の列挙値のリストを同時に送受信できます。  
  
 これを行うには、<xref:System.Runtime.Serialization.DataContractAttribute> 属性をフラグ列挙体に適用し、2 の累乗であるすべてのメンバーを、<xref:System.Runtime.Serialization.EnumMemberAttribute> 属性を使用してマークします。 フラグ列挙体を使用するには、数列は (1、2、4、8、16、32、64 のように) 2 の累乗の連続である必要があります。  
  
 フラグの列挙値を送信する手順を次に示します。  
  
1. 数値にマップする列挙メンバー (<xref:System.Runtime.Serialization.EnumMemberAttribute> 属性が適用されている) の検索を試みます。 見つかった場合、そのメンバーのみを含むリストを送信します。  
  
2. 合計の各部にマップされる列挙メンバー (それぞれに <xref:System.Runtime.Serialization.EnumMemberAttribute> 属性が適用されている) が存在するような形で、数値をこの合計に分割します。 このメンバーすべてのリストを送信します。 このような合計を見つけるために*最長一致アルゴリズム*が使用されるため、このような合計が存在する場合でも、そのような合計が検出されるという保証はありません。 この問題を回避するには、列挙メンバーの数値を必ず 2 の累乗数にします。  
  
3. 前の 2 つの手順が失敗し、数値がゼロ以外の場合、<xref:System.Runtime.Serialization.SerializationException> をスローします。 数値がゼロの場合、空のリストを送信します。  
  
### <a name="example"></a>例  
 フラグ操作で使用できる列挙の例を次に示します。  
  
 [!code-csharp[c_DataContractEnumerations#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#4)]
 [!code-vb[c_DataContractEnumerations#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#4)]  
  
 次の各値は、示されているようにシリアル化されます。  
  
 [!code-csharp[c_DataContractEnumerations#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#5)]
 [!code-vb[c_DataContractEnumerations#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#5)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.DataContractSerializer>
- [データ コントラクトの使用](using-data-contracts.md)
- [サービス コントラクトでのデータ転送の指定](specifying-data-transfer-in-service-contracts.md)
