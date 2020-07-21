---
title: シリアル化プロセスの手順
description: シリアル化プロセスは、フォーマッタでシリアル化メソッドが呼び出されると開始されます。 この記事では、一連のイベントについて説明します。
ms.date: 08/07/2017
helpviewer_keywords:
- binary serialization, steps
- serialization, steps
ms.assetid: 4bcbc883-2a91-418f-b968-6c86a25e9737
ms.openlocfilehash: 1f749b9102182e78bc3fda436cf386a9f5759d5a
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379101"
---
# <a name="steps-in-the-serialization-process"></a>シリアル化プロセスの手順
[フォーマッタ](xref:System.Runtime.Serialization.Formatter)で <xref:System.Runtime.Serialization.Formatter.Serialize%2A> メソッドが呼び出されると、次の一連の規則に従って、オブジェクトのシリアル化プロセスが実行されます。

- フォーマッタにサロゲート セレクターが存在するかどうかをチェックします。 サロゲート セレクターが存在する場合は、そのサロゲート セレクターが指定された型のオブジェクトを処理できるかどうかをチェックします。 そのオブジェクトの型を処理できる場合は、サロゲート セレクターで <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=nameWithType> を呼び出します。

- サロゲート セレクターが存在しないか、またはサロゲート セレクターがそのオブジェクトの型を処理しない場合は、オブジェクトが [Serializable](xref:System.SerializableAttribute) 属性でマークされているかどうかをチェックします。 オブジェクトにそのマークがない場合、<xref:System.Runtime.Serialization.SerializationException> がスローされます。

- オブジェクトが適切にマークされている場合は、オブジェクトが <xref:System.Runtime.Serialization.ISerializable> インターフェイスを実装しているかどうかをチェックします。 実装している場合は、そのオブジェクトで <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> を呼び出します。
  
- オブジェクトが <xref:System.Runtime.Serialization.ISerializable> を実装していない場合は、既定のシリアル化ポリシーを適用して、[NonSerialized](xref:System.NonSerializedAttribute) としてマークされていないすべてのフィールドをシリアル化します。

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]
  
## <a name="see-also"></a>関連項目

- [バイナリ シリアル化](binary-serialization.md)
- [XML シリアル化および SOAP シリアル化](xml-and-soap-serialization.md)
