---
title: イベントのデザイン
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- pre-events
- events [.NET Framework], design guidelines
- member design guidelines, events
- event handlers [.NET Framework], event design guidelines
- post-events
- signatures, event handling
ms.assetid: 67b3c6e2-6a8f-480d-a78f-ebeeaca1b95a
ms.openlocfilehash: 852c99b1a41691911f7ae82d3b8104526811757d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289825"
---
# <a name="event-design"></a>イベントのデザイン
イベントは、最も一般的に使用されるコールバックの形式です (フレームワークがユーザーコードを呼び出すことを許可するコンストラクト)。 その他のコールバックメカニズムには、デリゲート、仮想メンバー、およびインターフェイスベースのプラグインを使用するメンバーが含まれます。ユーザビリティ研究からのデータは、開発者の多くが、他のコールバック機構を使用しているよりもイベントを使用した方が快適であることを示しています。 イベントは、Visual Studio と多くの言語に適切に統合されています。

 イベントのグループは2つあることに注意してください。システムの状態が変更される前に発生するイベント (前のイベントと呼ばれます) と、状態の変更後に発生するイベント (ポストイベント) です。 前のイベントの例として `Form.Closing` 、フォームが閉じられる前にが発生します。 ポストイベントの例としては `Form.Closed` 、フォームが閉じられた後に発生するがあります。

 ✔️は、"火災" や "トリガー" ではなく、イベントに "raise" という用語を使用します。

 <xref:System.EventHandler%601?displayProperty=nameWithType>イベントハンドラーとして使用する新しいデリゲートを手動で作成する代わりに、を使用✔️ます。

 イベントがイベント処理メソッドにデータを渡す必要がないことが確実である場合を除き、のサブクラスをイベント引数として使用することを検討してください <xref:System.EventArgs> 。この場合、型を直接使用でき `EventArgs` ます。✔️

 直接を使用して API を出荷する場合 `EventArgs` 、互換性を損なうことなく、イベントに含まれるデータを追加することはできません。 サブクラスを使用する場合、最初は完全に空であっても、必要に応じてサブクラスにプロパティを追加できます。

 ✔️、保護された仮想メソッドを使用して各イベントを発生させることができます。 これは、構造体、シールクラス、または静的イベントではなく、シールされていないクラスの非静的イベントにのみ適用されます。

 メソッドの目的は、派生クラスがオーバーライドを使用してイベントを処理する方法を提供することです。 オーバーライドは、派生クラスの基底クラスのイベントを処理するための、より柔軟で高速で、より自然な方法です。 慣例として、メソッドの名前は "On" で始まり、その後にイベントの名前を指定する必要があります。

 派生クラスは、オーバーライドでメソッドの基本実装を呼び出さないことを選択できます。 基底クラスが正常に動作するために必要なメソッドに処理を含めないで、これを準備してください。

 ✔️は、イベントを発生させるプロテクトメソッドに対して1つのパラメーターを受け取ります。

 パラメーターにはという名前を付け、 `e` イベント引数クラスとして型指定する必要があります。

 ❌非静的イベントを発生させるときに、送信者として null を渡さないでください。

 静的なイベントを発生させるときに、送信者として null を渡す✔️ます。

 ❌イベントの発生時には、イベントデータパラメーターとして null を渡さないでください。

 `EventArgs.Empty`イベント処理メソッドにデータを渡さない場合は、を渡す必要があります。 開発者は、このパラメーターを null にすることを想定していません。

 エンドユーザーがキャンセルできるイベントの発生を✔️検討します。 これは、前のイベントにのみ適用されます。

 <xref:System.ComponentModel.CancelEventArgs?displayProperty=nameWithType>またはそのサブクラスをイベント引数として使用し、エンドユーザーがイベントをキャンセルできるようにします。

### <a name="custom-event-handler-design"></a>カスタムイベントハンドラーのデザイン
 を使用できないケースがあります `EventHandler<T>` 。たとえば、フレームワークが以前のバージョンの CLR を使用する必要があり、そのためにジェネリックがサポートされていない場合などです。 このような場合は、カスタムイベントハンドラーデリゲートの設計と開発が必要になることがあります。

 ✔️は、イベントハンドラーに戻り値の型 void を使用します。

 イベントハンドラーは複数のイベント処理メソッド (場合によっては複数のオブジェクト) を呼び出すことができます。 イベント処理メソッドで値を返すことが許可された場合、イベントの呼び出しごとに複数の戻り値が返されます。

 ✔️は、 `object` イベントハンドラーの最初のパラメーターの型としてを使用し、それを呼び出し `sender` ます。

 <xref:System.EventArgs?displayProperty=nameWithType>イベントハンドラーの2番目のパラメーターの型としてまたはそのサブクラスを使用✔️、それを呼び出し `e` ます。

 ❌イベントハンドラーに2つ以上のパラメーターを含めることはできません。

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [メンバーデザインのガイドライン](member.md)
- [フレームワークデザインのガイドライン](index.md)
