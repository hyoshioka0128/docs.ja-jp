---
title: <configuration> の <configSections> 要素
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections
helpviewer_keywords:
- configSections Element
- <configSections> Element
ms.assetid: 9f963c1b-dc3f-4220-a8b6-2dd7a5a8e039
ms.openlocfilehash: 1e4bb7a7cfb0b140ca6d13c162708c3c30bd496d
ms.sourcegitcommit: 2543a78be6e246aa010a01decf58889de53d1636
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2020
ms.locfileid: "86441688"
---
# <a name="configsections-element-for-configuration"></a>\<configuration> の \<configSections> 要素

構成セクションと名前空間の宣言が含まれています。

[**\<configuration>**](configuration-element.md) &nbsp;&nbsp;**\<configSections>**

## <a name="attributes"></a>属性

なし

## <a name="parent-element"></a>親要素

|     | 説明 |
| --- | ----------- |
| [**\<configuration>**](configuration-element.md) | 共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。 |

## <a name="child-elements"></a>子要素

|     | 説明 |
| --- | ----------- |
| [**\<section>**](section-element.md) | 構成セクションの宣言が含まれています。 |
| [**\<sectionGroup>**](sectiongroup-element-for-configsections.md) | 構成セクションの名前空間を定義します。 |

## <a name="remarks"></a>解説

この要素が構成ファイル内にある場合は、要素の最初の子要素である必要があり **\<configuration>** ます。

## <a name="example"></a>例

次の例は、構成セクションを定義し、そのセクションの設定を定義する方法を示しています。

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

この要素は、アプリケーション構成ファイル、マシン構成ファイル (*Machine.config*)、およびアプリケーションディレクトリレベルではないファイル*Web.config*で使用できます。

## <a name="see-also"></a>関連項目

- [.NET Framework の構成ファイルスキーマ](index.md)
