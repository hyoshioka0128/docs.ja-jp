---
title: ローカル システムで定義されているタイム ゾーンの検索
ms.date: 04/10/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- time zones [.NET Framework], local
- time zones [.NET Framework], finding local system time zones
- time zone identifiers [.NET Framework]
- local time zone access
- time zones [.NET Framework], retrieving
- UTC times, finding local system time zones
- time zones [.NET Framework], UTC
ms.assetid: 3f63b1bc-9a4b-4bde-84ea-ab028a80d3e1
ms.openlocfilehash: d313bbed3cc525a74b90537dd4f1742c09c62cd4
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84277025"
---
# <a name="finding-the-time-zones-defined-on-a-local-system"></a>ローカル システムで定義されているタイム ゾーンの検索

<xref:System.TimeZoneInfo> クラスは、パブリック コンストラクターを公開しません。 そのため、`new` キーワードを使用して新しい <xref:System.TimeZoneInfo> オブジェクトを作成することはできません。 <xref:System.TimeZoneInfo> オブジェクトをインスタンス化するには、代わりに、定義済みのタイム ゾーンの情報をレジストリから取得するか、カスタム タイム ゾーンを作成します。 このトピックでは、レジストリに格納されているデータからタイム ゾーンをインスタンス化する方法について説明します。 また、<xref:System.TimeZoneInfo> クラスの `static` (Visual Basic では `shared`) プロパティを使用すると、世界協定時刻 (UTC: Coordinated Universal Time) およびローカル タイム ゾーンにアクセスできます。

> [!NOTE]
> レジストリで定義されていないタイム ゾーンの場合は、<xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> メソッドのオーバーロードを呼び出すことによりカスタム タイム ゾーンを作成できます。 カスタムタイムゾーンの作成については、 [「方法: 調整規則のないタイムゾーンを作成](create-time-zones-without-adjustment-rules.md)する」および[「方法: 調整規則を使用してタイムゾーンを作成する](create-time-zones-with-adjustment-rules.md)」トピックを参考にしてください。 さらに、<xref:System.TimeZoneInfo.FromSerializedString%2A> メソッドを使用して、シリアル化された文字列から復元することにより、<xref:System.TimeZoneInfo> オブジェクトをインスタンス化することもできます。 オブジェクトのシリアル化と逆シリアル化に <xref:System.TimeZoneInfo> ついては、 [「方法: 埋め込みリソースにタイムゾーンを保存](save-time-zones-to-an-embedded-resource.md)する」および[「方法: 埋め込みリソースからタイムゾーンを復元する](restore-time-zones-from-an-embedded-resource.md)」のトピックを参考にしてください。

## <a name="accessing-individual-time-zones"></a>個別のタイムゾーンへのアクセス

<xref:System.TimeZoneInfo> クラスには、UTC 時刻とローカル タイム ゾーンを表す 2 つの定義済みタイム ゾーン オブジェクトがあります。 これらは、それぞれ <xref:System.TimeZoneInfo.Utc%2A> プロパティと <xref:System.TimeZoneInfo.Local%2A> プロパティから取得できます。 UTC またはローカルタイムゾーンにアクセスする方法については、「[方法: 定義済みの utc オブジェクトおよびローカルタイムゾーンオブジェクトにアクセスする](access-utc-and-local.md)」を参照してください。

また、レジストリで定義されているタイム ゾーンを表す <xref:System.TimeZoneInfo> オブジェクトをインスタンス化することもできます。 特定のタイムゾーンオブジェクトをインスタンス化する方法については、「[方法: TimeZoneInfo オブジェクトをインスタンス化](instantiate-time-zone-info.md)する」を参照してください。

## <a name="time-zone-identifiers"></a>タイムゾーン id

タイム ゾーン ID は、タイム ゾーンを一意に識別するキー フィールドです。 ほとんどのキーは比較的短いですが、タイム ゾーン ID はいくぶん長めです。 ほとんどの場合、ID の値は、タイム ゾーンの標準時刻の名前を表すために使用される <xref:System.TimeZoneInfo.StandardName%2A?displayProperty=nameWithType> プロパティに対応します。 ただし、例外もあります。 有効な ID を確実に指定する最良の方法は、システムで使用できるタイム ゾーンを列挙し、それに対応するタイム ゾーン ID を記録することです。

## <a name="see-also"></a>関連項目

- [日付、時刻、およびタイム ゾーン](index.md)
- [方法: 定義済みの UTC オブジェクトおよびローカル タイム ゾーン オブジェクトにアクセスする](access-utc-and-local.md)
- [方法: TimeZoneInfo オブジェクトをインスタンス化する](instantiate-time-zone-info.md)
- [タイムゾーン間での時刻の変換](converting-between-time-zones.md)
