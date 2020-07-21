---
title: <requiredRuntime> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#requiredRuntime
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup/requiredRuntime
helpviewer_keywords:
- requiredRuntime element
- <requiredRuntime> element
- container tags, <requiredRuntime> element
ms.assetid: 9fa1639e-beb8-43be-b7a4-12f7b229c34b
ms.openlocfilehash: fe96673b95f48cb75d36662a680bf56a59363f9f
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "71697495"
---
# <a name="requiredruntime-element"></a>\<requiredRuntime> 要素

バージョン 1.0 の共通言語ランタイムのみがアプリケーションでサポートされることを指定します。 この要素は非推奨とされ、使用できなくなります。 [`supportedRuntime`](supportedruntime-element.md)代わりに、要素を使用してください。

[**\<configuration>**](../configuration-element.md)  
&nbsp;&nbsp;[**\<startup>**](startup-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp;**\<requiredRuntime>**  

## <a name="syntax"></a>構文

```xml
   <requiredRuntime  
version="runtime version"
safemode="true|false"/>
```

## <a name="attributes-and-elements"></a>属性と要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`version`|省略可能な属性です。<br /><br /> このアプリケーションでサポートされている .NET Framework のバージョンを指定する文字列値。 文字列値は、.NET Framework のインストールルートの下にあるディレクトリ名と一致する必要があります。 文字列値の内容は解析されません。|
|`safemode`|省略可能な属性です。<br /><br /> ランタイムスタートアップコードがレジストリを検索してランタイムバージョンを確認するかどうかを指定します。|

## <a name="safemode-attribute"></a>セーフ属性

|値|Description|
|-----------|-----------------|
|`false`|ランタイムスタートアップコードによって、レジストリが検索されます。 これが既定値です。|
|`true`|ランタイムスタートアップコードでは、レジストリが検索されません。|

### <a name="child-elements"></a>子要素

なし。

### <a name="parent-elements"></a>親要素

|要素|Description|
|-------------|-----------------|
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|
|`startup`|要素が含まれてい `<requiredRuntime>` ます。|

## <a name="remarks"></a>解説
 ランタイムのバージョン1.0 のみをサポートするようにビルドされたアプリケーションでは、要素を使用する必要があり `<requiredRuntime>` ます。 ランタイムのバージョン1.1 以降を使用してビルドされたアプリケーションでは、要素を使用する必要があり `<supportedRuntime>` ます。

> [!NOTE]
> [Corbindtoruntimebycfg](../../../unmanaged-api/hosting/corbindtoruntimebycfg-function.md)関数を使用して構成ファイルを指定する場合は、すべてのバージョンのランタイムで要素を使用する必要があり `<requiredRuntime>` ます。 `<supportedRuntime>` [Corbindtoruntimebycfg](../../../unmanaged-api/hosting/corbindtoruntimebycfg-function.md)を使用する場合、要素は無視されます。

 `version`属性文字列は、.NET Framework の指定したバージョンのインストールフォルダー名と一致している必要があります。 この文字列は解釈されません。 ランタイムスタートアップコードが一致するフォルダーを見つけられない場合、ランタイムは読み込まれません。スタートアップコードによってエラーメッセージが表示され、終了します。

> [!NOTE]
> Microsoft Internet Explorer でホストされているアプリケーションのスタートアップコードは、要素を無視し `<requiredRuntime>` ます。

## <a name="example"></a>例

次の例は、構成ファイルでランタイムバージョンを指定する方法を示しています。

```xml
<configuration>
   <startup>
      <requiredRuntime version="v1.0.3705" safemode="true"/>
   </startup>
</configuration>
```

## <a name="see-also"></a>関連項目

- [スタートアップ設定スキーマ](index.md)
- [構成ファイル スキーマ](../index.md)
- [方法: .NET Framework 4 以降のバージョンをサポートするアプリを構成する](../../../migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)
