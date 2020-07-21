---
title: コレクションに関するガイドライン
ms.date: 10/22/2008
ms.technology: dotnet-standard
ms.assetid: 297b8f1d-b11f-4dc6-960a-8e990817304e
ms.openlocfilehash: cc853be2310cf72c4eb559f625c6a37a44ed7db8
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84276050"
---
# <a name="guidelines-for-collections"></a>コレクションに関するガイドライン
一般的な特性を持つオブジェクトのグループを操作するために特に設計された型はすべて、コレクションと見なすことができます。 ほとんどの場合、このような型はまたはを実装するのに適してい <xref:System.Collections.IEnumerable> <xref:System.Collections.Generic.IEnumerable%601> ます。したがって、このセクションでは、これらのインターフェイスのいずれかまたは両方を実装する型のみをコレクションにすることを検討します。

 ❌パブリック Api では、弱く型指定されたコレクションを使用しないでください。

 コレクションアイテムを表すすべての戻り値とパラメーターの型は、その基本型ではなく、完全な項目の種類である必要があります (これはコレクションのパブリックメンバーにのみ適用されます)。

 ❌<xref:System.Collections.ArrayList>パブリック api でまたはを使用しない <xref:System.Collections.Generic.List%601> でください。

 これらの型は、パブリック Api ではなく、内部実装で使用するように設計されたデータ構造です。 `List<T>`は、Api と柔軟性の cleanness を犠牲にしてパフォーマンスと性能を高めるために最適化されています。 たとえば、を返した場合、 `List<T>` クライアントコードがコレクションを変更したときに通知を受け取ることはできません。 また、は、 `List<T>` <xref:System.Collections.Generic.List%601.BinarySearch%2A> 多くのシナリオでは役に立たない、または適用できないなど、多くのメンバーを公開します。 次の2つのセクションでは、パブリック Api 専用に設計された型 (抽象化) について説明します。

 ❌`Hashtable`パブリック api でまたはを使用しない `Dictionary<TKey,TValue>` でください。

 これらの型は、内部実装で使用するように設計されたデータ構造体です。 パブリック Api では <xref:System.Collections.IDictionary> 、、 `IDictionary <TKey, TValue>` 、またはインターフェイスの一方または両方を実装するカスタム型を使用する必要があります。

 ❌<xref:System.Collections.Generic.IEnumerator%601> <xref:System.Collections.IEnumerator> メソッドの戻り値の型を除き、、、またはこれらのインターフェイスのいずれかを実装するその他の型は使用しないでください `GetEnumerator` 。

 以外のメソッドから列挙子を返す型は `GetEnumerator` 、ステートメントでは使用できません `foreach` 。

 ❌との両方を `IEnumerator<T>` `IEnumerable<T>` 同じ型に実装しないでください。 これは、非ジェネリックインターフェイスとにも当てはまり `IEnumerator` `IEnumerable` ます。

## <a name="collection-parameters"></a>コレクションパラメーター
 ✔️は、パラメーター型として可能な限り、最も特殊化されていない型を使用します。 コレクションをパラメーターとして受け取るほとんどのメンバーは、インターフェイスを使用し `IEnumerable<T>` ます。

 ❌プロパティに <xref:System.Collections.Generic.ICollection%601> アクセスする場合は、パラメーターとしてまたはを使用しない <xref:System.Collections.ICollection> で `Count` ください。

 代わりに、またはを使用して、 `IEnumerable<T>` `IEnumerable` オブジェクトがまたはを実装しているかどうかを動的に確認してください `ICollection<T>` `ICollection` 。

## <a name="collection-properties-and-return-values"></a>コレクションのプロパティと戻り値
 ❌設定可能なコレクションプロパティを指定しないでください。

 コレクションの内容を置き換えるには、まずコレクションをクリアしてから、新しい内容を追加します。 コレクション全体を置き換えることが一般的なシナリオである場合は、コレクションに対してメソッドを指定することを検討してください `AddRange` 。

 `Collection<T>` `Collection<T>` プロパティまたは読み取り/書き込みコレクションを表す戻り値には、またはのサブクラスを使用✔️ます。

 `Collection<T>`がいくつかの要件を満たしていない場合 (コレクションでを実装する必要がない場合など) は、、 <xref:System.Collections.IList> 、またはを実装してカスタムコレクションを使用し `IEnumerable<T>` `ICollection<T>` <xref:System.Collections.Generic.IList%601> ます。

 ✔️は <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 、のサブクラスである `ReadOnlyCollection<T>` か、または読み取り専用の `IEnumerable<T>` コレクションを表すプロパティまたは戻り値のまれなケースで使用します。

 一般的には、を優先 `ReadOnlyCollection<T>` します。 要件を満たしていない場合 (コレクションでを実装する必要がない場合など) は、、 `IList` `IEnumerable<T>` `ICollection<T>` 、またはを実装してカスタムコレクションを使用します `IList<T>` 。 カスタムの読み取り専用コレクションを実装する場合は、を実装して `ICollection<T>.IsReadOnly` を返し `true` ます。

 サポートするシナリオが、順方向専用イテレーションだけであることが確実な場合は、単にを使用でき `IEnumerable<T>` ます。

 コレクションを直接使用するのではなく、ジェネリック基本コレクションのサブクラスの使用を検討✔️。

 これにより、より適切な名前を使用したり、基本コレクション型に存在しないヘルパーメンバーを追加したりすることができます。 これは、特に高レベルの Api に適用されます。

 ✔️、 `Collection<T>` `ReadOnlyCollection<T>` よく使用されるメソッドとプロパティから、またはのサブクラスを返すことを検討してください。

 これにより、後でヘルパーメソッドを追加したり、コレクションの実装を変更したりできるようになります。

 コレクションに格納されている項目に一意のキー (名前、Id など) が含まれている場合は、キー付きコレクションの使用を検討✔️。 キー付きコレクションは、整数とキーの両方でインデックスを作成できるコレクションで、通常はから継承することによって実装され `KeyedCollection<TKey,TItem>` ます。

 キー付きコレクションは、通常、メモリフットプリントが大きいため、メモリのオーバーヘッドがキーの利点よりも大きなメリットを上回る場合は使用しないでください。

 ❌コレクションプロパティから、またはコレクションを返すメソッドからは、null 値を返さないでください。 代わりに空のコレクションまたは空の配列を返します。

 一般的な規則として、null と空の (0 項目) のコレクションまたは配列は同じように扱う必要があります。

### <a name="snapshots-versus-live-collections"></a>スナップショットとライブコレクション
 ある時点の状態を表すコレクションは、スナップショットコレクションと呼ばれます。 たとえば、データベースクエリから返された行を含むコレクションはスナップショットです。 常に現在の状態を表すコレクションは、live collections と呼ばれます。 たとえば、項目のコレクション `ComboBox` はライブコレクションです。

 ❌プロパティからスナップショットコレクションを返さないようにします。 プロパティはライブコレクションを返します。

 プロパティの getter は、非常に軽量な操作である必要があります。 スナップショットを返すには、O (n) 操作で内部コレクションのコピーを作成する必要があります。

 スナップショットコレクションまたはライブ `IEnumerable<T>` (またはそのサブタイプ) のいずれかを使用して、揮発性のコレクション (つまり、コレクションを明示的に変更することなく変更できる) を表す✔️ます。

 一般に、共有リソース (ディレクトリ内のファイルなど) を表すすべてのコレクションは揮発性です。 このようなコレクションは、実装が単なる順方向専用列挙子の場合を除き、ライブコレクションとして実装するのは非常に困難または不可能です。

## <a name="choosing-between-arrays-and-collections"></a>配列とコレクションの選択
 ✔️は、配列に対してコレクションを優先します。

 コレクションを使用すると、コンテンツの制御が強化され、時間の経過と共に進化して、より使いやすくなります。 また、配列の複製にかかるコストが膨大であるため、読み取り専用のシナリオに配列を使用することはお勧めしません。 使いやすさの研究では、コレクションベースの Api を使用する開発者の方が快適であることがわかりました。

 ただし、低レベルの Api を開発している場合は、読み取り/書き込みのシナリオで配列を使用する方が適切な場合があります。 配列のメモリフットプリントは小さくなるため、ワーキングセットを減らすことができます。また、配列内の要素へのアクセスは、ランタイムによって最適化されるため、より高速になります。

 メモリ消費を最小限に抑え、パフォーマンスを最大化するために、低レベルの Api で配列を使用することを検討して✔️。

 ✔️バイトのコレクションではなく、バイト配列を使用します。

 ❌プロパティ getter が呼び出されるたびに、プロパティが新しい配列 (内部配列のコピーなど) を返す必要がある場合は、プロパティに配列を使用しないでください。

## <a name="implementing-custom-collections"></a>カスタムコレクションの実装
 `Collection<T>` `ReadOnlyCollection<T>` `KeyedCollection<TKey,TItem>` 新しいコレクションをデザインするときに、、、またはから継承することを検討✔️。

 `IEnumerable<T>`新しいコレクションをデザインする場合は、✔️を実装します。 `ICollection<T>`またはを実装する `IList<T>` ことを検討してください。

 このようなカスタムコレクションを実装する場合は、によって確立された API パターンに従い `Collection<T>` `ReadOnlyCollection<T>` ます。 つまり、同じメンバーを明示的に実装し、これらの2つのコレクションのようなパラメーターに名前を付けるなどです。

 `IList` `ICollection` これらのインターフェイスを入力として使用する api にコレクションが渡されることが多い場合は、非ジェネリックコレクションインターフェイス (および) を実装する✔️を検討してください。

 ❌コレクションの概念とは関係のない複雑な Api を使用して、型にコレクションインターフェイスを実装しないようにします。

 ❌などの非ジェネリック基本コレクションから継承しません `CollectionBase` 。 代わりに `Collection<T>`、`ReadOnlyCollection<T>`、および `KeyedCollection<TKey,TItem>` 型を使用してください。

### <a name="naming-custom-collections"></a>カスタムコレクションの名前付け
 コレクション (を実装する型 `IEnumerable` ) は主に2つの理由で作成されます。 (1) 構造固有の操作を使用して新しいデータ構造を作成し、多くの場合、既存のデータ構造 (、、など) とは異なるパフォーマンス特性を作成し、 <xref:System.Collections.Generic.List%601> <xref:System.Collections.Generic.LinkedList%601> <xref:System.Collections.Generic.Stack%601> (2) 特定の項目セットを保持するための特殊なコレクションを作成 <xref:System.Collections.Specialized.StringCollection> します データ構造は、アプリケーションとライブラリの内部実装で最もよく使用されます。 特に、特化されたコレクションは Api で公開されます (プロパティとパラメーターの型として)。

 ✔️は、またはを実装する抽象化の名前に "Dictionary" サフィックスを使用し `IDictionary` `IDictionary<TKey,TValue>` ます。

 ✔️は、 `IEnumerable` (またはその子孫のいずれか) を実装し、項目のリストを表す型の名前で "Collection" サフィックスを使用します。

 ✔️カスタムデータ構造には、適切なデータ構造名を使用します。

 ❌コレクションの抽象化の名前に "LinkedList" や "Hashtable" などの特定の実装を意味するサフィックスは使用しないようにしてください。

 コレクション名の前に項目の種類の名前を付けることを✔️してください。 たとえば、(を実装する) 型の項目を格納するコレクションには `Address` `IEnumerable<Address>` という名前を付ける必要があり `AddressCollection` ます。 項目の種類がインターフェイスの場合は、項目の種類の "I" プレフィックスを省略できます。 したがって、項目のコレクションを <xref:System.IDisposable> 呼び出すことができ `DisposableCollection` ます。

 対応する書き込み可能なコレクションが追加されているか、既にフレームワークに存在する可能性がある場合は、読み取り専用コレクションの名前に "ReadOnly" プレフィックスを使用することを✔️してください。

 たとえば、文字列の読み取り専用コレクションを呼び出す必要があり `ReadOnlyStringCollection` ます。

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [フレームワークデザインのガイドライン](index.md)
- [使用に関するガイドライン](usage-guidelines.md)
