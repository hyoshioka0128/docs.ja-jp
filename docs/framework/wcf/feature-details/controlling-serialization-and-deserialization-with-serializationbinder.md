---
title: SerializationBinder を使用したシリアル化および逆シリアル化の制御
ms.date: 07/14/2020
ms.assetid: ba8dcecf-acc7-467c-939d-021bbac797d4
ms.openlocfilehash: 5a7d0bf2aabfcdf789a77cf0fcfeb26357575806
ms.sourcegitcommit: 2543a78be6e246aa010a01decf58889de53d1636
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2020
ms.locfileid: "86444483"
---
# <a name="controlling-serialization-and-deserialization-with-serializationbinder"></a>SerializationBinder を使用したシリアル化および逆シリアル化の制御

> [!WARNING]
> <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>はセキュリティで保護されていないため、セキュリティで保護することはできませ***ん***。 詳細については、「 [Binaryformatter セキュリティガイド](../../../standard/serialization/binaryformatter-security-guide.md)」を参照してください。

シリアル化中に、フォーマッタは、正しい型およびバージョンのオブジェクトのインスタンスを作成するために必要な情報を送信します。 通常、この情報には、オブジェクトの完全な型名および完全なアセンブリ名が含まれます。 既定では、逆シリアル化でこの情報を使用して、同一のオブジェクトのインスタンスを作成します。 場合によっては、シリアル化するクラスと逆シリアル化するクラスの制御が必要となります。これは、元のクラスが逆シリアル化を実行するコンピューター上に存在していない可能性がある場合、元のクラスがアセンブリ間で移動されている場合、または、サーバー上とクライアント上では異なるバージョンのクラスが必要である場合です。 詳細については、「[シリアル化バインダーの使用](../samples/usage-of-serialization-binder.md)」を参照してください。  
  
> [!WARNING]
> この機能は、<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> または <xref:System.Runtime.Serialization.NetDataContractSerializer> を使用してのみ、使用可能です。  
  
## <a name="using-serializationbinder"></a>SerializationBinder の使用  
 <xref:System.Runtime.Serialization.SerializationBinder> は、シリアル化中および逆シリアル化中に使用される実際の型を制御するために使用される抽象クラスです。 シリアル化中および逆シリアル化中に使用される型を制御するには、<xref:System.Runtime.Serialization.SerializationBinder> の派生クラスを作成し、<xref:System.Runtime.Serialization.SerializationBinder.BindToName(System.Type,System.String@,System.String@)> メソッドと <xref:System.Runtime.Serialization.SerializationBinder.BindToType(System.String,System.String)> メソッドをオーバーライドします。 <xref:System.Runtime.Serialization.SerializationBinder.BindToName(System.Type,System.String@,System.String@)> メソッドは <xref:System.Type> を受け取り、アセンブリと型名を返します。 <xref:System.Runtime.Serialization.SerializationBinder.BindToType(System.String,System.String)> メソッドはアセンブリと型名を受け取り、<xref:System.Type> を返します。  
  
## <a name="see-also"></a>関連項目

- [シリアル化と逆シリアル化](serialization-and-deserialization.md)
- [シリアル化バインダーの使用](../samples/usage-of-serialization-binder.md)
