---
title: '方法: 定義済みの UTC オブジェクトおよびローカル タイム ゾーン オブジェクトにアクセスする'
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], local
- predefined time zones
- UTC times, predefined
- local time zone access
- time zones [.NET Framework], retrieving
- time zones [.NET Framework], UTC
ms.assetid: 961fb70b-83f0-4dab-a042-cb5fcd817cf5
ms.openlocfilehash: ebb07800b2a35f4faf312dc55b8c5679079b4b68
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291410"
---
# <a name="how-to-access-the-predefined-utc-and-local-time-zone-objects"></a>方法: 定義済みの UTC オブジェクトおよびローカル タイム ゾーン オブジェクトにアクセスする

<xref:System.TimeZoneInfo>クラスには、とという2つのプロパティが用意されており、これにより、 <xref:System.TimeZoneInfo.Utc%2A> <xref:System.TimeZoneInfo.Local%2A> 定義済みのタイムゾーンオブジェクトにコードからアクセスできるようになります。 このトピックでは、これらのプロパティから返される <xref:System.TimeZoneInfo> オブジェクトにアクセスする方法について説明します。

### <a name="to-access-the-coordinated-universal-time-utc-timezoneinfo-object"></a>世界協定時刻 (UTC) の TimeZoneInfo オブジェクトにアクセスするには

1. `static`( `Shared` Visual Basic) プロパティを使用して、 <xref:System.TimeZoneInfo.Utc%2A?displayProperty=nameWithType> 協定世界時にアクセスします。

2. <xref:System.TimeZoneInfo>プロパティによって返されたオブジェクトをオブジェクト変数に割り当てるのではなく、プロパティを使用して世界協定時刻にアクセスし続け <xref:System.TimeZoneInfo.Utc%2A?displayProperty=nameWithType> ます。

### <a name="to-access-the-local-time-zone"></a>ローカル タイム ゾーンにアクセスするには

1. `static` `Shared` <xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> ローカルシステムのタイムゾーンにアクセスするには、(Visual Basic) プロパティを使用します。

2. <xref:System.TimeZoneInfo>プロパティによって返されたオブジェクトをオブジェクト変数に割り当てるのではなく、引き続きプロパティを使用してローカルタイムゾーンにアクセスし <xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> ます。

## <a name="example"></a>例

次のコードでは、 <xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> プロパティとプロパティを使用し <xref:System.TimeZoneInfo.Utc%2A?displayProperty=nameWithType> て、米国およびカナダ東部標準時のタイムゾーンから時刻を変換し、タイムゾーン名をコンソールに表示します。

[!code-csharp[System.TimeZone2.Concepts#13](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#13)]
[!code-vb[System.TimeZone2.Concepts#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#13)]

ローカルタイムゾーンは、 <xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> ローカルタイムゾーンをオブジェクト変数に割り当てるのではなく、常にプロパティを使用してアクセスする必要があり <xref:System.TimeZoneInfo> ます。 同様に、 <xref:System.TimeZoneInfo.Utc%2A?displayProperty=nameWithType> UTC ゾーンをオブジェクト変数に割り当てるのではなく、常にプロパティを使用して世界協定時刻にアクセスする必要があり <xref:System.TimeZoneInfo> ます。 これにより、 <xref:System.TimeZoneInfo> メソッドの呼び出しによってオブジェクト変数が無効になるのを防ぐことができ <xref:System.TimeZoneInfo.ClearCachedData%2A?displayProperty=nameWithType> ます。

## <a name="compiling-the-code"></a>コードのコンパイル

この例で必要な要素は次のとおりです。

- <xref:System> `using` ステートメント (C# コードでは必須) を使用して名前空間をインポートする。

## <a name="see-also"></a>関連項目

- [日付、時刻、およびタイム ゾーン](index.md)
- [ローカル システムで定義されているタイム ゾーンの検索](finding-the-time-zones-on-local-system.md)
- [方法: TimeZoneInfo オブジェクトをインスタンス化する](instantiate-time-zone-info.md)
