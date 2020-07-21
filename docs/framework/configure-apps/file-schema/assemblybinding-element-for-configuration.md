---
title: <configuration> の <assemblyBinding> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/assemblyBinding
helpviewer_keywords:
- assemblyBinding Element
- <assemblyBinding> Element
ms.assetid: 6cc55983-b894-449b-8e26-b258e53939cd
ms.openlocfilehash: 21cf5e749b0dae310c3326f8abf82c6678fc97e9
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79155480"
---
# <a name="assemblybinding-element-for-configuration"></a>\<configuration> の \<assemblyBinding> 要素

構成レベルでのアセンブリ バインディング ポリシーを指定します。

[**\<configuration>**](configuration-element.md) &nbsp;&nbsp;**\<assemblyBinding>**

## <a name="syntax"></a>構文

```xml
<assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
  <!-- Configuration files to include. -->
</assemblyBinding>
```

## <a name="attribute"></a>属性

|           | [説明] |
| --------- | ----------- |
| **xmlns** | 必須の属性です。<br><br>アセンブリのバインディングに必要な XML 名前空間を指定します。 値として、文字列 "urn:schemas-microsoft-com:asm.v1" を使用します。 |

## <a name="parent-element"></a>親要素

|     | Description |
| --- | ----------- |
| [**\<configuration>**](configuration-element.md) | 共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。 |

## <a name="child-element"></a>子要素

|     | 説明 |
| --- | ----------- |
| [**\<linkedConfiguration>**](linkedconfiguration-element.md) | インクルードする構成ファイルを指定します。 |

## <a name="remarks"></a>解説

要素は、 [**\<linkedConfiguration>**](linkedconfiguration-element.md) アセンブリ構成設定を複製するのではなく、アプリケーション構成ファイルに既知の場所にアセンブリ構成ファイルを含めることができるようにすることで、コンポーネントアセンブリの管理を簡略化します。

> [!NOTE]
> **\<linkedConfiguration>** 要素は、Windows サイドバイサイドマニフェストを持つアプリケーションではサポートされていません。

## <a name="example"></a>例

次の例は、ローカルのハードディスクに構成ファイルを含める方法を示しています。

```xml
<configuration>
  <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
    <linkedConfiguration href="file://c:\Program Files\Contoso\sharedConfig.xml" />
  </assemblyBinding>
</configuration>
```

## <a name="see-also"></a>関連項目

- [.NET Framework の構成ファイルスキーマ](index.md)
