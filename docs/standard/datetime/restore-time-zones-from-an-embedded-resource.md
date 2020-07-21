---
title: '方法: 埋め込みリソースからタイム ゾーンを復元する'
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], deserializing
- time zones [.NET Framework], restoring
ms.assetid: 6b7b4de9-da07-47e3-8f4c-823f81798ee7
ms.openlocfilehash: b1cece13c88b3a49c9c4c90045a07dd009d4282d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84281324"
---
# <a name="how-to-restore-time-zones-from-an-embedded-resource"></a>方法: 埋め込みリソースからタイム ゾーンを復元する

このトピックでは、リソースファイルに保存されているタイムゾーンを復元する方法について説明します。 タイムゾーンの保存に関する情報および手順については、「[方法: 埋め込みリソースにタイムゾーンを保存する](save-time-zones-to-an-embedded-resource.md)」を参照してください。

### <a name="to-deserialize-a-timezoneinfo-object-from-an-embedded-resource"></a>埋め込みリソースから TimeZoneInfo オブジェクトを逆シリアル化するには

1. 取得するタイムゾーンがカスタムタイムゾーンでない場合は、メソッドを使用してインスタンス化し <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> ます。

2. <xref:System.Resources.ResourceManager>埋め込みリソースファイルの完全修飾名と、リソースファイルを含むアセンブリへの参照を渡すことによって、オブジェクトをインスタンス化します。

   埋め込まれたリソースファイルの完全修飾名を特定できない場合は、 [ildasm.exe (IL 逆アセンブラー)](../../framework/tools/ildasm-exe-il-disassembler.md)を使用して、アセンブリのマニフェストを確認します。 `.mresource`リソースを識別するエントリ。 この例では、リソースの完全修飾名は `SerializeTimeZoneData.SerializedTimeZones` です。

   リソースファイルが、タイムゾーンのインスタンス化コードを含む同じアセンブリに埋め込まれている場合は、 `static` (Visual Basic) メソッドを呼び出すことによって、そのファイルへの参照を取得でき `Shared` <xref:System.Reflection.Assembly.GetExecutingAssembly%2A> ます。

3. メソッドの呼び出しが失敗した場合 <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> 、またはカスタムタイムゾーンをインスタンス化する場合は、メソッドを呼び出して、シリアル化されたタイムゾーンを含む文字列を取得し <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=nameWithType> ます。

4. メソッドを呼び出してタイムゾーンデータを逆シリアル化し <xref:System.TimeZoneInfo.FromSerializedString%2A> ます。

## <a name="example"></a>例

次の例では、 <xref:System.TimeZoneInfo> 埋め込み .NET XML リソースファイルに格納されているオブジェクトを逆シリアル化します。

[!code-csharp[TimeZone2.Serialization#3](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#3)]
[!code-vb[TimeZone2.Serialization#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#3)]

このコード <xref:System.TimeZoneInfo> は、アプリケーションに必要なオブジェクトが存在することを確認するための例外処理を示しています。 まず、 <xref:System.TimeZoneInfo> メソッドを使用してレジストリからオブジェクトを取得することによって、オブジェクトのインスタンス化を試み <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> ます。 タイムゾーンをインスタンス化できない場合、コードは埋め込みリソースファイルからタイムゾーンを取得します。

カスタムタイムゾーン (メソッドを使用してインスタンス化されたタイムゾーン) のデータはレジストリに格納されないため、コードはを <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 呼び出して、 <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> 南極のタイムゾーンをインスタンス化しません。 代わりに、埋め込みリソースファイルをすぐに検索して、メソッドを呼び出す前にタイムゾーンのデータを含む文字列を取得し <xref:System.TimeZoneInfo.FromSerializedString%2A> ます。

## <a name="compiling-the-code"></a>コードのコンパイル

この例で必要な要素は次のとおりです。

- このプロジェクトには、System. .dll と system.servicemodel への参照を追加する必要があります。

- 次の名前空間がインポートされます。

  [!code-csharp[TimeZone2.Serialization#2](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#2)]
  [!code-vb[TimeZone2.Serialization#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#2)]

## <a name="see-also"></a>関連項目

- [日付、時刻、およびタイム ゾーン](index.md)
- [タイム ゾーンの概要](time-zone-overview.md)
- [方法: 埋め込みリソースにタイム ゾーンを保存する](save-time-zones-to-an-embedded-resource.md)
