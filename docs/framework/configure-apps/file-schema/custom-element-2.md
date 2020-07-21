---
title: NameValueSectionHandler および DictionarySectionHandler の Custom 要素
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/sectionName
helpviewer_keywords:
- custom element
ms.assetid: 2303031f-4c1d-4df4-bca1-e9bd96ca40dc
ms.openlocfilehash: e5c5c6cf5744aa385e6f6700cad623751a4d7427
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "77215473"
---
# <a name="custom-element-for-namevaluesectionhandler-and-dictionarysectionhandler"></a>NameValueSectionHandler および DictionarySectionHandler の Custom 要素

クラスおよびクラスを使用するカスタム構成セクションの設定を定義し <xref:System.Configuration.NameValueSectionHandler> <xref:System.Configuration.DictionarySectionHandler> ます。

[**\<configuration>**](configuration-element.md)\
&nbsp;&nbsp;**\<sectionName>**

## <a name="attributes"></a>属性

なし

## <a name="parent-element"></a>親要素

|     | 説明 |
| --- | ----------- |
| [**\<configuration>**](configuration-element.md) | 共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。 |

## <a name="child-elements"></a>子要素

|     | Description |
| --- | ----------- |
| [**\<add>**](add-element-for-custom-2.md)およびの場合 <xref:System.Configuration.NameValueSectionHandler><xref:System.Configuration.DictionarySectionHandler>  | カスタムアプリケーション設定を追加します。 |
| [**\<remove>**](remove-element-for-custom-2.md)およびの場合 <xref:System.Configuration.NameValueSectionHandler><xref:System.Configuration.DictionarySectionHandler> | 以前に定義した設定を削除します。 |
| [**\<clear>**](clear-element-for-custom-2.md)およびの場合 <xref:System.Configuration.NameValueSectionHandler><xref:System.Configuration.DictionarySectionHandler> | セクションで以前に定義したすべての設定を消去します。 |

## <a name="remarks"></a>解説

要素は、 **\<sectionName>** **\<section>** 要素内のタグによって定義されたカスタム要素です **\<configSections>** 。

次の表は、ConfigurationSettings. GetConfig メソッドが各構成セクションハンドラーに対して返すオブジェクトの種類を示しています。

| 構成セクションハンドラー                        | の戻り値の型 :                                                |
| ---------------------------------------------------- | ---------------------------------------------------------- |
| <xref:System.Configuration.NameValueSectionHandler>  | <xref:System.Collections.Specialized.NameValueCollection>  |
| <xref:System.Configuration.DictionarySectionHandler> | <xref:System.Collections.IDictionary>                      |

## <a name="example"></a>例

次の例は、クラスとクラスを使用するセクションを宣言する方法を示して <xref:System.Configuration.DictionarySectionHandler> <xref:System.Configuration.NameValueSectionHandler> います。

最初のカスタム要素はです。これには、 **\<dictionarySample>** <xref:System.Configuration.DictionarySectionHandler> アセンブリ内のクラスによって読み取られた設定が含まれ `System.dll` ます。 2番目のカスタム要素はです。これには、 **\<mySection>** アセンブリ内のクラスによって読み取られた設定が含まれ <xref:System.Configuration.NameValueSectionHandler> `System.dll` ます。

```xml
<configuration>
  <configSections>
    <section name="dictionarySample" type="System.Configuration.DictionarySectionHandler,System" />
    <sectionGroup name="mySectionGroup">
      <section name="mySection" type="System.Configuration.NameValueSectionHandler,System" />
    </sectionGroup>
  </configSections>
  <dictionarySample>
    <add key="myKey" value="myValue" />
  </dictionarySample>
  <mySectionGroup>
    <mySection>
      <add key="key1" value="value1" />
    </mySection>
  </mySectionGroup>
</configuration>
```

## <a name="configuration-file"></a>構成ファイル

この要素は、アプリケーション構成ファイル *、コンピューター構成*ファイル (machine.config)、およびアプリケーションディレクトリレベルでは*ない web.config ファイル*で使用できます。

## <a name="see-also"></a>関連項目

- [.NET Framework の構成ファイルスキーマ](index.md)
