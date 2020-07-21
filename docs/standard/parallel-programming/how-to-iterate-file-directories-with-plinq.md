---
title: '方法: PLINQ を使用してファイル ディレクトリを反復処理する'
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- PLINQ queries, how to iterate directories
ms.assetid: 354e8ce3-35c4-431c-99ca-7661d1f3901b
ms.openlocfilehash: abf31ea69af6a85140efb783959a9a586ef6a59e
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84278000"
---
# <a name="how-to-iterate-file-directories-with-plinq"></a>方法: PLINQ を使用してファイル ディレクトリを反復処理する

この記事では、ファイル ディレクトリに対する操作を並列化する 2 とおりの方法を示します。 最初のクエリでは、<xref:System.IO.Directory.GetFiles%2A> メソッドを使用して、ディレクトリとすべてのサブディレクトリ内のファイル名の配列を作成します。 このメソッドでは、配列全体が設定されるまで戻されないため、操作の開始時に待機時間が発生する可能性があります。 ただし、配列が作成されたら、PLINQ は配列を迅速に並列処理できます。  
  
2 番目のクエリでは、即座に結果を返し始める静的な <xref:System.IO.Directory.EnumerateDirectories%2A> メソッドと <xref:System.IO.DirectoryInfo.EnumerateFiles%2A> メソッドを使用します。 この方法での処理は、大規模なディレクトリ ツリーの反復処理では高速になる場合がありますが、処理時間は最初の例に比べると多くの要素に左右されます。  
  
> [!NOTE]
> これらの例は使用法を示すことを目的としており、同等の LINQ to Objects 順次クエリよりも実行速度が遅い場合があります。 高速化の詳細については、「[PLINQ での高速化について](understanding-speedup-in-plinq.md)」を参照してください。  
  
## <a name="getfiles-example"></a>GetFiles の例

 この例では、ツリー内のすべてのディレクトリにアクセスできる場合、ファイル サイズが大きくない場合、アクセス時間が重要ではない場合の単純なシナリオで、ファイル ディレクトリを反復処理する方法を示しています。 この方法では、ファイル名の配列が作成されている間、最初に待機時間が発生します。  
  
 [!code-csharp[PLINQ#33](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqfileiteration.cs#33)]  
  
## <a name="enumeratefiles-example"></a>EnumerateFiles の例

 この例では、ツリー内のすべてのディレクトリにアクセスできる場合、ファイル サイズが大きくない場合、アクセス時間が重要ではない場合の単純なシナリオで、ファイル ディレクトリを反復処理する方法を示しています。 この方法では、前の例よりも迅速に結果を生成し始めます。  
  
 [!code-csharp[PLINQ#34](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqfileiteration.cs#34)]  
  
 <xref:System.IO.Directory.GetFiles%2A> を使用する場合は、ツリー内のすべてのディレクトリに対して必要なアクセス許可があることを確認してください。 アクセス許可がないと例外がスローされ、結果は返されません。 PLINQ クエリで <xref:System.IO.Directory.EnumerateDirectories%2A> を使用する場合、反復処理を続行できるように I/O 例外を適切に処理することが問題となります。 コードで I/O 例外または承認されていないアクセスの例外を処理する必要がある場合は、「[方法: Parallel クラスを使用してファイル ディレクトリを反復処理する](how-to-iterate-file-directories-with-the-parallel-class.md)」で説明する方法を検討することをお勧めします。  
  
 ネットワーク経由のファイル I/O などで I/O の待機時間が問題となる場合は、「[TPL と従来の .NET 非同期プログラミング](tpl-and-traditional-async-programming.md)」およびこの[ブログの投稿](https://devblogs.microsoft.com/pfxteam/parallel-extensions-and-io/)で説明する非同期 I/O の手法のいずれかを使用することを検討してください。  
  
## <a name="see-also"></a>関連項目

- [Parallel LINQ (PLINQ)](introduction-to-plinq.md)
