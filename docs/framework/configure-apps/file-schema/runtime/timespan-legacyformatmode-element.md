---
title: <TimeSpan_LegacyFormatMode> 要素
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- <TimeSpan_LegacyFormatMode> element
- TimeSpan_LegacyFormatMode element
ms.assetid: 865e7207-d050-4442-b574-57ea29d5e2d6
ms.openlocfilehash: 9d9eedf52f5d711412e4549e39e6ea23abb68ff3
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "73968908"
---
# <a name="timespan_legacyformatmode-element"></a>\<TimeSpan_LegacyFormatMode> 要素

値を使用して、ランタイムが書式設定操作で従来の動作を保持するかどうかを決定し <xref:System.TimeSpan?displayProperty=nameWithType> ます。

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<TimeSpan_LegacyFormatMode>**  

## <a name="syntax"></a>構文

```xml
<TimeSpan_LegacyFormatMode
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>属性および要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`enabled`|必須の属性です。<br /><br /> ランタイムが従来の書式設定動作を値と共に使用するかどうかを指定し <xref:System.TimeSpan?displayProperty=nameWithType> ます。|

## <a name="enabled-attribute"></a>enabled 属性

|値|Description|
|-----------|-----------------|
|`false`|ランタイムでは、従来の書式設定動作は復元されません。|
|`true`|ランタイムは、従来の書式設定動作を復元します。|

### <a name="child-elements"></a>子要素

なし。

### <a name="parent-elements"></a>親要素

|要素|Description|
|-------------|-----------------|
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|
|`runtime`|ランタイム初期化オプションに関する情報を含んでいます。|

## <a name="remarks"></a>解説

.NET Framework 4 以降では、 <xref:System.TimeSpan?displayProperty=nameWithType> 構造体はインターフェイスを実装 <xref:System.IFormattable> し、標準およびカスタムの書式指定文字列を使用した書式設定操作をサポートします。 解析メソッドで、サポートされていない書式指定子または書式指定文字列が検出されると、がスローさ <xref:System.FormatException> れます。

以前のバージョンの .NET Framework では、構造体がを実装しておらず、 <xref:System.TimeSpan> <xref:System.IFormattable> 書式指定文字列をサポートしていませんでした。 しかし、多くの開発者は、 <xref:System.TimeSpan> 書式指定文字列のセットをサポートし、などのメソッドを使用して[複合書式指定操作](../../../../standard/base-types/composite-formatting.md)で使用したことを誤って想定していました <xref:System.String.Format%2A?displayProperty=nameWithType> 。 通常、型がを実装 <xref:System.IFormattable> し、書式指定文字列をサポートする場合、サポートされていない書式指定文字列を使用した書式指定メソッドの呼び出しは、通常、をスロー <xref:System.FormatException> します。 ただし、が <xref:System.TimeSpan> 実装されていないため、 <xref:System.IFormattable> ランタイムは書式指定文字列を無視し、代わりにメソッドを呼び出しました <xref:System.TimeSpan.ToString?displayProperty=nameWithType> 。 これは、書式指定文字列が書式設定操作に影響を与えないことを意味しますが、その存在はになりませんでした <xref:System.FormatException> 。

レガシコードによって複合書式指定メソッドと無効な書式指定文字列が渡され、そのコードを再コンパイルできない場合は、要素を使用して `<TimeSpan_LegacyFormatMode>` 従来の動作を復元でき <xref:System.TimeSpan> ます。 `enabled`この要素の属性をに設定すると、 `true` 複合書式指定メソッドによってではなくが呼び出され、 <xref:System.TimeSpan.ToString?displayProperty=nameWithType> がスローされ <xref:System.TimeSpan.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> <xref:System.FormatException> ません。

## <a name="example"></a>例

次の例では、オブジェクトをインスタンス化 <xref:System.TimeSpan> し、 <xref:System.String.Format%28System.String%2CSystem.Object%29?displayProperty=nameWithType> サポートされていない標準書式指定文字列を使用して、メソッドを使用して書式設定を試みます。

[!code-csharp[TimeSpan.BreakingChanges#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/timespan.breakingchanges/cs/legacyformatmode1.cs#1)]
[!code-vb[TimeSpan.BreakingChanges#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/timespan.breakingchanges/vb/legacyformatmode1.vb#1)]

.NET Framework 3.5 またはそれ以前のバージョンでこの例を実行すると、次の出力が表示されます。

```console
12:30:45
```

これは、.NET Framework 4 以降のバージョンで例を実行した場合の出力とは大きく異なります。

```console
Invalid Format
```

ただし、次の構成ファイルを例のディレクトリに追加した後、.NET Framework 4 以降のバージョンでこの例を実行すると、出力は、.NET Framework 3.5 で実行されたときに例で生成されたものと同じになります。

```xml
<?xml version ="1.0"?>
<configuration>
   <runtime>
      <TimeSpan_LegacyFormatMode enabled="true"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>関連項目

- [ランタイム設定スキーマ](index.md)
- [構成ファイル スキーマ](../index.md)
