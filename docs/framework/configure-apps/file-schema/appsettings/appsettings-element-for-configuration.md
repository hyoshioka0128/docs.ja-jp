---
title: <configuration> の <appSettings> 要素
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/appSettings
helpviewer_keywords:
- appSettings Element
- <appSettings> Element
ms.assetid: 39694cc4-6b84-45a6-9329-385a0d8b48fe
ms.openlocfilehash: ea341d562f4b163a3a1771da0f20903b7d64bcdf
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79155532"
---
# <a name="appsettings-element-for-configuration"></a>\<configuration> の \<appSettings> 要素

カスタムアプリケーション設定が含まれます。 これは、.NET Framework によって提供される定義済みの構成セクションです。

[**\<configuration>**](../configuration-element.md) &nbsp;&nbsp;**\<appSettings>**

## <a name="syntax"></a>構文

```xml
<appSettings>
  <!-- Elements to add, clear, or remove configuration settings -->
</appSettings>
```

## <a name="attribute"></a>属性

|           | [説明] |
| --------- | ----------- |
| **拡張子**  | 省略可能な属性です。<br><br>カスタムアプリケーション構成設定を含む外部ファイルへの相対パスを指定します。 指定したファイルには、、、およびの各要素で指定したものと同じ種類の設定が含まれて **\<add>** **\<remove>** おり、これらの **\<clear>** 要素と同じキー/値ペアの形式を使用します。<br><br>指定されたパスは、メイン構成ファイルに対する相対パスです。 Windows フォームアプリケーションの場合、これはアプリケーション構成ファイルの場所ではなく、バイナリフォルダー ( */bin/debug*など) です。 Web フォームアプリケーションの場合、パスは、web.config ファイルが配置さ*れている*アプリケーションルートに対する相対パスです。<br><br>指定されたファイルが見つからない場合、ランタイムは属性を無視します。 |

## <a name="parent-element"></a>親要素

|     | 説明 |
| --- | ----------- |
| [**\<configuration>** Element](../configuration-element.md) | 共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。 |

## <a name="child-elements"></a>子要素

|     | Description |
| --- | ----------- |
| [**\<add>**](add-element-for-appsettings.md) | カスタムアプリケーション設定を追加します。 |
| [**\<clear>**](clear-element-for-appsettings.md) | 以前に定義したアプリケーション設定をすべてクリアします。 |
| [**\<remove>**](remove-element-for-appsettings.md) | 以前に定義したアプリケーション設定を削除します。 |

## <a name="remarks"></a>解説

要素には、 **\<appSettings>** データベース接続文字列、ファイルパス、XML Web サービス url などのカスタムアプリケーション構成情報、またはアプリケーションのその他のカスタム構成情報が格納されます。 要素で指定されたキーと値のペア **\<appSettings>** は、クラスを使用してコードでアクセスされ <xref:System.Configuration.ConfigurationSettings> ます。

Web.config**ファイル** **\<appSettings>** とアプリケーション構成ファイルの要素で file 属性*Web.config*を使用できます。 この属性は、追加設定を提供するか、要素で指定された設定をオーバーライドする構成ファイルを指定し **\<appSettings>** ます。 **ファイル**属性は、アプリケーション構成ファイルで指定されたプロジェクト設定をユーザーがオーバーライドする必要がある場合など、ソース管理チームの開発シナリオで使用できます。

**File**属性で指定される構成ファイルは、ではなく、のルートノードである必要があり **\<appSettings>** **\<configuration>** ます。

## <a name="example"></a>例

次の例は、カスタム アプリケーション設定を定義する外部アプリケーション設定ファイル (*custom.config*) を示しています。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<appSettings>
  <add key="MyCustomSetting" value="MyCustomSettingValue" />
</appSettings>
```

次の例は、外部設定ファイルで設定を使用して、独自のアプリケーション設定を設定するアプリケーション構成ファイルを示しています。

```xml
<configuration>
  <appSettings file="custom.config">
    <add key="ApplicationName" value="MyApplication" />
  </appSettings>
</configuration>
```

## <a name="configuration-file"></a>構成ファイル

この要素は、アプリケーション構成ファイル *、コンピューター構成*ファイル (machine.config)、およびアプリケーションディレクトリレベルでは*ない web.config ファイル*で使用できます。

## <a name="see-also"></a>関連項目

- [.NET Framework の構成ファイルスキーマ](../index.md)
