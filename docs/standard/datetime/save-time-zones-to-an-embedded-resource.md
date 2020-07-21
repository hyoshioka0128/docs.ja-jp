---
title: '方法: 埋め込みリソースにタイム ゾーンを保存する'
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], saving
- time zone objects [.NET Framework], serializing
- time zone objects [.NET Framework], saving
ms.assetid: 3c96d83a-a057-4496-abb0-8f4b12712558
ms.openlocfilehash: c8084cb8edff64b9d598f4fd0a62a362491c7aa7
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84281246"
---
# <a name="how-to-save-time-zones-to-an-embedded-resource"></a>方法: 埋め込みリソースにタイム ゾーンを保存する

タイムゾーンに対応するアプリケーションでは、多くの場合、特定のタイムゾーンが存在する必要があります。 ただし、個々のオブジェクトの可用性は、 <xref:System.TimeZoneInfo> ローカルシステムのレジストリに格納されている情報によって異なるため、通常使用可能なタイムゾーンも存在しない可能性があります。 また、メソッドを使用してインスタンス化されたカスタムタイムゾーンに関する情報 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> は、他のタイムゾーン情報と共にレジストリに格納されるわけではありません。 これらのタイムゾーンが必要なときに確実に使用できるようにするには、それらをシリアル化して保存し、後でそれらを逆シリアル化して復元します。

通常、オブジェクトのシリアル化は、 <xref:System.TimeZoneInfo> タイムゾーン対応アプリケーションとは別に行われます。 シリアル化されたオブジェクトを保持するために使用するデータストアに応じて <xref:System.TimeZoneInfo> 、タイムゾーンデータは、セットアップまたはインストールルーチンの一部としてシリアル化できます (たとえば、データがレジストリのアプリケーションキーに格納されている場合)。または、最終的なアプリケーションをコンパイルする前に実行されるユーティリティルーチンの一部としてシリアル化されます (たとえば、シリアル化されたデータが .NET XML リソース (.resx) ファイル

アプリケーションと共にコンパイルされるリソースファイルに加えて、他のいくつかのデータストアをタイムゾーン情報に使用できます。 次に例を示します。

- レジストリ。 アプリケーションでは、独自のアプリケーションキーのサブキーを使用して、HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones のサブキーを使用するのではなく、カスタムタイムゾーンデータを格納する必要があることに注意してください。

- 構成ファイル。

- その他のシステムファイル。

### <a name="to-save-a-time-zone-by-serializing-it-to-a-resx-file"></a>.Resx ファイルにシリアル化してタイムゾーンを保存するには

1. 既存のタイムゾーンを取得するか、新しいタイムゾーンを作成します。

   既存のタイムゾーンを取得する方法については、「[方法: 定義済みの UTC オブジェクトおよびローカルタイムゾーンオブジェクトにアクセス](access-utc-and-local.md)する」および「[方法: TimeZoneInfo オブジェクトをインスタンス化](instantiate-time-zone-info.md)する」を参照してください。

   新しいタイムゾーンを作成するには、メソッドのいずれかのオーバーロードを呼び出し <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> ます。 詳細については、「[方法: 調整規則のないタイムゾーンを作成](create-time-zones-without-adjustment-rules.md)する」および「[方法: 調整規則を使用してタイムゾーンを作成する](create-time-zones-with-adjustment-rules.md)」を参照してください。

2. メソッドを呼び出し <xref:System.TimeZoneInfo.ToSerializedString%2A> て、タイムゾーンのデータを含む文字列を作成します。

3. <xref:System.IO.StreamWriter>名前を指定し、必要に応じてクラスコンストラクターに .resx ファイルのパスを指定して、オブジェクトをインスタンス化 <xref:System.IO.StreamWriter> します。

4. オブジェクトを <xref:System.Resources.ResXResourceWriter> クラスコンストラクターに渡すことによって、オブジェクトをインスタンス化 <xref:System.IO.StreamWriter> <xref:System.Resources.ResXResourceWriter> します。

5. タイムゾーンのシリアル化された文字列をメソッドに渡し <xref:System.Resources.ResXResourceWriter.AddResource%2A?displayProperty=nameWithType> ます。

6. <xref:System.Resources.ResXResourceWriter.Generate%2A?displayProperty=nameWithType> メソッドを呼び出します。

7. <xref:System.Resources.ResXResourceWriter.Close%2A?displayProperty=nameWithType> メソッドを呼び出します。

8. <xref:System.IO.StreamWriter>メソッドを呼び出して、オブジェクトを閉じ <xref:System.IO.StreamWriter.Close%2A> ます。

9. 生成された .resx ファイルをアプリケーションの Visual Studio プロジェクトに追加します。

10. Visual Studio の [**プロパティ**] ウィンドウを使用して、.resx ファイルの [**ビルドアクション**] プロパティが [**埋め込みリソース**] に設定されていることを確認します。

## <a name="example"></a>例

次の例では、中部標準時を表すオブジェクトをシリアル化し、 <xref:System.TimeZoneInfo> <xref:System.TimeZoneInfo> SerializedTimeZones という名前の .net XML リソースファイルの南極 Time を表すオブジェクトをシリアル化します。 通常、中部標準時はレジストリで定義されています。パーマーステーション、南極はカスタムタイムゾーンです。

[!code-csharp[TimeZone2.Serialization#1](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#1)]
[!code-vb[TimeZone2.Serialization#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#1)]

この例で <xref:System.TimeZoneInfo> は、コンパイル時にリソースファイルで使用できるようにオブジェクトをシリアル化します。

メソッドは、 <xref:System.Resources.ResXResourceWriter.Generate%2A?displayProperty=nameWithType> 完全なヘッダー情報を .NET XML リソースファイルに追加するため、既存のファイルにリソースを追加するために使用することはできません。 この例では、SerializedTimeZones ファイルを確認し、存在する場合は、2つのシリアル化されたタイムゾーン以外のすべてのリソースを汎用オブジェクトに格納することで、この処理を行い <xref:System.Collections.Generic.Dictionary%602> ます。 その後、既存のファイルが削除され、既存のリソースが新しい SerializedTimeZones ファイルに追加されます。 シリアル化されたタイムゾーンデータもこのファイルに追加されます。

リソースのキー (または**名前**) フィールドには、空白を埋め込むことはできません。 <xref:System.String.Replace%28System.String%2CSystem.String%29>メソッドは、リソースファイルに割り当てられる前に、タイムゾーン識別子内のすべての埋め込みスペースを削除するために呼び出されます。

## <a name="compiling-the-code"></a>コードのコンパイル

この例で必要な要素は次のとおりです。

- このプロジェクトには、System. .dll と system.servicemodel への参照を追加する必要があります。

- 次の名前空間がインポートされます。

  [!code-csharp[TimeZone2.Serialization#2](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#2)]
  [!code-vb[TimeZone2.Serialization#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#2)]

## <a name="see-also"></a>関連項目

- [日付、時刻、およびタイム ゾーン](index.md)
- [タイム ゾーンの概要](time-zone-overview.md)
- [方法: 埋め込みリソースからタイム ゾーンを復元する](restore-time-zones-from-an-embedded-resource.md)
