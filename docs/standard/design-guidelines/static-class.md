---
title: 静的クラスのデザイン
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- type design guidelines, static classes
- class library design guidelines [.NET Framework], classes
- classes [.NET Framework], static
- static classes [.NET Framework]
- classes [.NET Framework], design guidelines
- type design guidelines, classes
ms.assetid: d67c14d8-c4dd-443f-affb-4ccae677c9b6
ms.openlocfilehash: c906502ed071e8515f101996ec42a04772f72b12
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291930"
---
# <a name="static-class-design"></a>静的クラスのデザイン
静的クラスは、静的メンバーのみを含むクラスとして定義されます (もちろん、から継承されたインスタンスメンバーと、場合によって <xref:System.Object?displayProperty=nameWithType> はプライベートコンストラクターを除く)。 一部の言語では、静的クラスのサポートが組み込まれています。 C# 2.0 以降では、クラスが静的として宣言されている場合、そのクラスは sealed で abstract であり、インスタンスメンバーをオーバーライドまたは宣言することはできません。

 静的クラスは、純粋なオブジェクト指向設計と単純さの間で妥協をします。 一般的に、他の操作 (など <xref:System.IO.File?displayProperty=nameWithType> )、拡張メソッドの所有者、または完全なオブジェクト指向ラッパーが認められされている機能 (など) へのショートカットを提供するために使用され <xref:System.Environment?displayProperty=nameWithType> ます。

 ✔️静的クラスは控えめに使用してください。

 静的クラスは、フレームワークのオブジェクト指向コアのサポートクラスとしてのみ使用する必要があります。

 ❌静的クラスをその他のバケットとして扱うことは避けてください。

 ❌静的クラスでインスタンスメンバーを宣言したりオーバーライドしたりしないでください。

 静的クラスが静的クラスに対して組み込みサポートされていない場合は、静的なクラスをシール、抽象型として宣言し、プライベートインスタンスコンストラクターを追加✔️ます。

 *©2005、2009 Microsoft Corporation の部分。すべての権限が予約されています。*

 *2008 年 10 月 22 日に Microsoft Windows Development シリーズの一部として、Addison-Wesley Professional によって発行された、Krzysztof Cwalina および Brad Abrams による「[Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)」 (フレームワーク デザイン ガイドライン: 再利用可能な .NET ライブラリの規則、用法、パターン、第 2 版) から Pearson Education, Inc. の許可を得て再印刷されています。*

## <a name="see-also"></a>関連項目

- [型デザインのガイドライン](type.md)
- [フレームワークデザインのガイドライン](index.md)
