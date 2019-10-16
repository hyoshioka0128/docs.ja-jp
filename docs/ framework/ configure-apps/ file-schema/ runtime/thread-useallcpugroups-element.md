---
title: <Thread_UseAllCpuGroups> 要素
ms.date: 03/30/2017
ms.assetid: d30fe7c5-8469-46e2-b804-e3eec7b24256
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e964f1b2861926803b0449be06cbfd9567ac74a3
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252271"
---
# <a name="thread_useallcpugroups-element"></a>\<Thread_UseAllCpuGroups> 要素

ランタイムによって、すべての CPU グループにマネージド スレッドを分散するかどうかを指定します。

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<runtime>** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<Thread_UseAllCpuGroups >**  

## <a name="syntax"></a>構文

```xml
<Thread_UseAllCpuGroups
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>属性および要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`enabled`|必須の属性です。<br /><br /> ランタイムによって、すべての CPU グループにマネージド スレッドを分散するかどうかを指定します。|

## <a name="enabled-attribute"></a>enabled 属性

|値|説明|
|-----------|-----------------|
|`false`|ランタイムは、複数の CPU グループにマネージド スレッドを分散しません。 既定値です。|
|`true`|コンピューターに複数の cpu グループ[ \<](gccpugroup-element.md)があり、GCCpuGroup > 要素が有効になっている場合、ランタイムは複数の cpu グループにマネージスレッドを分散します。|

### <a name="child-elements"></a>子要素

なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|
|`runtime`|アセンブリのバインディングとガベージ コレクションに関する情報が含まれています。|

## <a name="remarks"></a>Remarks

コンピューターに複数の CPU グループがある場合、この要素を有効にすると、ランタイムは、すべての CPU グループにマネージド スレッドを分散します。 この機能を使用するには、 [ \<GCCpuGroup >](gccpugroup-element.md)要素も有効にする必要があります。これにより、ガベージコレクションがすべての CPU グループに拡張され、ヒープを作成および分散するときにすべてのコアが考慮されます。 [ \<GCCpuGroup >](gccpugroup-element.md)要素を有効にするには、 [ \<gcServer >](gcserver-element.md)要素を有効にする必要があります。 これらの要素が有効でない場合、`<Thread_UseAllCpuGroups>` 要素を有効にしても効力はありません。

## <a name="example"></a>例

次の例は、複数の CPU グループのサポートを有効にする方法を示しています。

```xml
<configuration>
   <runtime>
      <Thread_UseAllCpuGroups enabled="true"/>
      <GCCpuGroup enabled="true"/>
      <gcServer enabled="true"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>関連項目

- [ランタイム設定スキーマ](index.md)
- [構成ファイル スキーマ](../index.md)
- [\<GCCpuGroup > 要素](gccpugroup-element.md)
