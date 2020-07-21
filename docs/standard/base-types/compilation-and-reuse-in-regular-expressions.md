---
title: 正規表現におけるコンパイルと再利用
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- parsing text with regular expressions, compilation
- searching with regular expressions, compilation
- .NET Framework regular expressions, engines
- .NET Framework regular expressions, compilation
- regular expressions, compilation
- compilation, regular expressions
- pattern-matching with regular expressions, compilation
- regular expressions, engines
ms.assetid: 182ec76d-5a01-4d73-996c-0b0d14fcea18
ms.openlocfilehash: 54f14a4f31bef00dd222686cc523935b2d9dd5fa
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84279039"
---
# <a name="compilation-and-reuse-in-regular-expressions"></a>正規表現におけるコンパイルと再利用
正規表現エンジンが式をどのようにコンパイルするか、および正規表現がどのようにキャッシュされるかを理解することで、正規表現を幅広く使用するアプリケーションのパフォーマンスを最適化できます。 このトピックでは、コンパイルとキャッシュの両方について説明します。  
  
## <a name="compiled-regular-expressions"></a>コンパイルされた正規表現  
 既定では、正規表現エンジンは、内部命令のシーケンス (Microsoft 中間言語 (MSIL) とは異なる高度なコード) に正規表現をコンパイルします。 エンジンは、正規表現を実行するときに内部コードを解釈します。  
  
 <xref:System.Text.RegularExpressions.RegexOptions.Compiled?displayProperty=nameWithType> オプションを使用して <xref:System.Text.RegularExpressions.Regex> オブジェクトを構築した場合、このオブジェクトは、高度な正規表現の内部命令ではなく明示的な MSIL コードに正規表現をコンパイルします。 これにより、.NET の Just-In-Time (JIT) コンパイラは、式をネイティブのマシン コードに変換してパフォーマンスを高めることができます。  <xref:System.Text.RegularExpressions.Regex> オブジェクトの作成にかかるコストは高くなる場合がありますが、それとの照合の実行にかかるコストは大幅に小さくなる可能性があります。

 事前にコンパイルされた正規表現を使用するという方法もあります。 <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A> メソッドを利用し、すべての式をコンパイルして再利用可能な DLL を作成できます。 これにより、コンパイルされた高速な正規表現を利用しながら、実行時にコンパイルする必要性を回避できます。  
  
## <a name="the-regular-expressions-cache"></a>正規表現のキャッシュ  
 パフォーマンスを高めるために、正規表現エンジンは、コンパイルされた正規表現のアプリケーション全体のキャッシュを保持します。 キャッシュは、静的メソッド呼び出しでのみ使用される正規表現パターンを格納します (インスタンス メソッドに渡される正規表現パターンはキャッシュされません)。これにより、式を使用するたびに高度なバイト コードに再解析する必要がなくなります。  
  
 キャッシュされる正規表現の最大数は、`static` (Visual Basic では `Shared`) <xref:System.Text.RegularExpressions.Regex.CacheSize%2A?displayProperty=nameWithType> プロパティの値によって決定されます。 既定では、正規表現エンジンは最大 15 個のコンパイルされた正規表現をキャッシュします。 コンパイルされた正規表現の数がキャッシュ サイズを超えた場合は、最近の使用頻度が最も低い正規表現が破棄され、新しい正規表現がキャッシュされます。  
  
 アプリケーションでは、次の 2 つの方法のいずれかで正規表現を再利用できます。  
  
- <xref:System.Text.RegularExpressions.Regex> オブジェクトの静的メソッドを使用して、正規表現を定義する。 別の静的メソッド呼び出しで既に定義されている正規表現パターンを使用している場合、正規表現エンジンではキャッシュからのその取得が試みられます。 キャッシュに使用できるものがない場合、エンジンによって正規表現がコンパイルされてキャッシュに追加されます。
  
- 既存の <xref:System.Text.RegularExpressions.Regex> オブジェクトの正規表現パターンが必要な間、このオブジェクトを再利用する。  
  
 オブジェクトのインスタンス化および正規表現のコンパイルのオーバーヘッドが原因となり、さまざまな <xref:System.Text.RegularExpressions.Regex> オブジェクトを作成してすぐに破棄するプロセスは非常にコストがかかります。 多数の異なる正規表現を使用するアプリケーションの場合は、静的 `Regex` メソッドの呼び出しを使用することで、および場合によっては正規表現キャッシュのサイズを大きくすることで、パフォーマンスを最適化できます。  
  
## <a name="see-also"></a>関連項目

- [.NET の正規表現](regular-expressions.md)
