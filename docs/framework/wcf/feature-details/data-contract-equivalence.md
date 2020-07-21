---
title: データ コントラクトの等価性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data contracts [WCF], equivalence
ms.assetid: f06f3c7e-c235-4ec1-b200-68142edf1ed1
ms.openlocfilehash: b96a32f5e11ed4808f8f35d02802afd1f48c3072
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84601323"
---
# <a name="data-contract-equivalence"></a>データ コントラクトの等価性
クライアントがサービスに特定の型のデータを正常に送信するために、またはサービスがクライアントにデータを正常に送信するために、送信する型が受信側に存在する必要があるとは限りません。 両方の型のデータ コントラクトが同等であるということが唯一の要件です ([データコントラクトのバージョン管理](data-contract-versioning.md)に関するセクションで説明されているように、厳密な等価性は必要ない場合があります)。  
  
 データ コントラクトを同等にするには、そのデータ コントラクトに同じ名前空間と名前を使用する必要があります。 また、一方のデータ コントラクトの各データ メンバーには、他方のデータ コントラクトに同等のデータ メンバーがある必要があります。  
  
 データ メンバーを同等にするには、そのデータ メンバーに同じ名前を使用する必要があります。 さらに、データ メンバーは同じ型のデータを表す必要があります。つまり、データ コントラクトが同等である必要があります。  
  
> [!NOTE]
> データ コントラクト名と名前空間、およびデータ メンバー名は、大文字と小文字を区別します。  
  
 データコントラクト名と名前空間、およびデータメンバー名の詳細については、「[データコントラクト名](data-contract-names.md)」を参照してください。  
  
 2 つの型が両側 (送信者と受信者) に存在し、そのデータ コントラクトが同等でない場合 (たとえば、異なるデータ メンバーを含んでいる場合)、そのデータ コントラクトに同じ名前と名前空間を使用しないでください。 同じ名前と名前空間を使用すると、例外がスローされる可能性があります。  
  
 次の型のデータ コントラクトは同等です。  
  
 [!code-csharp[C_DataContractNames#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#5)]
 [!code-vb[C_DataContractNames#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#5)]  
  
## <a name="data-member-order-and-data-contract-equivalence"></a>データ メンバーの順序とデータ コントラクトの等価性  
 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> クラスの <xref:System.Runtime.Serialization.DataMemberAttribute> プロパティの使用は、データ コントラクトの等価性に影響を与えることがあります。 データ コントラクトを同等にするには、データ メンバーが同じ順序で現れる必要があります。 既定の順序はアルファベット順です。 詳細については、「[データメンバーの順序](data-member-order.md)」を参照してください。  
  
 たとえば、次のコードでは、同等なデータ コントラクトが生成されます。  
  
 [!code-csharp[C_DataContractNames#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#6)]
 [!code-vb[C_DataContractNames#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#6)]  
  
 次のコードでは、同等なデータ コントラクトは生成されません。  
  
 [!code-csharp[C_DataContractNames#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#7)]
 [!code-vb[C_DataContractNames#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#7)]  
  
## <a name="inheritance-interfaces-and-data-contract-equivalence"></a>継承、インターフェイス、およびデータ コントラクトの等価性  
 等価性を判断するとき、別のデータ コントラクトから継承したデータ コントラクトは、基本型のすべてのデータ メンバーを含んでいる 1 つのデータ コントラクトとして扱われます。 データ メンバーの順序が一致する必要があり、基本型のメンバーは派生型のメンバーより前に現れる必要があります。 さらに、次のコード例のように、2 つのデータ メンバーの順序の値が同じ場合、そのデータ メンバーの順序はアルファベット順になります。 詳細については、「[データメンバーの順序](data-member-order.md)」を参照してください。  
  
 次の例では、型 `Employee` のデータ コントラクトは型 `Worker` のデータ コントラクトと同等です。  
  
 [!code-csharp[C_DataContractNames#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#8)]
 [!code-vb[C_DataContractNames#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#8)]  
  
 クライアントとサービスの間でパラメーターを渡し、値を返すとき、受信エンドポイントが派生クラスからのデータ コントラクトを予期している場合、基本クラスからのデータ コントラクトを送信できません。 これは、オブジェクト指向プログラミングの原則に基づいています。 前の例では、が予期されるときに、型のオブジェクトを `Person` 送信できません `Employee` 。  
  
 基本クラスからのデータ コントラクトが予期されるときに派生クラスからのデータ コントラクトを送信することは可能ですが、受信エンドポイントが <xref:System.Runtime.Serialization.KnownTypeAttribute> を使用して派生型を認識している場合に限ります。 詳細については、「[データコントラクトの既知の型](data-contract-known-types.md)」を参照してください。 上記の例では、`Employee` が予期されるときに、受信者のコードが既知の型のリストに `Person` を追加するために <xref:System.Runtime.Serialization.KnownTypeAttribute> を使用している場合のみ、型 Employee のオブジェクトを送信できます。  
  
 アプリケーション間でパラメーターを渡し、値を返すとき、予期される型がインターフェイスの場合、その型は、型が <xref:System.Object> の予期される型と同等です。 すべての型は最終的に <xref:System.Object> から派生するので、すべてのデータ コントラクトは最終的に、<xref:System.Object> のデータ コントラクトから派生します。 したがって、インターフェイスが予期されるとき、すべてのデータ コントラクト型を渡すことができます。 インターフェイスを正常に動作させるには、追加の手順が必要です。詳細については、「[データコントラクトの既知の型](data-contract-known-types.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- [データ メンバーの順序](data-member-order.md)
- [既知のデータ コントラクト型](data-contract-known-types.md)
- [データ コントラクト名](data-contract-names.md)
