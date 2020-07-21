---
title: イベントとコールバック
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- events [.NET Framework], extensibility
- methods [.NET Framework], callback
- callback methods
- callbacks
ms.assetid: 48b55c60-495f-4089-9396-97f9122bba7c
ms.openlocfilehash: 4000944c3b913f71bc18462cea9062e9237ae53f
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619534"
---
# <a name="events-and-callbacks"></a>イベントとコールバック
コールバックは、フレームワークがデリゲートを通じてユーザーコードにコールバックすることを可能にする拡張ポイントです。 これらのデリゲートは、通常、メソッドのパラメーターを使用してフレームワークに渡されます。

 イベントは、デリゲート (イベントハンドラー) を提供するための便利で一貫性のある構文をサポートする、特殊なコールバックのケースです。 さらに、Visual Studio のステートメント入力候補とデザイナーは、イベントベースの Api の使用に関するヘルプを提供します。 (「[イベントの設計](event.md)」を参照してください)。

 ✔️コールバックを使用して、ユーザーがフレームワークによって実行されるカスタムコードを提供できるようにすることを検討してください。

 ✔️イベントを使用して、ユーザーがオブジェクト指向設計を理解しなくても、フレームワークの動作をカスタマイズできるようにすることを検討してください。

 ✔️は、より幅広い開発者を対象とし、Visual Studio のステートメント入力候補と統合されるため、プレーンコールバックでイベントを優先します。

 ❌パフォーマンスを重視する Api ではコールバックを使用しないでください。

 `Func<...>` `Action<...>` `Expression<...>` コールバックを使用して api を定義するときは、カスタムデリゲートではなく、新しい型、型、または型を使用✔️ます。

 `Func<...>`とは `Action<...>` 汎用デリゲートを表します。 `Expression<...>`コンパイル後に実行時に呼び出すことができる関数定義を表しますが、シリアル化してリモートプロセスに渡すこともできます。

 とデリゲートを使用する代わりに、を使用してパフォーマンスへの影響を測定し、理解する✔️ `Expression<...>` `Func<...>` `Action<...>` ます。

 `Expression<...>`型は、ほとんどの場合 `Func<...>` 、とデリゲートと論理的に等価です `Action<...>` 。 これらの主な違いは、デリゲートはローカルプロセスシナリオで使用することを意図していることです。式は、リモートのプロセスまたはコンピューターで式を評価することが有益であるケースを対象としています。

 デリゲートを呼び出すことによって、任意のコードを実行し、セキュリティ、正確性、および互換性の影響を与える可能性があることを✔️理解することができます。

 *部分 &copy; 2005、2009 Microsoft Corporation。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [機能拡張のデザイン](designing-for-extensibility.md)
- [フレームワークデザインのガイドライン](index.md)
