---
title: 例外とパフォーマンス
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- tester-doer pattern
- TryParse pattern
- exceptions, throwing
- exceptions, performance
- throwing exceptions, performance
ms.assetid: 3ad6aad9-08e6-4232-b336-0e301f2493e6
ms.openlocfilehash: a558547f0e6770e7e76ca31f760d6e2f55c712db
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289786"
---
# <a name="exceptions-and-performance"></a>例外とパフォーマンス
例外に関する一般的な懸念事項の1つとして、定期的に失敗するコードに例外を使用すると、実装のパフォーマンスが許容されなくなることがあります。 これは有効な問題です。 メンバーが例外をスローすると、パフォーマンスが低下することがあります。 ただし、エラーコードの使用を禁止する例外ガイドラインに厳密に準拠しながら、パフォーマンスを向上させることができます。 このセクションで説明する2つのパターンは、この方法を示しています。

 ❌エラーコードは、例外がパフォーマンスに悪影響を与える可能性があるため、使用しないでください。

 パフォーマンスを向上させるために、次の2つのセクションで説明するように、テスト担当者またはテスト用のパターンを使用することができます。

## <a name="tester-doer-pattern"></a>テスト担当者-Doer パターン
 メンバーを2つに分割すると、例外スローメンバーのパフォーマンスを向上させることができます。 では、インターフェイスのメソッドを見てみましょう <xref:System.Collections.Generic.ICollection%601.Add%2A> <xref:System.Collections.Generic.ICollection%601> 。

```csharp
ICollection<int> numbers = ...
numbers.Add(1);
```

 コレクションが読み取り専用の場合、メソッドはを `Add` スローします。 これは、メソッドの呼び出しが頻繁に失敗することが予想されるシナリオでパフォーマンスの問題になる可能性があります。 問題を軽減する方法の1つは、値を追加する前に、コレクションが書き込み可能かどうかをテストすることです。

```csharp
ICollection<int> numbers = ...
...
if (!numbers.IsReadOnly)
{
    numbers.Add(1);
}
```

 条件をテストするために使用されるメンバー (この例ではプロパティ) は、テスト `IsReadOnly` 担当者と呼ばれています。 スローされる可能性のある操作を実行するために使用するメンバーは、この `Add` 例のメソッドを doer と呼びます。

 ✔️、例外に関連するパフォーマンスの問題を回避するために、一般的なシナリオで例外をスローする可能性のあるメンバーに対してテスト担当者のパターンを検討してください。

## <a name="try-parse-pattern"></a>Try 解析パターン
 パフォーマンスが非常に重要な Api では、前のセクションで説明したテスト担当者のパターンよりも高速なパターンを使用する必要があります。 このパターンでは、メンバー名を調整して、適切に定義されたテストケースをメンバーセマンティクスの一部にするためのを呼び出します。 たとえば、は、 <xref:System.DateTime> <xref:System.DateTime.Parse%2A> 文字列の解析が失敗した場合に例外をスローするメソッドを定義します。 また、解析を試行する対応するメソッドも定義 <xref:System.DateTime.TryParse%2A> しますが、解析が失敗した場合は false を返し、パラメーターを使用して解析の成功の結果を返し `out` ます。

```csharp
public struct DateTime
{
    public static DateTime Parse(string dateTime)
    {
        ...
    }
    public static bool TryParse(string dateTime, out DateTime result)
    {
        ...
    }
}
```

 このパターンを使用する場合は、厳密な用語で try 機能を定義することが重要です。 明確に定義された try 以外の理由でメンバーが失敗した場合でも、メンバーは対応する例外をスローする必要があります。

 ✔️、例外に関連するパフォーマンスの問題を回避するために、一般的なシナリオで例外をスローする可能性のあるメンバーのために、Try 解析パターンを検討してください。

 このパターンを実装するメソッドには、"Try" というプレフィックスとブール型の戻り値の型を使用✔️ます。

 ✔️、Try 解析パターンを使用して、メンバーごとに例外スローメンバーを提供します。

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [フレームワークデザインのガイドライン](index.md)
- [例外のデザインのガイドライン](exceptions.md)
