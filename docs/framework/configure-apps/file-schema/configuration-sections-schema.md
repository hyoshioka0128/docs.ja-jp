---
title: 構成セクションのスキーマ
ms.date: 05/02/2017
helpviewer_keywords:
- configuration settings [.NET Framework], custom
- schema configuration settings
- configuration sections [.NET Framework]
- custom elements
- configuration schema [.NET Framework], custom settings in configuration files
- elements [.NET Framework], custom settings in configuration files
ms.assetid: 6e4cc793-c526-4007-b4e9-37d56295f2cb
ms.openlocfilehash: fc43a9c32ba33629b6e89120cf57f6d212ab3a56
ms.sourcegitcommit: 2543a78be6e246aa010a01decf58889de53d1636
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2020
ms.locfileid: "86441662"
---
# <a name="configuration-sections-schema"></a>構成セクションのスキーマ

構成セクションスキーマには、構成ファイルのカスタム設定を定義する要素が含まれています。 構成ファイルとスキーマに関する一般的な情報については、 [.NET Framework の構成ファイルスキーマ](index.md)に関する説明を参照してください。

[**\<configuration>**](configuration-element.md)
[**\<configSections>**](configsections-element-for-configuration.md)
[**\<section>**](section-element.md)
[**\<sectionGroup>**](sectiongroup-element-for-configsections.md)

|     | 説明 |
| --- | ----------- |
| [**\<configSections>**](configsections-element-for-configuration.md) | 構成セクションと名前空間の宣言が含まれています。 |
| [**\<section>** およびの場合 **\<configSections>****\<sectionGroup>**](section-element.md) | 構成セクションの宣言が含まれています。 |
| [**\<sectionGroup>** の**\<configSections>**](sectiongroup-element-for-configsections.md) | 構成セクションの名前空間を定義します。 |

<a name="dep"></a>

## <a name="unimplemented-elements"></a>未実装の要素

次の要素は影響を与えないため、使用しないでください。

* **\<clear>**
* **\<remove>**
