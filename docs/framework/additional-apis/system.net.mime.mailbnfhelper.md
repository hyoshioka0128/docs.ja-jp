---
title: MailbSystem.Net Helper クラス ()
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.Mime.MailBnfHelper
- System.Net.Mime.MailBnfHelper.Ascii7bitMaxValue
- System.Net.Mime.MailBnfHelper.Atext
- System.Net.Mime.MailBnfHelper.CR
- System.Net.Mime.MailBnfHelper.Ctext
- System.Net.Mime.MailBnfHelper.Dot
- System.Net.Mime.MailBnfHelper.EndComment
- System.Net.Mime.MailBnfHelper.LF
- System.Net.Mime.MailBnfHelper.Space
- System.Net.Mime.MailBnfHelper.StartComment
- System.Net.Mime.MailBnfHelper.Tab
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: 86c98726a7886285917b6be8c7631ca1e9e425e6
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84990536"
---
# <a name="mailbnfhelper-class"></a>Mailbnfsd ヘルパークラス

インターネットメッセージ形式の文字列を解析するためのユーティリティメソッドが含まれています。 このクラスは継承できません。

```csharp
internal static class MailBnfHelper
```

> [!WARNING]
> このクラスは内部的なものであり、コードで直接使用するためのものではありません。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでのこのクラスの使用はサポートしていません。

## <a name="ascii7bitmaxvalue-field"></a>Ascii7bitMaxValue フィールド

7ビット Ascii 値の最大値を表します。

```csharp
internal static readonly int Ascii7bitMaxValue
```

## <a name="atext-field"></a>フィールドの入力

アトムで使用できる文字を表します。

```csharp
internal static bool[] Atext
```

## <a name="cr-field"></a>CR フィールド

キャリッジリターン文字を表します。

```csharp
internal static readonly char CR
```

## <a name="ctext-field"></a>Ctext フィールド

コメント内で使用できる文字を表します。

```csharp
internal static bool[] Ctext
```

## <a name="dot-field"></a>ドットフィールド

フルストップ文字 () を表し `.` ます。

```csharp
internal static readonly char Dot
```

## <a name="endcomment-field"></a>EndComment フィールド

コメントの末尾を指定する文字を表します。

```csharp
internal static readonly char EndComment
```

## <a name="lf-field"></a>LF フィールド

ラインフィード文字を表します。

```csharp
internal static readonly char LF
```

## <a name="space-field"></a>スペースフィールド

空白文字を表します。

```csharp
internal static readonly char Space
```

## <a name="startcomment-field"></a>StartComment フィールド

コメントの先頭を指定する文字を表します。

```csharp
internal static readonly char StartComment
```

## <a name="tab-field"></a>タブフィールド

タブ文字を表します。

```csharp
internal static readonly char Tab
```

## <a name="requirements"></a>必要条件

**名前空間:** <xref:System.Net>

**アセンブリ:** システム (System.dll)
