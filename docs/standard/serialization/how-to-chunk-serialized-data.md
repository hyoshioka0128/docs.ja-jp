---
title: '方法 : シリアル化されたデータをチャンクする'
description: データをチャンクして、大きなデータセットに関する問題を回避することができます。 IXmlSerializable インターフェイスを実装して、シリアル化と逆シリアル化を制御します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- chunking serialized data
- data chunking
- binary serialization, chunking data
- large data set chunking
- serialization, chunking data
- serialization, examples
- binary serialization, examples
ms.assetid: 22f1b818-7e0d-428a-8680-f17d6ebdd185
ms.openlocfilehash: 860fdcae0d1937f53ee964d9d4631ec812b3d379
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379137"
---
# <a name="how-to-chunk-serialized-data"></a>方法 : シリアル化されたデータをチャンクする

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]

Web サービス メッセージ内で大きなデータ セットを送信すると、次の 2 つの問題が発生します。  
  
1. シリアル化エンジンのバッファリングによるワーキング セット (メモリ) の巨大化  
  
2. Base64 エンコーディングの実行後はサイズが 33% 増大することによる、帯域幅の過剰消費  
  
 これらの問題を解決するには、シリアル化と逆シリアル化を制御する <xref:System.Xml.Serialization.IXmlSerializable> インターフェイスを実装します。 特に、<xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> メソッドと <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> メソッドを実装することで、データをチャンクします。  
  
### <a name="to-implement-server-side-chunking"></a>サーバー側チャンク処理を実装するには  
  
1. サーバー コンピューター上で、Web メソッドが ASP.NET バッファリングを無効にし、<xref:System.Xml.Serialization.IXmlSerializable> を実装する型を返す必要があります。  
  
2. <xref:System.Xml.Serialization.IXmlSerializable> を実装する型は、<xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> メソッド内でデータをチャンクします。  
  
### <a name="to-implement-client-side-processing"></a>クライアント側の処理を実装するには  
  
1. クライアント プロキシ上で <xref:System.Xml.Serialization.IXmlSerializable> を実装する型を返すように Web メソッドを変更します。 <xref:System.Xml.Serialization.Advanced.SchemaImporterExtension> を使用すると、この処理を自動化できますが、この方法はここでは説明しません。  
  
2. チャンクされたデータ ストリームを読み込み、バイトをディスクに書き込むための <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> メソッドを実装します。 この実装により、進行状況イベントも発生します。これは、プログレス バーなどのグラフィック コントロールに使用できます。  
  
## <a name="example"></a>例  
次のコード例では、クライアント上で ASP.NET バッファリングを無効にする Web メソッドを示します。 また、<xref:System.Xml.Serialization.IXmlSerializable> メソッドにおいてデータをチャンクする <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> インターフェイスをクライアント側で実装する方法も示します。  
  
[!code-csharp[HowToChunkSerializedData#1](../../../samples/snippets/csharp/VS_Snippets_Remoting/HowToChunkSerializedData/CS/SerializationChunk.cs#1)]
[!code-vb[HowToChunkSerializedData#1](../../../samples/snippets/visualbasic/VS_Snippets_Remoting/HowToChunkSerializedData/VB/SerializationChunk.vb#1)]  
[!code-csharp[HowToChunkSerializedData#2](../../../samples/snippets/csharp/VS_Snippets_Remoting/HowToChunkSerializedData/CS/SerializationChunk.cs#2)]
[!code-vb[HowToChunkSerializedData#2](../../../samples/snippets/visualbasic/VS_Snippets_Remoting/HowToChunkSerializedData/VB/SerializationChunk.vb#2)]  
[!code-csharp[HowToChunkSerializedData#3](../../../samples/snippets/csharp/VS_Snippets_Remoting/HowToChunkSerializedData/CS/SerializationChunk.cs#3)]
[!code-vb[HowToChunkSerializedData#3](../../../samples/snippets/visualbasic/VS_Snippets_Remoting/HowToChunkSerializedData/VB/SerializationChunk.vb#3)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
  
- このコードでは、<xref:System>、<xref:System.Runtime.Serialization>、<xref:System.Web.Services>、<xref:System.Web.Services.Protocols>、<xref:System.Xml>、<xref:System.Xml.Serialization>、および <xref:System.Xml.Schema> の各名前空間を使用しています。  
  
## <a name="see-also"></a>関連項目

- [カスタムのシリアル化](custom-serialization.md)
