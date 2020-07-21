---
title: アプリケーション設定スキーマ
ms.date: 03/30/2017
helpviewer_keywords:
- schema application settings
- application settings, schema [Windows Forms]
- Windows Forms, application settings schema
- configuration schema [.NET Framework], application settings
ms.assetid: 5797fcff-6081-4e8c-bebf-63d9c70cf14b
ms.openlocfilehash: 90d471888950347c041b4824b659ce33fda512d7
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "81242830"
---
# <a name="application-settings-schema"></a>アプリケーション設定スキーマ

アプリケーション設定を使用すると、Windows フォームまたは ASP.NET アプリケーションで、アプリケーションスコープの設定とユーザースコープの設定を格納および取得できます。 このコンテキストでは、*設定*は、アプリケーションに固有の情報、または現在のユーザーに固有の情報です。データベース接続文字列からユーザーの優先される既定のウィンドウサイズに至るまでのあらゆるものです。

既定では、Windows フォームアプリケーションのアプリケーション設定はクラスを使用します。このクラスは、 <xref:System.Configuration.LocalFileSettingsProvider> .net 構成システムを使用して XML 構成ファイルに設定を格納します。 アプリケーション設定で使用されるファイルの詳細については、「[アプリケーション設定アーキテクチャ](../../winforms/advanced/application-settings-architecture.md)」を参照してください。

アプリケーション設定は、使用する構成ファイルの一部として、次の要素を定義します。

| 要素                    | Description                                                                           |
| -------------------------- | ------------------------------------------------------------------------------------- |
| **\<applicationSettings>** | **\<setting>** アプリケーションに固有のすべてのタグが含まれます。                         |
| **\<userSettings>**        | **\<setting>** 現在のユーザーに固有のすべてのタグが含まれます。                        |
| **\<setting>**             | 設定を定義します。 **\<applicationSettings>** またはの子 **\<userSettings>** 。 |
| **\<value>**               | 設定の値を定義します。 の子 **\<setting>** 。                                   |

## <a name="applicationsettings-element"></a>\<applicationSettings> 要素

この要素に **\<setting>** は、クライアントコンピューター上のアプリケーションのインスタンスに固有のすべてのタグが含まれます。 属性は定義されません。

## <a name="usersettings-element"></a>\<userSettings> 要素

この要素 **\<setting>** には、アプリケーションを現在使用しているユーザーに固有のすべてのタグが含まれます。 属性は定義されません。

## <a name="setting-element"></a>\<setting> 要素

この要素は、設定を定義します。 これには次の属性があります。

| 属性        | 説明 |
| ---------------- | ----------- |
| **name**         | 必須。 設定の一意の ID。 Visual Studio で作成された設定は、という名前で保存され `ProjectName.Properties.Settings` ます。 |
| **serializeAs** | 必須。 値をテキストにシリアル化するために使用する形式。 有効な値は次のとおりです。<br><br>- `string`. 値は、を使用して文字列としてシリアル化され <xref:System.ComponentModel.TypeConverter> ます。<br>- `xml`. 値は、XML シリアル化を使用してシリアル化されます。<br>- `binary`. この値は、バイナリシリアル化を使用して、テキストエンコードバイナリとしてシリアル化されます。<br />- `custom`. 設定プロバイダーは、この設定に固有の情報を持ち、シリアル化および逆シリアル化を行います。 |

## <a name="value-element"></a>\<value> 要素

この要素には、設定の値が含まれます。

## <a name="example"></a>例

次の例は、2つのアプリケーションスコープ設定と2つのユーザースコープ設定を定義するアプリケーション設定ファイルを示しています。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <sectionGroup name="applicationSettings" type="System.Configuration.ApplicationSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">
      <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
    </sectionGroup>
    <sectionGroup name="userSettings" type="System.Configuration.UserSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">
      <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" allowExeDefinition="MachineToLocalUser" />
    </sectionGroup>
  </configSections>
  <applicationSettings>
    <WindowsApplication1.Properties.Settings>
      <setting name="Cursor" serializeAs="String">
        <value>Default</value>
      </setting>
      <setting name="DoubleBuffering" serializeAs="String">
        <value>False</value>
      </setting>
    </WindowsApplication1.Properties.Settings>
  </applicationSettings>
  <userSettings>
    <WindowsApplication1.Properties.Settings>
      <setting name="FormTitle" serializeAs="String">
        <value>Form1</value>
      </setting>
      <setting name="FormSize" serializeAs="String">
        <value>595, 536</value>
      </setting>
    </WindowsApplication1.Properties.Settings>
  </userSettings>
</configuration>
```

## <a name="see-also"></a>関連項目

- [アプリケーション設定の概要](../../winforms/advanced/application-settings-overview.md)
- [アプリケーション設定アーキテクチャ](../../winforms/advanced/application-settings-architecture.md)
