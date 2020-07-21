---
title: Dispose メソッドの実装
description: この記事では、.NET のコードで使用されるアンマネージド リソースを解放する Dispose メソッドを実装する方法について説明します。
ms.date: 05/27/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Dispose method
- garbage collection, Dispose method
ms.assetid: eb4e1af0-3b48-4fbc-ad4e-fc2f64138bf9
ms.openlocfilehash: c8b4b9a79577776bc049ef77e222d63374178708
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2020
ms.locfileid: "84447174"
---
# <a name="implement-a-dispose-method"></a>Dispose メソッドの実装

<xref:System.IDisposable.Dispose%2A> メソッドを実装するのは、主に、コードによって使用されるアンマネージ リソースをリリースするためです。 <xref:System.IDisposable> の実装であるインスタンス メンバーを使用する場合は、<xref:System.IDisposable.Dispose%2A> 呼び出しをカスケードするのが一般的です。 また、以前行った処理を元に戻すなど、<xref:System.IDisposable.Dispose%2A> を実装するその他の理由もあります。 たとえば、割り当てられたメモリを解放したり、コレクションに追加された項目を削除したり、取得されていたロックのリリースを通知したりします。

[.NET のガベージ コレクター](index.md)は、アンマネージド メモリの割り当てや解放を行いません。 破棄パターンと呼ばれる、オブジェクトを破棄するパターンによって、オブジェクトの有効期間に順番が付けられます。 破棄パターンは、<xref:System.IDisposable> インターフェイスを実装するオブジェクトでのみ使用され、ファイルおよびパイプ ハンドル、レジストリ ハンドル、待機ハンドル、またはアンマネージド メモリ ブロックのポインターを操作する際に一般的です。 これは、ガベージ コレクターは、アンマネージド オブジェクトを再利用できないためです。

<xref:System.IDisposable.Dispose%2A> メソッドをべき等にする (複数回呼び出し可能など) 必要がある場合でも、例外をスローすることなく呼び出されるようにして、リソースが常に適切にクリーンアップされるようにする必要があります。 さらに、後続の <xref:System.IDisposable.Dispose%2A> の呼び出しでは、何も行ってはなりません。

<xref:System.GC.KeepAlive%2A?displayProperty=nameWithType> メソッドに関して提供されたコード例では、オブジェクトまたはそのメンバーへのアンマネージ参照がまだ使用中であるにも関わらず、ガベージ コレクションによりファイナライザーがどのように実行される可能性があるのかを示しています。 現在のルーチンの開始時点からこのメソッドが呼び出される時点まで、<xref:System.GC.KeepAlive%2A?displayProperty=nameWithType> を利用してそのオブジェクトをガベージ コレクションの対象から外すことは理にかなっていると考えられます。

## <a name="safe-handles"></a>セーフ ハンドル

オブジェクトのファイナライザーのコードを記述することは、正しく行わないと問題が発生する可能性がある複雑なタスクです。 そのため、ファイナライザーを実装するのではなく、<xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType> オブジェクトを構築することをお勧めします。

<xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType> は、アンマネージ リソースを識別する <xref:System.IntPtr?displayProperty=nameWithType> をラップする抽象マネージド型です。 Windows ではハンドルを識別しますが、Unix ではファイル記述子を識別します。 これが、このリソースが 1 回しか解放されないことを保証するために必要なすべてのロジックを提供するのは、`SafeHandle` が破棄されるとき、または `SafeHandle` へのすべての参照が削除され、`SafeHandle` インスタンスが終了するときです。

<xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType> は抽象基底クラスです。 派生クラスは、さまざまな種類のハンドルのために特定のインスタンスを提供します。 これらの派生クラスは、<xref:System.IntPtr?displayProperty=nameWithType> のどの値が無効と見なされるかを検証し、実際にハンドルを解放する方法を検証します。 たとえば、<xref:Microsoft.Win32.SafeHandles.SafeFileHandle> は `SafeHandle` から派生し、開いているファイル ハンドル/記述子を識別する `IntPtrs` をラップし、その <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle?displayProperty=nameWithType> メソッドをオーバーライドして閉じます (Unix では `close` 関数または Windows では `CloseHandle` 関数)。 アンマネージ リソースを作成する .NET ライブラリのほとんどの API は、それを `SafeHandle` でラップし、生ポインターを渡す代わりに、必要に応じて `SafeHandle` をユーザーに返します。 アンマネージ コンポーネントと対話し、アンマネージ リソースの `IntPtr` を取得する状況では、独自の `SafeHandle` 型を作成してラップすることができます。 その結果、`SafeHandle` 以外の型でファイナライザーを実装する必要があるのはごく少数になります。ほとんどの破棄可能パターンの実装では、`SafeHandle` を含む他の管理対象リソースをラップするだけで終了します。

<xref:Microsoft.Win32.SafeHandles> 名前空間の次の派生クラスは、セーフ ハンドルを提供します。

- ファイル、メモリ マップ ファイルおよびパイプのための <xref:Microsoft.Win32.SafeHandles.SafeFileHandle>、<xref:Microsoft.Win32.SafeHandles.SafeMemoryMappedFileHandle>、<xref:Microsoft.Win32.SafeHandles.SafePipeHandle> クラス。
- メモリ ビューのための <xref:Microsoft.Win32.SafeHandles.SafeMemoryMappedViewHandle> クラス。
- 暗号の構成要素のための <xref:Microsoft.Win32.SafeHandles.SafeNCryptKeyHandle>、<xref:Microsoft.Win32.SafeHandles.SafeNCryptProviderHandle>、<xref:Microsoft.Win32.SafeHandles.SafeNCryptSecretHandle> クラス。
- レジストリ キーのための <xref:Microsoft.Win32.SafeHandles.SafeRegistryHandle> クラス。
- 待機ハンドルのための <xref:Microsoft.Win32.SafeHandles.SafeWaitHandle> クラス。

## <a name="dispose-and-disposebool"></a>Dispose() と Dispose(bool)

<xref:System.IDisposable> インターフェイスでは、パラメーターのない <xref:System.IDisposable.Dispose%2A> メソッドを 1 つ実装する必要があります。 また、すべての非シールド クラスは、追加の `Dispose(bool)` オーバーロード メソッドを実装する必要があります。

- `public` で非仮想 (Visual Basic では `NonInheritable`) の <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> の実装。パラメーターはありません。

- `protected virtual` (Visual Basic では `Overridable`) の `Dispose` メソッド。シグネチャは次のとおりです。

  [!code-csharp[Conceptual.Disposable#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/dispose1.cs#8)]
  [!code-vb[Conceptual.Disposable#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/dispose1.vb#8)]

  > [!IMPORTANT]
  > `disposing` パラメーターは、ファイナライザーから呼び出されたときは `false`、<xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> メソッドから呼び出されたときは `true` にする必要があります。 つまり、確定的に呼び出されたときは `true`、非確定的に呼び出されたときは `false` です。

### <a name="the-dispose-method"></a>Dispose() メソッド

この `public` で非仮想 (Visual Basic では `NonInheritable`)、パラメーターなしの `Dispose` メソッドは、型のコンシューマーによって呼び出されるため、その目的は、アンマネージ リソースを解放し、通常のクリーンアップを実行し、ファイナライザーが存在する場合、それを実行する必要がないことを示すことです。 マネージド オブジェクトに関連付けられている実際のメモリを解放するのは、常に[ガベージ コレクター](index.md)のドメインです。 このため、次のような標準的な実装があります。

[!code-csharp[Conceptual.Disposable#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/dispose1.cs#7)]
[!code-vb[Conceptual.Disposable#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/dispose1.vb#7)]

`Dispose` メソッドはオブジェクトのクリーンアップをすべて実行するため、ガベージ コレクターはもはやオブジェクトの <xref:System.Object.Finalize%2A?displayProperty=nameWithType> のオーバーライドを呼び出す必要はありません。 そこで、<xref:System.GC.SuppressFinalize%2A> メソッドを呼び出して、ガベージ コレクターによるファイナライザーの実行を抑制します。 型にファイナライザーがない場合、<xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType> を呼び出しても無効です。 実際のクリーンアップは、`Dispose(bool)` メソッド オーバーロードによって実行されることに注意してください。

### <a name="the-disposebool-method-overload"></a>Dispose (bool) メソッドオーバーロード

オーバーロードでは、`disposing` パラメーターは <xref:System.Boolean> で、メソッドの呼び出し元が <xref:System.IDisposable.Dispose%2A> メソッドか (値は `true`)、それともファイナライザーか (値は `false`) を示します。

メソッドの本体は 2 つのコード ブロックで構成されます。

- アンマネージ リソースを解放するブロック。 このブロックは、`disposing` パラメーターの値に関係なく実行されます。
- マネージド リソースを解放する条件付きブロック。 このブロックは、`disposing` の値が `true` の場合に実行されます。 解放するマネージド リソースには、次のオブジェクトを含めることができます。

  - **<xref:System.IDisposable> を実装するマネージド オブジェクト。** 条件付きブロックを使用して <xref:System.IDisposable.Dispose%2A> の実装を呼び出すことができます (カスケード破棄)。 <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType> の派生クラスを使用してアンマネージ リソースをラップしている場合は、ここで <xref:System.Runtime.InteropServices.SafeHandle.Dispose?displayProperty=nameWithType> の実装を呼び出す必要があります。

  - **大量のメモリを消費するか、不足しているリソースを消費するマネージド オブジェクト。** `null` に大きなマネージド オブジェクト参照を割り当てて、到達不能の可能性が高くなるようにします。 こうすると、非確定的に再利用された場合よりも、速く解放されます。

メソッドの呼び出し元がファイナライザーの場合、アンマネージ リソースを解放するコードだけを実行する必要があります。 実装側は、正しくないパスが、再利用された可能性があるマネージド オブジェクトと対話しないことを保証する必要があります。 これが重要なのは、ガベージ コレクターがマネージド オブジェクトを破棄する順序が非確定的であるためです。

## <a name="cascade-dispose-calls"></a>カスケード破棄呼び出し

クラスがフィールドまたはプロパティを所有しており、その型が <xref:System.IDisposable> を実装する場合、それを含むクラスそのものが <xref:System.IDisposable> も実装する必要があります。 <xref:System.IDisposable> の実装をインスタンス化して、それをインスタンス メンバーとして格納するクラスも、そのクリーンアップを担当します。 これで、参照される破棄可能な型が、<xref:System.IDisposable.Dispose%2A> メソッドを介してクリーンアップを確定的に実行できるようになります。 この例では、クラスは `sealed` (または Visual Basic では `NotInheritable`) です。

[!code-csharp[Conceptual.Disposable#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/disposable1.cs#1)]
[!code-vb[Conceptual.Disposable#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/disposable1.vb#1)]

## <a name="implement-the-dispose-pattern"></a>破棄パターンの実装

非シールド クラス (つまり `NotInheritable` として修飾されない Visual Basic クラス) は、継承される可能性があるため、潜在的な基底クラスと見なす必要があります。 潜在的な基底クラスの破棄パターンを実装する場合、以下を用意する必要があります。

- <xref:System.IDisposable.Dispose%2A> メソッドを呼び出す `Dispose(bool)` の実装。
- 実際のクリーンアップを実行する `Dispose(bool)` メソッド。
- アンマネージ リソースをラップする <xref:System.Runtime.InteropServices.SafeHandle> から派生したクラス (推奨)、または、<xref:System.Object.Finalize%2A?displayProperty=nameWithType> メソッドのオーバーライド。 <xref:System.Runtime.InteropServices.SafeHandle> クラスにはファイナライザーが用意されているので、自分で作成する必要はありません。

> [!IMPORTANT]
> 基底クラスはマネージド オブジェクトを参照するだけで、破棄パターンを実装することができます。 このような場合、ファイナライザーは不要です。 ファイナライザーは、アンマネージ リソースを直接参照する場合にのみ必要です。

セーフ ハンドルを使用して基底クラスで Dispose パターンを実装する一般的なパターンを次に示します。

[!code-csharp[System.IDisposable#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/base1.cs#3)]
[!code-vb[System.IDisposable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/base1.vb#3)]

> [!NOTE]
> 前の例では、<xref:Microsoft.Win32.SafeHandles.SafeFileHandle> オブジェクトを使用してパターンを示しています。代わりに、<xref:System.Runtime.InteropServices.SafeHandle> から派生した任意のオブジェクトを使用することもできます。 例では、<xref:Microsoft.Win32.SafeHandles.SafeFileHandle> オブジェクトを正しくインスタンス化していないことに注意してください。

<xref:System.Object.Finalize%2A?displayProperty=nameWithType> をオーバーライドして基底クラスで Dispose パターンを実装する一般的なパターンを次に示します。

[!code-csharp[System.IDisposable#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/base2.cs#5)]
[!code-vb[System.IDisposable#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/base2.vb#5)]

> [!TIP]
> C# では、<xref:System.Object.Finalize%2A?displayProperty=nameWithType> をオーバーライドして[ファイナライザー](../../csharp/programming-guide/classes-and-structs/destructors.md)を作成します。 Visual Basic では、これは `Protected Overrides Sub Finalize()` を使用して行われます。

## <a name="implement-the-dispose-pattern-for-a-derived-class"></a>派生クラスの破棄パターンの実装

<xref:System.IDisposable> インターフェイスを実装するクラスから派生したクラスは、<xref:System.IDisposable> の基底クラスでの実装が派生クラスに継承されるため、<xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> を実装しないでください。 代わりに、派生クラスをクリーンアップするには、以下を用意します。

- 基底クラスのメソッドをオーバーライドして、派生クラスの実際のクリーンアップを実行する `protected override void Dispose(bool)` メソッド。 このメソッドは、基底クラスの `base.Dispose(bool)` (Visual Basic では `MyBase.Dispose(bool)`) メソッドも呼び出して、引数の破棄状態を渡す必要があります。
- アンマネージ リソースをラップする <xref:System.Runtime.InteropServices.SafeHandle> から派生したクラス (推奨)、または、<xref:System.Object.Finalize%2A?displayProperty=nameWithType> メソッドのオーバーライド。 <xref:System.Runtime.InteropServices.SafeHandle> クラスには、コーディングが不要なファイナライザーが用意されています。 ファイナライザーを用意する場合は、`disposing` 引数を `false` として `Dispose(bool)` オーバーロードを呼び出す必要があります。

セーフ ハンドルを使用して派生クラスで Dispose パターンを実装する一般的なパターンを次に示します。

[!code-csharp[System.IDisposable#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/derived1.cs#4)]
[!code-vb[System.IDisposable#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/derived1.vb#4)]

> [!NOTE]
> 前の例では、<xref:Microsoft.Win32.SafeHandles.SafeFileHandle> オブジェクトを使用してパターンを示しています。代わりに、<xref:System.Runtime.InteropServices.SafeHandle> から派生した任意のオブジェクトを使用することもできます。 例では、<xref:Microsoft.Win32.SafeHandles.SafeFileHandle> オブジェクトを正しくインスタンス化していないことに注意してください。

<xref:System.Object.Finalize%2A?displayProperty=nameWithType> をオーバーライドして派生クラスで Dispose パターンを実装する一般的なパターンを次に示します。

[!code-csharp[System.IDisposable#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/derived2.cs#6)]
[!code-vb[System.IDisposable#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/derived2.vb#6)]

## <a name="implement-the-dispose-pattern-with-safe-handles"></a>セーフ ハンドルを使用した破棄パターンの実装

次の例は、セーフ ハンドルを使用してアンマネージ リソースをカプセル化する、基底クラス `DisposableStreamResource` での Dispose パターンを示します。 例では、`DisposableStreamResource` を使用して、開いているファイルを表す <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> オブジェクトをラップする <xref:System.IO.Stream> クラスを定義しています。 このクラスには、ファイル ストリームの合計バイト数を返す `Size` プロパティも含まれています。

[!code-csharp[Conceptual.Disposable#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/base1.cs#9)]
[!code-vb[Conceptual.Disposable#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/base1.vb#9)]

## <a name="implement-the-dispose-pattern-for-a-derived-class-with-safe-handles"></a>セーフ ハンドルを使用した派生クラスの破棄パターンの実装

次の例は、前の例で挙げた `DisposableStreamResource2` クラスを継承した派生クラス `DisposableStreamResource` での Dispose パターンを示します。 このクラスは `WriteFileInfo` メソッドを追加し、<xref:Microsoft.Win32.SafeHandles.SafeFileHandle> オブジェクトを使用して書き込み可能ファイル ハンドルをラップしています。

[!code-csharp[Conceptual.Disposable#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/derived1.cs#10)]
[!code-vb[Conceptual.Disposable#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/derived1.vb#10)]

## <a name="see-also"></a>関連項目

- <xref:System.GC.SuppressFinalize%2A>
- <xref:System.IDisposable>
- <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>
- <xref:Microsoft.Win32.SafeHandles>
- <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType>
- <xref:System.Object.Finalize%2A?displayProperty=nameWithType>
- [クラスと構造体を定義および使用する (C++/CLI)](/cpp/dotnet/how-to-define-and-consume-classes-and-structs-cpp-cli)
