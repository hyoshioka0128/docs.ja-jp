---
title: GCNoAffinitize 要素
ms.date: 11/08/2019
helpviewer_keywords:
- gcNoAffinitize element
- <gcNoAffinitize> element
ms.openlocfilehash: 16d6e5adefe2b632d7251669650058d7df7cea70
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "84004739"
---
# <a name="gcnoaffinitize-element"></a>\<GCNoAffinitize> 要素

Cpu を使用してサーバー GC スレッドを関係付けするかどうかを指定します。

\<configuration>\
&nbsp;&nbsp;\<runtime>\
&nbsp;&nbsp;&nbsp;&nbsp;\<GCNoAffinitize>

## <a name="syntax"></a>構文

```xml
<GCNoAffinitize
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>属性と要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`enabled`|必須の属性です。<br /><br />サーバー GC スレッド/ヒープをコンピューターで使用可能なプロセッサと関連付けるかどうかを指定します。|

#### <a name="enabled-attribute"></a>enabled 属性

|値|Description|
|-----------|-----------------|
|`false`|アフィニティ化する server GC スレッドと Cpu。 既定値です。|
|`true`|では、Cpu を使用してサーバー GC スレッドを関係付けません。|

### <a name="child-elements"></a>子要素

なし。

### <a name="parent-elements"></a>親要素

|要素|Description|
|-------------|-----------------|
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|
|`runtime`|アセンブリのバインディングとガベージ コレクションに関する情報が含まれています。|

## <a name="remarks"></a>解説

既定では、サーバー GC スレッドはそれぞれの Cpu とハード関係があります。 システムの使用可能な各プロセッサには、独自の GC ヒープとスレッドがあります。 これは、キャッシュの使用を最適化するため、通常は推奨される設定です。 4.6.2 .NET Framework 以降では、 **GCNoAffinitize**要素の属性をに設定することにより、 `enabled` `true` サーバー GC スレッドと cpu を密に結合しないように指定できます。

Cpu を使用してサーバー GC スレッドを関係付けしないように、 **GCNoAffinitize**構成要素のみを指定できます。 また、アプリケーションで使用される GC ヒープとスレッドの数を制御するために、この要素を[Gの Apcount](gcheapcount-element.md)要素と共に使用することもできます。

`enabled` **GCNoAffinitize**要素の属性が `false` (既定値) の場合は、 [g apcount](gcheapcount-element.md)要素を使用して gc スレッドとヒープの数を指定することもできます。また、 [GCHEAPAFFINITIZEMASK](gcheapaffinitizemask-element.md)要素を使用して、gc スレッドとヒープが関連付けられているプロセッサを指定することもできます。

## <a name="example"></a>例

次の例では、サーバー GC スレッドをハード関係付けしていません。

```xml
<configuration>
   <runtime>
      <gcServer enabled="true"/>
      <GCNoAffinitize enabled="true"/>
   </runtime>
</configuration>
```

次の例では、サーバー GC スレッドを関係付けせず、GC ヒープ/スレッドの数を10に制限しています。

```xml
<configuration>
   <runtime>
      <gcServer enabled="true"/>
      <GCHeapCount enabled="10"/>
      <GCNoAffinitize enabled="true"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>関連項目

- <xref:System.Runtime.GCSettings.IsServerGC%2A?displayProperty=nameWithType>
- [GCHeapAffinitizeMask 要素](gcheapaffinitizemask-element.md)
- [G不正 Apcount 要素](gcheapcount-element.md)
- [ガベージ コレクションの基礎](../../../../standard/garbage-collection/fundamentals.md)
- [ランタイム設定スキーマ](index.md)
- [構成ファイル スキーマ](../index.md)
