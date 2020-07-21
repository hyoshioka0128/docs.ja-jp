---
title: Mailaddressparc Ser クラス (System.Net)
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.Mail.MailAddressParser
- System.Net.Mail.MailAddressParser.ParseAddress
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: ff83f6946539fa262ccde980052627f98c75601d
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051351"
---
# <a name="mailaddressparser-class"></a>MailAddressParser クラス

RFC 2822 で説明されているように、電子メールアドレスを解析します。 このクラスは継承できません。

```csharp
internal static class MailAddressParser
```

> [!WARNING]
> このクラスは内部的なものであり、コードで直接使用するためのものではありません。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでのこのクラスの使用はサポートしていません。

## <a name="parseaddress-method"></a>ParseAddress メソッド

指定した文字列から1つの電子メールアドレスを解析します。

```csharp
internal static MailAddress ParseAddress(string data)
```

### <a name="parameters"></a>パラメーター

`data` <xref:System.String>

解析する電子メールアドレスを含む文字列。

### <a name="return-value"></a>戻り値

<xref:System.Net.Mail.MailAddress>

有効な電子メールアドレス。

### <a name="exceptions"></a>例外

<xref:System.FormatException?displayProperty=nameWithType>

電子メールアドレスが無効です。

## <a name="requirements"></a>必要条件

**名前空間:** <xref:System.Net>

**アセンブリ:** システム (System.dll)
