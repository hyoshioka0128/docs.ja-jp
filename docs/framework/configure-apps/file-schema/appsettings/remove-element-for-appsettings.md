---
title: <appSettings> の <remove> 要素
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/appSettings/remove
helpviewer_keywords:
- remove Element
- <remove> Element
ms.assetid: 218c4464-e007-4539-803f-7c8b0a909fd8
ms.openlocfilehash: 83abbdbf0d3e4dfd16c0e8c649200c4ecc7329f7
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "77215489"
---
# <a name="remove-element-for-appsettings"></a>\<appSettings> の \<remove> 要素

カスタムアプリケーション設定を削除します。

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<appSettings>**](appsettings-element-for-configuration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<remove>**

## <a name="syntax"></a>構文

```xml
<appSettings>
  <remove key="Key of custom setting" />
</appSettings>
```

### <a name="attribute"></a>属性

|         | 説明 |
| ------- | ----------- |
| **key** | 必須の属性です。<br><br>削除するキーの名前を指定します。 |

### <a name="parent-element"></a>親要素

|     | 説明 |
| --- | ----------- |
| [**\<appSettings>**](appsettings-element-for-configuration.md) | ファイル パス、XML Web サービス URL、またはアプリケーションのその他のカスタム構成情報など、カスタム アプリケーションの設定が含まれています。 |

## <a name="child-elements"></a>子要素

なし

## <a name="example"></a>例

次の例は、のカスタム構成設定を削除する方法を示してい `ApplicationName` ます。

```xml
<appSettings>
  <remove key="ApplicationName" />
</appSettings>
```

## <a name="see-also"></a>関連項目

- [.NET Framework の構成ファイルスキーマ](../index.md)
