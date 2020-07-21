---
title: '方法: コンピューター上に存在するタイム ゾーンを列挙する'
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], enumerating
- enumerating time zones [.NET Framework]
ms.assetid: bb7a42ab-6bd9-4c5c-b734-5546d51f8669
ms.openlocfilehash: 8f1cc9d58bc0f169d458854eac6568caaa4481c7
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286133"
---
# <a name="how-to-enumerate-time-zones-present-on-a-computer"></a>方法: コンピューター上に存在するタイム ゾーンを列挙する

指定されたタイム ゾーンを正しく処理するには、そのタイム ゾーンに関する情報がシステムで使用できる必要があります。 Windows XP および Windows Vista オペレーティングシステムでは、この情報はレジストリに格納されます。 しかし、世界中に存在するタイム ゾーンの合計数は大きいものの、レジストリにはそれらの一部に関する情報しか含まれません。 さらに、レジストリ自体は、内容が意図的に、および誤って変更される可能性がある動的な構造です。 その結果、アプリケーションは、特定のタイム ゾーンがシステムで定義され、使用できると常に想定することができません。 タイム ゾーン情報のアプリケーションを使用する多くのアプリケーションの最初の手順は、必要なタイム ゾーンがローカル システムで使用できるかどうかを判断する、またはタイム ゾーンの一覧をユーザーに提供して選択させることです。 これには、アプリケーションがローカル システムで定義されているタイム ゾーンを列挙する必要があります。

> [!NOTE]
> アプリケーションが、ローカルシステムで定義されていない特定のタイムゾーンの存在に依存している場合は、タイムゾーンに関する情報をシリアル化および逆シリアル化することによって、アプリケーションの存在を確認できます。 タイムゾーンは、アプリケーションユーザーが選択できるように、リストコントロールに追加できます。 詳細については、「[方法: 埋め込みリソースにタイムゾーンを保存](save-time-zones-to-an-embedded-resource.md)する」および「[方法: 埋め込みリソースからタイムゾーンを復元](restore-time-zones-from-an-embedded-resource.md)する」を参照してください。

### <a name="to-enumerate-the-time-zones-present-on-the-local-system"></a>ローカル システムに存在するタイム ゾーンを列挙するには

1. <xref:System.TimeZoneInfo.GetSystemTimeZones%2A?displayProperty=nameWithType> メソッドを呼び出します。 メソッドは、 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> オブジェクトのジェネリックコレクションを返し <xref:System.TimeZoneInfo> ます。 コレクション内のエントリは、プロパティによって並べ替えられ <xref:System.TimeZoneInfo.DisplayName%2A> ます。 次に例を示します。

   [!code-csharp[System.TimeZone2.Concepts#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#1)]
   [!code-vb[System.TimeZone2.Concepts#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#1)]

2. <xref:System.TimeZoneInfo> `foreach` ループ (C# の場合) または... を使用して、コレクション内の個々のオブジェクトを列挙します。 `For Each``Next` ループ (Visual Basic) を実行し、各オブジェクトに対して必要な処理を実行します。 たとえば、次のコードは、 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> <xref:System.TimeZoneInfo> 手順1で返されたオブジェクトのコレクションを列挙し、各タイムゾーンの表示名をコンソールに表示します。

   [!code-csharp[System.TimeZone2.Concepts#12](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#12)]
   [!code-vb[System.TimeZone2.Concepts#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#12)]

### <a name="to-present-the-user-with-a-list-of-time-zones-present-on-the-local-system"></a>ローカルシステム上に存在するタイムゾーンの一覧をユーザーに表示するには

1. <xref:System.TimeZoneInfo.GetSystemTimeZones%2A?displayProperty=nameWithType> メソッドを呼び出します。 メソッドは、 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> オブジェクトのジェネリックコレクションを返し <xref:System.TimeZoneInfo> ます。

2. 手順 1. で返されたコレクションを、 `DataSource` Windows フォームまたは ASP.NET list コントロールのプロパティに割り当てます。

3. <xref:System.TimeZoneInfo>ユーザーが選択したオブジェクトを取得します。

この例は、Windows アプリケーションの図解を示しています。

## <a name="example"></a>例

この例では、システムで定義されているタイムゾーンをリストボックスに表示する Windows アプリケーションを起動します。 この例では、 <xref:System.TimeZoneInfo.DisplayName%2A> ユーザーによって選択されたタイムゾーンオブジェクトのプロパティの値を含むダイアログボックスが表示されます。

[!code-csharp[System.TimeZone2.Concepts#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#2)]
[!code-vb[System.TimeZone2.Concepts#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#2)]

ほとんどのリストコントロール (やコントロールなど) を使用すると、 <xref:System.Windows.Forms.ListBox?displayProperty=nameWithType> <xref:System.Web.UI.WebControls.BulletedList?displayProperty=nameWithType> `DataSource` そのコレクションがインターフェイスを実装している限り、オブジェクト変数のコレクションをそのプロパティに割り当てることができ <xref:System.Collections.IEnumerable> ます。 (ジェネリッククラスはこれを行い <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> ます)。コレクション内の個々のオブジェクトを表示するために、コントロールはそのオブジェクトのメソッドを呼び出して、 `ToString` オブジェクトを表すために使用される文字列を抽出します。 オブジェクトの場合 <xref:System.TimeZoneInfo> 、 `ToString` メソッドは <xref:System.TimeZoneInfo> オブジェクトの表示名 (プロパティの値) を返し <xref:System.TimeZoneInfo.DisplayName%2A> ます。

> [!NOTE]
> リストコントロールはオブジェクトのメソッドを呼び出すため、オブジェクト `ToString` のコレクションを <xref:System.TimeZoneInfo> コントロールに割り当て、各オブジェクトに対してわかりやすい名前をコントロールに表示し、ユーザーが選択したオブジェクトを取得することができ <xref:System.TimeZoneInfo> ます。 これにより、コレクション内の各オブジェクトに対して文字列を抽出し、その文字列をコントロールのプロパティに割り当てられているコレクションに割り当て、 `DataSource` ユーザーが選択した文字列を取得して、この文字列を使用して記述されたオブジェクトを抽出する必要がなくなります。

## <a name="compiling-the-code"></a>コードのコンパイル

この例で必要な要素は次のとおりです。

- 次の名前空間がインポートされます。

  <xref:System>(C# コードの場合)

  <xref:System.Collections.ObjectModel>

## <a name="see-also"></a>関連項目

- [日付、時刻、およびタイム ゾーン](index.md)
- [方法: 埋め込みリソースにタイム ゾーンを保存する](save-time-zones-to-an-embedded-resource.md)
- [方法: 埋め込みリソースからタイム ゾーンを復元する](restore-time-zones-from-an-embedded-resource.md)
