---
title: <add>NameValueSectionHandler および DictionarySectionHandler の要素
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/sectionName/add
helpviewer_keywords:
- add Element
- <add> Element
ms.assetid: 0d4ddb53-eb2b-49c0-9c33-a8dec5c39b46
ms.openlocfilehash: 57722f3518fad12cb8e6e35d68f40bb8465bdd86
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "77215435"
---
# <a name="add-element-for-namevaluesectionhandler-and-dictionarysectionhandler"></a>\<add>NameValueSectionHandler および DictionarySectionHandler の要素

カスタムアプリケーション設定を追加します。 各 **\<add>** タグには、キーと値のペアが含まれています。

[**\<configuration>**](configuration-element.md)\
&nbsp;&nbsp;[**\<sectionName>**](custom-element-2.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**

## <a name="syntax"></a>構文

```xml
<add key="key" value="value" />
```

## <a name="attributes"></a>属性

| 属性 | 説明 |
| --------- | ----------- |
| **key**   | 必須の属性です。<br><br>設定の名前を指定します。 |
| **value** | 必須の属性です。<br><br>設定の値を指定します。 |

## <a name="parent-element"></a>親要素

| 要素 | Description |
| ------- | ------------|
| [**\<sectionName>** Element](custom-element-2.md) | クラスおよびクラスを使用するカスタム構成セクションの設定を定義し <xref:System.Configuration.NameValueSectionHandler> <xref:System.Configuration.DictionarySectionHandler> ます。 |

## <a name="child-elements"></a>子要素

なし

## <a name="example"></a>例

次の例は、カスタム構成セクションを定義し、要素を使用して設定をセクションに格納する方法を示してい **\<add>** ます。

```xml
<configuration>
  <configSections>
    <section name="dictionarySample" type="System.Configuration.DictionarySectionHandler,System" />
  </configSections>
  <dictionarySample>
    <add key="myKey" value="myValue" />
  </dictionarySample>
</configuration>
```

## <a name="configuration-file"></a>構成ファイル

この要素は、アプリケーション構成ファイル *、コンピューター構成*ファイル (machine.config)、およびアプリケーションディレクトリレベルでは*ない web.config ファイル*で使用できます。

## <a name="see-also"></a>関連項目

- [.NET Framework の構成ファイルスキーマ](index.md)
