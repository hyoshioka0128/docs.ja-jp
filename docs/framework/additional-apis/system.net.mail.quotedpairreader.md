---
title: QuotedPairReader クラス (System.Net)
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.Mail.QuotedPairReader
- System.Net.Mail.QuotedPairReader.CountQuotedChars
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: 898c6e9d2d5dd02f3d5f9c096ad470b5dd445d1d
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051312"
---
# <a name="quotedpairreader-class"></a>QuotedPairReader クラス

引用符で囲まれた文字列で引用符で囲まれた文字 (エスケープ) を決定します。 このクラスは継承できません。

```csharp
internal static class QuotedPairReader
```

> [!WARNING]
> このクラスは内部的なものであり、コードで直接使用するためのものではありません。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでのこのクラスの使用はサポートしていません。

## <a name="countquotedchars-method"></a>CountQuotedChars メソッド

指定した文字列に含まれる、前に引用符で囲まれた複数の円記号を含む、連続する引用符で囲まれた文字の数をカウントします。 たとえば、文字列とのインデックスを指定した場合、メソッドはを `a\\\b` `4` 返します。これは、 `4` `b` が引用符で囲まれており、その前に3つの円記号があるためです。

```csharp
internal static int CountQuotedChars(string data, int index, bool permitUnicodeEscaping)
```

### <a name="parameters"></a>パラメーター

- `data` <xref:System.String>

  連続する引用符で囲まれた文字をカウントするデータ文字列。

- `index` <xref:System.Int32>

  連続する引用符で囲まれた文字を含む、指定した文字列内の位置。

- `permitUnicodeEscaping` <xref:System.Boolean>

  `true`Unicode 文字のエスケープを許可するにはそれ以外の場合は `false` 。

### <a name="return-value"></a>戻り値

<xref:System.Int32?displayProperty=nameWithType>

`0`指定したインデックス位置にある文字がエスケープされない場合は。それ以外の場合は、の文字を含む、連続する引用符で囲まれた文字の数 `index` 。

### <a name="exceptions"></a>例外

<xref:System.FormatException?displayProperty=nameWithType>

エスケープされた Unicode 文字が見つかりましたが、許可されていません。

## <a name="requirements"></a>必要条件

**名前空間:** <xref:System.Net>

**アセンブリ:** システム (System.dll)
