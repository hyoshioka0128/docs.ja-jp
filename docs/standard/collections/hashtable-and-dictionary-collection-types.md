---
title: Hashtable コレクション型と Dictionary コレクション型
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- Hashtable class, grouping data in collections
- Hashtable collection type
- hash tables
- grouping data in collections, Hashtable collection type
- hash function
- collections [.NET Framework], Hashtable collection type
ms.assetid: bfc20837-3d02-4fc7-8a8f-c5215b6b7913
ms.openlocfilehash: b228f5db16ba01969b77d601becfb94ac0506d1e
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287966"
---
# <a name="hashtable-and-dictionary-collection-types"></a>Hashtable コレクション型と Dictionary コレクション型
<xref:System.Collections.Hashtable?displayProperty=nameWithType> クラス、および <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType> と <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=nameWithType> ジェネリック クラスは、<xref:System.Collections.IDictionary?displayProperty=nameWithType> インターフェイスを実装します。 <xref:System.Collections.Generic.Dictionary%602> ジェネリック クラスも <xref:System.Collections.Generic.IDictionary%602> ジェネリック インターフェイスを実装します。 そのため、これらのコレクション内の各要素は、キーと値のペアになります。  
  
 <xref:System.Collections.Hashtable> オブジェクトは、コレクションの要素を含むバケットので構成されます。 バケットは<xref:System.Collections.Hashtable> に含まれる要素の仮想サブグループで、これを使用することにより、ほとんどのコレクションで検索と取得がより簡単で高速になります。 各バケットは、ハッシュ関数を使用して生成され、要素のキーに基づいている、ハッシュ コードに関連付けられています。  
  
 ジェネリック <xref:System.Collections.Generic.HashSet%601> クラスは、一意の要素を格納するための順序付けられていないコレクションです。  
  
 ハッシュ関数は、キーに基づく数値のハッシュ コードを返すアルゴリズムです。 キーは、格納されているオブジェクトのいくつかのプロパティの値です。 ハッシュ関数は、同じキーに対して常に同じハッシュ コードを返す必要があります。 ハッシュ関数によって 2 つの異なるキーを持つ同一のハッシュ コードを生成することも可能ですが、一意のキーごとに一意のハッシュ コードを生成するハッシュ関数のほうが、ハッシュ テーブルから要素を取得する際により優れたパフォーマンスを実現します。  
  
 <xref:System.Collections.Hashtable> で要素として使用されている各オブジェクトは、<xref:System.Object.GetHashCode%2A> メソッドの実装を使用して、それ自体のハッシュ コードを生成できる必要があります。 ただし、<xref:System.Collections.IHashCodeProvider> 実装をパラメーターの 1 つとして受け入れる <xref:System.Collections.Hashtable> コンストラクターを使用して、<xref:System.Collections.Hashtable> のすべての要素のハッシュ関数を指定することもできます。  
  
 オブジェクトは、<xref:System.Collections.Hashtable> に追加されるとき、そのオブジェクトのハッシュ コードと一致するハッシュ コードに関連付けられたバケットに格納されます。 値が <xref:System.Collections.Hashtable> 内で検索されるとき、その値のハッシュ コードが生成されて、そのハッシュ コードに関連付けられたバケットが検索されます。  
  
 たとえば、文字列のハッシュ関数は、文字列内の各文字の ASCII コードを取得し、それらを加え合わせて 1 つのハッシュ コードを生成することができます。 その場合、文字列「picnic」のハッシュ コードは文字列「basket」のハッシュ コードと異なるので、文字列「picnic」と「basket」は異なるバケットに格納されます。 それに対して、「stressed」と「desserts」は同じハッシュ コードを持つので、同じバケットに格納されます。  
  
 <xref:System.Collections.Generic.Dictionary%602> および <xref:System.Collections.Concurrent.ConcurrentDictionary%602> クラスには、<xref:System.Collections.Hashtable> クラスと同じ機能があります。 特定の型 (<xref:System.Object> を除く) の<xref:System.Collections.Generic.Dictionary%602> は、値型の <xref:System.Collections.Hashtable> よりも優れたパフォーマンスを実現します。 これは、<xref:System.Collections.Hashtable> の要素の型が <xref:System.Object> であるため、値型を格納したり取得したりすると、ボックス化とボックス化解除が通常発生するためです。 複数のスレッドが同時にコレクションにアクセスするときには、<xref:System.Collections.Concurrent.ConcurrentDictionary%602> クラスを使用する必要があります。  
  
## <a name="see-also"></a>参照

- <xref:System.Collections.Hashtable>
- <xref:System.Collections.IDictionary>
- <xref:System.Collections.IHashCodeProvider>
- <xref:System.Collections.Generic.Dictionary%602>
- <xref:System.Collections.Generic.IDictionary%602?displayProperty=nameWithType>
- <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=nameWithType>
- [ 一般的に使用されるコレクション型](commonly-used-collection-types.md)
