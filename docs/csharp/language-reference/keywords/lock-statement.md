---
title: lock ステートメント - C# リファレンス
description: C# lock ステートメントを使用し、共有リソースへのスレッド アクセスを同期します
ms.date: 04/02/2020
f1_keywords:
- lock_CSharpKeyword
- lock
helpviewer_keywords:
- lock keyword [C#]
ms.assetid: 656da1a4-707e-4ef6-9c6e-6d13b646af42
ms.openlocfilehash: 6e9a6975977588ba7692c925d7940cd2ec26671f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406691"
---
# <a name="lock-statement-c-reference"></a>lock ステートメント (C# リファレンス)

`lock` ステートメントは、指定のオブジェクトに対する相互排他ロックを取得し、ステートメント ブロックを実行してからロックを解放します。 ロックが保持されている間、ロックを保持するスレッドではロックを再度取得し、解放することができます。 他のスレッドはブロックされてロックを取得できず、ロックが解放されるまで待機します。

`lock` ステートメントの形式は次のようになります。

```csharp
lock (x)
{
    // Your code...
}
```

`x` は[参照型](reference-types.md)の式です。 これは次にまったく等しくなります。

```csharp
object __lockObj = x;
bool __lockWasTaken = false;
try
{
    System.Threading.Monitor.Enter(__lockObj, ref __lockWasTaken);
    // Your code...
}
finally
{
    if (__lockWasTaken) System.Threading.Monitor.Exit(__lockObj);
}
```

このコードでは [try...finally](try-finally.md) ブロックが使用されているため、`lock` ステートメントの本文内で例外がスローされた場合でもロックは解放されます。

`lock` ステートメントの本文で [await](../operators/await.md) 演算子を使用することはできません。

## <a name="guidelines"></a>ガイドライン

共有リソースへのスレッド アクセスを同期する場合、専用オブジェクト インスタンス (`private readonly object balanceLock = new object();` など) またはコードの関連のない部分によってロック オブジェクトとして使用される可能性がない別のインスタンスをロックします。 異なる共有リソースに対して同じロック オブジェクト インスタンスを使用することは避けてください。デッドロックやロックの競合が発生する可能性があります。 特に、以下をロック オブジェクトとして使用しないでください。

- `this`。ロックとして呼び出し元に使用される可能性があります。
- <xref:System.Type> インスタンス。[typeof](../operators/type-testing-and-cast.md#typeof-operator) 演算子またはリフレクションによって取得される可能性があります。
- 文字列リテラルを含む文字列インスタンス。[インターン処理](/dotnet/api/system.string.intern#remarks)される可能性があります。

ロックの競合を減らすために、できるだけ短い時間ロックを保持します。

## <a name="example"></a>例

次の例では、専用 `balanceLock` インスタンスをロックすることでそのプライベート `balance` フィールドへのアクセスを同期する `Account` クラスが定義されます。 ロッキングに同じインスタンスを使用すると、2 つのスレッドが `Debit` または `Credit` メソッドを同時に呼び出すことによって `balance` フィールドを同時に更新することができなくなります。

[!code-csharp[lock-statement-example](snippets/LockStatementExample.cs)]

## <a name="c-language-specification"></a>C# 言語仕様

詳細については、「[C# 言語仕様](~/_csharplang/spec/introduction.md)」の [lock ステートメント](~/_csharplang/spec/statements.md#the-lock-statement)に関するセクションを参照してください。

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# キーワード](index.md)
- <xref:System.Threading.Monitor?displayProperty=nameWithType>
- <xref:System.Threading.SpinLock?displayProperty=nameWithType>
- <xref:System.Threading.Interlocked?displayProperty=nameWithType>
- [同期プリミティブの概要](../../../standard/threading/overview-of-synchronization-primitives.md)
