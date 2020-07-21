---
title: SingleTagSectionHandler のカスタム要素
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/sectionName
helpviewer_keywords:
- custom element
ms.assetid: e62056c6-b351-40eb-afc0-cc13fc44e45e
ms.openlocfilehash: a40f35838655f6021af0b2e966335803ec8c16b4
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "80635400"
---
# <a name="custom-element-for-singletagsectionhandler"></a>SingleTagSectionHandler のカスタム要素

要素によって定義され、クラスを使用するカスタム構成セクションの設定を定義 \<section> し <xref:System.Configuration.SingleTagSectionHandler> ます。

[**\<configuration>**](configuration-element.md) &nbsp;&nbsp;*\<sectionName>*

## <a name="syntax"></a>構文

```xml
<sectionName key="value" key2="value2" />
```

## <a name="attributes"></a>属性

属性と属性値はユーザーが定義します。

## <a name="parent-element"></a>親要素

|     | 説明 |
| --- | ----------- |
| [**\<configuration>**](configuration-element.md) | 共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。 |

## <a name="child-elements"></a>子要素

なし

## <a name="remarks"></a>解説

要素は、 **\<sectionName>** [**\<section>**](section-element.md) 要素内のタグによって定義されたカスタム要素です [**\<configSections>**](configsections-element-for-configuration.md) 。 を呼び出すと、構成システムからオブジェクトが返され <xref:System.Collections.IDictionary> <xref:System.Configuration.Configuration.GetSection(System.String)?displayProperty=nameWithType> ます。

## <a name="example"></a>例

次の例では、 **\<sampleSection>** クラスによって読み取られた設定を含むというカスタム要素を宣言してい <xref:System.Configuration.SingleTagSectionHandler> ます。

```xml
<configuration>
  <configSections>
    <section name="sampleSection"
             type="System.Configuration.SingleTagSectionHandler" />
  </configSections>
  <sampleSection setting1="Value1"
                 setting2="value two"
                 setting3="third value" />
</configuration>
```

## <a name="configuration-file"></a>構成ファイル

この要素は、アプリケーション構成ファイル *、マシン構成ファイル (machine.config*)、およびアプリケーションディレクトリレベルではない*web.config ファイル*で使用できます。

## <a name="see-also"></a>関連項目

- [.NET Framework の構成ファイルスキーマ](index.md)
